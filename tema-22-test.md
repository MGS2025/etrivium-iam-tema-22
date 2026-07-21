# Tema 22 — Test de Autoevaluación

> **Título**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.
> **Formato**: 60 preguntas tipo test A/B/C (formato oficial oposición)
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid
> **Versión**: v1.0 — Pendiente validación
> **Fecha**: 2026-07-21
> **Fuentes**: ver tema-22-fuentes.md

---

## Instrucciones

- Cada pregunta tiene **3 opciones** (A, B, C). Solo una es correcta.
- Penalización en examen real: respuesta incorrecta descuenta **1/3** del valor de una correcta.
- Tiempo orientativo: 1 minuto por pregunta.
- Distribución: Introducción (P1-P5), Cliente/servidor (P6-P14), Modelos 2/3/n-Tier (P15-P22), Multicapas (P23-P30), Orientación a servicios (P31-P39), Protocolos y estándares (P40-P53), Tendencias actuales (P54-P60).

---

### Pregunta 1

**¿Qué distingue a la "arquitectura de sistemas" de la "arquitectura de red"?**

A) La arquitectura de sistemas organiza componentes software y sus relaciones; la de red es la topología física/lógica de los dispositivos de comunicaciones
B) Son sinónimos exactos, usados indistintamente en toda la literatura técnica
C) La arquitectura de red incluye siempre a la de sistemas como subconjunto

<details><summary>Respuesta</summary>

**Correcta: A) La arquitectura de sistemas organiza componentes software y sus relaciones; la de red es la topología física/lógica de los dispositivos de comunicaciones** Son nociones relacionadas pero independientes: una misma arquitectura de sistemas puede desplegarse sobre topologías de red distintas.

*Referencia: §1.1 [FOWLER-PEAA]*
</details>

---

### Pregunta 2

**¿Qué avance tecnológico hizo posible la transición del modelo centralizado (mainframe) al modelo cliente/servidor?**

A) La sustitución de las terminales tontas por impresoras de red
B) La popularización del PC y de las redes de área local (LAN) a finales de los 80
C) La invención del protocolo HTTP en 1991

<details><summary>Respuesta</summary>

**Correcta: B) La popularización del PC y de las redes de área local (LAN) a finales de los 80** Permitió repartir la lógica y la interfaz entre puestos de usuario, mientras los recursos compartidos seguían en servidores especializados.

*Referencia: §1.2.2 [GARTNER-3TIER]*
</details>

---

### Pregunta 3

**¿Cuál de los siguientes es un "atributo de calidad" (requisito no funcional) que persigue una arquitectura de sistemas?**

A) El número de líneas de código del proyecto
B) El lenguaje de programación elegido por el equipo
C) La escalabilidad, entendida como capacidad de crecer en carga sin rediseñar

<details><summary>Respuesta</summary>

**Correcta: C) La escalabilidad, entendida como capacidad de crecer en carga sin rediseñar** Junto con disponibilidad, mantenibilidad, seguridad, rendimiento e interoperabilidad, son los atributos que determinan si una arquitectura es adecuada para un contexto dado.

*Referencia: §1.1 [FOWLER-PEAA]*
</details>

---

### Pregunta 4

**Ordenando cronológicamente la evolución de los modelos arquitectónicos, ¿qué secuencia es correcta?**

A) Centralizado → cliente/servidor → 3/n-capas → SOA → microservicios/contenedores/nube
B) SOA → microservicios → cliente/servidor → centralizado
C) Microservicios → 3-capas → SOA → cliente/servidor

<details><summary>Respuesta</summary>

**Correcta: A) Centralizado → cliente/servidor → 3/n-capas → SOA → microservicios/contenedores/nube** Cada oleada resuelve limitaciones de la anterior, sin eliminar por completo a las precedentes (SOAP sigue en uso, por ejemplo).

*Referencia: §1.2.3*
</details>

---

### Pregunta 5

**¿Qué relación existe entre este Tema 22 y el Tema 31 del temario?**

A) Son temas idénticos que se repiten por error en el temario oficial
B) El Tema 31 desarrolla en profundidad IaaS/PaaS/SaaS y los modelos de despliegue de nube que el Tema 22 solo sitúa como cierre de la evolución arquitectónica
C) El Tema 31 trata exclusivamente de seguridad y no tiene relación con este tema

<details><summary>Respuesta</summary>

**Correcta: B) El Tema 31 desarrolla en profundidad IaaS/PaaS/SaaS y los modelos de despliegue de nube que el Tema 22 solo sitúa como cierre de la evolución arquitectónica** Este tema sienta las bases arquitectónicas (cliente/servidor, capas, servicios) sobre las que se apoya la infraestructura de provisión que trata el Tema 31.

*Referencia: §1.2.3 [REFERENCIA CRUZADA]*
</details>

---

### Pregunta 6

**En la relación cliente/servidor, ¿qué característica define el patrón de interacción "petición-respuesta"?**

A) El servidor inicia siempre la comunicación hacia el cliente
B) Cliente y servidor envían mensajes de forma simultánea sin orden definido
C) El cliente inicia la comunicación solicitando un servicio; el servidor responde, sin iniciativa propia hacia el cliente en el modelo clásico

<details><summary>Respuesta</summary>

**Correcta: C) El cliente inicia la comunicación solicitando un servicio; el servidor responde, sin iniciativa propia hacia el cliente en el modelo clásico** Es una relación asimétrica: el cliente conoce (o localiza) al servidor, no al revés.

*Referencia: §2.1 [FOWLER-PEAA]*
</details>

---

### Pregunta 7

