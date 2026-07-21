# Tema 22 — Índice

> **Título oficial**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.
>
> **Bloque**: Parte II — Técnico (Temas 11-40)
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid

---

## Estructura del tema

1. **Introducción a la arquitectura de sistemas**
   1.1. Concepto de arquitectura de sistemas
   1.2. Evolución de los modelos centralizados a los sistemas distribuidos
   1.2.1. Sistemas centralizados: mainframe y terminales tontas
   1.2.2. La revolución cliente/servidor
   1.2.3. De cliente/servidor a la computación distribuida y la nube

2. **Arquitectura cliente/servidor**
   2.1. Definición y fundamentos
   2.2. Componentes principales
   2.2.1. Cliente: cliente ligero y cliente pesado
   2.2.2. Servidor: gestión de recursos y concurrencia
   2.2.3. Middleware: conectividad y abstracción
   2.2.4. Infraestructura de comunicaciones

3. **Modelos de arquitectura cliente/servidor**
   3.1. Arquitectura de dos capas (2-Tier)
   3.2. Arquitectura de tres capas (3-Tier)
   3.3. Arquitecturas n-capas (n-Tier)
   3.4. Comparativa entre modelos

4. **Arquitecturas multicapas**
   4.1. Principios de separación de responsabilidades
   4.2. Capa de presentación
   4.3. Capa de lógica de negocio
   4.4. Capa de acceso a datos
   4.5. Flujo de procesamiento de una petición
   4.6. Beneficios en escalabilidad, mantenimiento y seguridad

5. **Arquitecturas orientadas a servicios**
   5.1. Concepto de servicio y reutilización funcional
   5.2. Arquitectura orientada a servicios (SOA)
   5.3. Servicios web: definición y características
   5.4. Tipologías de servicios web
   5.4.1. Servicios SOAP
   5.4.2. Servicios REST

6. **Protocolos y estándares asociados**
   6.1. HTTP y HTTPS
   6.2. Autenticación y autorización (OAuth 2.0 y JWT)
   6.3. XML y JSON
   6.4. SOAP, WSDL y UDDI
   6.5. RPC y RMI
   6.6. API REST y principios RESTful

7. **Tendencias actuales en arquitecturas distribuidas**
   7.1. Microservicios
   7.2. Arquitectura orientada a eventos (EDA)
   7.3. Contenedores y orquestación
   7.4. Computación en la nube

---

## Conceptos clave para memorizar

| Concepto | Dato clave |
|---|---|
| Arquitectura de sistemas | Organización de los componentes hardware/software de una aplicación y de las relaciones entre ellos y con su entorno; distinta de la arquitectura de red (cableado/topología) aunque ambas se apoyan mutuamente |
| Cliente/servidor | Modelo de cómputo distribuido en el que un proceso **cliente** solicita un servicio y un proceso **servidor** lo atiende, comunicados por red mediante un protocolo acordado |
| Cliente ligero vs pesado | El ligero (*thin client*) delega la lógica en el servidor y solo renderiza (navegador web); el pesado (*thick/fat client*) ejecuta lógica de negocio local, reduce tráfico de red pero complica el despliegue |
| Middleware | Software de conectividad entre capas/sistemas heterogéneos: oculta la complejidad de red, ofrece servicios transversales (transacciones, colas, seguridad) — ejemplos: ORB CORBA, MOM (JMS/MQ), ODBC/JDBC |
| 2-Tier vs 3-Tier | En 2 capas la lógica de negocio se reparte entre cliente y BD (procedimientos almacenados), acoplando fuerte; en 3 capas la lógica vive en un servidor de aplicaciones intermedio, desacoplando presentación de datos |
| n-Tier | Generalización de 3-Tier con más niveles físicos (balanceador, caché, colas, microservicios); las capas **lógicas** no siempre coinciden con niveles **físicos** de despliegue |
| Separación de responsabilidades | Cada capa expone una interfaz y oculta su implementación (encapsulación); las dependencias fluyen en una única dirección: presentación → negocio → datos |
| SOA | Estilo arquitectónico basado en servicios reutilizables, débilmente acoplados, descubribles y con contrato explícito; anterior y más amplio que "servicios web", que es su implementación más común |
| Servicio web | Componente de software identificado por URI, cuya interfaz es descubrible/invocable mediante mensajes en formatos estándar (XML/JSON) sobre protocolos de red comunes (HTTP principalmente) |
| SOAP vs REST | SOAP es un **protocolo** con envoltura XML, contrato formal (WSDL) y extensiones WS-* (seguridad, transacciones); REST es un **estilo arquitectónico** sobre HTTP orientado a recursos, sin contrato obligatorio, con JSON como formato dominante |
| Restricciones REST | Cliente-servidor, sin estado (*stateless*), cacheable, interfaz uniforme, sistema en capas, código bajo demanda (opcional) — definidas por Fielding en su tesis de 2000 |
| Nivel de madurez de Richardson | 0 (RPC sobre HTTP) → 1 (recursos) → 2 (verbos HTTP + códigos de estado) → 3 (HATEOAS, hipermedia como motor del estado de la aplicación) |
| HTTP vs HTTPS | HTTPS = HTTP sobre TLS: cifrado del canal, integridad y autenticación del servidor (y opcionalmente del cliente) mediante certificados X.509 |
| OAuth 2.0 | Framework de **autorización delegada**: un cliente obtiene un *token* de acceso sin conocer las credenciales del usuario, mediante un servidor de autorización y distintos *grant types* |
| JWT | Formato de token autocontenido (*header.payload.signature* en Base64URL) que transporta reclamaciones (*claims*) firmadas; no es en sí un protocolo de autorización, sino un formato que OAuth 2.0/OIDC pueden usar como token |
| WSDL / UDDI | WSDL describe la interfaz de un servicio SOAP (operaciones, mensajes, *binding*, *endpoint*); UDDI es un registro para publicar y descubrir esos servicios — en la práctica, en desuso frente a catálogos de API (Swagger/OpenAPI) |
| RPC / RMI | RPC invoca procedimientos remotos como si fueran locales, ocultando la serialización y el transporte; RMI es la variante nativa de Java (objetos remotos, *stubs/skeletons*) |
| Microservicios | Evolución de SOA hacia servicios pequeños, autónomos, con base de datos propia y despliegue independiente; a cambio de flexibilidad, añaden complejidad operacional (observabilidad, consistencia eventual) |
| EDA | Arquitectura orientada a eventos: los componentes se comunican publicando y consumiendo eventos de forma asíncrona (broker de mensajería), desacoplando emisor y receptor en tiempo y espacio |
| Contenedores | Unidad de empaquetado ligera que virtualiza a nivel de SO (*namespaces*, *cgroups* en Linux), no de hardware; **orquestación** (Kubernetes) automatiza despliegue, escalado y recuperación de contenedores |
| Computación en la nube | Modelo de provisión de recursos bajo demanda (NIST SP 800-145): IaaS/PaaS/SaaS y nubes pública/privada/híbrida — desarrollado en profundidad en el Tema 31 |

---

*Tiempo estimado de estudio: 14-16 horas*
*Extensión del contenido: ~12.000 palabras · 12 diagramas SVG embebidos*
