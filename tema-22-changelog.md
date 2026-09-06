# Tema 22 — Changelog

> **Título oficial**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.

---

## v1.2 — 2026-09-06 — Marcado del apartado complementario

**Estado**: pendiente de validación por el IAM.

**Motivo**: criterio de literalidad del título fijado por el IAM (Jesús Cuadrado, 02-09-2026).

### Alcance

- El apartado final que **el enunciado oficial del tema no nombra** queda marcado como **material complementario**, en el índice y al principio del propio apartado, con la advertencia de que lo exigible es lo que enumera el título.
- **Sin cambios de contenido**: el apartado se mantiene íntegro.

---

## v1.1 — 2026-09-06 — Ficha de extensión y tiempo de estudio

**Estado**: sin cambios de contenido. Solo se añade información sobre el propio tema.

**Motivo**: petición del IAM (Jesús Cuadrado, 02-09-2026) al validar el Tema 30. Acepta la extensión de los temas «compuestos» a condición de que se informe de «su extensión en palabras y tiempo estimado de estudio». Al revisarlo se vio que ese dato solo aparecía en 16 de los 40 temas, y que faltaba justo en los más largos.

### Alcance

- Ficha bajo la cabecera del tema, y al final de la pestaña Índice donde esa pestaña existe:
  - **Extensión**: ~9.600 palabras · 12 diagramas · 60 preguntas de test
  - **Tiempo estimado de estudio**: 10-12 horas (primera vuelta completa, sin contar repasos)
- La cifra de palabras de la tabla de entregables se sincroniza con la ficha, para que el tema no muestre dos recuentos distintos.
- Las horas salen de una fórmula común a los 40 temas, para que sean comparables entre sí: contenido a 1.500 palabras/hora (ritmo de estudio activo), diagramas a una hora por cada cinco y test a dos minutos por pregunta. Se publica como intervalo de dos horas.
- Generado con `_tools-qa/ficha_estudio.py`, idempotente y reejecutable tras cualquier regeneración con `build_tNN.py`.

---

## v1.0 — 2026-07-21 — Primera versión

**Estado**: pendiente de validación por María y Ana, y de revisión técnica del IAM (Jesús Cuadrado).

**Motivo**: desarrollo del Tema 22, dentro de la serie de temas técnicos generados desde cero (tras T11-T21), replicando la estructura y el formato de los Temas 11-21 ya consolidados, con pestaña Índice y listas anidadas correctas desde el inicio. Generado a petición expresa de Joan, con revisión previa del esqueleto oficial y consulta de 4 puntos abiertos antes de empezar.

### Alcance de la v1.0

| Entregable | Cantidad |
|---|---|
| Contenido teórico | ~9.300 palabras · 7 secciones (esqueleto oficial completo) con 30 epígrafes numerados |
| Diagramas SVG inline | 12 (accesibles con `role`/`aria-label`, clases con sufijo único anti-colisión) |
| Banco de preguntas tipo test | 60 preguntas A/B/C con explicación y referencia, balanceadas **20/20/20** |
| Casos prácticos | 3 (n-capas y API REST de la Sede Electrónica; integración de un servicio SOAP heredado de Tributos; evolución del módulo de notificaciones a microservicios/eventos/contenedores) · 10 puntos cada uno |
| Fuentes Tier 1 | 22 referencias canónicas (RFC IETF, especificaciones W3C/OASIS, NIST SP 800-145, Fielding, Fowler, Erl, Newman, Kubernetes docs, ENI) |

### Decisiones de generación (consultadas con Joan antes de empezar)

1. **Sección 7 "Tendencias actuales en arquitecturas distribuidas"** (microservicios, EDA, contenedores, cloud) desarrollada **completa**, pese a no figurar literalmente en el enunciado oficial BOAM y solapar parcialmente con el Tema 31 (cloud/IaaS-PaaS-SaaS) — decisión explícita de Joan. El solape se gestiona con referencias cruzadas explícitas al Tema 31, sin repetir su nivel de detalle de infraestructura de provisión.
2. **SOAP/REST/WSDL/UDDI tratados con el mismo nivel de detalle que en el Tema 21** (Java EE/JAX-WS/JAX-RS) — decisión explícita de Joan, en lugar del enfoque más genérico inicialmente propuesto. La diferencia de enfoque entre ambos temas queda en que T21 los sitúa dentro de la plataforma Java EE concreta y T22 los trata como estilos/protocolos agnósticos de lenguaje, con referencia cruzada explícita entre ambos.
3. **Caso de referencia elegido por Claude, a criterio propio** (Joan delegó la elección): la **arquitectura de la Sede Electrónica municipal**, que permite ilustrar en un único hilo narrativo el cliente ligero, el n-capas, la convivencia SOAP/REST y la evolución hacia EDA/microservicios/contenedores.
4. **Extensión objetivo igual que el Tema 21** (~11.000 palabras teóricas, 12 diagramas) — decisión de Joan; la extensión final de contenido.md (~9.300 palabras) queda algo por debajo del objetivo debido a la mayor densidad de secciones cortas frente a la profundidad de una única plataforma (caso de T21), compensada por la extensión adicional de diagramas, test y casos prácticos.
5. **Snippets en HTTP/JSON/XML/WSDL, no en un lenguaje de programación concreto**: a diferencia de T21 (Java/Jakarta EE reales, porque el tema trata de esa plataforma), este tema es agnóstico de lenguaje y plataforma, y los ejemplos usan los formatos de intercambio propios del dominio.
6. **Frontera con temas vecinos** cuidada: SO/hardware al Tema 11; SGBD y diseño de datos a los Temas 15-17; SQL/procedimientos almacenados al Tema 19; Java EE concreto al Tema 21; desarrollo web front-end al Tema 23; virtualización de máquinas (hipervisores) al Tema 28, distinguida explícitamente de los contenedores de este tema; cloud (IaaS/PaaS/SaaS) al Tema 31; criptografía/firma digital al Tema 32; TCP/IP y OSI al Tema 34; TLS/SSL en detalle al Tema 35; ENI/ENS al Tema 39.
7. **Referencias cruzadas validadas contra BOAM 10.032**: T15, T16, T17, T19, T21, T23, T24, T28, T31, T32, T34, T35, T39. Todas comprobadas contra el enunciado oficial de cada tema.
8. **Anti-colisión de SVG**: las clases CSS de cada diagrama llevan **sufijo numérico único** (`.t1`…`.t12`), evitando el bug sistémico de estilos que leakean entre los 12 SVG embebidos en la misma página (lección de T5).
9. **Test**: generado con 60 preguntas y balanceado 20/20/20 mediante script de verificación/rebalanceo automático (detectó y corrigió 3 preguntas con la letra de respuesta correcta mal etiquetada durante la redacción manual, antes de publicar).

### Pendientes para QA / próxima iteración

- Validación de profundidad por María/Ana/IAM (¿la sección 7 de Tendencias debe recortarse en favor de mayor detalle en §5-6, dado que no está en el enunciado oficial?).
- Confirmación del escenario de caso práctico (Sede Electrónica) con Jesús, por si el Ayuntamiento prefiere otro escenario real más específico.
- Verificación ortográfica con corrector es_ES (cuidado con falsos positivos por términos técnicos en inglés: *middleware*, *thin/thick client*, *stateless*, *broker*, *namespace*, *pool*, *token*, *endpoint*, *gateway*…).