**¿Qué caracteriza a un "cliente ligero" (thin client) frente a un "cliente pesado"?**

A) Concentra en el servidor casi toda la lógica de negocio; el cliente solo renderiza — el navegador web es el ejemplo paradigmático
B) Mantiene siempre una copia local completa de la base de datos
C) No puede comunicarse con ningún servidor remoto

<details><summary>Respuesta</summary>

**Correcta: A) Concentra en el servidor casi toda la lógica de negocio; el cliente solo renderiza — el navegador web es el ejemplo paradigmático** El cliente pesado, en cambio, ejecuta lógica de negocio local y complica el despliegue.

*Referencia: §2.2.1 [FOWLER-PEAA]*
</details>

---

### Pregunta 8

**¿Cuál fue el motor histórico que impulsó la migración de aplicaciones de escritorio (cliente pesado) hacia aplicaciones web (cliente ligero)?**

A) La desaparición de los sistemas operativos de escritorio
B) El problema de despliegue del cliente pesado: instalar y actualizar software en cada puesto tiene un coste de mantenimiento alto
C) La obligación legal de usar exclusivamente HTML

<details><summary>Respuesta</summary>

**Correcta: B) El problema de despliegue del cliente pesado: instalar y actualizar software en cada puesto tiene un coste de mantenimiento alto** Un cliente ligero centraliza la actualización en el servidor, transparente al usuario final.

*Referencia: §2.2.1 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 9

**¿Qué responsabilidad es propia del servidor y no tiene equivalente directo en el cliente clásico?**

A) La renderización de la interfaz de usuario
B) La validación del formato de un correo electrónico introducido en un formulario
C) La gestión de recursos compartidos y el control de concurrencia ante accesos simultáneos de varios clientes

<details><summary>Respuesta</summary>

**Correcta: C) La gestión de recursos compartidos y el control de concurrencia ante accesos simultáneos de varios clientes** Exige mecanismos como bloqueos, control de concurrencia optimista o transacciones para evitar que accesos simultáneos corrompan el recurso.

*Referencia: §2.2.2*
</details>

---

### Pregunta 10

**¿Qué diferencia al escalado "vertical" del escalado "horizontal"?**

A) El vertical añade más CPU/memoria a una misma máquina (con límite físico); el horizontal añade más máquinas/instancias en paralelo, sin techo físico
B) Son términos sinónimos usados indistintamente
C) El horizontal solo es aplicable a bases de datos, nunca a servidores de aplicaciones

<details><summary>Respuesta</summary>

**Correcta: A) El vertical añade más CPU/memoria a una misma máquina (con límite físico); el horizontal añade más máquinas/instancias en paralelo, sin techo físico** Las arquitecturas modernas priorizan el horizontal porque además aporta tolerancia a fallos.

*Referencia: §2.2.2 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 11

**¿Qué es el "middleware" en una arquitectura cliente/servidor?**

A) Un sinónimo de "servidor de base de datos"
B) Software intermedio que oculta la complejidad de la comunicación distribuida, ofreciendo una interfaz de más alto nivel (p. ej. ODBC/JDBC, MOM, ORB)
C) El conjunto de cables y conmutadores de la red física

<details><summary>Respuesta</summary>

**Correcta: B) Software intermedio que oculta la complejidad de la comunicación distribuida, ofreciendo una interfaz de más alto nivel (p. ej. ODBC/JDBC, MOM, ORB)** Sin él, cada aplicación tendría que resolver por sí misma la serialización, la localización de servicios o la tolerancia a fallos de red.

*Referencia: §2.2.3 [FOWLER-PEAA]*
</details>

---

### Pregunta 12

**¿Qué tipo de middleware es la base técnica de la arquitectura orientada a eventos (EDA, §7.2)?**

A) El middleware de acceso a datos (ODBC/JDBC)
B) El middleware transaccional de commit en dos fases
C) El middleware orientado a mensajes (MOM), como JMS, RabbitMQ o Kafka

<details><summary>Respuesta</summary>

**Correcta: C) El middleware orientado a mensajes (MOM), como JMS, RabbitMQ o Kafka** Permite el envío de mensajes/eventos asíncronos entre aplicaciones sin acoplamiento directo emisor-receptor.

*Referencia: §2.2.3 [REFERENCIA CRUZADA]*
</details>

---

### Pregunta 13

**El Tema 34 del temario desarrolla en profundidad...**

A) El modelo TCP/IP y el modelo OSI: la infraestructura de comunicaciones sobre la que se apoyan, sin necesidad de conocerla en detalle, los protocolos de aplicación de este Tema 22
B) Los procedimientos almacenados y disparadores de bases de datos relacionales
C) El diseño de interfaces de usuario accesibles

<details><summary>Respuesta</summary>

**Correcta: A) El modelo TCP/IP y el modelo OSI: la infraestructura de comunicaciones sobre la que se apoyan, sin necesidad de conocerla en detalle, los protocolos de aplicación de este Tema 22** Este tema se sitúa deliberadamente en el nivel de aplicación de la pila de protocolos.

*Referencia: §2.2.4 [REFERENCIA CRUZADA]*
</details>

---

### Pregunta 14

**En días de campaña de renovación del Padrón, con picos de tráfico en la Sede Electrónica, ¿qué estrategia de escalado permite añadir capacidad solo durante el pico y retirarla después?**

A) El escalado vertical exclusivamente
B) El escalado horizontal, añadiendo instancias temporales del servidor de aplicaciones detrás de un balanceador de carga
C) Reducir el número de campos del formulario de solicitud

<details><summary>Respuesta</summary>

