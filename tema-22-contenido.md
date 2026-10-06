# Tema 22 — Contenido Teórico

> **Título oficial**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.
>
> **Bloque**: Parte II — Técnico
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid
> **Versión**: v1.0 — Pendiente validación
> **Fecha generación**: 2026-07-21
> **Fuentes**: Ver tema-22-fuentes.md · **Diagramas**: Ver tema-22-diagramas.md · **Cambios**: Ver tema-22-changelog.md
>
> *Extensión: ~12.000 palabras · 12 diagramas SVG embebidos · 4 tipos de callout transversales*

---

## Convenciones del documento

Este tema incluye cuatro tipos de **cajas callout** para facilitar el estudio:

> **[DATO CLAVE]** Información de alta densidad memorística.

> **[EJERCICIO RESUELTO]** Problema + solución paso a paso (elección arquitectónica razonada, diseño de una interfaz de servicio).

> **[EJEMPLO DE APLICACIÓN EN EL AYTO]** Aplicación real de la teoría al entorno municipal (Sede Electrónica, Padrón, tributos, datos abiertos).

> **[RELACIÓN CON OTROS TEMAS]** Enlace conceptual a otros temas del temario oficial.

Este tema es **agnóstico de lenguaje y plataforma**: a diferencia del Tema 21 (Java EE, donde el código Java tiene sentido porque el tema trata de esa plataforma concreta), aquí los ejemplos se expresan en los **formatos de intercambio propios del dominio** — peticiones HTTP, JSON, XML, fragmentos de WSDL — porque son los que un opositor debe reconocer con independencia de en qué lenguaje esté programado el cliente o el servidor. Las fuentes se citan con etiquetas breves tipo `[RFC9110]` o `[FIELDING, cap. 5]`; el registro completo está en `tema-22-fuentes.md`.

**Caso de referencia usado en todo el tema** (contexto Ayuntamiento de Madrid, simplificado): la **arquitectura de la Sede Electrónica municipal**, en la que un ciudadano usa un navegador (cliente ligero) para iniciar un trámite; la petición llega a un servidor de presentación que delega en una capa de negocio (API REST propia, orientada a servicios) la validación del trámite; esa capa de negocio, a su vez, se integra con sistemas municipales heredados (Padrón, Registro, Tributos) mediante **servicios web** —algunos SOAP por antigüedad, otros REST de nueva construcción— y con un **bus de eventos** que notifica a otros departamentos cuando cambia el estado de un expediente.

---

## 1. Introducción a la arquitectura de sistemas

### 1.1. Concepto de arquitectura de sistemas

La **arquitectura de sistemas** es la organización estructural de los componentes hardware y software de una aplicación o de un conjunto de aplicaciones, junto con las **relaciones** que existen entre esos componentes y con el entorno en el que operan [FOWLER-PEAA, cap. 1]. No se trata únicamente de «dónde vive cada pieza», sino de **cómo se comunican, quién depende de quién y qué contrato respeta cada una** frente al resto.

Conviene distinguir con precisión dos nociones que se confunden con frecuencia en el lenguaje coloquial:

- **Arquitectura de sistemas** (objeto de este tema): la organización lógica de componentes software —capas, servicios, procesos— y su forma de cooperar para resolver un problema de negocio.
- **Arquitectura de red**: la topología física y lógica de los dispositivos de comunicaciones (cableado, conmutadores, encaminadores) que transportan los mensajes entre esos componentes — objeto de temas posteriores del bloque de comunicaciones (Temas 33-37).

Ambas nociones están relacionadas pero son independientes: una misma arquitectura de sistemas (por ejemplo, cliente/servidor de tres capas) puede desplegarse sobre topologías de red muy distintas, y viceversa.

> **[DATO CLAVE]** No confundir **arquitectura de sistemas** (organización de componentes software: capas, servicios) con **arquitectura de red** (topología física/lógica de dispositivos de comunicaciones).

Toda arquitectura de sistemas se diseña persiguiendo un conjunto de **atributos de calidad** (también llamados *requisitos no funcionales*), que son los que en la práctica determinan si una arquitectura es «buena» para un contexto dado: **escalabilidad** (capacidad de crecer en carga sin rediseñar), **disponibilidad** (tiempo de servicio), **mantenibilidad** (coste de modificar), **seguridad**, **rendimiento** y **interoperabilidad** (capacidad de comunicarse con sistemas de terceros mediante estándares). Este tema recorre precisamente los modelos arquitectónicos —cliente/servidor, multicapa, orientado a servicios— que la industria ha ido desarrollando para maximizar estos atributos.

### 1.2. Evolución de los modelos centralizados a los sistemas distribuidos

#### 1.2.1. Sistemas centralizados: mainframe y terminales tontas

Hasta mediados de los años 80, el modelo dominante de computación empresarial era **centralizado**: un único **mainframe** (u ordenador central) concentraba toda la capacidad de proceso, almacenamiento y lógica de aplicación. Los usuarios accedían mediante **terminales tontos** (*dumb terminals*), dispositivos sin capacidad de procesamiento propio que se limitaban a enviar pulsaciones de teclado y a mostrar el texto que el mainframe les devolvía [GARTNER-3TIER].

Este modelo tenía ventajas de gestión notables —un único punto de administración, control total sobre los datos, seguridad centralizada— pero también limitaciones estructurales: el mainframe era un **punto único de fallo**, escalar significaba comprar hardware cada vez más caro (escalado *vertical*), y la experiencia de usuario estaba limitada por el paradigma de terminal de texto.

#### 1.2.2. La revolución cliente/servidor

La popularización del **PC** (ordenador personal) y de las **redes de área local** (LAN) a finales de los 80 y principios de los 90 hizo posible un cambio de paradigma: en lugar de que toda la capacidad de proceso residiera en un único equipo central, parte de la lógica y de la interfaz de usuario podía ejecutarse en el **puesto del usuario**, mientras que los recursos compartidos (bases de datos, ficheros, impresoras) seguían gestionados por **servidores** especializados [GARTNER-3TIER; FOWLER-PEAA, cap. 1].

Nace así el modelo **cliente/servidor**, que se desarrolla en profundidad en el §2 de este tema. Este modelo democratiza el desarrollo de aplicaciones (cualquier PC puede ser un cliente), aprovecha la capacidad de proceso distribuida entre múltiples máquinas y ofrece interfaces gráficas más ricas que el terminal de texto — pero introduce también nuevos problemas: la complejidad de coordinar múltiples clientes concurrentes contra un mismo servidor, la necesidad de proteger la comunicación en red y el llamado **problema de despliegue del cliente pesado**, que se aborda en el §2.2.1.

#### 1.2.3. De cliente/servidor a la computación distribuida y la nube

La evolución no se detiene en el cliente/servidor clásico. A medida que las aplicaciones empresariales crecen en complejidad y en número de usuarios, el modelo se refina en sucesivas oleadas, cada una abordada en un apartado propio de este tema:

| Década | Modelo dominante | Tratado en |
|---|---|---|
| Años 90 | Cliente/servidor de 2 capas | §3.1 |
| Finales 90 – 2000s | Arquitecturas de 3 capas y n-capas, con servidor de aplicaciones intermedio | §3.2, §3.3 |
| 2000s | Arquitectura orientada a servicios (SOA) y servicios web | §5 |
| 2010s | Microservicios, arquitectura orientada a eventos | §7.1, §7.2 |
| 2010s-actualidad | Contenedores, orquestación y computación en la nube | §7.3, §7.4 |

> **[RELACIÓN CON OTROS TEMAS]** El **Tema 31** (paradigmas de computación distribuida y servicios en la nube: IaaS, PaaS, SaaS) desarrolla en profundidad el último eslabón de esta evolución. Este tema (22) sienta las bases arquitectónicas —cliente/servidor, capas, servicios— sobre las que se apoya todo lo que el Tema 31 trata a nivel de infraestructura de provisión.

