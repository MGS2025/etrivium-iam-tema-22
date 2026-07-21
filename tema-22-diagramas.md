# Tema 22 — Catálogo de Diagramas

> **Título oficial**: Arquitectura de sistemas cliente/servidor y multicapas: componentes y operación. Arquitecturas de servicios web y protocolos asociados.
>
> **Versión**: v1.0
> **Fecha**: 2026-07-21
> **Autor**: ETRIVIUM
> **Formato**: SVG inline (zero-dependencias, escalable, imprimible, accesible con role/aria-label)
> **Paleta**: Ayuntamiento de Madrid #0055a0 (primario) + #d13c3c (alertas) + #2d8659 (ventajas) + #e89822 (callouts)
> **Nota técnica**: las clases CSS de cada SVG llevan sufijo numérico único (`.t1`, `.h1`…) para evitar colisiones de estilos entre los 12 diagramas embebidos en la misma página.

---

## Índice de diagramas

| ID | Título | Sección | Tipo | Formato |
|---|---|---|---|---|
| D1 | De los sistemas centralizados a la nube: línea de tiempo | §1.2 | Línea de tiempo | 680×320 |
| D2 | Componentes de la arquitectura cliente/servidor | §2.2 | Bloques | 680×340 |
| D3 | Cliente ligero frente a cliente pesado | §2.2.1 | Comparativa | 660×320 |
| D4 | 2-Tier, 3-Tier y n-Tier | §3 | Comparativa | 680×360 |
| D5 | Flujo de una petición en arquitectura multicapa | §4.5 | Flujo | 680×360 |
| D6 | Principios de SOA | §5.2 | Radial | 660×380 |
| D7 | SOAP frente a REST | §5.4 | Comparativa | 680×340 |
| D8 | Pila de protocolos y estándares de servicios web | §6 | Pila | 660×360 |
| D9 | OAuth 2.0: roles y flujo del token | §6.2 | Flujo | 680×340 |
| D10 | Verbos HTTP, códigos de estado y modelo de madurez de Richardson | §6.6 | Cheat sheet | 680×360 |
| D11 | Monolito frente a microservicios | §7.1 | Comparativa | 680×340 |
| D12 | Contenedores, orquestación y nube | §7.3-7.4 | Bloques apilados | 660×360 |

---

## D1 · De los sistemas centralizados a la nube: línea de tiempo

**Sección**: §1.2 — Evolución de los modelos centralizados a los sistemas distribuidos
**Propósito**: Fijar la secuencia histórica mainframe → cliente/servidor → 3 capas → SOA → microservicios/cloud.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 720 320" role="img" aria-label="Línea de tiempo desde los sistemas centralizados con mainframe y terminales tontos hasta finales de los 80, pasando por cliente servidor en los 90, tres capas y n capas a finales de los 90 y 2000, arquitectura orientada a servicios en los 2000, y microservicios, contenedores y computación en la nube desde los 2010">
  <style>.t1{font:700 11px system-ui,sans-serif;fill:#fff}.s1{font:9.5px system-ui,sans-serif;fill:#fff}.l1{font:11px system-ui,sans-serif;fill:#444}.h1{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="360" y="22" text-anchor="middle" class="h1">De los sistemas centralizados a la nube</text>
  <line x1="30" y1="60" x2="670" y2="60" stroke="#0055a0" stroke-width="3"/>
  <circle cx="50" cy="60" r="7" fill="#888"/><text x="50" y="42" text-anchor="middle" class="l1">&lt;1985</text><text x="50" y="80" text-anchor="middle" class="l1">Mainframe</text>
  <circle cx="150" cy="60" r="7" fill="#0055a0"/><text x="150" y="42" text-anchor="middle" class="l1">años 90</text><text x="150" y="80" text-anchor="middle" style="font:700 10px system-ui;fill:#0055a0">Cliente/servidor</text>
  <circle cx="250" cy="60" r="7" fill="#0055a0"/><text x="250" y="42" text-anchor="middle" class="l1">fin 90</text><text x="250" y="80" text-anchor="middle" style="font:700 10px system-ui;fill:#0055a0">3/n capas</text>
  <circle cx="360" cy="60" r="7" fill="#2d8659"/><text x="360" y="42" text-anchor="middle" class="l1">2000s</text><text x="360" y="80" text-anchor="middle" style="font:700 10px system-ui;fill:#2d8659">SOA / servicios web</text>
  <circle cx="500" cy="60" r="7" fill="#e89822"/><text x="500" y="42" text-anchor="middle" class="l1">2010s</text><text x="500" y="80" text-anchor="middle" style="font:700 10px system-ui;fill:#e89822">Microservicios / EDA</text>
  <circle cx="650" cy="60" r="7" fill="#d13c3c"/><text x="650" y="42" text-anchor="middle" class="l1">actual</text><text x="650" y="80" text-anchor="middle" style="font:700 10px system-ui;fill:#d13c3c">Contenedores/nube</text>
  <rect x="20" y="110" width="190" height="56" rx="5" fill="#888"/><text x="115" y="132" text-anchor="middle" class="t1">Centralizado</text><text x="115" y="150" text-anchor="middle" class="s1">Mainframe + terminal tonto</text>
  <rect x="225" y="110" width="240" height="56" rx="5" fill="#0055a0"/><text x="345" y="132" text-anchor="middle" class="t1">Cliente/servidor · n-capas</text><text x="345" y="150" text-anchor="middle" class="s1">§2-3 de este tema</text>
  <rect x="480" y="110" width="220" height="56" rx="5" fill="#2d8659"/><text x="590" y="132" text-anchor="middle" class="t1">SOA · servicios web</text><text x="590" y="150" text-anchor="middle" class="s1">§5-6 de este tema</text>
  <rect x="130" y="182" width="460" height="56" rx="5" fill="#e89822"/><text x="360" y="204" text-anchor="middle" class="t1">Microservicios · EDA · contenedores · cloud</text><text x="360" y="222" text-anchor="middle" class="s1">§7 de este tema · desarrollado en profundidad en el Tema 31</text>
  <text x="360" y="264" text-anchor="middle" style="font:700 11px system-ui;fill:#0055a0">El escalado vertical de un único servidor cede paso a arquitecturas distribuidas y elásticas</text>
  <text x="360" y="284" text-anchor="middle" class="l1">Cada oleada resuelve limitaciones de la anterior, sin eliminar del todo a las precedentes</text>
  <text x="700" y="312" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: GARTNER-3TIER; FOWLER-PEAA]</text>
