# Tema 22 — Casos Prácticos

> **Título oficial**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.
>
> **Formato**: 3 casos prácticos sobre supuestos reales del Ayuntamiento de Madrid. Cada caso suma **10 puntos**.
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid

Los tres casos recorren el escenario de referencia **arquitectura de la Sede Electrónica** (ver tema-22-contenido.md, «Convenciones»): el **Caso 1** trabaja el **diseño n-capas y la API REST** de cara al ciudadano (§3-4, §6.6); el **Caso 2**, la **integración de servicios web heredados** (SOAP/WSDL) con la nueva capa de negocio orientada a servicios (§5); y el **Caso 3**, la **evolución hacia microservicios, eventos y contenedores** del módulo de notificaciones (§7).

---

## Caso 1 — Diseño n-capas y API REST de la Sede Electrónica

### Enunciado

El Ayuntamiento va a modernizar el acceso ciudadano a la consulta de expedientes. Actualmente existe una aplicación de escritorio (cliente pesado) que se conecta directamente a la base de datos de expedientes; se quiere sustituirla por una **Sede Electrónica web**, capaz de soportar picos de tráfico en campañas de plazos y de escalar sin comprar hardware cada vez más caro.

### Cuestiones

**Cuestión 1 — Modelo arquitectónico (2 puntos).** Justifique por qué se debe abandonar el modelo de 2 capas actual y adoptar un modelo de 3 o más capas para la nueva Sede Electrónica.

**Cuestión 2 — Estrategia de escalado (3 puntos).** Ante picos de tráfico en campañas de plazos fiscales, ¿qué estrategia de escalado recomienda para el nuevo servidor de aplicaciones, y por qué no basta con la estrategia usada por el modelo antiguo?

**Cuestión 3 — Diseño del recurso REST (3 puntos).** Diseñe, en términos de URI y verbo HTTP, cómo se consultaría el expediente `EXP-2026-004821` y cómo se marcaría como "revisado" desde el panel del gestor. Indique el nivel del modelo de madurez de Richardson que alcanza este diseño.

**Cuestión 4 — Separación de responsabilidades (2 puntos).** ¿En qué capa debe residir la comprobación de que el ciudadano autenticado es efectivamente el titular del expediente que consulta, y por qué no puede delegarse esa comprobación en el cliente web?

### Solución orientativa

- **C1**: en el modelo de 2 capas actual, la lógica de negocio está repartida de forma ambigua entre el cliente pesado y la base de datos (procedimientos almacenados), lo que **acopla fuertemente** el cliente al esquema de datos y limita la escalabilidad, porque cada cliente mantiene una conexión directa al SGBD (§3.1). Un modelo de 3 capas introduce un **servidor de aplicaciones** que desacopla al cliente del esquema de datos y permite **agrupar conexiones** mediante un *pool*, mejorando sustancialmente la escalabilidad (§3.2).

- **C2**: **escalado horizontal**: añadir instancias temporales del servidor de aplicaciones detrás de un balanceador de carga durante el pico, y retirarlas después (§2.2.2). El modelo antiguo, con el cliente conectado directamente al SGBD, solo permitía en la práctica **escalado vertical** del propio servidor de base de datos, con un límite físico y un coste ocioso el resto del año.

```http
GET /api/expedientes/EXP-2026-004821 HTTP/1.1
Host: sede.madrid.es
Accept: application/json
Authorization: Bearer <jwt>
```
```http
PATCH /api/expedientes/EXP-2026-004821 HTTP/1.1
Host: sede.madrid.es
Content-Type: application/json
Authorization: Bearer <jwt>

{"estado": "revisado"}
```

- **C3**: `GET /api/expedientes/{id}` para consultar (recurso identificado por URI) y `PATCH /api/expedientes/{id}` para la actualización parcial de estado, ambos con el código de estado adecuado en la respuesta (`200 OK`, `404 Not Found`). Este diseño —recursos por URI + verbos HTTP + códigos de estado, sin hipermedia— corresponde al **nivel 2** del modelo de madurez de Richardson (§6.6), el nivel donde se sitúa la inmensa mayoría de las APIs REST reales.