---

## 2. Arquitectura cliente/servidor

### 2.1. Definición y fundamentos

La **arquitectura cliente/servidor** es un modelo de computación distribuida en el que las responsabilidades se reparten entre dos tipos de procesos que cooperan a través de una red:

- El **cliente** inicia la comunicación, **solicitando** un servicio o un recurso.
- El **servidor** permanece a la escucha, **atendiendo** peticiones de uno o varios clientes y devolviendo una respuesta.

Esta relación es **asimétrica**: el cliente conoce la dirección del servidor (o de un intermediario que lo localiza), pero el servidor, en el modelo clásico de petición-respuesta, no inicia comunicación por iniciativa propia hacia el cliente — solo responde a lo que se le pide [FOWLER-PEAA, cap. 1]. Este patrón de interacción se conoce como **petición-respuesta** (*request-response*) y es la base de HTTP (§6.1) y de la inmensa mayoría de los protocolos de aplicación estudiados en este tema.

Un mismo proceso puede desempeñar simultáneamente ambos roles frente a distintos interlocutores: un servidor de aplicaciones es «servidor» frente al navegador del usuario, pero actúa como «cliente» cuando consulta a un servidor de base de datos o invoca un servicio web externo. Este encadenamiento de relaciones cliente/servidor es precisamente lo que hace posible las arquitecturas multicapa del §4.

> **[DATO CLAVE]** La relación cliente/servidor es **asimétrica y basada en petición-respuesta**: el cliente inicia, el servidor responde. Un mismo componente puede ser cliente en una relación y servidor en otra — es la clave para entender por qué las arquitecturas n-capa (§3.3) son, en el fondo, **cadenas** de relaciones cliente/servidor.

### 2.2. Componentes principales

Toda arquitectura cliente/servidor, con independencia de su complejidad, se construye a partir de cuatro elementos: el cliente, el servidor, el middleware que los conecta y la infraestructura de comunicaciones que transporta los mensajes.

#### 2.2.1. Cliente: cliente ligero y pesado

El **cliente** es el proceso que solicita el servicio y, habitualmente, presenta los resultados al usuario final. Según cuánta lógica de aplicación ejecute localmente, se distinguen dos extremos de un continuo:

- **Cliente ligero** (*thin client*): concentra en el servidor casi toda la lógica de negocio y de acceso a datos; el cliente se limita a **renderizar** la interfaz y a enviar/recibir datos. El caso paradigmático es el **navegador web**, que interpreta HTML/CSS/JavaScript pero no contiene lógica de negocio propia del dominio de la aplicación.
- **Cliente pesado** (*thick client* o *fat client*): ejecuta una parte sustancial de la lógica de negocio y, a veces, mantiene una copia local de los datos; se instala y actualiza en cada puesto (aplicaciones de escritorio clásicas tipo Visual Basic/Delphi de los 90, o aplicaciones de escritorio modernas basadas en Electron o frameworks nativos).

| | Cliente ligero | Cliente pesado |
|---|---|---|
| Lógica de negocio | En el servidor | Total o parcialmente en el cliente |
| Despliegue/actualización | Centralizado, transparente al usuario | Hay que instalar/actualizar cada puesto |
| Uso de red | Mayor (cada acción implica ida y vuelta) | Menor (puede trabajar con datos locales) |
| Capacidad offline | Limitada o nula | Posible con sincronización posterior |
| Coste de mantenimiento | Bajo (un solo lugar que actualizar) | Alto (parque de puestos heterogéneo) |

> **[DATO CLAVE]** El **problema de despliegue del cliente pesado** (necesidad de instalar/actualizar software en cada puesto) fue uno de los motores históricos que impulsó la migración hacia **clientes ligeros basados en navegador** desde finales de los 90, y sigue siendo el argumento arquitectónico dominante a favor de las aplicaciones web frente a las de escritorio tradicionales.

> **[RELACIÓN CON OTROS TEMAS]** El **Tema 23** (aplicaciones web: desarrollo front-end, HTML, navegadores, lenguajes de script) desarrolla en detalle la implementación concreta del cliente ligero. El **Tema 24** (desarrollo para dispositivos móviles) trata el caso particular de clientes nativos frente a híbridos, un continuo similar entre «pesado» (app nativa) y «ligero» (web app/PWA).

#### 2.2.2. Servidor: gestión de recursos y concurrencia

El **servidor** es el proceso que posee o controla el acceso a un recurso compartido —datos, ficheros, capacidad de cómputo, un servicio de negocio— y lo pone a disposición de los clientes que lo soliciten, respetando las reglas de acceso que correspondan (autenticación, autorización, integridad).

Dos responsabilidades son propias del servidor y no tienen equivalente en el cliente clásico:

- **Gestión de recursos compartidos**: el servidor debe evitar que el acceso concurrente de varios clientes corrompa el recurso (por ejemplo, dos actualizaciones simultáneas sobre el mismo registro de una base de datos). Esto exige mecanismos de **control de concurrencia** (bloqueos, control de concurrencia optimista, transacciones).
- **Escalabilidad ante múltiples clientes**: un servidor debe atender, en el caso general, a **muchos** clientes simultáneos. Las estrategias típicas incluyen el uso de **multihilo/multiproceso** (un hilo o proceso por conexión, o un *pool* de hilos reutilizado), **E/S asíncrona no bloqueante** (un único hilo que multiplexa muchas conexiones, como en servidores basados en eventos) y, a mayor escala, el **escalado horizontal** mediante varias instancias del servidor detrás de un balanceador de carga.

> **[DATO CLAVE]** Existen dos estrategias de **escalado**: **vertical** (añadir más CPU/memoria a una misma máquina, con un límite físico y de coste) y **horizontal** (añadir más máquinas/instancias en paralelo, coordinadas por un balanceador). Las arquitecturas modernas —n-capas, microservicios, cloud— priorizan el escalado horizontal precisamente porque no tiene techo físico y permite tolerancia a fallos (si una instancia cae, las demás siguen sirviendo).

> **[EJEMPLO DE APLICACIÓN EN EL AYTO]** En días de campaña de renovación del Padrón o de plazos fiscales, el servidor de la Sede Electrónica recibe picos de tráfico muy superiores a la media. Una arquitectura que solo permita escalado vertical obligaría a sobredimensionar permanentemente el hardware (coste ocioso el resto del año); una arquitectura preparada para escalado horizontal puede añadir instancias temporales del servidor de aplicaciones solo durante el pico, y retirarlas después.

#### 2.2.3. Middleware: conectividad y abstracción

El **middleware** («software intermedio») es la capa de software que se sitúa entre el sistema operativo/red y las aplicaciones, y que **oculta la complejidad de la comunicación distribuida** ofreciendo una interfaz de más alto nivel [FOWLER-PEAA, cap. 1]. Sin middleware, cada aplicación tendría que resolver por sí misma problemas como la serialización de datos, la localización de servicios remotos, la tolerancia a fallos de red o la gestión de transacciones distribuidas.

Se distinguen varias familias de middleware según el servicio que abstraen:

| Tipo de middleware | Qué abstrae | Ejemplos |
|---|---|---|
| **Middleware de acceso a datos** | El dialecto concreto de cada SGBD | ODBC, JDBC (Tema 15) |
| **Middleware orientado a objetos** (ORB) | La invocación de métodos en objetos remotos | CORBA, Java RMI (§6.5) |
| **Middleware orientado a mensajes** (MOM) | El envío de mensajes asíncronos entre aplicaciones | JMS, RabbitMQ, Apache Kafka |
| **Middleware de servicios web** | El descubrimiento e invocación de servicios remotos mediante estándares abiertos | Contenedores SOAP, *gateways* API REST |
| **Middleware transaccional** | La coordinación de transacciones que abarcan varios recursos | Gestores de transacciones distribuidas (protocolo de *commit* en dos fases) |