**Correcta: B) El escalado horizontal, añadiendo instancias temporales del servidor de aplicaciones detrás de un balanceador de carga** El escalado vertical exigiría sobredimensionar permanentemente el hardware, con coste ocioso el resto del año.

*Referencia: §2.2.2 [EJEMPLO AYTO MADRID]*
</details>

---

### Pregunta 15

**En la arquitectura de dos capas (2-Tier), ¿dónde reside la lógica de negocio?**

A) Exclusivamente en un servidor de aplicaciones intermedio
B) Nunca en el cliente, siempre en un tercer nivel
C) De forma ambigua, repartida entre el cliente y el servidor de datos (procedimientos almacenados y disparadores)

<details><summary>Respuesta</summary>

**Correcta: C) De forma ambigua, repartida entre el cliente y el servidor de datos (procedimientos almacenados y disparadores)** Esta ambigüedad es precisamente lo que resuelve el modelo de 3 capas al introducir un lugar único y claro para la lógica de negocio.

*Referencia: §3.1 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 16

**¿Qué tema del temario desarrolla en detalle los procedimientos almacenados y disparadores que en 2-Tier concentran lógica en el servidor de datos?**

A) El Tema 19 (lenguajes de interrogación de bases de datos, ANSI SQL, procedimientos almacenados y disparadores)
B) El Tema 24 (desarrollo para dispositivos móviles)
C) El Tema 33 (comunicaciones y medios de transmisión)

<details><summary>Respuesta</summary>

**Correcta: A) El Tema 19 (lenguajes de interrogación de bases de datos, ANSI SQL, procedimientos almacenados y disparadores)** Es una referencia cruzada explícita señalada en el §3.1 de este tema.

*Referencia: §3.1 [REFERENCIA CRUZADA]*
</details>

---

### Pregunta 17

**¿Cuál es la ventaja arquitectónica central de introducir el servidor de aplicaciones en el modelo de 3 capas?**

A) Eliminar por completo la necesidad de una base de datos
B) El desacoplamiento: el cliente ya no conoce el esquema de datos, solo el contrato que expone la capa de negocio
C) Reducir a la mitad el número de líneas de código del cliente

<details><summary>Respuesta</summary>

**Correcta: B) El desacoplamiento: el cliente ya no conoce el esquema de datos, solo el contrato que expone la capa de negocio** Cambiar el modelo de datos, o incluso el motor de base de datos, no debería requerir tocar el cliente.

*Referencia: §3.2 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 18

**Además del desacoplamiento, ¿qué mejora de rendimiento aporta el servidor de aplicaciones frente a que cada cliente se conecte directamente al SGBD (como en 2-Tier)?**

A) Elimina por completo la necesidad de autenticación
B) Convierte automáticamente el SGBD relacional en NoSQL
C) Puede agrupar y reutilizar conexiones a la base de datos mediante un pool de conexiones, en lugar de que cada cliente mantenga la suya propia

<details><summary>Respuesta</summary>

**Correcta: C) Puede agrupar y reutilizar conexiones a la base de datos mediante un pool de conexiones, en lugar de que cada cliente mantenga la suya propia** El número de conexiones concurrentes al SGBD es un recurso finito, y esto mejora sustancialmente la escalabilidad.

*Referencia: §3.2*
</details>

---

### Pregunta 19

**¿Qué distingue una "capa lógica" (layer) de un "nivel físico" (tier)?**

A) La capa lógica es una agrupación de responsabilidades en el diseño (presentación, negocio, datos); el nivel físico es la máquina o proceso donde se despliega — no siempre coinciden en número
B) Son sinónimos exactos y siempre coinciden en número
C) El nivel físico siempre es menor en número que las capas lógicas

<details><summary>Respuesta</summary>

**Correcta: A) La capa lógica es una agrupación de responsabilidades en el diseño (presentación, negocio, datos); el nivel físico es la máquina o proceso donde se despliega — no siempre coinciden en número** Una aplicación con 3 capas lógicas puede desplegarse en 5 o más niveles físicos en producción.

*Referencia: §3.3 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 20

**En producción, la Sede Electrónica del Ayuntamiento reparte peticiones entre varias instancias del servidor de aplicaciones mediante un balanceador, y usa una capa de caché para el callejero antes de llegar al clúster de base de datos. ¿Cuántas capas lógicas y niveles físicos hay, respectivamente?**

A) 3 capas lógicas y exactamente 3 niveles físicos
B) 3 capas lógicas y bastantes más de 3 niveles físicos
C) 1 capa lógica y 1 nivel físico

<details><summary>Respuesta</summary>

**Correcta: B) 3 capas lógicas y bastantes más de 3 niveles físicos** Presentación, negocio y datos son las 3 capas lógicas clásicas, desplegadas sobre balanceador, varias instancias de aplicación, caché y clúster de datos.

*Referencia: §3.3 [EJEMPLO AYTO MADRID]*
</details>

---

### Pregunta 21

**Comparando 2-Tier, 3-Tier y n-Tier, ¿qué modelo ofrece mayor escalabilidad y mayor complejidad operativa simultáneamente?**

A) 2-Tier
B) Ninguno de los tres modelos es más complejo que otro
C) n-Tier, al permitir escalado horizontal en cada nivel a costa de mayor complejidad de operación

<details><summary>Respuesta</summary>

**Correcta: C) n-Tier, al permitir escalado horizontal en cada nivel a costa de mayor complejidad de operación** 2-Tier tiene escalabilidad limitada y baja complejidad; n-Tier invierte ese equilibrio.

*Referencia: §3.4*
</details>

---

### Pregunta 22

**¿Qué caso de uso típico corresponde mejor a una arquitectura de 2-Tier?**

