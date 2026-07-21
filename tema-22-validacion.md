# Tema 22 — Checklist de Validación

> **Título oficial**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.
> **Versión**: v1.0 — Pendiente validación
> **Fecha**: 2026-07-21
> **Revisores**: María y Ana (eTrivium) · revisión técnica IAM (Jesús Cuadrado)
> **Instrucciones**: marcar cada ítem. Los cambios no se guardan en la web (imprimir o exportar a PDF si se desea fijarlos).

---

## 1. Cobertura del temario oficial

- [ ] **Introducción**: concepto de arquitectura de sistemas, evolución de centralizado a distribuido — §1
- [ ] **Cliente/servidor**: definición, componentes (cliente, servidor, middleware, comunicaciones) — §2
- [ ] **Modelos**: 2-Tier, 3-Tier, n-Tier, comparativa — §3
- [ ] **Multicapas**: separación de responsabilidades, capas, flujo de petición, beneficios — §4
- [ ] **Orientación a servicios**: SOA, servicios web, SOAP, REST — §5
- [ ] **Protocolos**: HTTP/HTTPS, OAuth 2.0/JWT, XML/JSON, SOAP/WSDL/UDDI, RPC/RMI, REST — §6
- [ ] **Tendencias actuales**: microservicios, EDA, contenedores, cloud — §7

## 2. Contenido teórico

- [ ] El nivel de profundidad (7 secciones, sección 7 "Tendencias" desarrollada completa por decisión de Joan pese a no estar literal en el enunciado oficial) es adecuado para C1
- [ ] El solape con el Tema 21 en SOAP/REST/WSDL/UDDI está tratado con el mismo nivel de detalle, por decisión de Joan (sin diferenciar enfoque agnóstico/Java)
- [ ] El solape con el Tema 31 (cloud, §7.4) y con el Tema 35 (HTTP/HTTPS/TLS, §6.1) está correctamente acotado mediante referencias cruzadas, sin duplicar contenido de detalle
- [ ] Las distinciones clave (layer≠tier, SOA≠servicios web, OAuth≠JWT, RPC≠RMI, contenedor≠VM) son correctas y están bien remarcadas
- [ ] El caso de referencia (arquitectura de la Sede Electrónica) es verosímil y coherente en todo el tema
- [ ] La decisión de usar snippets HTTP/JSON/XML/WSDL (agnósticos de lenguaje) en lugar de código en un lenguaje concreto es adecuada para este tema

## 3. Fuentes

- [ ] Todas las afirmaciones técnicas están respaldadas por fuente Tier 1 (RFC, W3C, OASIS, NIST, obras canónicas)
- [ ] Las referencias inline se corresponden con `tema-22-fuentes.md`
- [ ] Todas las fuentes Tier 1 listadas están citadas al menos una vez en el contenido

## 4. Test (60 preguntas)

- [ ] Cada pregunta tiene una sola respuesta correcta e inequívoca
- [ ] Los distractores (A/B/C) son plausibles
- [ ] La distribución de la opción correcta entre A/B/C está equilibrada (20/20/20 — verificado por script)
- [ ] Las explicaciones y referencias de cada respuesta son correctas

## 5. Casos prácticos (3)

- [ ] Realistas y propios del Ayuntamiento (n-capas/REST de la Sede, integración SOAP heredado de Tributos, evolución a microservicios/eventos/contenedores de notificaciones)
- [ ] Soluciones orientativas técnicamente correctas
- [ ] La puntuación de cada caso suma 10 puntos

## 6. Diagramas (12 SVG)

- [ ] Cada diagrama es correcto y legible (también impreso en B/N)
- [ ] Accesibilidad: todos tienen `role="img"` y `aria-label`
- [ ] Sin desbordes de texto ni colisiones de estilo entre SVG (clases con sufijo único `.t1`…`.t12`, QA de caja contenedora)

## 7. Referencias cruzadas a otros temas

- [ ] Validadas contra BOAM 10.032 (T15, T16, T17, T19, T21, T23, T24, T28, T31, T32, T34, T35, T39)
- [ ] Ninguna referencia cruzada cita un enunciado de tema incorrecto

## 8. Calidad editorial

- [ ] Ortografía verificada (tildes y ñ) — sin diacríticos perdidos
- [ ] Coherencia de versión (v1.0) en title, badges, banner y footer del `index.html`
- [ ] El `index.html` abre, navega entre las 8 pestañas y el motor de test funciona
- [ ] Las listas anidadas del Contenido se muestran con sus niveles (sin aplanar)
- [ ] Los bloques de código (HTTP/JSON/XML) se muestran correctamente formateados, sin markdown crudo

---

## Observaciones abiertas

_(Espacio para anotaciones de María, Ana y la revisión IAM.)_