</svg>
```

---

## D2 · Componentes de la arquitectura cliente/servidor

**Sección**: §2.2 — Componentes principales
**Propósito**: Situar cliente, servidor, middleware e infraestructura de comunicaciones en una única imagen.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 360" role="img" aria-label="Componentes de la arquitectura cliente servidor: un cliente ligero o pesado que inicia la petición, una infraestructura de comunicaciones que la transporta, un middleware que la traduce y abstrae, y un servidor que gestiona recursos compartidos y concurrencia">
  <style>.t2{font:700 12px system-ui,sans-serif;fill:#fff}.s2{font:9.5px system-ui,sans-serif;fill:#fff}.l2{font:11px system-ui,sans-serif;fill:#444}.h2{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h2">Arquitectura cliente/servidor: cuatro componentes</text>
  <rect x="20" y="50" width="150" height="80" rx="6" fill="#0055a0"/><text x="95" y="76" text-anchor="middle" class="t2">CLIENTE</text><text x="95" y="94" text-anchor="middle" class="s2">Ligero (navegador) o</text><text x="95" y="108" text-anchor="middle" class="s2">pesado (§2.2.1)</text>
  <path d="M172 90 L198 90" stroke="#888" stroke-width="3" marker-end="url(#a2)"/>
  <rect x="200" y="50" width="260" height="80" rx="6" fill="#3778b5"/><text x="330" y="74" text-anchor="middle" style="font:700 10.5px system-ui;fill:#fff">INFRAESTRUCTURA DE COMUNICACIONES</text><text x="330" y="94" text-anchor="middle" class="s2">Red física/lógica + pila TCP/IP</text><text x="330" y="110" text-anchor="middle" class="s2">(desarrollado en el Tema 34)</text>
  <path d="M462 90 L488 90" stroke="#888" stroke-width="3" marker-end="url(#a2)"/>
  <rect x="490" y="50" width="170" height="80" rx="6" fill="#0055a0"/><text x="575" y="76" text-anchor="middle" class="t2">SERVIDOR</text><text x="575" y="94" text-anchor="middle" class="s2">Gestión de recursos</text><text x="575" y="108" text-anchor="middle" class="s2">y concurrencia (§2.2.2)</text>
  <rect x="130" y="160" width="420" height="86" rx="6" fill="#2d8659"/><text x="340" y="180" text-anchor="middle" class="t2">MIDDLEWARE (§2.2.3)</text><text x="340" y="198" text-anchor="middle" class="s2">Acceso a datos · orientado a objetos · MOM</text><text x="340" y="214" text-anchor="middle" class="s2">Servicios web · transaccional</text><text x="340" y="232" text-anchor="middle" class="s2">Oculta la complejidad de la comunicación distribuida</text>
  <path d="M340 132 L340 158" stroke="#888" stroke-width="3" marker-end="url(#a2)"/>
  <defs><marker id="a2" markerWidth="9" markerHeight="9" refX="4.5" refY="4.5" orient="auto"><path d="M0 0 L9 4.5 L0 9 z" fill="#888"/></marker></defs>
  <text x="340" y="280" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">Relación asimétrica y de petición-respuesta: el cliente inicia, el servidor responde</text>
  <text x="340" y="300" text-anchor="middle" class="l2">Un mismo proceso puede ser servidor frente a un interlocutor y cliente frente a otro</text>
  <text x="670" y="352" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: FOWLER-PEAA, cap. 1]</text>
</svg>
```

---

## D3 · Cliente ligero frente a cliente pesado

**Sección**: §2.2.1 — Cliente: cliente ligero y pesado
**Propósito**: Comparar en una sola vista dónde vive la lógica, el despliegue y el uso de red de cada modelo de cliente.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 660 320" role="img" aria-label="Comparativa entre cliente ligero, que renderiza en el navegador con lógica en el servidor y actualización centralizada, y cliente pesado, que ejecuta lógica local, mantiene datos locales y requiere instalación y actualización en cada puesto">
  <style>.t3{font:700 12px system-ui,sans-serif;fill:#fff}.s3{font:9.5px system-ui,sans-serif;fill:#fff}.l3{font:10.5px system-ui,sans-serif;fill:#444}.h3{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="330" y="20" text-anchor="middle" class="h3">Cliente ligero vs. cliente pesado</text>
  <rect x="30" y="40" width="280" height="34" rx="5" fill="#0055a0"/><text x="170" y="62" text-anchor="middle" class="t3">CLIENTE LIGERO (thin client)</text>
  <rect x="350" y="40" width="280" height="34" rx="5" fill="#e89822"/><text x="490" y="62" text-anchor="middle" class="t3">CLIENTE PESADO (thick/fat client)</text>
  <rect x="30" y="84" width="280" height="42" rx="4" fill="#eef4fb" stroke="#0055a0"/><text x="170" y="102" text-anchor="middle" class="l3">Lógica de negocio: en el servidor</text><text x="170" y="118" text-anchor="middle" class="l3">Ejemplo: navegador web</text>
  <rect x="350" y="84" width="280" height="42" rx="4" fill="#fdf3e2" stroke="#e89822"/><text x="490" y="102" text-anchor="middle" class="l3">Lógica de negocio: total o parcial en cliente</text><text x="490" y="118" text-anchor="middle" class="l3">Ejemplo: app de escritorio clásica</text>
  <rect x="30" y="132" width="280" height="42" rx="4" fill="#eef4fb" stroke="#0055a0"/><text x="170" y="150" text-anchor="middle" class="l3">Despliegue: centralizado, transparente</text><text x="170" y="166" text-anchor="middle" class="l3">Nada que instalar en el puesto</text>
  <rect x="350" y="132" width="280" height="42" rx="4" fill="#fdf3e2" stroke="#e89822"/><text x="490" y="150" text-anchor="middle" class="l3">Despliegue: instalar/actualizar cada puesto</text><text x="490" y="166" text-anchor="middle" class="l3">Coste de mantenimiento alto</text>
  <rect x="30" y="180" width="280" height="42" rx="4" fill="#eef4fb" stroke="#0055a0"/><text x="170" y="198" text-anchor="middle" class="l3">Uso de red: mayor (ida/vuelta por acción)</text><text x="170" y="214" text-anchor="middle" class="l3">Offline: limitado o nulo</text>
  <rect x="350" y="180" width="280" height="42" rx="4" fill="#fdf3e2" stroke="#e89822"/><text x="490" y="198" text-anchor="middle" class="l3">Uso de red: menor (datos locales)</text><text x="490" y="214" text-anchor="middle" class="l3">Offline: posible con sincronización</text>
  <text x="330" y="256" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">El problema de despliegue del cliente pesado impulsó la migración al cliente ligero web</text>
  <text x="330" y="276" text-anchor="middle" class="l3">Temas 23 (front-end web) y 24 (móvil nativo/híbrido) desarrollan cada extremo</text>
  <text x="650" y="308" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: FOWLER-PEAA]</text>