A) Aplicaciones departamentales pequeñas o herramientas internas con pocos usuarios concurrentes en red local
B) Sistemas de alta disponibilidad e integración masiva con terceros
C) APIs públicas consumidas por millones de usuarios simultáneos

<details><summary>Respuesta</summary>

**Correcta: A) Aplicaciones departamentales pequeñas o herramientas internas con pocos usuarios concurrentes en red local** Es donde su sencillez conceptual y buen rendimiento en LAN compensan sus limitaciones de escalabilidad.

*Referencia: §3.4*
</details>

---

### Pregunta 23

**¿Cuáles son las dos reglas estructurales de la arquitectura multicapa?**

A) Máxima velocidad de red y mínimo número de servidores
B) Encapsulación (cada capa oculta su implementación tras una interfaz) y dependencia unidireccional (de arriba hacia abajo)
C) Uso obligatorio de XML y prohibición de JSON

<details><summary>Respuesta</summary>

**Correcta: B) Encapsulación (cada capa oculta su implementación tras una interfaz) y dependencia unidireccional (de arriba hacia abajo)** Permiten sustituir una capa sin afectar a las demás, siempre que el contrato entre capas se respete.

*Referencia: §4.1 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 24

**¿Cuál es la responsabilidad exclusiva de la capa de presentación?**

A) Calcular la liquidación de una tasa municipal
B) Almacenar de forma duradera el estado de la aplicación
C) La interacción con el usuario: recoger entrada, mostrar resultados y validar el formato superficial de los datos, sin lógica de negocio

<details><summary>Respuesta</summary>

**Correcta: C) La interacción con el usuario: recoger entrada, mostrar resultados y validar el formato superficial de los datos, sin lógica de negocio** Su única responsabilidad es traducir entre el modelo interno y lo que percibe el usuario.

*Referencia: §4.2*
</details>

---

### Pregunta 25

**Un ciudadano presenta una solicitud de licencia de obra. ¿Qué capa decide si la documentación aportada cumple los requisitos normativos para admitir a trámite la solicitud?**

A) La capa de lógica de negocio, porque esa decisión depende de la normativa urbanística vigente, no de la tecnología de la interfaz
B) La capa de presentación, mediante validación de formato de campos
C) La capa de acceso a datos, al ejecutar la consulta SQL

<details><summary>Respuesta</summary>

**Correcta: A) La capa de lógica de negocio, porque esa decisión depende de la normativa urbanística vigente, no de la tecnología de la interfaz** La capa de presentación solo puede hacer validaciones superficiales (campo obligatorio, tamaño de fichero).

*Referencia: §4.3 [EJERCICIO RESUELTO]*
</details>

---

### Pregunta 26

**¿Qué responsabilidad tiene la capa de acceso a datos frente a la capa de negocio?**

A) Decidir si un usuario tiene permiso para realizar una acción de negocio
B) Leer/escribir el estado persistente y traducir entre el modelo de la capa de negocio y el modelo de almacenamiento, sin exponer el esquema interno
C) Renderizar la interfaz gráfica del usuario final

<details><summary>Respuesta</summary>

**Correcta: B) Leer/escribir el estado persistente y traducir entre el modelo de la capa de negocio y el modelo de almacenamiento, sin exponer el esquema interno** El diseño concreto de esta capa es objeto de los Temas 15, 16 y 17.

*Referencia: §4.4 [REFERENCIA CRUZADA]*
</details>

---

### Pregunta 27

**En el flujo de procesamiento de una petición en arquitectura multicapa, ¿en qué sentido viaja la petición y en qué sentido la respuesta?**

A) Ambas viajan siempre de abajo hacia arriba
B) La petición salta directamente de presentación a datos, sin pasar por negocio
C) La petición viaja de arriba hacia abajo (presentación→negocio→datos); la respuesta, de abajo hacia arriba, por el mismo camino en sentido inverso

<details><summary>Respuesta</summary>

**Correcta: C) La petición viaja de arriba hacia abajo (presentación→negocio→datos); la respuesta, de abajo hacia arriba, por el mismo camino en sentido inverso** En ningún punto la capa de datos invoca directamente a la de presentación.

*Referencia: §4.5*
</details>

---

### Pregunta 28

**¿Cuál de las siguientes situaciones constituye una violación de la regla de dependencia unidireccional en arquitectura multicapa?**

A) La capa de acceso a datos invoca directamente a la capa de presentación para notificar un cambio
B) La capa de presentación llama a la capa de negocio
C) La capa de negocio llama a la capa de acceso a datos

<details><summary>Respuesta</summary>

**Correcta: A) La capa de acceso a datos invoca directamente a la capa de presentación para notificar un cambio** Es el antipatrón más citado en exámenes de este bloque: las dependencias deben fluir siempre en una única dirección.

*Referencia: §4.1 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 29

**¿Qué beneficio en escalabilidad aporta el desacoplamiento entre capas de una arquitectura multicapa?**

A) Obliga a escalar siempre las tres capas a la vez, en la misma proporción
B) Se puede escalar de forma independiente la capa que más lo necesite, sin tocar las demás
C) Elimina por completo la necesidad de un servidor de base de datos

<details><summary>Respuesta</summary>

**Correcta: B) Se puede escalar de forma independiente la capa que más lo necesite, sin tocar las demás** Si el cuello de botella está en presentación, se añaden instancias de esa capa sin tocar la de datos, y viceversa.

*Referencia: §4.6*
</details>

---

### Pregunta 30

**¿Por qué no se debe confiar en la validación del lado cliente como mecanismo de seguridad?**