> **[RELACIÓN CON OTROS TEMAS]** El middleware orientado a mensajes (MOM) es la base técnica de la **arquitectura orientada a eventos** (EDA), desarrollada en el §7.2 de este mismo tema, y de la integración asíncrona entre sistemas heredados que se ilustra en el caso de referencia de la Sede Electrónica.

#### 2.2.4. Infraestructura de comunicaciones

Por último, ningún componente cliente/servidor puede comunicarse sin una **infraestructura de comunicaciones** subyacente: la red física y lógica (cableado, conmutadores, encaminadores, direccionamiento IP) y la **pila de protocolos** que garantiza el transporte fiable de los mensajes entre cliente y servidor.

> **[RELACIÓN CON OTROS TEMAS]** La infraestructura de comunicaciones —el modelo TCP/IP y el modelo OSI, los protocolos de nivel de transporte y de red— se desarrolla en profundidad en el **Tema 34**. Este tema (22) se sitúa deliberadamente en el **nivel de aplicación** de esa pila: los protocolos que aquí se estudian (HTTP, SOAP, REST) se apoyan sobre TCP/IP sin necesidad de conocer sus detalles internos, del mismo modo que una aplicación cliente/servidor no necesita saber cómo se enruta cada paquete.

---

## 3. Modelos de arquitectura cliente/servidor

### 3.1. Arquitectura de dos capas (2-Tier)

En la arquitectura de **dos capas** (2-Tier), la aplicación se divide en exactamente dos **niveles físicos**: el **cliente**, que concentra la presentación y, con frecuencia, buena parte de la lógica de negocio, y el **servidor de base de datos**, que además de almacenar los datos suele albergar parte de la lógica mediante **procedimientos almacenados y disparadores** [GARTNER-3TIER].

Es el modelo cliente/servidor «clásico» de finales de los 80 y los 90: un cliente pesado (§2.2.1) con una interfaz gráfica de escritorio que se conecta **directamente** al SGBD mediante un *driver* (ODBC/JDBC), sin ningún componente intermedio.

**Ventajas**: sencillez conceptual, buen rendimiento cuando el número de clientes es reducido y están en la misma red local, y aprovechamiento de las capacidades transaccionales del propio SGBD.

**Inconvenientes**, que motivaron la evolución hacia el modelo de 3 capas: **acoplamiento fuerte** entre el cliente y el esquema de la base de datos (cualquier cambio en el modelo de datos obliga a tocar el cliente); **escalabilidad limitada**, porque cada cliente mantiene una conexión directa y persistente al SGBD, cuyo número de conexiones concurrentes es un recurso finito; **problema de despliegue del cliente pesado** (§2.2.1); y **seguridad más difícil de centralizar**, porque las reglas de negocio ejecutadas en el cliente son, en última instancia, manipulables por quien controla ese puesto.

> **[DATO CLAVE]** En 2 capas, la lógica de negocio se reparte de forma **ambigua** entre el cliente (código de la aplicación) y el servidor de datos (procedimientos almacenados/disparadores) — no hay un lugar único y claro donde «vive» la regla de negocio. Esta ambigüedad es precisamente lo que resuelve el modelo de 3 capas.

> **[RELACIÓN CON OTROS TEMAS]** Los **procedimientos almacenados y disparadores** que en 2 capas concentran parte de la lógica de negocio en el servidor de datos son objeto específico del **Tema 19** (lenguajes de interrogación de bases de datos, ANSI SQL, procedimientos almacenados, eventos y disparadores).

### 3.2. Arquitectura de tres capas (3-Tier)

La arquitectura de **tres capas** introduce un nivel intermedio, el **servidor de aplicaciones**, entre el cliente y el servidor de datos. Cada capa asume una responsabilidad clara y se comunica solo con la capa adyacente:

1. **Capa de presentación**: interfaz con la que interactúa el usuario (cliente ligero o pesado).
2. **Capa de lógica de negocio** (o capa de aplicación): reglas, validaciones y procesos de negocio, ejecutados en el **servidor de aplicaciones**.
3. **Capa de datos**: almacenamiento persistente, gestionado por el SGBD.

Esta separación —desarrollada con más detalle en el §4 de este tema, dedicado íntegramente a las arquitecturas multicapa— resuelve directamente los problemas del modelo de 2 capas: el cliente se **desacopla** del esquema de datos (solo conoce la interfaz que expone el servidor de aplicaciones), la lógica de negocio tiene un **lugar único y bien definido**, y el servidor de aplicaciones puede **agrupar y reutilizar conexiones** al SGBD mediante un *pool* de conexiones, en lugar de que cada cliente mantenga la suya propia — lo que mejora sustancialmente la escalabilidad.

> **[DATO CLAVE]** La ventaja arquitectónica central de pasar de 2 a 3 capas es el **desacoplamiento**: el cliente ya no conoce el esquema de la base de datos, sino únicamente el **contrato** (interfaz) que le ofrece la capa de negocio. Cambiar el modelo de datos, o incluso el motor de base de datos, no debería requerir tocar el cliente.

### 3.3. Arquitecturas n-capas (n-Tier)

Las arquitecturas **n-capas** generalizan el modelo de 3 capas añadiendo **niveles adicionales**, tanto lógicos como físicos, según las necesidades de la aplicación: un balanceador de carga delante de varios servidores de aplicaciones, una capa de caché entre la capa de negocio y la de datos, una capa de integración que habla con sistemas externos mediante servicios web, o una capa de colas de mensajes para procesamiento asíncrono.

Es fundamental distinguir dos nociones:

- **Capa lógica** (*layer*): una agrupación de responsabilidades en el diseño del software (presentación, negocio, datos, integración…), independiente de dónde se despliegue físicamente.
- **Nivel físico** (*tier*): una máquina o proceso independiente donde se despliega una o varias capas lógicas.

No siempre coinciden: una aplicación puede tener **tres capas lógicas** (presentación, negocio, datos) desplegadas en **un único nivel físico** (todo en el mismo servidor, típico de un entorno de desarrollo), o **tres capas lógicas** repartidas en **cinco niveles físicos** (balanceador + dos servidores de aplicaciones + caché + clúster de base de datos), típico de un entorno de producción de alta disponibilidad.

> **[DATO CLAVE]** *Layer* (capa lógica de responsabilidad) ≠ *Tier* (nivel físico de despliegue). El número de capas lógicas de un diseño no tiene por qué coincidir con el número de servidores físicos en los que se despliega.

> **[EJEMPLO DE APLICACIÓN EN EL AYTO]** La Sede Electrónica del Ayuntamiento, en producción, no se despliega en una única máquina: un **balanceador de carga** reparte las peticiones entre varias instancias del **servidor de aplicaciones** (capa de negocio replicada por alta disponibilidad), que a su vez consultan una **capa de caché** para las operaciones de solo lectura más frecuentes (por ejemplo, el callejero) antes de llegar al **clúster de base de datos**. Son tres capas lógicas clásicas, desplegadas en bastantes más de tres niveles físicos.

### 3.4. Comparativa entre modelos

| | 2-Tier | 3-Tier | n-Tier |
|---|---|---|---|
| Niveles físicos | 2 | 3 | 3 o más |
| Ubicación de la lógica de negocio | Ambigua (cliente + SGBD) | Servidor de aplicaciones | Servidor(es) de aplicaciones/servicios |
| Acoplamiento cliente-datos | Fuerte | Débil | Débil |
| Escalabilidad | Limitada | Buena | Alta (horizontal en cada nivel) |
| Complejidad operativa | Baja | Media | Alta |
| Caso de uso típico | Aplicaciones departamentales pequeñas, herramientas internas | Aplicaciones empresariales estándar | Sistemas de alta disponibilidad y carga, integración con terceros |