</svg>
```

---

## D4 · 2-Tier, 3-Tier y n-Tier

**Sección**: §3 — Modelos de arquitectura cliente/servidor
**Propósito**: Visualizar cómo se añade el servidor de aplicaciones al pasar de 2 a 3 capas, y cómo n-Tier añade niveles físicos adicionales.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 360" role="img" aria-label="Comparativa de tres modelos: dos capas con cliente pesado conectado directamente a la base de datos, tres capas con cliente, servidor de aplicaciones y base de datos, y n capas con balanceador, varios servidores de aplicaciones, cache y base de datos">
  <style>.t4{font:700 11px system-ui,sans-serif;fill:#fff}.s4{font:9px system-ui,sans-serif;fill:#fff}.l4{font:10.5px system-ui,sans-serif;fill:#444}.h4{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="18" text-anchor="middle" class="h4">2-Tier · 3-Tier · n-Tier</text>
  <text x="80" y="40" text-anchor="middle" class="l4">2-TIER</text>
  <rect x="20" y="48" width="120" height="44" rx="5" fill="#888"/><text x="80" y="66" text-anchor="middle" class="t4">Cliente pesado</text><text x="80" y="82" text-anchor="middle" class="s4">+ lógica ambigua</text>
  <path d="M80 92 L80 116" stroke="#888" stroke-width="2.5" marker-end="url(#a4)"/>
  <rect x="20" y="118" width="120" height="44" rx="5" fill="#d13c3c"/><text x="80" y="136" text-anchor="middle" class="t4">Base de datos</text><text x="80" y="152" text-anchor="middle" class="s4">+ procedimientos</text>
  <text x="270" y="40" text-anchor="middle" class="l4">3-TIER</text>
  <rect x="200" y="48" width="120" height="36" rx="5" fill="#0055a0"/><text x="260" y="70" text-anchor="middle" class="t4">Cliente (presentación)</text>
  <path d="M260 84 L260 104" stroke="#888" stroke-width="2.5" marker-end="url(#a4)"/>
  <rect x="200" y="106" width="120" height="36" rx="5" fill="#2d8659"/><text x="260" y="128" text-anchor="middle" class="t4">Servidor aplicaciones</text>
  <path d="M260 142 L260 162" stroke="#888" stroke-width="2.5" marker-end="url(#a4)"/>
  <rect x="200" y="164" width="120" height="36" rx="5" fill="#e89822"/><text x="260" y="186" text-anchor="middle" class="t4">Base de datos</text>
  <text x="500" y="40" text-anchor="middle" class="l4">N-TIER</text>
  <rect x="420" y="48" width="160" height="30" rx="5" fill="#0055a0"/><text x="500" y="68" text-anchor="middle" class="t4">Balanceador de carga</text>
  <path d="M460 78 L440 98" stroke="#888" stroke-width="2" marker-end="url(#a4)"/><path d="M540 78 L560 98" stroke="#888" stroke-width="2" marker-end="url(#a4)"/>
  <rect x="400" y="100" width="90" height="34" rx="5" fill="#2d8659"/><text x="445" y="121" text-anchor="middle" class="s4">App server A</text>
  <rect x="510" y="100" width="90" height="34" rx="5" fill="#2d8659"/><text x="555" y="121" text-anchor="middle" class="s4">App server B</text>
  <path d="M445 134 L490 156" stroke="#888" stroke-width="2" marker-end="url(#a4)"/><path d="M555 134 L510 156" stroke="#888" stroke-width="2" marker-end="url(#a4)"/>
  <rect x="440" y="158" width="120" height="30" rx="5" fill="#3778b5"/><text x="500" y="178" text-anchor="middle" class="s4">Caché</text>
  <path d="M500 188 L500 208" stroke="#888" stroke-width="2.5" marker-end="url(#a4)"/>
  <rect x="420" y="210" width="160" height="34" rx="5" fill="#e89822"/><text x="500" y="231" text-anchor="middle" class="t4">Clúster de datos</text>
  <defs><marker id="a4" markerWidth="8" markerHeight="8" refX="4" refY="4" orient="auto"><path d="M0 0 L8 4 L0 8 z" fill="#888"/></marker></defs>
  <rect x="20" y="266" width="640" height="54" rx="6" fill="#f4f4f4" stroke="#ccc"/>
  <text x="340" y="288" text-anchor="middle" style="font:700 11px system-ui;fill:#0055a0">Capa lógica (layer) ≠ nivel físico (tier): n-Tier puede tener 3 capas lógicas en 5+ niveles físicos</text>
  <text x="340" y="306" text-anchor="middle" class="l4">2-Tier acopla cliente y datos · 3-Tier los desacopla con el servidor de aplicaciones intermedio</text>
  <text x="670" y="352" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: GARTNER-3TIER]</text>
</svg>
```