A) Porque el navegador nunca ejecuta JavaScript
B) Porque HTTPS lo impide técnicamente
C) Porque un cliente ligero es manipulable por el propio usuario (herramientas de desarrollador, peticiones directas a la API); la validación autoritativa debe repetirse siempre en el servidor

<details><summary>Respuesta</summary>

**Correcta: C) Porque un cliente ligero es manipulable por el propio usuario (herramientas de desarrollador, peticiones directas a la API); la validación autoritativa debe repetirse siempre en el servidor** Centralizar la seguridad en la capa de negocio evita que dependa de un cliente que el usuario controla.

*Referencia: §4.6 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 31

**¿Qué es un "servicio", en sentido arquitectónico?**

A) Una unidad de funcionalidad autocontenida, con interfaz explícita y débilmente acoplada, que puede ser descubierta e invocada por distintos consumidores
B) Un sinónimo exacto de "clase Java"
C) Un fichero de configuración XML sin comportamiento

<details><summary>Respuesta</summary>

**Correcta: A) Una unidad de funcionalidad autocontenida, con interfaz explícita y débilmente acoplada, que puede ser descubierta e invocada por distintos consumidores** La motivación de fondo es la reutilización funcional: exponer la lógica una vez, en lugar de duplicarla en cada aplicación.

*Referencia: §5.1 [ERL-SOA]*
</details>

---

### Pregunta 32

**¿Qué es SOA (Service-Oriented Architecture)?**

A) Un protocolo de red concreto equivalente a HTTP
B) Un estilo arquitectónico que estructura un sistema como un conjunto de servicios débilmente acoplados que se comunican mediante contratos explícitos
C) Una marca comercial de un fabricante de software

<details><summary>Respuesta</summary>

**Correcta: B) Un estilo arquitectónico que estructura un sistema como un conjunto de servicios débilmente acoplados que se comunican mediante contratos explícitos** No es una tecnología concreta; los servicios web son su implementación más habitual, pero no la única.

*Referencia: §5.2 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 33

**¿Cuál de los siguientes NO es uno de los principios de diseño de SOA?**

A) Bajo acoplamiento
B) Contrato explícito
C) Dependencia obligatoria de un único lenguaje de programación para todos los servicios

<details><summary>Respuesta</summary>

**Correcta: C) Dependencia obligatoria de un único lenguaje de programación para todos los servicios** SOA persigue justamente lo contrario: interoperabilidad entre servicios implementados en tecnologías distintas, gracias a la abstracción del contrato.

*Referencia: §5.2 [ERL-SOA]*
</details>

---

### Pregunta 34

**¿Qué diferencia principal se señala entre SOA "clásico" y los microservicios (§7.1)?**

A) SOA tiende a compartir infraestructura común (bus de servicios empresarial, ESB); los microservicios enfatizan la autonomía total, incluida a menudo la de los datos
B) Los microservicios no usan nunca HTTP
C) SOA es posterior cronológicamente a los microservicios

<details><summary>Respuesta</summary>

**Correcta: A) SOA tiende a compartir infraestructura común (bus de servicios empresarial, ESB); los microservicios enfatizan la autonomía total, incluida a menudo la de los datos** Los microservicios se presentan como una evolución o reinterpretación radical de los principios SOA.

*Referencia: §5.2 [REFERENCIA CRUZADA]*
</details>

---

### Pregunta 35

**¿Qué garantiza a un servicio web su "interoperabilidad" entre sistemas de tecnologías distintas?**

A) Que todos los sistemas involucrados usen la misma base de datos física
B) El uso de protocolos y formatos estándar y abiertos (HTTP, XML/JSON), independientes de un lenguaje o fabricante concreto
C) Que el servicio se ejecute exclusivamente en la nube

<details><summary>Respuesta</summary>

**Correcta: B) El uso de protocolos y formatos estándar y abiertos (HTTP, XML/JSON), independientes de un lenguaje o fabricante concreto** Un cliente Java puede así invocar un servicio implementado en Python sin conflicto.

*Referencia: §5.3 [W3C-SOAP]*
</details>

---

### Pregunta 36

**¿Cuál de las siguientes NO es una característica definitoria de un servicio web?**

A) Interoperabilidad
B) Uso de protocolos y formatos estándar
C) Acoplamiento fuerte obligatorio entre consumidor e implementación interna del proveedor

<details><summary>Respuesta</summary>

**Correcta: C) Acoplamiento fuerte obligatorio entre consumidor e implementación interna del proveedor** Es justo lo contrario: un servicio web se caracteriza por el débil acoplamiento — el consumidor solo conoce el contrato público, no la implementación.

*Referencia: §5.3*
</details>

---

### Pregunta 37

**¿Qué estructura formal define la especificación de un mensaje SOAP?**

A) Un "sobre" (envelope) en XML, con cabecera (metadatos) y cuerpo (datos de la operación)
B) Un objeto JSON con una única clave "data"
C) Un fichero binario propietario sin especificación pública

<details><summary>Respuesta</summary>

**Correcta: A) Un "sobre" (envelope) en XML, con cabecera (metadatos) y cuerpo (datos de la operación)** La cabecera puede transportar extensiones WS-* (seguridad, transacciones); el cuerpo, la operación invocada.

*Referencia: §5.4.1 [W3C-SOAP]*
</details>

---

### Pregunta 38

**¿Cómo describe REST los recursos que expone un servicio, frente al modelo de "operaciones nombradas" de SOAP?**

A) Mediante procedimientos remotos con nombres arbitrarios sin relación con HTTP
B) Mediante URIs que identifican recursos, manipulados con los verbos estándar de HTTP
C) Mediante ficheros WSDL obligatorios

