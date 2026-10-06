# Tema 22 — Fuentes

> **Título oficial**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.
>
> **Versión**: v1.0 · 2026-07-21

---

## Tier 1 — Fuentes canónicas (citadas inline)

| ID | Fuente |
|---|---|
| `[RFC9110]` | IETF RFC 9110 — HTTP Semantics (junio 2022, sustituye a RFC 7230-7235) |
| `[RFC9112]` | IETF RFC 9112 — HTTP/1.1 |
| `[RFC9113]` | IETF RFC 9113 — HTTP/2 |
| `[RFC9114]` | IETF RFC 9114 — HTTP/3 |
| `[RFC9846]` | IETF RFC 9846 — The Transport Layer Security (TLS) Protocol Version 1.3 (julio de 2026). Obsoleta los RFC 5077, 5246, 6961, 7627, 8422 y 8446: es la especificación vigente de TLS 1.3 y sustituye a la de 2018 |
| `[RFC8446]` | IETF RFC 8446 — The Transport Layer Security (TLS) Protocol Version 1.3 (agosto de 2018). Obsoletado por el RFC 9846. Se conserva la referencia porque es la que recogen los temarios al uso |
| `[FIELDING]` | Fielding, R. — *Architectural Styles and the Design of Network-based Software Architectures* (tesis doctoral, UC Irvine, 2000) — origen de REST |
| `[RFC6749]` | IETF RFC 6749 — The OAuth 2.0 Authorization Framework |
| `[RFC7519]` | IETF RFC 7519 — JSON Web Token (JWT) |
| `[RFC8259]` | IETF RFC 8259 — The JavaScript Object Notation (JSON) Data Interchange Format |
| `[W3C-XML]` | W3C — Extensible Markup Language (XML) 1.0 (Fifth Edition) |
| `[W3C-SOAP]` | W3C — SOAP Version 1.2 Part 1: Messaging Framework |
| `[W3C-WSDL]` | W3C — Web Services Description Language (WSDL) 1.1 / 2.0 |
| `[OASIS-UDDI]` | OASIS — UDDI Version 3.0.2 |
| `[RFC5531]` | IETF RFC 5531 — RPC: Remote Procedure Call Protocol Specification Version 2 (mayo de 2009). Obsoleta el RFC 1831: mismo título y mismo protocolo (RPC versión 2); es la especificación vigente |
| `[RFC1831]` | IETF RFC 1831 — RPC: Remote Procedure Call Protocol Specification Version 2 (agosto de 1995). Obsoletado por el RFC 5531. Se conserva la referencia porque es la que recogen los temarios al uso |
| `[GARTNER-3TIER]` | Sinha, A. — *Client-Server Computing: Current Technology Review* (Comm. ACM, 1992) — origen del modelo 2/3 capas |
| `[FOWLER-PEAA]` | Fowler, M. — *Patterns of Enterprise Application Architecture* (Addison-Wesley, 2002) — capas, patrones de acceso a datos |
| `[ERL-SOA]` | Erl, T. — *SOA: Principles of Service Design* (Prentice Hall, 2007) |
| `[NEWMAN]` | Newman, S. — *Building Microservices*, 2ª ed. (O'Reilly, 2021) |
| `[EDA-FOWLER]` | Fowler, M. — *What do you mean by "Event-Driven"* (martinfowler.com, 2017) |
| `[NIST800145]` | NIST SP 800-145 — The NIST Definition of Cloud Computing |
| `[K8S-DOCS]` | Kubernetes.io — Documentación oficial de conceptos (Pods, Services, orquestación) |
| `[ENI]` | Real Decreto 4/2010 — Esquema Nacional de Interoperabilidad, Anexo (catálogo de estándares) |
| `[MADRID-API]` | Ayuntamiento de Madrid — Portal de Datos Abiertos, documentación técnica API REST (datos.madrid.es) |

## Tier 2 — Referencias de apoyo (contexto, no citadas inline en todas las secciones)

- Richardson, L. & Ruby, S. — *RESTful Web Services* (O'Reilly, 2007) — modelo de madurez de Richardson
- Josuttis, N. — *SOA in Practice* (O'Reilly, 2007)
- OWASP — *REST Security Cheat Sheet* / *Authentication Cheat Sheet*
- MDN Web Docs — HTTP overview, HTTP caching, CORS
- Google Cloud Architecture Center — Microservices vs. monolith, event-driven architectures
- Documentación oficial Docker — arquitectura de contenedores (namespaces, cgroups)

## Tier 3 — Consultadas, no citadas directamente

- Tanenbaum, A. & Van Steen, M. — *Distributed Systems*, 3ª ed. — marco conceptual general de sistemas distribuidos
- Endpoints internos de la Sede Electrónica y del Portal de Transparencia del Ayuntamiento de Madrid (uso ilustrativo en casos prácticos, sin acceso a especificación interna real)

---

*Convención de cita inline en `tema-22-contenido.md`: `[ID, referencia concreta]`, p. ej. `[RFC9110, §9.3]`, `[FIELDING, cap. 5]`.*