---

## D5 · Flujo de una petición en arquitectura multicapa

**Sección**: §4.5 — Flujo de procesamiento de una petición
**Propósito**: Trazar el recorrido de ida (arriba→abajo) y de vuelta (abajo→arriba) de una petición a través de las tres capas lógicas.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 360" role="img" aria-label="Flujo de una petición de consulta de expediente: el navegador envia una petición HTTP a la capa de presentación, que la traduce a una llamada a la capa de negocio, que aplica reglas y solicita datos a la capa de acceso a datos, y la respuesta recorre el camino inverso hasta el navegador">
  <style>.t5{font:700 11.5px system-ui,sans-serif;fill:#fff}.s5{font:9.5px system-ui,sans-serif;fill:#fff}.l5{font:10.5px system-ui,sans-serif;fill:#444}.h5{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h5">Flujo de una petición: consultar un expediente</text>
  <rect x="30" y="40" width="140" height="50" rx="5" fill="#888"/><text x="100" y="62" text-anchor="middle" class="t5">Navegador</text><text x="100" y="78" text-anchor="middle" class="s5">(cliente ligero)</text>
  <rect x="270" y="40" width="140" height="50" rx="5" fill="#0055a0"/><text x="340" y="62" text-anchor="middle" class="t5">Presentación</text><text x="340" y="78" text-anchor="middle" class="s5">Controlador</text>
  <rect x="510" y="40" width="140" height="50" rx="5" fill="#2d8659"/><text x="580" y="62" text-anchor="middle" class="t5">Negocio</text><text x="580" y="78" text-anchor="middle" class="s5">Reglas · permisos</text>
  <path d="M170 65 L268 65" stroke="#0055a0" stroke-width="2.5" marker-end="url(#a5)"/><text x="220" y="58" text-anchor="middle" style="font:9px system-ui;fill:#0055a0">1. GET HTTP</text>
  <path d="M410 65 L508 65" stroke="#0055a0" stroke-width="2.5" marker-end="url(#a5)"/><text x="460" y="58" text-anchor="middle" style="font:9px system-ui;fill:#0055a0">2-3. llamada</text>
  <rect x="510" y="130" width="140" height="50" rx="5" fill="#e89822"/><text x="580" y="152" text-anchor="middle" class="t5">Acceso a datos</text><text x="580" y="168" text-anchor="middle" class="s5">Consulta SGBD</text>
  <path d="M580 92 L580 128" stroke="#0055a0" stroke-width="2.5" marker-end="url(#a5)"/><text x="605" y="112" text-anchor="middle" style="font:9px system-ui;fill:#0055a0">4</text>
  <path d="M508 158 L412 158" stroke="#2d8659" stroke-width="2.5" marker-end="url(#a5)"/>
  <rect x="270" y="130" width="140" height="50" rx="5" fill="#0055a0"/><text x="340" y="152" text-anchor="middle" class="t5">Presentación</text><text x="340" y="168" text-anchor="middle" class="s5">Formatea respuesta</text>
  <path d="M268 158 L172 158" stroke="#2d8659" stroke-width="2.5" marker-end="url(#a5)"/>
  <rect x="30" y="130" width="140" height="50" rx="5" fill="#888"/><text x="100" y="152" text-anchor="middle" class="t5">Navegador</text><text x="100" y="168" text-anchor="middle" class="s5">Muestra resultado</text>
  <text x="340" y="212" text-anchor="middle" style="font:10px system-ui;fill:#666">Ida (1→4): arriba → abajo · Vuelta (5→6): abajo → arriba, mismo camino, sentido inverso</text>
  <defs><marker id="a5" markerWidth="8" markerHeight="8" refX="4" refY="4" orient="auto"><path d="M0 0 L8 4 L0 8 z" fill="context-fill"/></marker></defs>
  <rect x="30" y="234" width="620" height="60" rx="6" fill="#f4f4f4" stroke="#ccc"/>
  <text x="340" y="258" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">En ningún punto la capa de datos invoca directamente a la de presentación</text>
  <text x="340" y="278" text-anchor="middle" class="l5">La dependencia unidireccional (§4.1) se respeta en todo el recorrido de ida y vuelta</text>
  <text x="670" y="352" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: FOWLER-PEAA, cap. 1]</text>