<details><summary>Respuesta</summary>

**Correcta: B) Mediante URIs que identifican recursos, manipulados con los verbos estándar de HTTP** REST no es un protocolo de mensajería como SOAP, sino un estilo arquitectónico que aprovecha las capacidades ya existentes de HTTP.

*Referencia: §5.4.2 [FIELDING]*
</details>

---

### Pregunta 39

**En el caso de referencia, el sistema de Tributos, heredado, expone su lógica de liquidación mediante SOAP con WSDL formal, mientras que la nueva capa de negocio de la Sede expone hacia el navegador una API REST en JSON. ¿Qué principio arquitectónico ilustra esta convivencia?**

A) Que REST siempre sustituye a SOAP en cualquier escenario
B) Que SOAP y REST son técnicamente idénticos y solo cambia el nombre
C) Que ambos estilos conviven en la misma arquitectura, cada uno donde mejor encaja: SOAP en integración estable y crítica, REST en clientes web/móviles modernos

<details><summary>Respuesta</summary>

**Correcta: C) Que ambos estilos conviven en la misma arquitectura, cada uno donde mejor encaja: SOAP en integración estable y crítica, REST en clientes web/móviles modernos** SOAP no está "muerto"; sigue siendo el estándar de facto en integraciones que requieren garantías formales fuertes.

*Referencia: §5.4.2 [EJEMPLO AYTO MADRID]*
</details>

---

### Pregunta 40

**¿Qué elementos componen una petición/respuesta HTTP?**

A) Método (verbo), cabeceras, cuerpo y, en la respuesta, un código de estado de tres dígitos
B) Únicamente una URL, sin ningún otro dato
C) Un certificado X.509 obligatorio en toda petición, incluso sin HTTPS

<details><summary>Respuesta</summary>

**Correcta: A) Método (verbo), cabeceras, cuerpo y, en la respuesta, un código de estado de tres dígitos** HTTP es el protocolo de aplicación que sirve de transporte a la inmensa mayoría de los servicios web.

*Referencia: §6.1 [RFC9110]*
</details>

---

### Pregunta 41

**¿Qué diferencia hay entre los códigos de estado HTTP 401 y 403?**

A) 401 significa "recurso no encontrado" y 403 significa "error del servidor"
B) 401 (Unauthorized) indica que el cliente no está autenticado o su autenticación no es válida; 403 (Forbidden) indica que está autenticado pero no tiene permiso para esa acción
C) Ambos códigos son sinónimos exactos y pueden usarse indistintamente

<details><summary>Respuesta</summary>

**Correcta: B) 401 (Unauthorized) indica que el cliente no está autenticado o su autenticación no es válida; 403 (Forbidden) indica que está autenticado pero no tiene permiso para esa acción** Es una de las confusiones más explotadas en preguntas tipo test de este bloque.

*Referencia: §6.1 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 42

**¿Qué garantías aporta TLS a una conexión HTTPS?**

A) Ninguna: HTTPS es idéntico a HTTP salvo por el puerto usado
B) Solo velocidad de transferencia, sin relación con la seguridad
C) Confidencialidad (cifrado del contenido), integridad (detección de alteraciones) y autenticación del servidor mediante certificado X.509

<details><summary>Respuesta</summary>

**Correcta: C) Confidencialidad (cifrado del contenido), integridad (detección de alteraciones) y autenticación del servidor mediante certificado X.509** HTTPS no es un protocolo distinto de HTTP, sino HTTP transportado sobre una conexión cifrada con TLS.

*Referencia: §6.1 [RFC8446]*
</details>

---

### Pregunta 43

**¿Qué mejora introduce fundamentalmente HTTP/2 respecto a HTTP/1.1?**

A) La multiplexación: varias peticiones y respuestas viajan intercaladas sobre una única conexión TCP, eliminando el bloqueo de cabecera de línea a nivel de aplicación
B) Cambia por completo la semántica de los verbos HTTP (GET, POST dejan de existir)
C) Elimina la necesidad de usar códigos de estado

<details><summary>Respuesta</summary>

**Correcta: A) La multiplexación: varias peticiones y respuestas viajan intercaladas sobre una única conexión TCP, eliminando el bloqueo de cabecera de línea a nivel de aplicación** Los verbos, cabeceras y códigos de estado son los mismos en HTTP/1.1, /2 y /3.

*Referencia: §6.1 [RFC9113]*
</details>

---

### Pregunta 44

**¿Qué es OAuth 2.0?**

A) Un formato de token JSON firmado
B) Un framework de autorización delegada que permite a una aplicación acceder a un recurso en nombre del usuario sin conocer sus credenciales
C) Un algoritmo de cifrado simétrico

<details><summary>Respuesta</summary>

**Correcta: B) Un framework de autorización delegada que permite a una aplicación acceder a un recurso en nombre del usuario sin conocer sus credenciales** Distingue los roles resource owner, client, authorization server y resource server.

*Referencia: §6.2 [RFC6749]*
</details>

---

### Pregunta 45

**En el flujo de OAuth 2.0, ¿qué rol emite el token de acceso al cliente?**

A) El propio resource owner (usuario)
B) El resource server directamente, sin intermediarios
C) El authorization server, tras verificar la autorización concedida por el resource owner

<details><summary>Respuesta</summary>

**Correcta: C) El authorization server, tras verificar la autorización concedida por el resource owner** El cliente presenta después ese token al resource server para acceder al recurso protegido.

*Referencia: §6.2 [RFC6749]*
</details>

---

### Pregunta 46