---

## 4. Arquitecturas multicapas

### 4.1. Principios de separación de responsabilidades

La **arquitectura multicapa** (o *layered architecture*) organiza el software en **capas lógicas** apiladas, cada una responsable de un aspecto concreto del sistema, con dos reglas estructurales [FOWLER-PEAA, cap. 1]:

- **Encapsulación**: cada capa expone una **interfaz** hacia la capa adyacente y oculta los detalles internos de su implementación. La capa de negocio, por ejemplo, no necesita saber si los datos vienen de una base de datos relacional o de un servicio externo.
- **Dependencia unidireccional**: las dependencias fluyen en una única dirección, típicamente **de arriba hacia abajo** (presentación depende de negocio, negocio depende de datos), nunca al revés. Una capa inferior no debe conocer ni depender de una superior.

Esta disciplina, aparentemente sencilla, es la que permite **sustituir** una capa sin afectar a las demás: cambiar la interfaz de usuario (de web a app móvil) sin tocar la lógica de negocio, o cambiar el motor de base de datos sin tocar la capa de presentación, siempre que el contrato entre capas se respete.

> **[DATO CLAVE]** Las dos reglas de la arquitectura en capas son **encapsulación** (cada capa oculta su implementación tras una interfaz) y **dependencia unidireccional** (de arriba hacia abajo, nunca al revés). Violar la segunda regla —por ejemplo, que la capa de datos invoque directamente a la de presentación— es el antipatrón más habitual.

### 4.2. Capa de presentación

La **capa de presentación** es responsable de la **interacción con el usuario**: recoger su entrada, mostrarle resultados y validar el formato de los datos introducidos (validaciones superficiales, no reglas de negocio). No debe contener lógica de negocio: su única responsabilidad es traducir entre el modelo interno de la aplicación y la interfaz que percibe el usuario.

En el caso de referencia de la Sede Electrónica, la capa de presentación es el conjunto de páginas y formularios web que el ciudadano ve en su navegador —el cliente ligero del §2.2.1— más el conjunto de controladores del lado servidor que reciben esas peticiones HTTP y las traducen a llamadas a la capa de negocio.

### 4.3. Capa de lógica de negocio

La **capa de lógica de negocio** (o capa de aplicación) contiene las **reglas del dominio**: qué trámites puede iniciar un ciudadano, qué requisitos debe cumplir un expediente para pasar de un estado a otro, cómo se calcula la liquidación de una tasa. Es el «cerebro» de la aplicación, y es la capa que debería cambiar con menor frecuencia por motivos puramente técnicos (un cambio de framework de presentación o de motor de base de datos no debería obligar a tocarla).

> **[EJERCICIO RESUELTO]** *Un ciudadano presenta una solicitud de licencia de obra a través de la Sede Electrónica. ¿Qué capa decide si la documentación aportada es suficiente para admitir a trámite la solicitud?* — La **capa de negocio**, no la de presentación. La capa de presentación puede hacer validaciones superficiales (por ejemplo, que un campo obligatorio no esté vacío, o que un fichero adjunto no supere el tamaño máximo), pero la decisión de si la documentación aportada cumple los requisitos normativos para admitir a trámite es una **regla de negocio** —depende de la normativa urbanística vigente, no de la tecnología de la interfaz— y por tanto pertenece a la capa de lógica de negocio.

### 4.4. Capa de acceso a datos

La **capa de acceso a datos** (o de persistencia) es responsable de **leer y escribir** el estado de la aplicación en un almacenamiento duradero —típicamente un SGBD relacional, aunque puede ser NoSQL, un sistema de ficheros o un servicio externo—, y de **traducir** entre el modelo de objetos/estructuras que usa la capa de negocio y el modelo de almacenamiento subyacente.

> **[RELACIÓN CON OTROS TEMAS]** El diseño concreto de esta capa —modelo entidad-relación, normalización, SGBD relacionales frente a NoSQL— es objeto de los **Temas 15, 16 y 17**. Este tema (22) se limita a situar la capa de datos como el nivel más bajo de la arquitectura multicapa, sin entrar en el diseño interno del modelo de datos.

### 4.5. Flujo de procesamiento de una petición

Un ejemplo concreto ayuda a fijar cómo cooperan las tres capas ante una única petición del usuario. Tomando el caso de referencia (un ciudadano consulta el estado de un expediente en la Sede Electrónica):

1. El **navegador** (capa de presentación, cliente) envía una petición HTTP con el identificador del expediente.
2. El **controlador** de la capa de presentación, en el servidor, recibe la petición, valida su formato (¿el identificador tiene el formato esperado?) y la traduce en una llamada a la capa de negocio.
3. La **capa de negocio** aplica las reglas pertinentes (¿tiene el usuario autenticado permiso para consultar ese expediente concreto?) y solicita los datos a la capa de acceso a datos.
4. La **capa de acceso a datos** ejecuta la consulta contra el SGBD y devuelve el resultado, ya traducido a estructuras que la capa de negocio entiende, sin exponer detalles del esquema relacional.
5. La capa de negocio aplica cualquier transformación adicional (por ejemplo, calcular un texto descriptivo del estado) y devuelve el resultado a la capa de presentación.
6. La capa de presentación formatea la respuesta (HTML o JSON, según el tipo de cliente) y la envía de vuelta al navegador.

Nótese que la petición **atraviesa las capas de arriba hacia abajo** y la respuesta las atraviesa **de abajo hacia arriba**, respetando en todo momento la regla de dependencia unidireccional del §4.1: en ningún punto la capa de datos invoca directamente a la de presentación, ni la salta.

### 4.6. Beneficios en escalabilidad, mantenimiento y seguridad

La arquitectura multicapa no es solo una cuestión de «orden»: tiene consecuencias prácticas directas sobre tres atributos de calidad clave:

- **Escalabilidad**: al estar cada capa desacoplada, se puede **escalar de forma independiente** la capa que más lo necesite. Si el cuello de botella es la capa de presentación (muchos usuarios concurrentes navegando), se añaden más instancias de esa capa sin tocar la de datos, y viceversa.
- **Mantenimiento**: un cambio localizado en una capa (por ejemplo, rediseñar la interfaz de usuario) tiene un **radio de impacto limitado** a esa capa, siempre que el contrato con las capas adyacentes se mantenga estable. Esto reduce el riesgo y el coste de las modificaciones.
- **Seguridad**: centralizar las reglas de negocio y de autorización en una única capa (la de negocio) evita que la seguridad dependa de un cliente que el usuario controla y puede manipular; la capa de presentación puede ofrecer una experiencia amigable, pero la decisión de seguridad real se toma en el servidor.

> **[DATO CLAVE]** Nunca confiar en la **validación del lado cliente** como mecanismo de seguridad: un cliente ligero (navegador) es manipulable por el propio usuario (herramientas de desarrollador, peticiones directas a la API). La validación de negocio y de seguridad **siempre** debe repetirse, de forma autoritativa, en el servidor.

---

## 5. Arquitecturas orientadas a servicios

### 5.1. Concepto de servicio y reutilización funcional

Un **servicio**, en sentido arquitectónico, es una unidad de funcionalidad **autocontenida**, con una **interfaz explícita** y **débilmente acoplada** al resto del sistema, que puede ser **descubierta e invocada** por distintos consumidores sin que estos necesiten conocer su implementación interna [ERL-SOA, cap. 2].