</svg>
```

---

## D6 · Principios de SOA

**Sección**: §5.2 — Arquitectura orientada a servicios (SOA)
**Propósito**: Reunir en un esquema radial los seis principios de diseño de SOA en torno al concepto de «servicio».

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 660 380" role="img" aria-label="Seis principios de diseño de la arquitectura orientada a servicios alrededor del concepto central de servicio: bajo acoplamiento, contrato explícito, abstracción, reutilización, autonomía y componibilidad">
  <style>.t6{font:700 11px system-ui,sans-serif;fill:#fff}.s6{font:9px system-ui,sans-serif;fill:#fff}.l6{font:10.5px system-ui,sans-serif;fill:#444}.h6{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="330" y="20" text-anchor="middle" class="h6">SOA: seis principios alrededor del «servicio»</text>
  <circle cx="330" cy="200" r="52" fill="#0055a0"/><text x="330" y="196" text-anchor="middle" class="t6">SERVICIO</text><text x="330" y="212" text-anchor="middle" class="s6">§5.1</text>
  <rect x="250" y="60" width="160" height="46" rx="5" fill="#2d8659"/><text x="330" y="80" text-anchor="middle" class="t6">Bajo acoplamiento</text><text x="330" y="96" text-anchor="middle" class="s6">Mínimas dependencias</text>
  <line x1="330" y1="106" x2="330" y2="150" stroke="#888" stroke-width="2"/>
  <rect x="470" y="120" width="170" height="46" rx="5" fill="#2d8659"/><text x="555" y="140" text-anchor="middle" class="t6">Contrato explícito</text><text x="555" y="156" text-anchor="middle" class="s6">Interfaz formal</text>
  <line x1="468" y1="143" x2="380" y2="175" stroke="#888" stroke-width="2"/>
  <rect x="470" y="216" width="170" height="46" rx="5" fill="#2d8659"/><text x="555" y="236" text-anchor="middle" class="t6">Abstracción</text><text x="555" y="252" text-anchor="middle" class="s6">Oculta implementación</text>
  <line x1="468" y1="239" x2="380" y2="222" stroke="#888" stroke-width="2"/>
  <rect x="250" y="278" width="160" height="46" rx="5" fill="#2d8659"/><text x="330" y="298" text-anchor="middle" class="t6">Reutilización</text><text x="330" y="314" text-anchor="middle" class="s6">Múltiples consumidores</text>
  <line x1="330" y1="278" x2="330" y2="252" stroke="#888" stroke-width="2"/>
  <rect x="20" y="216" width="170" height="46" rx="5" fill="#2d8659"/><text x="105" y="236" text-anchor="middle" class="t6">Autonomía</text><text x="105" y="252" text-anchor="middle" class="s6">Controla su lógica/datos</text>
  <line x1="192" y1="239" x2="280" y2="222" stroke="#888" stroke-width="2"/>
  <rect x="20" y="120" width="170" height="46" rx="5" fill="#2d8659"/><text x="105" y="140" text-anchor="middle" class="t6">Componibilidad</text><text x="105" y="156" text-anchor="middle" class="s6">Orquestación/coreografía</text>
  <line x1="192" y1="143" x2="280" y2="175" stroke="#888" stroke-width="2"/>
  <text x="330" y="352" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">SOA es un estilo arquitectónico — los servicios web son su implementación más habitual, no la única</text>
  <text x="650" y="372" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: ERL-SOA, cap. 2-3]</text>
</svg>
```

---

## D7 · SOAP frente a REST

**Sección**: §5.4 — Tipologías de servicios web
**Propósito**: Comparativa directa de naturaleza, formato, modelo, contrato y seguridad entre ambos estilos.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Comparativa entre SOAP, protocolo de mensajería con XML estricto, contrato WSDL formal y extensiones WS-star, y REST, estilo arquitectónico sobre HTTP orientado a recursos con JSON habitual y contrato opcional mediante OpenAPI">
  <style>.t7{font:700 12px system-ui,sans-serif;fill:#fff}.s7{font:9.5px system-ui,sans-serif;fill:#fff}.l7{font:10.5px system-ui,sans-serif;fill:#444}.h7{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h7">SOAP vs. REST</text>
  <rect x="30" y="38" width="290" height="34" rx="5" fill="#0055a0"/><text x="175" y="60" text-anchor="middle" class="t7">SOAP</text>
  <rect x="360" y="38" width="290" height="34" rx="5" fill="#2d8659"/><text x="505" y="60" text-anchor="middle" class="t7">REST</text>
  <rect x="30" y="80" width="290" height="38" fill="#eef4fb"/><text x="175" y="103" text-anchor="middle" class="l7">Protocolo de mensajería (XML)</text>
  <rect x="360" y="80" width="290" height="38" fill="#eafaf1"/><text x="505" y="103" text-anchor="middle" class="l7">Estilo arquitectónico sobre HTTP</text>
  <rect x="30" y="120" width="290" height="38" fill="#f7fafd"/><text x="175" y="143" text-anchor="middle" class="l7">Modelo: operaciones (RPC-like)</text>
  <rect x="360" y="120" width="290" height="38" fill="#f2fbf6"/><text x="505" y="143" text-anchor="middle" class="l7">Modelo: recursos + verbos HTTP</text>
  <rect x="30" y="160" width="290" height="38" fill="#eef4fb"/><text x="175" y="183" text-anchor="middle" class="l7">Contrato: WSDL, formal y obligatorio</text>
  <rect x="360" y="160" width="290" height="38" fill="#eafaf1"/><text x="505" y="183" text-anchor="middle" class="l7">Contrato: opcional (OpenAPI/Swagger)</text>
  <rect x="30" y="200" width="290" height="38" fill="#f7fafd"/><text x="175" y="223" text-anchor="middle" class="l7">Seguridad: WS-Security (nivel mensaje)</text>
  <rect x="360" y="200" width="290" height="38" fill="#f2fbf6"/><text x="505" y="223" text-anchor="middle" class="l7">Seguridad: OAuth 2.0/JWT + TLS</text>
  <rect x="30" y="240" width="290" height="38" fill="#eef4fb"/><text x="175" y="263" text-anchor="middle" class="l7">Uso: integración crítica, sistemas heredados</text>
  <rect x="360" y="240" width="290" height="38" fill="#eafaf1"/><text x="505" y="263" text-anchor="middle" class="l7">Uso: APIs públicas, apps web/móviles</text>
  <text x="340" y="300" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">No hay ganador absoluto: cada estilo domina en escenarios distintos</text>
  <text x="670" y="330" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: W3C-SOAP; FIELDING]</text>