**¿Qué es un JWT (JSON Web Token)?**

A) Un formato de token autocontenido, compuesto por header.payload.signature en Base64URL, cuyas reclamaciones (claims) van firmadas
B) Un protocolo de autorización alternativo a OAuth 2.0
C) Un tipo de certificado digital X.509

<details><summary>Respuesta</summary>

**Correcta: A) Un formato de token autocontenido, compuesto por header.payload.signature en Base64URL, cuyas reclamaciones (claims) van firmadas** Es autocontenido: permite verificar su validez sin consultar una base de datos central en cada petición.

*Referencia: §6.2 [RFC7519]*
</details>

---

### Pregunta 47

**¿Cuál es la relación correcta entre OAuth 2.0 y JWT?**

A) Son sinónimos: implementar JWT equivale a implementar OAuth 2.0
B) OAuth 2.0 es un framework de autorización (cómo se obtiene un token de forma segura); JWT es, con frecuencia, el formato concreto que adopta ese token
C) JWT sustituyó por completo a OAuth 2.0 desde 2020

<details><summary>Respuesta</summary>

**Correcta: B) OAuth 2.0 es un framework de autorización (cómo se obtiene un token de forma segura); JWT es, con frecuencia, el formato concreto que adopta ese token** Confundir "usar JWT" con "implementar OAuth 2.0" es un error frecuente y muy preguntado.

*Referencia: §6.2 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 48

**¿Qué diferencia principal existe entre XML y JSON como formatos de intercambio de datos?**

A) JSON solo puede transportar números, nunca texto
B) XML no permite anidar estructuras, JSON sí
C) XML es más verboso pero soporta espacios de nombres y validación robusta (XSD); JSON es más ligero y de mapeo más natural a estructuras de programación

<details><summary>Respuesta</summary>

**Correcta: C) XML es más verboso pero soporta espacios de nombres y validación robusta (XSD); JSON es más ligero y de mapeo más natural a estructuras de programación** XML domina en SOAP y estándares de Administración; JSON domina en APIs REST modernas.

*Referencia: §6.3 [W3C-XML; RFC8259]*
</details>

---

### Pregunta 49

**¿Qué es el Esquema Nacional de Interoperabilidad (ENI) en relación con XML y JSON?**

A) Un catálogo de estándares abiertos —entre ellos XML y JSON— de uso obligatorio en los sistemas de información de las Administraciones Públicas españolas
B) Un protocolo de cifrado exclusivo del Ayuntamiento de Madrid
C) Una versión obsoleta de XML sin uso actual

<details><summary>Respuesta</summary>

**Correcta: A) Un catálogo de estándares abiertos —entre ellos XML y JSON— de uso obligatorio en los sistemas de información de las Administraciones Públicas españolas** Garantiza el intercambio de información entre organismos.

*Referencia: §6.3 [ENI]*
</details>

---

### Pregunta 50

**¿Qué describe formalmente el documento WSDL de un servicio SOAP?**

A) La contraseña de acceso al servidor
B) Las operaciones que ofrece el servicio, los mensajes que espera y devuelve cada una, los tipos de datos y el endpoint de red
C) El diseño gráfico de la interfaz de usuario

<details><summary>Respuesta</summary>

**Correcta: B) Las operaciones que ofrece el servicio, los mensajes que espera y devuelve cada una, los tipos de datos y el endpoint de red** Es el contrato formal que hace posible que un consumidor genere automáticamente el código cliente.

*Referencia: §6.4 [W3C-WSDL]*
</details>

---

### Pregunta 51

**¿Cuál es la situación actual de UDDI como registro de descubrimiento de servicios?**

A) Es el estándar dominante en todas las nuevas APIs REST
B) Sustituyó completamente a WSDL desde 2015
C) Está en desuso en la práctica: su función de catálogo descubrible ha sido sustituida por catálogos de API modernos (OpenAPI/Swagger)

<details><summary>Respuesta</summary>

**Correcta: C) Está en desuso en la práctica: su función de catálogo descubrible ha sido sustituida por catálogos de API modernos (OpenAPI/Swagger)** La promesa de un registro público universal de servicios nunca llegó a adoptarse a gran escala.

*Referencia: §6.4 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 52

**¿Qué es RPC (Remote Procedure Call)?**

A) Un paradigma de comunicación en el que se invoca un procedimiento en otro espacio de direcciones como si fuera una llamada local, ocultando serialización y transporte
B) La implementación específica de Java para invocar objetos remotos
C) Un formato de fichero de configuración

<details><summary>Respuesta</summary>

**Correcta: A) Un paradigma de comunicación en el que se invoca un procedimiento en otro espacio de direcciones como si fuera una llamada local, ocultando serialización y transporte** Es el paradigma conceptual subyacente al modelo de "operaciones" de SOAP.

*Referencia: §6.5 [RFC1831]*
</details>

---

### Pregunta 53

**¿Qué relación existe entre RPC y RMI?**

A) RMI es el paradigma general; RPC es su implementación específica en Java
B) RPC es el paradigma general de invocación remota; RMI es su implementación nativa en la plataforma Java, con stubs y skeletons
C) No tienen ninguna relación conceptual entre sí

<details><summary>Respuesta</summary>

**Correcta: B) RPC es el paradigma general de invocación remota; RMI es su implementación nativa en la plataforma Java, con stubs y skeletons** RMI está limitado a comunicación entre extremos Java, a diferencia de SOAP, neutral respecto al lenguaje.

*Referencia: §6.5 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 54

**¿Qué son los microservicios?**