La motivación de fondo es la **reutilización funcional**: en lugar de que cada aplicación reimplemente su propia lógica de «calcular una liquidación de tasa» o «validar un NIF», esa lógica se expone **una vez**, como servicio, y cualquier aplicación autorizada de la organización puede consumirla, garantizando además que **todas** las aplicaciones aplican exactamente la misma regla (evitando el problema clásico de lógica de negocio duplicada e inconsistente entre sistemas).

### 5.2. Arquitectura orientada a servicios (SOA)

La **arquitectura orientada a servicios** (*Service-Oriented Architecture*, SOA) es un **estilo arquitectónico** —no una tecnología concreta— que estructura un sistema como un conjunto de **servicios** débilmente acoplados que se comunican mediante **contratos** explícitos [ERL-SOA, cap. 2-3]. Sus principios de diseño más citados son:

- **Bajo acoplamiento**: los servicios minimizan las dependencias entre sí; un cambio interno en un servicio no debería obligar a modificar a sus consumidores mientras el contrato se respete.
- **Contrato explícito**: la interfaz de un servicio (operaciones que ofrece, formato de los mensajes) se describe formalmente y es independiente de la implementación.
- **Abstracción**: el consumidor solo conoce el contrato, nunca los detalles internos (lenguaje de programación, base de datos) del proveedor del servicio.
- **Reutilización**: un servicio se diseña para ser consumido por múltiples aplicaciones, no para una única aplicación cliente.
- **Autonomía**: cada servicio controla su propia lógica y, en el diseño más maduro, sus propios datos.
- **Componibilidad** (*composability*): los servicios pueden combinarse (**orquestación** o **coreografía**) para construir procesos de negocio más complejos.

> **[DATO CLAVE]** SOA es un **estilo arquitectónico**, no un producto ni un protocolo concreto. Los **servicios web** (§5.3) son la implementación más habitual de SOA, pero no la única —conceptualmente, SOA es anterior y más amplio que «servicios web», del mismo modo que «arquitectura cliente/servidor» es anterior y más amplia que «aplicación web».

> **[RELACIÓN CON OTROS TEMAS]** Los **microservicios** (§7.1) se presentan a menudo como una evolución o una reinterpretación moderna de SOA, con matices importantes que se explican en ese apartado: mientras SOA tiende a compartir infraestructura común (un **bus de servicios empresarial**, ESB), los microservicios enfatizan la autonomía total, incluida la de los datos.

### 5.3. Servicios web: definición y características

Un **servicio web** es un servicio (§5.1) cuya interfaz está descrita en un **formato legible por máquina** (típicamente XML o, en el estilo REST, mediante las convenciones de HTTP) y que se invoca a través de **protocolos de red estándar y abiertos** —fundamentalmente HTTP— lo que garantiza **interoperabilidad** entre sistemas construidos con tecnologías distintas [W3C-SOAP; FIELDING].

Sus características definitorias son:

- **Interoperabilidad**: un cliente Java puede invocar un servicio implementado en Python, o un cliente móvil en Kotlin puede invocar un servicio en .NET, porque el contrato de comunicación se apoya en estándares abiertos, no en un mecanismo propietario de un fabricante o lenguaje concreto.
- **Uso de protocolos y formatos estándar**: HTTP como transporte, XML o JSON como formato de los datos.
- **Descubribilidad** (en mayor o menor grado según el estilo, §5.4): la interfaz del servicio puede describirse formalmente para que otros sistemas la consuman sin necesidad de conocimiento previo directo del equipo desarrollador.
- **Débil acoplamiento**: el consumidor no necesita conocer la implementación interna del servicio, solo su contrato público.

### 5.4. Tipologías de servicios web

Existen dos estilos dominantes de servicios web, con filosofías de diseño distintas: **SOAP**, orientado a operaciones y con un contrato formal estricto, y **REST**, orientado a recursos y apoyado en las propias convenciones de HTTP.

#### 5.4.1. Servicios SOAP

**SOAP** (originalmente *Simple Object Access Protocol*, aunque el acrónimo se considera hoy obsoleto y se usa simplemente como nombre propio) es un **protocolo de mensajería** basado en **XML**, independiente del protocolo de transporte subyacente (aunque en la práctica se usa casi siempre sobre HTTP) [W3C-SOAP]. Un mensaje SOAP tiene una estructura formal en forma de **sobre** (*envelope*):

```xml
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
  <soap:Header>
    <!-- metadatos: seguridad (WS-Security), transacción, correlación -->
  </soap:Header>
  <soap:Body>
    <ConsultarExpediente xmlns="http://sede.madrid.es/tributos">
      <NumeroExpediente>EXP-2026-004821</NumeroExpediente>
    </ConsultarExpediente>
  </soap:Body>
</soap:Envelope>
```

Sus rasgos característicos son un **contrato formal y estricto**, descrito en WSDL (§6.4); un modelo de **operaciones nombradas** (RPC-like: `ConsultarExpediente`, `LiquidarTasa`) frente al modelo orientado a recursos de REST; y un ecosistema de extensiones estandarizadas conocido como **WS-\*** (WS-Security para seguridad a nivel de mensaje, WS-ReliableMessaging para entrega garantizada, WS-AtomicTransaction para transacciones distribuidas), que lo hacen especialmente robusto en escenarios empresariales exigentes —integración bancaria, sistemas de pago, transacciones distribuidas entre organismos— a cambio de mayor complejidad y verbosidad.

> **[DATO CLAVE]** SOAP no está «muerto»: sigue siendo el estándar de facto en integraciones empresariales que requieren **garantías formales fuertes** (transacciones distribuidas, seguridad a nivel de mensaje, contratos estrictos), típicas de banca, seguros y de muchos sistemas heredados de la Administración Pública. REST domina en APIs públicas y en aplicaciones web/móviles modernas, pero no ha sustituido a SOAP en todos los escenarios.

#### 5.4.2. Servicios REST

**REST** (*Representational State Transfer*) no es un protocolo, sino un **estilo arquitectónico** definido por Roy Fielding en su tesis doctoral de 2000, que aprovecha las capacidades ya existentes de **HTTP** en lugar de construir un protocolo de mensajería propio [FIELDING, cap. 5]. Un servicio REST expone **recursos** (identificados por una URI) que se manipulan mediante los **verbos HTTP** estándar:

```http
GET /api/expedientes/EXP-2026-004821 HTTP/1.1
Host: sede.madrid.es
Accept: application/json
```

```json
{
  "numeroExpediente": "EXP-2026-004821",
  "tipo": "licencia-obra",
  "estado": "en_tramitacion",
  "fechaAlta": "2026-06-02"
}
```

Este estilo se desarrolla con detalle en el §6.6 (API REST y principios RESTful), junto con las restricciones formales que definen a un sistema como «RESTful». La comparativa directa entre ambos estilos se resume en la siguiente tabla:

| | SOAP | REST |
|---|---|---|
| Naturaleza | Protocolo de mensajería | Estilo arquitectónico |
| Formato de datos | XML (estricto) | JSON habitual, también XML u otros |
| Modelo | Orientado a operaciones (RPC-like) | Orientado a recursos (URIs + verbos HTTP) |
| Contrato | Formal y obligatorio (WSDL) | Opcional, por convención (OpenAPI/Swagger) |
| Transporte | Independiente en teoría, HTTP en la práctica | HTTP de forma intrínseca |
| Seguridad avanzada | WS-Security (a nivel de mensaje) | OAuth 2.0/JWT (§6.2), TLS (a nivel de transporte) |
| Peso de los mensajes | Mayor (envoltorio XML) | Menor (JSON compacto) |
| Escenario típico | Integración empresarial crítica, sistemas heredados | APIs públicas, aplicaciones web/móviles |