</svg>
```

---

## D8 · Pila de protocolos y estándares de servicios web

**Sección**: §6 — Protocolos y estándares asociados
**Propósito**: Ordenar en capas los estándares del §6: transporte, formato de datos, contrato/descubrimiento y seguridad.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 660 360" role="img" aria-label="Pila de protocolos de servicios web: transporte con HTTP y HTTPS sobre TLS, formato de datos con XML y JSON, contrato y descubrimiento con SOAP, WSDL y UDDI o el estilo REST, y seguridad con OAuth 2.0 y JWT">
  <style>.t8{font:700 11.5px system-ui,sans-serif;fill:#fff}.s8{font:9.5px system-ui,sans-serif;fill:#fff}.l8{font:10.5px system-ui,sans-serif;fill:#444}.h8{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="330" y="20" text-anchor="middle" class="h8">Pila de protocolos de servicios web</text>
  <rect x="60" y="40" width="540" height="54" rx="5" fill="#0055a0"/><text x="330" y="62" text-anchor="middle" class="t8">TRANSPORTE — §6.1</text><text x="330" y="80" text-anchor="middle" class="s8">HTTP/1.1 · HTTP/2 · HTTP/3 · HTTPS (HTTP sobre TLS)</text>
  <rect x="60" y="102" width="540" height="54" rx="5" fill="#3778b5"/><text x="330" y="124" text-anchor="middle" class="t8">FORMATO DE DATOS — §6.3</text><text x="330" y="142" text-anchor="middle" class="s8">XML (SOAP, estándares AAPP) · JSON (REST)</text>
  <rect x="60" y="164" width="540" height="54" rx="5" fill="#2d8659"/><text x="330" y="186" text-anchor="middle" class="t8">CONTRATO Y DESCUBRIMIENTO — §6.4, §6.6</text><text x="330" y="204" text-anchor="middle" class="s8">SOAP: WSDL + UDDI (en desuso) · REST: OpenAPI/Swagger (convención)</text>
  <rect x="60" y="226" width="540" height="54" rx="5" fill="#e89822"/><text x="330" y="248" text-anchor="middle" class="t8">SEGURIDAD — §6.2</text><text x="330" y="266" text-anchor="middle" class="s8">OAuth 2.0 (autorización delegada) · JWT (formato de token) · TLS</text>
  <text x="330" y="306" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">Cada capa es independiente: un servicio REST puede usar XML, y uno SOAP puede viajar sobre HTTPS</text>
  <text x="330" y="326" text-anchor="middle" class="l8">RPC/RMI (§6.5) es el paradigma de invocación remota subyacente a SOAP</text>
  <text x="650" y="352" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: RFC9110; W3C-SOAP; RFC6749]</text>
</svg>
```

---

## D9 · OAuth 2.0: roles y flujo del token

**Sección**: §6.2 — Autenticación y autorización (OAuth 2.0 y JWT)
**Propósito**: Mostrar los cuatro roles de OAuth 2.0 y la secuencia por la que el cliente obtiene y usa un token sin conocer la contraseña del usuario.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Flujo OAuth 2.0: el propietario del recurso autoriza al cliente, el cliente solicita un token al servidor de autorización, recibe un token JWT firmado, y lo presenta al servidor de recursos para acceder sin conocer la contraseña del usuario">
  <style>.t9{font:700 11px system-ui,sans-serif;fill:#fff}.s9{font:9px system-ui,sans-serif;fill:#fff}.l9{font:10px system-ui,sans-serif;fill:#444}.h9{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h9">OAuth 2.0: roles y flujo del token</text>
  <rect x="30" y="46" width="140" height="50" rx="5" fill="#888"/><text x="100" y="68" text-anchor="middle" class="t9">Resource Owner</text><text x="100" y="84" text-anchor="middle" class="s9">El usuario/ciudadano</text>
  <rect x="270" y="46" width="140" height="50" rx="5" fill="#0055a0"/><text x="340" y="68" text-anchor="middle" class="t9">Client</text><text x="340" y="84" text-anchor="middle" class="s9">La aplicación</text>
  <rect x="510" y="46" width="140" height="50" rx="5" fill="#2d8659"/><text x="580" y="68" text-anchor="middle" class="t9">Authorization Server</text><text x="580" y="84" text-anchor="middle" class="s9">Emite el token</text>
  <rect x="510" y="150" width="140" height="50" rx="5" fill="#e89822"/><text x="580" y="172" text-anchor="middle" class="t9">Resource Server</text><text x="580" y="188" text-anchor="middle" class="s9">Protege el recurso</text>
  <path d="M100 96 L100 130 L268 130" stroke="#0055a0" stroke-width="2.5" marker-end="url(#a9)" fill="none"/><text x="170" y="122" text-anchor="middle" style="font:9px system-ui;fill:#0055a0">1. autoriza</text>
  <path d="M410 71 L508 71" stroke="#0055a0" stroke-width="2.5" marker-end="url(#a9)"/><text x="460" y="64" text-anchor="middle" style="font:9px system-ui;fill:#0055a0">2. solicita</text>
  <path d="M580 96 L580 148" stroke="#2d8659" stroke-width="2.5" marker-end="url(#a9)"/><text x="612" y="126" text-anchor="middle" style="font:9px system-ui;fill:#2d8659">3. token</text>
  <path d="M508 175 L412 96" stroke="#e89822" stroke-width="2.5" marker-end="url(#a9)" fill="none"/><text x="500" y="220" text-anchor="middle" style="font:9px system-ui;fill:#e89822">4. presenta token → accede</text>
  <defs><marker id="a9" markerWidth="8" markerHeight="8" refX="4" refY="4" orient="auto"><path d="M0 0 L8 4 L0 8 z" fill="context-fill"/></marker></defs>
  <rect x="30" y="240" width="620" height="66" rx="6" fill="#f4f4f4" stroke="#ccc"/>
  <text x="340" y="264" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">El cliente nunca ve ni almacena la contraseña del usuario</text>
  <text x="340" y="282" text-anchor="middle" class="l9">JWT (header.payload.signature) es, con frecuencia, el formato concreto del token — no un sinónimo de OAuth</text>
  <text x="340" y="298" text-anchor="middle" class="l9">La firma permite validar el token sin consultar al emisor en cada petición</text>
  <text x="670" y="330" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: RFC6749; RFC7519]</text>