A) Un sinónimo exacto e intercambiable de "servicio web SOAP"
B) Un componente único y monolítico que concentra toda la lógica de una aplicación
C) Un estilo arquitectónico que estructura una aplicación como servicios pequeños, autónomos y desplegables de forma independiente, organizados en torno a una capacidad de negocio

<details><summary>Respuesta</summary>

**Correcta: C) Un estilo arquitectónico que estructura una aplicación como servicios pequeños, autónomos y desplegables de forma independiente, organizados en torno a una capacidad de negocio** Se comunican mediante mecanismos ligeros, típicamente APIs REST o mensajería asíncrona.

*Referencia: §7.1 [NEWMAN]*
</details>

---

### Pregunta 55

**¿Qué "coste" arquitectónico se asume habitualmente al adoptar microservicios frente a un monolito?**

A) Mayor complejidad operacional (observabilidad, despliegue, red entre servicios) y, con frecuencia, renuncia a la consistencia transaccional fuerte en favor de la consistencia eventual
B) Ninguno: los microservicios son estrictamente superiores en todos los aspectos
C) La imposibilidad técnica de escalar de forma independiente cada servicio

<details><summary>Respuesta</summary>

**Correcta: A) Mayor complejidad operacional (observabilidad, despliegue, red entre servicios) y, con frecuencia, renuncia a la consistencia transaccional fuerte en favor de la consistencia eventual** No son "gratis": a cambio de flexibilidad, hay que monitorizar y versionar muchos más componentes.

*Referencia: §7.1 [DATO CLAVE EXAMEN]*
</details>

---

### Pregunta 56

**¿En qué consiste el desacoplamiento que aporta la arquitectura orientada a eventos (EDA)?**

A) Obliga a que emisor y receptor se ejecuten siempre en el mismo proceso
B) Desacopla emisor y receptor en el espacio (no conocen su dirección de red mutua) y en el tiempo (el consumidor no necesita estar disponible en el instante exacto de la publicación)
C) Elimina por completo la necesidad de cualquier tipo de middleware

<details><summary>Respuesta</summary>

**Correcta: B) Desacopla emisor y receptor en el espacio (no conocen su dirección de red mutua) y en el tiempo (el consumidor no necesita estar disponible en el instante exacto de la publicación)** El productor publica un evento en un canal sin conocer quién, si alguien, lo va a consumir.

*Referencia: §7.2 [EDA-FOWLER]*
</details>

---

### Pregunta 57

**En el caso de referencia, cuando un expediente cambia a estado "resuelto", ¿qué ventaja aporta que notificaciones y estadísticas se suscriban al evento correspondiente en lugar de que la capa de negocio los invoque directamente?**

A) Ninguna: es equivalente a invocarlos directamente
B) Que el evento solo pueda ser consumido por un único sistema como máximo
C) Que un tercer sistema interesado pueda darse de alta como nuevo suscriptor sin modificar en absoluto la capa de negocio que publica el evento

<details><summary>Respuesta</summary>

**Correcta: C) Que un tercer sistema interesado pueda darse de alta como nuevo suscriptor sin modificar en absoluto la capa de negocio que publica el evento** Es la ventaja central del desacoplamiento productor-consumidor propio de EDA.

*Referencia: §7.2 [EJEMPLO AYTO MADRID]*
</details>

---

### Pregunta 58

**¿Qué distingue a un contenedor de una máquina virtual tradicional?**

A) El contenedor virtualiza a nivel de sistema operativo (namespaces/cgroups), compartiendo el núcleo con el host; la máquina virtual virtualiza el hardware completo mediante un hipervisor
B) Son términos sinónimos y completamente intercambiables
C) El contenedor requiere siempre más tiempo de arranque que una máquina virtual

<details><summary>Respuesta</summary>

**Correcta: A) El contenedor virtualiza a nivel de sistema operativo (namespaces/cgroups), compartiendo el núcleo con el host; la máquina virtual virtualiza el hardware completo mediante un hipervisor** Por eso un contenedor arranca en segundos, frente a los minutos de una máquina virtual.

*Referencia: §7.3 [K8S-DOCS]*
</details>

---

### Pregunta 59

**¿Qué automatiza la orquestación de contenedores (p. ej. Kubernetes)?**

A) La escritura del código fuente de la aplicación
B) El arranque, reinicio ante fallo, balanceo de carga y escalado horizontal de un gran número de contenedores desplegados
C) El diseño del modelo entidad-relación de la base de datos

<details><summary>Respuesta</summary>

**Correcta: B) El arranque, reinicio ante fallo, balanceo de carga y escalado horizontal de un gran número de contenedores desplegados** Gestionar manualmente decenas o cientos de contenedores deja de ser viable sin esta automatización.

*Referencia: §7.3 [K8S-DOCS]*
</details>

---

### Pregunta 60

**Según la definición de referencia del NIST, ¿qué caracteriza a la computación en la nube?**

A) La obligación de comprar hardware físico dedicado para cada aplicación
B) Un modelo exclusivo para aplicaciones sin ningún requisito de disponibilidad
C) El acceso bajo demanda, a través de la red, a un conjunto compartido de recursos de cómputo configurables, que pueden aprovisionarse y liberarse rápidamente con un esfuerzo mínimo de gestión

<details><summary>Respuesta</summary>

**Correcta: C) El acceso bajo demanda, a través de la red, a un conjunto compartido de recursos de cómputo configurables, que pueden aprovisionarse y liberarse rápidamente con un esfuerzo mínimo de gestión** Sus modelos de servicio (IaaS/PaaS/SaaS) y de despliegue se desarrollan en profundidad en el Tema 31.

*Referencia: §7.4 [NIST800145]*
</details>