> **[EJEMPLO DE APLICACIÓN EN EL AYTO]** En el caso de referencia de la Sede Electrónica, el sistema de **Tributos**, heredado y construido hace más de una década, expone su lógica de liquidación mediante un servicio **SOAP** con WSDL formal (integración estable y crítica, con garantías transaccionales). La nueva capa de negocio de la Sede, en cambio, expone hacia el navegador y hacia aplicaciones móviles una **API REST** en JSON, más ligera y natural para clientes web modernos. Ambos estilos conviven en la misma arquitectura, cada uno donde mejor encaja.

---

## 6. Protocolos y estándares asociados

### 6.1. HTTP y HTTPS

**HTTP** (*Hypertext Transfer Protocol*) es el protocolo de nivel de aplicación que sirve de transporte a la inmensa mayoría de los servicios web —tanto SOAP como REST— y es, en sí mismo, un ejemplo canónico de protocolo cliente/servidor de petición-respuesta [RFC9110]. Sus elementos esenciales son:

- **Método** (o verbo): indica la acción que se solicita sobre un recurso (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`, entre otros; desarrollados en el §6.6 en su uso RESTful).
- **Cabeceras** (*headers*): metadatos de la petición o la respuesta (tipo de contenido, autenticación, caché).
- **Cuerpo** (*body*): los datos de la petición o la respuesta, en el formato que indique la cabecera `Content-Type` (JSON, XML, etc.).
- **Código de estado**: un número de tres dígitos que resume el resultado de la petición, agrupado por familias:

| Familia | Significado | Ejemplos |
|---|---|---|
| **1xx** | Informativa | `100 Continue` |
| **2xx** | Éxito | `200 OK`, `201 Created`, `204 No Content` |
| **3xx** | Redirección | `301 Moved Permanently`, `304 Not Modified` |
| **4xx** | Error del cliente | `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found` |
| **5xx** | Error del servidor | `500 Internal Server Error`, `503 Service Unavailable` |

> **[DATO CLAVE]** Distinguir bien **401 Unauthorized** (el cliente no está autenticado, o su autenticación no es válida) de **403 Forbidden** (el cliente está autenticado, pero no tiene permiso para esa acción concreta).

**HTTPS** no es un protocolo distinto de HTTP, sino **HTTP transportado sobre una conexión cifrada con TLS** (*Transport Layer Security*) [RFC9846]. TLS aporta tres garantías sobre el canal de comunicación: **confidencialidad** (el contenido viaja cifrado, ilegible para un tercero que intercepte el tráfico), **integridad** (cualquier alteración del mensaje en tránsito es detectable) y **autenticación del servidor** (mediante un **certificado digital X.509**, el cliente verifica que se está comunicando realmente con el servidor que dice ser, no con un impostor).

> **[RELACIÓN CON OTROS TEMAS]** El **Tema 35** (Internet: arquitectura de red, protocolos HTTP, HTTPS y SSL/TLS) desarrolla en profundidad el propio protocolo TLS —el proceso de negociación (*handshake*), las versiones históricas SSL/TLS y su papel en la pila de comunicaciones de Internet. Este tema (22) sitúa HTTP/HTTPS como el **protocolo de aplicación** sobre el que se construyen los servicios web, sin entrar en el detalle del cifrado. El **Tema 32** (seguridad de los sistemas de información: técnicas criptográficas, firma digital) completa la base criptográfica que sustenta TLS y la firma de tokens JWT (§6.2).

El propio protocolo HTTP ha evolucionado en varias versiones, relevantes para entender el rendimiento de los servicios web actuales: **HTTP/1.1** [RFC9112], vigente desde 1997 y aún el más extendido, procesa las peticiones de una conexión de forma esencialmente secuencial, lo que en páginas o APIs con muchas peticiones simultáneas provoca el problema conocido como *head-of-line blocking* (una petición lenta bloquea a las que la siguen en la misma conexión). **HTTP/2** [RFC9113] introduce la **multiplexación**: varias peticiones y respuestas viajan intercaladas sobre una **única conexión TCP**, eliminando ese bloqueo a nivel de aplicación y reduciendo la sobrecarga de abrir múltiples conexiones. **HTTP/3** [RFC9114] da un paso más y sustituye el transporte TCP por **QUIC** (sobre UDP), eliminando también el *head-of-line blocking* que persistía a nivel de transporte en HTTP/2 y acelerando la reconexión tras una pérdida de red — un cambio orientado especialmente a clientes móviles con conectividad inestable.

> **[DATO CLAVE]** La evolución HTTP/1.1 → HTTP/2 → HTTP/3 es, sobre todo, una evolución de **rendimiento del transporte** (multiplexación, menos bloqueo, menor latencia de reconexión), no un cambio en la semántica de la aplicación: los verbos, las cabeceras y los códigos de estado estudiados en este apartado son **los mismos** en las tres versiones [RFC9110].

### 6.2. Autenticación y autorización (OAuth 2.0 y JWT)

En una arquitectura de servicios distribuidos, resolver **quién es el usuario** (autenticación) y **qué puede hacer** (autorización) de forma segura y escalable es uno de los problemas de diseño más recurrentes. Dos estándares dominan hoy este espacio en el mundo de los servicios web:

**OAuth 2.0** [RFC6749] es un *framework* de **autorización delegada**: permite que una aplicación (el *cliente*) acceda a un recurso protegido en nombre de un usuario, **sin que la aplicación llegue a conocer las credenciales** del usuario (su contraseña). El flujo típico distingue varios roles —*resource owner* (el usuario), *client* (la aplicación que solicita acceso), *authorization server* (quien emite los *tokens*) y *resource server* (quien protege el recurso)— y se apoya en distintos **tipos de concesión** (*grant types*) según el escenario: código de autorización (aplicaciones web con backend), credenciales de cliente (comunicación servicio-a-servicio, sin usuario humano de por medio), entre otros.

**JWT** (*JSON Web Token*) [RFC7519] es un **formato** de token —no un protocolo de autorización en sí mismo— compuesto por tres partes codificadas en Base64URL y separadas por puntos: `header.payload.signature`. El *payload* contiene **reclamaciones** (*claims*): datos sobre el sujeto del token (identificador de usuario, roles, fecha de expiración), y la *signature* permite verificar que el token no ha sido alterado desde que se emitió, sin necesidad de consultar una base de datos central en cada petición (el token es **autocontenido**).

```
eyJhbGciOiJIUzI1NiJ9.        ← header (algoritmo de firma)
eyJzdWIiOiIxMjM0Iiwicm9sIjoiY2l1ZGFkYW5vIn0.  ← payload (claims: sub, rol…)
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c  ← signature
```

> **[DATO CLAVE]** OAuth 2.0 es un **framework de autorización**; JWT es un **formato de token**. No son alternativas entre sí ni sinónimos: OAuth 2.0 define **cómo se obtiene** un token de forma segura; JWT es, muy a menudo, **el formato concreto** que adopta ese token. Confundir «usar JWT» con «implementar OAuth 2.0» es un error frecuente.

> **[RELACIÓN CON OTROS TEMAS]** El **Tema 32** (conceptos de seguridad de los sistemas de información: técnicas criptográficas y mecanismos de firma digital) desarrolla el fundamento criptográfico —firma digital, funciones *hash*, criptografía asimétrica— que hace posible verificar la *signature* de un JWT sin contactar al emisor en cada petición.

### 6.3. XML y JSON

**XML** (*eXtensible Markup Language*) [W3C-XML] es un formato de marcado **extensible y autodescriptivo**, basado en etiquetas anidadas, que fue durante años el formato dominante de intercambio de datos entre sistemas —y sigue siendo obligatorio en SOAP (§5.4.1) y en muchos estándares de la Administración Pública—. **JSON** (*JavaScript Object Notation*) [RFC8259] es un formato más ligero, basado en pares clave-valor y estructuras anidadas de objetos y listas, que se ha convertido en el formato dominante de las APIs REST modernas por su menor verbosidad y su mapeo natural a las estructuras de datos de la mayoría de los lenguajes de programación.

```xml
<expediente>
  <numero>EXP-2026-004821</numero>
  <estado>en_tramitacion</estado>
</expediente>
```
```json
{"numero": "EXP-2026-004821", "estado": "en_tramitacion"}
```

| | XML | JSON |
|---|---|---|
| Verbosidad | Alta (etiquetas de apertura/cierre) | Baja |
| Esquema/validación | Robusta (XSD) | Más ligera (JSON Schema) |
| Espacios de nombres | Sí (permite mezclar vocabularios) | No de forma nativa |
| Uso dominante | SOAP, documentos estructurados complejos, estándares Administración | APIs REST, configuración, intercambio ligero |

> **[RELACIÓN CON OTROS TEMAS]** El **Esquema Nacional de Interoperabilidad** (ENI, desarrollado en el **Tema 39**) recoge un catálogo de estándares abiertos —entre ellos XML y JSON— de uso obligatorio en los sistemas de información de las Administraciones Públicas españolas para garantizar el intercambio de información entre organismos [ENI].

### 6.4. SOAP, WSDL y UDDI

Completando la tríada de estándares clásicos del ecosistema de servicios web «pesados»:

- **SOAP** (§5.4.1): el protocolo de mensajería.
- **WSDL** (*Web Services Description Language*) [W3C-WSDL]: el documento XML que describe **formalmente el contrato** de un servicio SOAP — qué operaciones ofrece, qué mensajes espera y devuelve cada una, qué tipos de datos usa y a qué dirección de red (*endpoint*) hay que dirigir las peticiones.
- **UDDI** (*Universal Description, Discovery and Integration*) [OASIS-UDDI]: un **registro** pensado para publicar y **descubrir** servicios web —una especie de «páginas amarillas» de servicios—, en el que un proveedor publica su WSDL y un consumidor lo busca por categoría o funcionalidad.

```xml
<!-- Fragmento simplificado de WSDL: describe la operación ConsultarExpediente -->
<wsdl:portType name="TributosPortType">
  <wsdl:operation name="ConsultarExpediente">
    <wsdl:input message="tns:ConsultarExpedienteRequest"/>
    <wsdl:output message="tns:ConsultarExpedienteResponse"/>
  </wsdl:operation>
</wsdl:portType>
```

> **[DATO CLAVE]** **UDDI** es, en la práctica actual, un estándar en **desuso**: la promesa de un registro público universal de servicios nunca llegó a adoptarse a gran escala, y su función de «catálogo descubrible» ha sido sustituida por **catálogos de API modernos** (portales de desarrollador, especificaciones OpenAPI/Swagger) en el mundo REST. Conserva interés por su papel histórico y porque puede aparecer citado en sistemas heredados.

### 6.5. RPC y RMI

**RPC** (*Remote Procedure Call*) [RFC5531] es un paradigma de comunicación en el que un programa invoca un procedimiento que se ejecuta en **otro espacio de direcciones** —habitualmente en otra máquina— **como si fuera una llamada local**, ocultando al programador los detalles de serialización de parámetros, transporte de red y deserialización de la respuesta. Es el paradigma conceptual subyacente a SOAP en su modelo de «operaciones» (§5.4.1) y a muchos middlewares orientados a objetos.

**RMI** (*Remote Method Invocation*) es la implementación nativa de este paradigma en la plataforma Java: permite invocar **métodos de objetos remotos** de forma transparente, apoyándose en *stubs* (representantes locales del objeto remoto, del lado del cliente) y *skeletons* (del lado del servidor), que se encargan de la serialización.

> **[DATO CLAVE]** RPC es el **paradigma general** («invocar algo remoto como si fuera local»); RMI es la **implementación específica de Java**. SOAP puede entenderse como una forma de RPC sobre HTTP con mensajes XML estandarizados y neutrales respecto al lenguaje, mientras que RMI está limitado a comunicación entre extremos Java.

> **[RELACIÓN CON OTROS TEMAS]** El **Tema 21** (arquitectura Java EE) trata RMI y su papel histórico dentro de EJB (los *Enterprise JavaBeans* originalmente se invocaban de forma remota mediante RMI-IIOP) con mayor detalle de implementación; aquí se sitúa como uno de los paradigmas de comunicación remota que preceden y conviven con los servicios web.

### 6.6. API REST y principios RESTful

Retomando el estilo REST introducido en el §5.4.2, Roy Fielding definió un conjunto de **restricciones arquitectónicas** que, aplicadas conjuntamente, caracterizan a un sistema como verdaderamente RESTful [FIELDING, cap. 5]:

| Restricción | Significado |
|---|---|
| **Cliente-servidor** | Separación de responsabilidades entre interfaz de usuario y almacenamiento/lógica (§2.1) |
| **Sin estado** (*stateless*) | Cada petición contiene **toda** la información necesaria para procesarla; el servidor no mantiene estado de sesión del cliente entre peticiones |
| **Cacheable** | Las respuestas deben indicar explícitamente si pueden almacenarse en caché, para mejorar rendimiento y escalabilidad |
| **Interfaz uniforme** | Un conjunto reducido y consistente de operaciones (los verbos HTTP) actúa sobre **recursos** identificados por URI |
| **Sistema en capas** | El cliente no puede saber, en general, si está hablando directamente con el servidor final o con un intermediario (proxy, *gateway*, balanceador) |
| **Código bajo demanda** (opcional) | El servidor puede, opcionalmente, enviar código ejecutable (por ejemplo, JavaScript) que el cliente ejecuta, extendiendo su funcionalidad |

Sobre la **interfaz uniforme**, los verbos HTTP se mapean de forma convencional a operaciones **CRUD** (crear, leer, actualizar, eliminar) sobre recursos:

| Verbo HTTP | Operación CRUD | Idempotente | Ejemplo |
|---|---|---|---|
| `GET` | Leer | Sí | `GET /expedientes/123` |
| `POST` | Crear | No | `POST /expedientes` |
| `PUT` | Actualizar (reemplazo completo) | Sí | `PUT /expedientes/123` |
| `PATCH` | Actualizar (parcial) | No (en general) | `PATCH /expedientes/123` |
| `DELETE` | Eliminar | Sí | `DELETE /expedientes/123` |

> **[DATO CLAVE]** **Idempotente** significa que ejecutar la misma operación varias veces produce el **mismo efecto** que ejecutarla una sola vez. `GET`, `PUT` y `DELETE` son idempotentes; `POST` no lo es (crear el mismo recurso dos veces produce, en general, dos recursos distintos). Es una propiedad con implicaciones prácticas: reintentar automáticamente una petición fallida solo es seguro sin efectos secundarios si el verbo es idempotente.

Por último, el **modelo de madurez de Richardson** —propuesto por Leonard Richardson, no por Fielding, aunque se aplica sobre las ideas de este último— clasifica en cuatro niveles cuán «RESTful» es realmente una API:

- **Nivel 0**: un único *endpoint*, todas las operaciones sobre `POST`, estilo RPC disfrazado de HTTP.
- **Nivel 1**: se introducen **recursos** identificados por URI distintas, pero se sigue usando mayormente un único verbo.
- **Nivel 2**: se usan correctamente los **verbos HTTP** y los **códigos de estado** — es el nivel en el que se sitúa la inmensa mayoría de las APIs REST reales en producción.
- **Nivel 3**: se añade **HATEOAS** (*Hypermedia as the Engine of Application State*): las respuestas incluyen enlaces a las acciones/recursos relacionados disponibles, de modo que el cliente puede navegar la API dinámicamente sin conocer de antemano todas las URIs — el nivel más purista y el menos adoptado en la práctica.

> **[EJEMPLO DE APLICACIÓN EN EL AYTO]** El **Portal de Datos Abiertos** del Ayuntamiento de Madrid (datos.madrid.es) expone su catálogo mediante una **API REST** en la que cada conjunto de datos es un recurso identificado por URI, consultable con `GET` y devuelto en JSON — un ejemplo público y accesible de nivel 2 del modelo de Richardson que cualquier ciudadano puede consultar sin autenticación [MADRID-API].

---

## 7. Tendencias actuales en arquitecturas distribuidas

> **Material complementario.** El enunciado oficial de este tema no nombra este apartado. Se mantiene porque esta materia envejece deprisa y conviene conocer su estado actual, pero lo exigible es lo que enumera el título del tema.

### 7.1. Microservicios

Los **microservicios** son un estilo arquitectónico que estructura una aplicación como un conjunto de **servicios pequeños, autónomos y desplegables de forma independiente**, cada uno organizado en torno a una **capacidad de negocio concreta** y comunicándose mediante mecanismos ligeros —típicamente APIs REST o mensajería asíncrona— [NEWMAN, cap. 1].

Se presentan habitualmente como una evolución de SOA (§5.2), llevando sus principios —bajo acoplamiento, autonomía— a un extremo más radical: mientras muchas implementaciones clásicas de SOA comparten infraestructura común a través de un **bus de servicios empresarial** (*Enterprise Service Bus*, ESB) que centraliza el enrutamiento y la transformación de mensajes, los microservicios evitan deliberadamente ese punto de coordinación central y enfatizan la **autonomía total**, incluida —a menudo— tener **cada servicio su propia base de datos**, para eliminar el acoplamiento a nivel de esquema de datos compartido.

| | Monolito | Microservicios |
|---|---|---|
| Unidad de despliegue | Toda la aplicación junta | Cada servicio, independiente |
| Escalado | De toda la aplicación a la vez | Selectivo, servicio a servicio |
| Base de datos | Habitualmente compartida | Habitualmente una por servicio |
| Complejidad de desarrollo inicial | Menor | Mayor (hay que diseñar los límites de cada servicio) |
| Complejidad operativa | Menor | Mayor (observabilidad, despliegue, red entre servicios) |
| Consistencia de datos | Transaccional, fuerte (ACID) | Con frecuencia, **consistencia eventual** entre servicios |

> **[DATO CLAVE]** Los microservicios no son «gratis»: a cambio de flexibilidad de despliegue y escalado independiente, introducen **complejidad operacional** significativa —hay que monitorizar, desplegar y versionar muchos más componentes— y a menudo renuncian a la **consistencia transaccional fuerte** entre servicios en favor de la **consistencia eventual**, un cambio de mentalidad de diseño no trivial.

### 7.2. Arquitectura orientada a eventos (EDA)

La **arquitectura orientada a eventos** (*Event-Driven Architecture*, EDA) estructura la comunicación entre componentes en torno a la **publicación y el consumo de eventos** —hechos que ya han ocurrido, como «expediente cambiado de estado»— en lugar de peticiones directas de un servicio a otro [EDA-FOWLER]. Un componente **productor** publica un evento en un **canal** (gestionado por un *broker* de mensajería, §2.2.3), sin conocer ni necesitar saber quién, si alguien, lo va a consumir; uno o varios componentes **consumidores** se suscriben a ese canal y reaccionan de forma asíncrona.

Esta forma de comunicación **desacopla emisor y receptor** en dos dimensiones simultáneamente: en el **espacio** (el productor no conoce la dirección de red de los consumidores, solo la del canal) y en el **tiempo** (el consumidor no necesita estar disponible en el instante exacto en que se publica el evento; el *broker* puede retener el mensaje hasta que el consumidor esté listo para procesarlo).

> **[EJEMPLO DE APLICACIÓN EN EL AYTO]** En el caso de referencia, cuando un expediente de licencia cambia a estado «resuelto», la capa de negocio de la Sede Electrónica **publica un evento** en el bus de mensajería, sin necesidad de conocer qué otros sistemas municipales están interesados. El sistema de **notificaciones** al ciudadano se suscribe a ese evento para enviar un aviso; el sistema de **estadísticas** de la Dirección General se suscribe para actualizar sus indicadores; si mañana se añade un tercer sistema interesado, no hay que modificar la capa de negocio en absoluto — solo dar de alta una nueva suscripción al mismo evento.

> **[RELACIÓN CON OTROS TEMAS]** EDA se apoya técnicamente en el **middleware orientado a mensajes** (MOM) presentado en el §2.2.3 de este mismo tema como una de las familias de middleware.

### 7.3. Contenedores y orquestación

Un **contenedor** es una unidad ligera de empaquetado y ejecución que virtualiza a **nivel del sistema operativo** —usando mecanismos del núcleo como los *namespaces* y los *cgroups* en Linux para aislar procesos, red y recursos—, en lugar de virtualizar hardware completo como hace una máquina virtual tradicional. Esto permite que un contenedor arranque en segundos (frente a los minutos de una máquina virtual) y que múltiples contenedores compartan el mismo núcleo de sistema operativo, siendo mucho más ligeros en consumo de recursos [K8S-DOCS].

Cuando una arquitectura de microservicios (§7.1) despliega decenas o cientos de contenedores, gestionarlos manualmente —arrancarlos, reiniciarlos si fallan, escalarlos según la carga, distribuirlos entre varias máquinas físicas— deja de ser viable. La **orquestación de contenedores**, con **Kubernetes** como estándar de facto de la industria, automatiza estas tareas: define de forma declarativa **cuántas réplicas** de cada servicio deben estar en ejecución, **reinicia automáticamente** los contenedores que fallan, **balancea la carga** entre las réplicas disponibles y **escala horizontalmente** añadiendo o quitando réplicas según reglas configuradas.

> **[RELACIÓN CON OTROS TEMAS]** El **Tema 28** (virtualización de sistemas y virtualización de puestos de usuario) trata la virtualización de máquinas completas (hipervisores), un nivel de abstracción distinto y anterior al de los contenedores presentados aquí — conviene no confundir ambos conceptos: contenedor virtualiza el sistema operativo; máquina virtual virtualiza el hardware.

### 7.4. Computación en la nube

La **computación en la nube** (*cloud computing*) es, según la definición de referencia del NIST, un modelo que permite el acceso **bajo demanda**, a través de la red, a un **conjunto compartido de recursos de cómputo configurables** (redes, servidores, almacenamiento, aplicaciones y servicios) que pueden **aprovisionarse y liberarse rápidamente** con un esfuerzo mínimo de gestión [NIST800145]. Sus modelos de servicio —**IaaS**, **PaaS** y **SaaS**— y sus modelos de despliegue —nube pública, privada e híbrida— son el objeto específico y detallado del **Tema 31** de este mismo temario.

En el contexto de este tema, la nube se cita como el **destino natural** de las arquitecturas distribuidas modernas: los servicios web (§5), los microservicios (§7.1) y los contenedores orquestados (§7.3) encuentran en las plataformas de nube pública el entorno de ejecución elástico —capaz de crecer y decrecer bajo demanda— que su diseño arquitectónico presupone.

> **[RELACIÓN CON OTROS TEMAS]** El **Tema 31** (paradigmas de computación distribuida y servicios en la nube) desarrolla en profundidad IaaS/PaaS/SaaS y los modelos de despliegue de nube; este tema (22) se limita a situar la nube como el cierre lógico de la evolución arquitectónica trazada desde el §1.2.3: de los sistemas centralizados, al cliente/servidor, a los servicios, a los microservicios y contenedores desplegados de forma elástica en la nube.