</svg>
```

---

## D10 · Verbos HTTP, códigos de estado y modelo de madurez de Richardson

**Sección**: §6.6 — API REST y principios RESTful
**Propósito**: Cheat sheet de verbos/idempotencia, familias de códigos de estado y los cuatro niveles del modelo de Richardson.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 360" role="img" aria-label="Cheat sheet REST: verbos HTTP GET POST PUT PATCH DELETE con su idempotencia, familias de codigos de estado 2xx exito 4xx error cliente 5xx error servidor, y los cuatro niveles del modelo de madurez de Richardson desde RPC disfrazado hasta HATEOAS">
  <style>.t10{font:700 11px system-ui,sans-serif;fill:#fff}.s10{font:9px system-ui,sans-serif;fill:#fff}.l10{font:10px system-ui,sans-serif;fill:#444}.h10{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="18" text-anchor="middle" class="h10">REST: verbos, códigos y modelo de madurez de Richardson</text>
  <rect x="20" y="32" width="90" height="30" rx="4" fill="#0055a0"/><text x="65" y="52" text-anchor="middle" class="t10">GET</text>
  <rect x="118" y="32" width="90" height="30" rx="4" fill="#d13c3c"/><text x="163" y="52" text-anchor="middle" class="t10">POST</text>
  <rect x="216" y="32" width="90" height="30" rx="4" fill="#0055a0"/><text x="261" y="52" text-anchor="middle" class="t10">PUT</text>
  <rect x="314" y="32" width="90" height="30" rx="4" fill="#d13c3c"/><text x="359" y="52" text-anchor="middle" class="t10">PATCH</text>
  <rect x="412" y="32" width="90" height="30" rx="4" fill="#0055a0"/><text x="457" y="52" text-anchor="middle" class="t10">DELETE</text>
  <text x="65" y="76" text-anchor="middle" class="l10">idempotente</text><text x="163" y="76" text-anchor="middle" class="l10">no idemp.</text><text x="261" y="76" text-anchor="middle" class="l10">idempotente</text><text x="359" y="76" text-anchor="middle" class="l10">no idemp.</text><text x="457" y="76" text-anchor="middle" class="l10">idempotente</text>
  <rect x="530" y="32" width="130" height="60" rx="5" fill="#f4f4f4" stroke="#ccc"/><text x="595" y="50" text-anchor="middle" style="font:700 9.5px system-ui;fill:#0055a0">Idempotente:</text><text x="595" y="65" text-anchor="middle" class="l10">repetir = mismo</text><text x="595" y="79" text-anchor="middle" class="l10">efecto que una vez</text>
  <rect x="20" y="102" width="200" height="40" rx="4" fill="#2d8659"/><text x="120" y="126" text-anchor="middle" class="t10">2xx — Éxito</text>
  <rect x="230" y="102" width="200" height="40" rx="4" fill="#e89822"/><text x="330" y="126" text-anchor="middle" class="t10">4xx — Error del cliente</text>
  <rect x="440" y="102" width="200" height="40" rx="4" fill="#d13c3c"/><text x="540" y="126" text-anchor="middle" class="t10">5xx — Error del servidor</text>
  <text x="120" y="156" text-anchor="middle" class="l10">200 OK · 201 · 204</text><text x="330" y="156" text-anchor="middle" class="l10">400 · 401 vs 403 · 404</text><text x="540" y="156" text-anchor="middle" class="l10">500 · 503</text>
  <rect x="20" y="182" width="150" height="46" rx="4" fill="#ccc"/><text x="95" y="202" text-anchor="middle" style="font:700 10px system-ui;fill:#333">Nivel 0</text><text x="95" y="218" text-anchor="middle" style="font:9px system-ui;fill:#333">RPC disfrazado</text>
  <rect x="188" y="182" width="150" height="46" rx="4" fill="#9db8cf"/><text x="263" y="202" text-anchor="middle" style="font:700 10px system-ui;fill:#fff">Nivel 1</text><text x="263" y="218" text-anchor="middle" class="s10">Recursos por URI</text>
  <rect x="356" y="182" width="150" height="46" rx="4" fill="#3778b5"/><text x="431" y="202" text-anchor="middle" style="font:700 10px system-ui;fill:#fff">Nivel 2</text><text x="431" y="218" text-anchor="middle" class="s10">Verbos + códigos</text>
  <rect x="524" y="182" width="136" height="46" rx="4" fill="#0055a0"/><text x="592" y="202" text-anchor="middle" style="font:700 10px system-ui;fill:#fff">Nivel 3</text><text x="592" y="218" text-anchor="middle" class="s10">HATEOAS</text>
  <path d="M170 205 L186 205" stroke="#888" stroke-width="2" marker-end="url(#a10)"/><path d="M338 205 L354 205" stroke="#888" stroke-width="2" marker-end="url(#a10)"/><path d="M506 205 L522 205" stroke="#888" stroke-width="2" marker-end="url(#a10)"/>
  <defs><marker id="a10" markerWidth="7" markerHeight="7" refX="3.5" refY="3.5" orient="auto"><path d="M0 0 L7 3.5 L0 7 z" fill="#888"/></marker></defs>
  <text x="340" y="252" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">401 = no autenticado · 403 = autenticado pero sin permiso</text>
  <text x="340" y="272" text-anchor="middle" class="l10">Nivel 2 es donde se sitúa la inmensa mayoría de las APIs REST reales</text>
  <text x="670" y="352" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: RFC9110; FIELDING]</text>
</svg>
```

---

## D11 · Monolito frente a microservicios