- **C4**: en la **capa de lógica de negocio** (§4.3, §4.6): es una regla de negocio y de seguridad, no una validación de formato. Delegarla en el cliente web sería inseguro, porque un cliente ligero es manipulable por el propio usuario (herramientas de desarrollador, peticiones directas a la API); la comprobación debe repetirse siempre, de forma autoritativa, en el servidor.

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Justificación correcta del paso de 2 a 3 capas (desacoplamiento) | 2 |
| Escalado horizontal identificado y contrastado con la limitación del modelo 2-Tier | 3 |
| Diseño REST correcto (URI, verbos, nivel 2 de Richardson) | 3 |
| Ubicación de la comprobación de titularidad en la capa de negocio, justificada | 2 |

---

## Caso 2 — Integración de un servicio SOAP heredado en la nueva arquitectura orientada a servicios

### Enunciado

El sistema de **Tributos**, en producción desde hace más de una década, expone su lógica de liquidación mediante un servicio **SOAP** con contrato WSDL formal. La nueva capa de negocio de la Sede Electrónica necesita **reutilizar** esa lógica —sin reescribirla— para ofrecer al ciudadano, en su API REST propia, la consulta del importe pendiente de un tributo.

### Cuestiones

**Cuestión 1 — Elección del estilo (2 puntos).** ¿Recomendaría sustituir el servicio SOAP de Tributos por uno REST antes de integrarlo? Justifique con los criterios de este tema.

**Cuestión 2 — Contrato del servicio (3 puntos).** ¿Qué documento describe formalmente las operaciones, mensajes y *endpoint* del servicio SOAP de Tributos, y qué papel jugaría un registro UDDI en este escenario?

**Cuestión 3 — Patrón de integración (3 puntos).** Describa, en términos arquitectónicos, cómo la capa de negocio de la Sede Electrónica actúa como intermediario entre el cliente REST del ciudadano y el servicio SOAP de Tributos, sin que el ciudadano tenga que conocer SOAP ni XML.

**Cuestión 4 — Seguridad del extremo REST (2 puntos).** El nuevo *endpoint* REST de consulta de tributos debe exigir que el ciudadano esté autenticado. ¿Qué estándar y qué formato de token usaría, y qué garantiza cada uno?

### Solución orientativa

- **C1**: **no**, no se recomienda sustituirlo. SOAP no está "muerto": sigue siendo el estándar de facto en integraciones empresariales que requieren garantías formales fuertes (WS-Security, transacciones distribuidas), típicas de sistemas heredados de tributación (§5.4.1). Reescribirlo introduciría riesgo y coste sin beneficio funcional; lo correcto es **envolverlo**, no sustituirlo.

- **C2**: el **WSDL** (§6.4), que describe las operaciones (p. ej. `ConsultarImportePendiente`), los mensajes de entrada/salida, los tipos de datos y el *endpoint* de red del servicio. Un registro **UDDI** sería, en teoría, el lugar donde publicar y descubrir ese WSDL, pero en la práctica actual UDDI está en **desuso**: el equipo ya conoce el WSDL del sistema de Tributos de forma directa, sin necesidad de un registro público de descubrimiento.

```xml
<wsdl:portType name="TributosPortType">
  <wsdl:operation name="ConsultarImportePendiente">
    <wsdl:input message="tns:ConsultaRequest"/>
    <wsdl:output message="tns:ConsultaResponse"/>
  </wsdl:operation>
</wsdl:portType>
```

- **C3**: la capa de negocio actúa como **intermediario/adaptador**: recibe la petición REST del ciudadano (`GET /api/tributos/{id}/pendiente`), construye internamente el mensaje SOAP con el sobre XML correspondiente, invoca el servicio de Tributos, y **traduce la respuesta SOAP/XML a JSON** antes de devolverla al ciudadano. El ciudadano nunca ve XML ni SOAP; solo JSON sobre REST — este patrón de traducción entre estilos es precisamente lo que permite que ambos convivan en la misma arquitectura (§5.4.2).

```http
GET /api/tributos/EXP-2026-004821/pendiente HTTP/1.1
Accept: application/json
```
```json
{"expediente": "EXP-2026-004821", "importePendiente": 145.30, "moneda": "EUR"}
```

- **C4**: **OAuth 2.0** (§6.2) como *framework* de autorización delegada, con un **JWT** como formato de token: el ciudadano se autentica una vez ante el servidor de autorización y el cliente presenta el token en cada petición REST, sin que la API de tributos necesite conocer la contraseña del ciudadano. La firma del JWT permite verificar su validez sin consultar al emisor en cada petición.

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Decisión razonada de no sustituir SOAP por REST | 2 |
| WSDL identificado correctamente + papel (en desuso) de UDDI | 3 |
| Patrón de intermediación/traducción SOAP↔REST descrito correctamente | 3 |
| OAuth 2.0 + JWT identificados con su función respectiva | 2 |