**Sección**: §7.1 — Microservicios
**Propósito**: Contrastar unidad de despliegue, escalado y base de datos entre el monolito y el microservicio.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Comparativa entre monolito, con toda la aplicacion desplegada junta y una base de datos compartida, y microservicios, con servicios pequenos autonomos desplegados y escalados de forma independiente y con base de datos propia cada uno">
  <style>.t11{font:700 11.5px system-ui,sans-serif;fill:#fff}.s11{font:9px system-ui,sans-serif;fill:#fff}.l11{font:10.5px system-ui,sans-serif;fill:#444}.h11{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h11">Monolito vs. microservicios</text>
  <text x="170" y="46" text-anchor="middle" style="font:700 12px system-ui;fill:#0055a0">MONOLITO</text>
  <rect x="60" y="56" width="220" height="120" rx="6" fill="#0055a0"/>
  <text x="170" y="82" text-anchor="middle" class="t11">Presentación</text><text x="170" y="106" text-anchor="middle" class="t11">Negocio</text><text x="170" y="130" text-anchor="middle" class="t11">Datos</text><text x="170" y="158" text-anchor="middle" class="s11">Un único despliegue</text>
  <line x1="80" y1="90" x2="260" y2="90" stroke="#fff" stroke-width="1"/><line x1="80" y1="114" x2="260" y2="114" stroke="#fff" stroke-width="1"/>
  <rect x="100" y="196" width="140" height="34" rx="4" fill="#3778b5"/><text x="170" y="217" text-anchor="middle" class="s11">1 BD compartida</text>
  <line x1="170" y1="176" x2="170" y2="196" stroke="#888" stroke-width="2"/>
  <text x="520" y="46" text-anchor="middle" style="font:700 12px system-ui;fill:#2d8659">MICROSERVICIOS</text>
  <rect x="400" y="56" width="90" height="60" rx="5" fill="#2d8659"/><text x="445" y="82" text-anchor="middle" class="t11">Servicio</text><text x="445" y="98" text-anchor="middle" class="s11">Expedientes</text>
  <rect x="500" y="56" width="90" height="60" rx="5" fill="#2d8659"/><text x="545" y="82" text-anchor="middle" class="t11">Servicio</text><text x="545" y="98" text-anchor="middle" class="s11">Tributos</text>
  <rect x="600" y="56" width="60" height="60" rx="5" fill="#2d8659"/><text x="630" y="82" text-anchor="middle" class="s11">Notif.</text>
  <rect x="400" y="196" width="90" height="34" rx="4" fill="#e89822"/><text x="445" y="217" text-anchor="middle" class="s11">BD propia</text>
  <rect x="500" y="196" width="90" height="34" rx="4" fill="#e89822"/><text x="545" y="217" text-anchor="middle" class="s11">BD propia</text>
  <rect x="600" y="196" width="60" height="34" rx="4" fill="#e89822"/><text x="630" y="217" text-anchor="middle" class="s11" style="font-size:8px">BD</text>
  <line x1="445" y1="116" x2="445" y2="196" stroke="#888" stroke-width="2"/><line x1="545" y1="116" x2="545" y2="196" stroke="#888" stroke-width="2"/><line x1="630" y1="116" x2="630" y2="196" stroke="#888" stroke-width="2"/>
  <rect x="30" y="256" width="620" height="66" rx="6" fill="#f4f4f4" stroke="#ccc"/>
  <text x="340" y="280" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">Escalado independiente y despliegue autónomo, a cambio de mayor complejidad operacional</text>
  <text x="340" y="298" text-anchor="middle" class="l11">Consistencia fuerte (ACID) en el monolito vs. consistencia eventual habitual entre microservicios</text>
  <text x="340" y="314" text-anchor="middle" class="l11">Los microservicios son una evolución radical de los principios de SOA (§5.2)</text>
  <text x="670" y="332" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: NEWMAN, cap. 1]</text>
</svg>
```

---

## D12 · Contenedores, orquestación y nube

**Sección**: §7.3-7.4 — Contenedores y orquestación · Computación en la nube
**Propósito**: Situar en niveles apilados el contenedor, la orquestación y la nube como destino de despliegue.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 660 360" role="img" aria-label="Niveles apilados de despliegue moderno: en la base los contenedores que virtualizan a nivel de sistema operativo, encima la orquestación con Kubernetes que automatiza despliegue escalado y recuperación, y arriba la computación en la nube que aporta el entorno elastico bajo demanda">
  <style>.t12{font:700 11.5px system-ui,sans-serif;fill:#fff}.s12{font:9.5px system-ui,sans-serif;fill:#fff}.l12{font:10.5px system-ui,sans-serif;fill:#444}.h12{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="330" y="20" text-anchor="middle" class="h12">Contenedores → orquestación → nube</text>
  <rect x="60" y="248" width="540" height="60" rx="6" fill="#0055a0"/><text x="330" y="272" text-anchor="middle" class="t12">CONTENEDORES — §7.3</text><text x="330" y="292" text-anchor="middle" class="s12">Virtualizan a nivel de SO (namespaces/cgroups), arranque en segundos</text>
  <path d="M330 246 L330 218" stroke="#888" stroke-width="3" marker-end="url(#a12)"/>
  <rect x="60" y="164" width="540" height="60" rx="6" fill="#2d8659"/><text x="330" y="188" text-anchor="middle" class="t12">ORQUESTACIÓN — §7.3</text><text x="330" y="208" text-anchor="middle" class="s12">Kubernetes: despliegue, autoescalado y recuperación automática</text>
  <path d="M330 162 L330 134" stroke="#888" stroke-width="3" marker-end="url(#a12)"/>
  <rect x="60" y="80" width="540" height="60" rx="6" fill="#e89822"/><text x="330" y="104" text-anchor="middle" class="t12">COMPUTACIÓN EN LA NUBE — §7.4</text><text x="330" y="124" text-anchor="middle" class="s12">IaaS/PaaS/SaaS bajo demanda — desarrollado en el Tema 31</text>
  <defs><marker id="a12" markerWidth="9" markerHeight="9" refX="4.5" refY="4.5" orient="auto"><path d="M0 0 L9 4.5 L0 9 z" fill="#888"/></marker></defs>
  <text x="330" y="336" text-anchor="middle" style="font:700 11px system-ui;fill:#d13c3c">Contenedor virtualiza el SO; máquina virtual (Tema 28) virtualiza el hardware — no confundir</text>
  <text x="650" y="356" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: K8S-DOCS; NIST800145]</text>
</svg>
```