---

## Caso 3 — Evolución del módulo de notificaciones hacia microservicios, eventos y contenedores

### Enunciado

Cuando un expediente cambia de estado, hoy la propia capa de negocio de la Sede Electrónica invoca **directamente** —dentro del mismo proceso— la función que envía la notificación al ciudadano. Se quiere rediseñar este módulo para que, en el futuro, cualquier número de sistemas municipales (notificaciones, estadísticas, un futuro sistema de auditoría) pueda reaccionar a ese cambio de estado sin modificar la capa de negocio cada vez que se añada uno nuevo, y que el propio módulo de notificaciones se pueda desplegar y escalar de forma independiente del resto de la aplicación.

### Cuestiones

**Cuestión 1 — Estilo de comunicación (3 puntos).** ¿Qué estilo arquitectónico recomienda para desacoplar la capa de negocio de los sistemas interesados en el cambio de estado, y qué papel juega el *middleware* en esa solución?

**Cuestión 2 — Unidad de despliegue (3 puntos).** ¿Recomendaría extraer el módulo de notificaciones como un microservicio independiente, con su propia base de datos? Razone ventajas e inconvenientes frente a mantenerlo dentro del monolito actual.

**Cuestión 3 — Empaquetado y escalado (2 puntos).** Si el módulo de notificaciones se extrae como microservicio independiente, ¿qué tecnología de empaquetado y qué mecanismo de automatización recomendaría para desplegarlo y escalarlo sin intervención manual constante?

**Cuestión 4 — Consistencia de datos (2 puntos).** Al pasar de una llamada directa dentro del mismo proceso a una comunicación asíncrona por eventos entre dos servicios con bases de datos separadas, ¿qué tipo de consistencia debe asumir el equipo, y por qué ya no es realista exigir consistencia transaccional fuerte entre ambos?

### Solución orientativa

- **C1**: una **arquitectura orientada a eventos (EDA)** (§7.2): la capa de negocio **publica** un evento («expediente cambiado de estado») en un canal, sin conocer ni necesitar saber quién lo va a consumir; los sistemas interesados se **suscriben** a ese canal. El **middleware orientado a mensajes** (MOM, §2.2.3) es quien gestiona la entrega del evento a todos los suscriptores, desacoplando emisor y receptor en el espacio y en el tiempo. Añadir un futuro sistema de auditoría no requeriría modificar en absoluto la capa de negocio: solo dar de alta una nueva suscripción.

- **C2**: **sí**, es razonable extraerlo como **microservicio** (§7.1) con base de datos propia, porque su ciclo de vida (frecuencia de cambios, patrón de carga) es distinto al del núcleo de tramitación, y así puede escalarse y desplegarse de forma independiente. El inconveniente es la **complejidad operacional** añadida —hay que monitorizar, desplegar y versionar un componente más— y la renuncia a la consistencia transaccional fuerte entre el módulo de expedientes y el de notificaciones, sustituida por consistencia eventual (§7.1).

- **C3**: **contenedores** (Docker o equivalente) para empaquetar el microservicio de forma ligera y reproducible, y un **orquestador** tipo Kubernetes (§7.3) para automatizar su arranque, reinicio ante fallo, balanceo de carga y escalado horizontal según la demanda, sin intervención manual.

- **C4**: **consistencia eventual**: el estado del expediente y el estado de la notificación pueden estar momentáneamente desincronizados (el expediente ya ha cambiado de estado, pero la notificación aún no se ha enviado), y se asume que **acabará** convergiendo. Ya no es realista exigir consistencia transaccional fuerte (ACID) entre ambos porque son **dos bases de datos independientes en dos servicios distintos**, comunicados de forma asíncrona por eventos — no existe una única transacción que abarque a ambos sin introducir un coordinador de transacciones distribuidas, que precisamente el diseño de microservicios busca evitar (§7.1).

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| EDA identificada + papel del middleware orientado a mensajes | 3 |
| Decisión de extracción a microservicio razonada (ventajas e inconvenientes) | 3 |
| Contenedores + orquestación identificados como mecanismo de despliegue/escalado | 2 |
| Consistencia eventual identificada y justificada frente a consistencia fuerte | 2 |
