# Decisiones de modelado en Archi

Registro de las decisiones tomadas al construir `modelo/recaudo.archimate`. Hay que actualizarlo cada vez que se agregue o cambie una vista, para que todo el equipo (y cualquier asistente de IA) trabaje con las mismas convenciones.

## 1. Convenciones generales

| Tema | Decisión | Motivo |
|---|---|---|
| Nombres de elementos | Se usa el nombre **sin código** (p. ej. «Gerencia General», no «INT01 Gerencia General») | El diagrama queda más limpio y el nombre es el mismo del glosario y del README |
| Códigos | El código del README (INT01, IMP01, EVA01, MET01, RES01, PRI01, REQ01, RESC01) va en la propiedad **`ID`** del elemento | Permite cruzar cada elemento con las tablas del README |
| Documentación | La descripción de la tabla del README se copia en la *Documentation* del elemento | El modelo se puede leer sin el README |
| Carpetas | Cada elemento en la carpeta de su capa (Motivation, Strategy, Business, Application). Todas las relaciones en *Relations* | Es la estructura por defecto de Archi |
| Viewpoint de las vistas | **None** cuando la vista mezcla capas (V1 incluye un componente de aplicación). Solo se usa un viewpoint restringido si la vista es de una sola capa | Con un viewpoint restringido Archi marca como inválidos los elementos de otras capas |
| Franjas y agrupaciones visuales | Se usan **grupos visuales** de Archi (*Group*, no el elemento *Grouping*) para las franjas de una vista | El grupo visual no agrega elementos ni relaciones al modelo |
| Colores | ArchiMate por defecto como base; las excepciones por vista se documentan en las secciones siguientes y en CLAUDE.md | Mantiene una base común sin borrar las codificaciones semánticas específicas |

## 2. Elementos compartidos entre vistas

| Elemento | Tipo | Creado en | Se debe reutilizar en |
|---|---|---|---|
| Aplicación de recaudo SIT | Componente de aplicación | V1 | V8 (lo componen los componentes de cada contexto), V10 (final de la cadena de trazabilidad) |
| Metas MET01–MET07 | Meta | V1 | V2 (realizadas por capacidades y cursos de acción), V10 |
| Requerimientos REQ01–REQ12 | Requerimiento | V1 | V4 y V10 (los realizan servicios de negocio y de aplicación) |

> Antes de crear un elemento, buscarlo en el árbol del modelo. Si ya existe, **arrastrarlo** a la vista en lugar de crear uno nuevo (si no, aparece duplicado y se rompe la trazabilidad).
> El nombre «Aplicación de recaudo SIT» es provisional hasta cerrar el glosario (T26). Si cambia, se renombra en un solo lugar.

## 3. V1 Motivación (T12)

**Contenido:** los 83 elementos de motivación del README §2 más el componente «Aplicación de recaudo SIT». Son 84 elementos y 120 relaciones, sin elementos huérfanos.

**Disposición:** 9 franjas de arriba abajo: Interesados → Impulsores → Evaluaciones → Metas → Resultados → Principios → Requerimientos → Aplicación → Restricciones. Las metas quedan en orden MET01–MET07 como ancla, y el resto de cada franja se ordenó para reducir los cruces de líneas.

**Semántica de las relaciones:**

| Desde | Relación | Hacia | Significado |
|---|---|---|---|
| Interesado | asociación | Impulsor | Al interesado le importa ese impulsor |
| Impulsor | asociación | Evaluación | El impulsor se manifiesta en ese problema |
| Evaluación | influencia (+) | Meta | El problema motiva la meta |
| Resultado | realización | Meta | El resultado medible hace realidad la meta |
| Principio | realización | Meta | El principio orienta cómo se logra la meta |
| Requerimiento | realización | Resultado / Principio / Meta | El requerimiento produce el resultado o aplica el principio |
| Restricción | influencia (−) | Requerimiento / Resultado / Meta | La restricción limita la solución |
| Aplicación de recaudo SIT | realización | REQ01–REQ12, RESC01, RESC02 | La aplicación cumple los requerimientos y las restricciones técnicas de interoperar con la plataforma existente |

**Relaciones concretas:**
- **Interesado → impulsor:** INT01 → IMP01, IMP02, IMP04, IMP07 · INT02 → IMP01, IMP03, IMP08 · INT03 → IMP04, IMP05 · INT04 → EVA05 (directo a la evaluación; ningún impulsor encaja) · INT05 → IMP04 · INT06 → IMP06 · INT07 → IMP02, IMP03 · INT08, INT09 → IMP03 · INT10 → IMP01 · INT11 → IMP04, IMP06, IMP07 · INT12 → IMP02 · INT13 → IMP05 · INT14 → IMP04 · INT15 → IMP02
- **Impulsor → evaluación:** IMP01 → EVA01 · IMP02 → EVA02, EVA11 · IMP03 → EVA02, EVA04, EVA09 · IMP04 → EVA06, EVA07, EVA08, EVA10, EVA12 · IMP05, IMP06 → EVA03 · IMP08 → EVA02 · IMP07 influye (+) directamente en RES09
- **Evaluación → meta:** EVA01 → MET01, MET06 · EVA02, EVA04, EVA09 → MET02 · EVA03 → MET01, MET07 · EVA05 → MET03 · EVA06, EVA07, EVA08, EVA10, EVA12 → MET04 · EVA11 → MET05
- **Resultado → meta:** RES01, RES02, RES03 → MET02 · RES03, RES08 → MET01 · RES04 → MET03 · RES05, RES06, RES07 → MET04 · RES08 → MET05 · RES09 → MET06
- **Principio → meta:** PRI01, PRI07, PRI08, PRI10 → MET03 · PRI02, PRI06, PRI09 → MET05 · PRI03 → MET02 · PRI04 → MET01, MET02 · PRI05 → MET04
- **Requerimiento →:** REQ01 → RES03, MET01, MET07 · REQ02 → PRI01, PRI02 · REQ03 → RES01, RES02, RES03 · REQ04 → PRI05 · REQ05 → RES05, RES06 · REQ06 → RES06 · REQ07 → RES04 · REQ08 → RES04, PRI08 · REQ09 → PRI09 · REQ10 → RES08 · REQ11 → RES06, RES07 · REQ12 → RES03, PRI04
- **Restricción (−):** RESC01, RESC02 → REQ01 · RESC03, RESC07, RESC08 → RES09 · RESC04 → MET06 · RESC05 → REQ09 · RESC06 → REQ03 · RESC09 → PRI07 · RESC10 → REQ12

**Decisiones particulares:**
- MET07 (integración metropolitana) no tiene un resultado medible en la entrevista. Por eso la realiza directamente REQ01 (intercambio de información).
- Las restricciones de proyecto (presupuesto, contratación, plazos, capacidad del equipo) influyen sobre la meta o el resultado de transición (MET06 y RES09), no sobre la aplicación, porque el software no las «cumple».
- Validación en Archi: el viewpoint *Motivation* rechazaba el componente de aplicación, así que la vista quedó con viewpoint **None**.

## 4. Pendientes para las siguientes vistas (resueltos)
- **V2:** las metas MET01–MET07 se relacionan con capacidades a través de los cursos de acción (resuelto en T34; ver §11).
- **V10:** se hicieron 3 cadenas: MET01, MET02 y MET04 (ver §11).

## 5. V4, V4b, V4c, V4d y V9 (T20, T21 y T22)

**Contenido nuevo:** 209 elementos y 240 relaciones. Cada elemento lleva su descripción en *Documentation* y un código en la propiedad `ID` (los servicios `SN-P1`, `SN-P1.1`, `SN-P1.1.1`; los contratos `CT-P1.1.1`; los externos `E1` a `E14`; las ACL `ACL-E1`…). Los nombres van sin código, como en V1.

**Vistas:**

| Vista | Qué muestra |
|---|---|
| V4 Descomposición de servicios | Capas 1 a 3: el servicio E2E, 10 servicios de plataforma y 19 de dominio funcional. En gris, los 6 servicios de plataforma que quedan fuera del alcance |
| V4b Contratos de servicio | Un objeto *Contract* por cada servicio de capa 4 (52). Entradas, salidas, errores y requisitos no funcionales están en la documentación de cada contrato |
| V4c Servicios básicos de subdominio | Capa 4, agrupada por servicio de dominio funcional, y los 8 servicios de capa 4 que no se implementan |
| V4d Roles, funciones y objetos de negocio | Rol y actor que ejecutan cada servicio de plataforma, la función que lo realiza y los objetos de negocio que maneja |
| V9 Interoperabilidad y anticorrupción | Los 14 externos de la tabla del README §4, con la dirección de cada flujo. 8 con ACL y 6 directos |

**Relaciones usadas:**

| Desde | Relación | Hacia | Significado |
|---|---|---|---|
| Servicio de una capa | agregación | Servicio de la capa de abajo | La capa de abajo compone a la de arriba. No se usó composición porque un servicio puede reutilizarse |
| Servicio de plataforma | realización | Requerimiento (REQ01 a REQ11 de V1) | El servicio realiza el requerimiento. Está en el modelo pero no se dibuja en V4 para no cargarla |
| Servicio básico | acceso (lectura) | Contrato | El contrato define cómo se llama el servicio |
| Función | realización | Servicio de plataforma | La función de negocio realiza el servicio |
| Rol | asignación | Función | Quién la ejecuta |
| Ente gestor | asignación | Rol | El ente gestor cumple los roles con sus áreas |
| Servicio de plataforma | acceso (lectura/escritura) | Objeto de negocio | Qué maneja el servicio |
| Externo / ACL / aplicación | flujo | Externo / ACL / aplicación | La información que se intercambia y su dirección, escrita en el nombre del flujo. Los que van en sentido contrario se dibujan con un quiebre para no taparse |
| Aplicación de recaudo SIT | composición | Interfaz de reportes y liquidación | La interfaz es parte de la aplicación |

**Decisiones particulares:**
- **Elementos reutilizados:** V9 usa el componente «Aplicación de recaudo SIT» que ya creó V1. Los servicios apuntan a los requerimientos REQ de V1 (no se crearon nuevos).
- **ACL o no:** tienen ACL los 8 externos cuyo modelo es ajeno o no controlamos (proveedor, PQR, finanzas, fiduciaria, adquirente, canales, instituciones y operaciones). Planeación y la autoridad de transporte son *conformistas*. Hacienda, operadores, entes de control y la autoridad reciben lo que el software les entrega por la *interfaz de reportes y liquidación* (lenguaje publicado). **V8 debe repetir estos patrones.**
- **V9 con viewpoint** `application_cooperation`: solo tiene elementos de la capa de aplicación, por eso no hay conflicto.
- **Liquidación a operadores (P8):** se incluye como servicio de plataforma, pero solo aplica las fórmulas de cada contrato; no las decide (RESC06).
- **Servicio de consulta (P10):** es un servicio de plataforma propio (tiene usuarios y reglas propias) aunque se alimenta de los demás. En DDD corresponde al dominio genérico DOM10 de V5, que solo lee lo que producen los dominios operacionales.

**Pendientes:** al hacer V5 a V8 y V10, reutilizar estos servicios (para V10, las cadenas meta → capacidad → servicio de negocio → componente pueden salir de estos servicios y de los REQ).

**Colores de V4, V4b, V4c, V4d y V9:** siguen la paleta de la presentación de TOGAF (`10_Arquitectura_Empresarial_TOGAF`) y no la de Archi por defecto. Negocio `#FEFF99` (amarillo), aplicación `#F0FFFF` (celeste muy claro), estrategia `#FBE0A7`, motivación `#ADB0FF` y tecnología `#CDFFCC`. Se guardan como color de relleno de cada objeto en la vista. En gris (`#D9D9D9`) van los servicios y los externos que quedan fuera del alcance. V1 y V2 conservan sus colores, y V2 usa colores propios por categoría (estratégica, misional y de apoyo). Esta es una excepción intencional a la paleta ArchiMate por defecto, limitada a estas vistas. V2, V5, V6, V7 y V8 conservan sus codificaciones específicas, descritas en esta guía y en CLAUDE.md.

## 6. V5 Dominios (T25)

**Contenido nuevo:** 11 elementos (los 10 dominios como elemento *Grouping* y el objeto de negocio «Solicitud de consulta») y 30 relaciones. Los dominios (DOM01 a DOM10) y su clasificación son los de README §5.4 y §5.5 (T23 y T24); la vista no los cambia.

| Relación | Desde | Hacia | Para qué |
|---|---|---|---|
| Agregación | Dominio | Objeto de negocio | Los conceptos principales del dominio. Los objetos de negocio son los que ya creó V4d, así que V4 y V5 comparten elementos |
| Asociación | Dominio | Servicio de plataforma de V4 (P1 a P10) | Cada dominio se apoya en el servicio de plataforma que corresponde (DOM01 con P1, DOM02 con P2, etc.). Está en el modelo pero no se dibuja |

**Decisiones:**
- Los dominios son el elemento *Grouping* (el enunciado pide «agrupación» en V5). Las franjas de la vista (centrales, de soporte, genérico) son *Group* visuales, como pide la convención de este archivo.
- El color de cada dominio sale de su clasificación, no de su capa: central salmón `#F8CBAD`, de soporte azul `#BDD7EE` y genérico gris `#D9D9D9`. V8 reutiliza exactamente esta codificación. Los objetos de negocio de V5 usan amarillo `#FEFF99`.
- La «Base de liquidación» se muestra en DOM08 (Liquidación a operadores), como en el README §5.4, aunque en V4 vive en el servicio de consolidación.
- V6 puede reutilizar estos objetos de negocio como raíces de agregado (objetos de datos que los realicen).

## 7. V7 Lenguaje ubicuo (T27)

**Contenido nuevo:** 61 elementos (37 significados `SIG01`–`SIG37`, 21 representaciones `REP01`–`REP21`, los roles «Pasajero» y «Cliente» y el objeto de negocio «Perfil de acceso» `O21`) y 60 relaciones. Reutiliza los 20 objetos de negocio de V4d/V5 y los actores «BA08 · Usuario del sistema», «Operadores de flota y operador del metro» y «BA01 · Proveedor de recaudo».

| Relación | Desde | Hacia | Para qué |
|---|---|---|---|
| Realización | Representación | Objeto de negocio | La forma concreta en que aparece el objeto (documento, archivo, pantalla) |
| Asociación | Significado | Objeto de negocio, actor o rol | La definición del glosario (README §5.8) que le da sentido |
| Asignación | Usuario del sistema | Pasajero, Cliente | La misma persona cumple papeles distintos |

**Decisiones:**
- El nombre de cada significado es «Término: definición corta»; la definición completa y la referencia al glosario están en su documentación.
- Los términos con doble significado (Tarifa, Saldo, Transacción, Perfil, Operador) se pintan en naranja `#FFC48C` y aparecen una vez por contexto. Los demás significados usan el lila de motivación `#ADB0FF` y los objetos de negocio y representaciones el amarillo `#FEFF99` (paleta de TOGAF, como V4 y V5).
- Las franjas por dominio son *Group* visuales; los términos de DDD del glosario no se modelan.
- **Duplicado resuelto:** había dos actores para los operadores («Operadores de flota y operador del metro» de V4d y «BA05 · Operadores del SIT» de V3) y dos para la fiduciaria («Fiduciaria» de V4d y «BA06 · Fiduciaria / patrimonio autónomo» de V3). Los de V3 no tenían relaciones, así que se borraron y V3 apunta ahora a los de V4d, que conservan su `ID` (A2 y A3) y recogen la documentación de los borrados.
- **Deuda de tarjeta y Cartera:** no se renombró el objeto de negocio. Son dos niveles del mismo concepto (una tarjeta frente al total que ve Finanzas), así que V7 asocia los dos significados al objeto «Deuda de tarjeta» y el glosario los diferencia.

## 8. V6a a V6j Agregados, comandos y eventos (T29)

**Contenido nuevo:** 107 elementos de aplicación (10 raíces `AG-DOMxx`, 2 entidades, 53 objetos de valor, 21 comandos `CMD-DOMxx` y 21 eventos `EVT-DOMxx`; DOM02 tiene tres comandos: emitir, recargar y bloquear) y 133 relaciones. Una vista por dominio; V6a reutiliza la vista vacía original y las otras nueve se crearon a continuación.

| Relación | Desde | Hacia | Para qué |
|---|---|---|---|
| Composición | Raíz (objeto de datos) | Entidad / objeto de valor | Lo que está dentro del límite del agregado. En la vista se muestra anidado |
| Realización | Raíz | Objeto de negocio de V5 | Traza el modelo táctico al estratégico |
| Acceso (lectura/escritura) | Comando (proceso de aplicación) | Raíz | El comando solo entra por la raíz |
| Disparo | Comando | Evento (evento de aplicación) | El evento que emite cuando la raíz acepta el comando |
| Disparo | Rol de V4d, evento de negocio de V3 o evento de otro dominio | Comando | Quién lo dispara. Entre dominios se nombra «política: …» |
| Realización | Evento de aplicación | Evento de negocio de V3 | ResultadoConciliaciónRegistrado → BE03/BE04; LiquidaciónAprobada → BE05 |

**Decisiones:**
- Colores: raíz `#9FC9F3` en negrita, entidad `#CFE4FA`, objeto de valor y elementos de aplicación `#F0FFFF`, negocio `#FEFF99` y elementos de otro dominio en gris `#D9D9D9`.
- Las invariantes van en una nota dentro del límite del agregado y también en la documentación de la raíz.
- Los objetos de valor con el mismo nombre en dominios distintos son elementos distintos (cada contexto tiene su modelo; no hay núcleo compartido).
- Las líneas de acceso de los comandos a la raíz usan puntos de quiebre para no cruzar las cajas; si se mueven elementos en Archi, hay que revisar esas líneas.

## 9. V8 Mapa de contextos (T31)

**Contenido nuevo:** 25 elementos de aplicación (10 componentes de contexto `BC01`–`BC10`, 12 servicios de aplicación `AS-Sxx` y 3 interfaces OHS `AI-BCxx`) y 52 relaciones. Reutiliza «Aplicación de recaudo SIT» (V1), la «Interfaz de reportes y liquidación», los 8 componentes ACL, los externos y todos los flujos de V9.

| Relación | Desde | Hacia | Para qué |
|---|---|---|---|
| Composición | Aplicación de recaudo SIT | Componente de contexto | La aplicación se compone de los 10 bounded contexts (se usa en V10) |
| Realización | Componente de contexto | Servicio de aplicación | Lo que el contexto ofrece a otros |
| Servicio | Servicio de aplicación | Componente que lo consume | Las 21 relaciones de README §7.2; el nombre es el patrón. Todas las salidas de los servicios de BC01, BC02 y BC07 se llaman «OHS + PL», porque el servicio abierto es una propiedad del proveedor y no de cada consumidor; las demás, «C/S + PL» |
| Composición | Contexto BC01, BC02 o BC07 | Interfaz «API pública … (OHS)» | El servicio abierto de §7.4 |
| Flujo | Componente de contexto | Componente de contexto | Eventos de las políticas de V6; el nombre es «evento: …» |

**Decisiones:**
- Nombres de los componentes: «Contexto de …», para no confundirlos con el *Grouping* del dominio de V5. El código `BCxx` va en la propiedad `ID`.
- Colores: el de la clasificación del dominio en V5 (central `#F8CBAD`, de soporte `#BDD7EE`, genérico `#D9D9D9`); servicios e interfaces `#F0FFFF`; externos `#E7E6E6`.
- Los externos se conectan al contenedor con los flujos de V9; los que tienen ida y vuelta se dibujan con un quiebre para que no se encimen.

## 10. V11 Bounded Context Canvas (T33)

**Contexto:** procesamiento de transacciones (BC05). Justificación y mapeo de secciones en README §8.

**Contenido nuevo:** 7 restricciones `RN-BC05-01`–`07` (reglas de negocio de la entrevista) y 29 relaciones: realización de BC05 hacia REQ01 y hacia cada restricción, y **asignación de cada contexto (V8) a sus comandos (V6)**, 21 en total.

**Decisiones:**
- Las 11 secciones del canvas son *Group* visuales numerados. Dentro van elementos ya existentes (V1, V3, V5, V6, V7, V8, V9) y notas solo para modelo de negocio, evolución, roles, supuestos, métricas del límite y preguntas abiertas.
- El contexto aparece dos veces: en «Nombre» y en el centro, donde contiene (anidados) sus comandos y su servicio para que las relaciones de comunicación entren y salgan de él.
- Viewpoint **None** (mezcla motivación, negocio y aplicación).
- Si se reorganiza, mantener la distribución de ddd-crew: identidad a la izquierda, comunicación en el centro, lenguaje y decisiones a la derecha, y supuestos, métricas y preguntas abajo.

## 11. V10 Trazabilidad vertical (T34)

**Corrección en V2:** CA01–CA06 pasaron de *Outcome* a *CourseOfAction* y a la carpeta Strategy. No tenían relaciones.

**Relaciones nuevas (61), todas de realización:**

| Desde | Hacia | Cuántas | Fuente |
|---|---|---|---|
| Servicio de plataforma (SN-P1…P10) | Capacidad | 23 | Columna «Capacidad en V2» de la tabla de descomposición (README §4) |
| Capacidad | Curso de acción | 18 | CA01 ← CAP25, 26 · CA02 ← CAP27, 28, 29, 30, 34 · CA03 ← CAP19, 20, 21, 22, 24 · CA04 ← CAP07, 32, 40 · CA05 ← CAP37 · CA06 ← CAP08, 10 |
| Curso de acción | Meta | 10 | CA01 → MET01, MET06 · CA02 → MET02 · CA03 → MET03, MET04 · CA04 → MET04, MET05 · CA05 → MET06, MET07 · CA06 → MET05 |
| Contexto (BC01…BC10) | Servicio de plataforma (P1…P10) | 10 | Correspondencia DOMxx ↔ Px de V5 |

**Vista:** tres cadenas (MET01 por BC05, MET02 por BC07 y BC08, MET04 por BC03) en franjas por capa: motivación, estrategia, negocio y aplicación. Las franjas son *Group* visuales. Viewpoint None.

**Resaltado de impacto en V2 (rúbrica):** las capacidades con impacto directo llevan borde rojo `#C00000` de grosor 3 y las de impacto indirecto borde naranja `#ED7D31` de grosor 2 (con `deriveElementLineColor = false` para que Archi no derive el borde del relleno). Las que no tienen impacto conservan su borde. El relleno sigue siendo por categoría. Leyenda al pie de la vista.

## 12. Revisión de calidad del modelo (T35)

**Resultado:** 597 elementos y 840 relaciones; 23 vistas (conteo actualizado después de la revisión externa, §13).

| Revisión | Resultado |
|---|---|
| Relaciones permitidas por ArchiMate (tabla de relaciones de Archi 5.10) | 0 inválidas |
| Elementos sin ninguna relación | 0 (había 51) |
| Elementos que no aparecen en ninguna vista | 0 |
| Elementos anidados en una vista sin relación con su contenedor | 0 |
| Relaciones repetidas (mismo tipo, origen y destino) | 0 |
| Vistas vacías | 0 |
| PNG de `/vistas` idénticos a la vista renderizada desde el modelo | 23 de 23 |

**Relaciones agregadas para quitar los 51 huérfanos (73, ninguna se dibuja, así que las vistas no cambian):**
- Servicios fuera de alcance de capa 2 (SN-X1 a X6): el proceso E2E los agrega, y realizan su capacidad (X1 → CAP17, X2 → CAP14 y CAP15, X3 → CAP13, X4 → CAP23, X5 → CAP33, X6 → CAP22).
- Servicios excluidos de capa 4 (SN-X7 a X14): cuelgan, por agregación, del servicio de quien los ejecuta (X7–X9 del proveedor, X10 de Operaciones, X11 de Cobro diferido, X12 de Esquema de remuneración, X13 de Perfiles tarifarios, X14 de Ciclo de vida de la tarjeta).
- Capacidades que no tenían relación: realizan el curso de acción que les corresponde (CAP02, 03, 04, 05, 06, 09, 11, 12, 18, 31, 38, 39, 41, 42).
- Recursos R01 a R05: asignados a las capacidades que habilitan.
- Capacidades de apoyo fuera del alcance (CAP01, 16, 35, 36, 43, 44): asociación con el actor «Ente gestor del SIT».
- V3: el equipo de Recaudo y Tarifas (BA03) se asigna a BP00, BP04–BP07; Finanzas (BA04) a BP08; redes de pago (BA02) y las instituciones (BA07) se asocian a BP01 y BP00; VS00 se compone de VS01–VS08.

**Advertencias aceptadas (no son errores):**
- *IdentificadorTarjeta* y *PeriodoVigencia* aparecen tres veces como objetos de datos: es intencional, cada contexto tiene su propio modelo (V6, sin núcleo compartido). Archi las puede mostrar como «posibles duplicados».
- Hay elementos de capas distintas con el mismo nombre (p. ej. el dominio «Liquidación a operadores» como *Grouping* y el servicio de negocio del mismo nombre). Es intencional: son el mismo concepto visto desde capas distintas.
- Los elementos de V2 y V3 (CAPxx, Rxx, CAxx, VSxx, BPxx, BExx, BAxx) llevan el código en el nombre, en contra de la convención §1. Se mantienen porque el README los cita por código en muchas secciones.

## 13. Correcciones por la revisión externa del proyecto

Un revisor independiente comparó el proyecto con la rúbrica. Estas son las correcciones que tocaron el modelo (las de texto están en el README):

| Hallazgo | Corrección en el modelo |
|---|---|
| V3 no reflejaba la corrección de la experta al proceso E2E (pregunta 2.9) | BP03 pasa a «Verificar tarifa esperada, perfil y transbordos» (la tarifa la aplica el validador). Se agregan BP11 (adquirir y recargar VAMOS), BP12 (cobro diferido de la tarjeta bancaria), BP13 (consignación de los canales a la fiducia, externo) y BP14 (bloqueos, devoluciones y reclamos), y un *Group* visual «Carril de excepciones» con BP06 y BP14. Los procesos que soporta la aplicación llevan borde azul grueso y una relación de servicio desde «Aplicación de recaudo SIT» (13 relaciones, no dibujadas); leyenda al pie |
| «Viaje» se usaba como sinónimo de una validación, en contra del glosario | La raíz de DOM05 pasa a `TransacciónDeValidación` y su evento a `TransacciónDeValidaciónProcesada` (V6e, V8, V11). BE08 pasa a «Validación registrada en el acceso (externo)» |
| «Perfil de titular» no seguía la regla «perfil tarifario / perfil de acceso» | El objeto de negocio pasa a «Perfil tarifario del titular» (V4d, V5, V6c, V7) |
| DOM02 no tenía la emisión de la tarjeta ni la regla del viaje de emergencia | Comando `EmitirTarjeta` → `TarjetaEmitida` (lo dispara el asesor de Servicio al Cliente) e invariante 4 de `TarjetaVAMOS`: el saldo calculado nunca es menor que menos una tarifa |
| El patrón OHS se aplicaba por consumidor | Todas las salidas de los servicios OHS de BC01, BC02 y BC07 se llaman «OHS + PL» (V8) |
| La regla de no validar dos veces en el mismo punto en 10 minutos no estaba en el diseño | Restricción `RN-BC05-07` en V11 |
| CAP24 (ajustes y devoluciones) estaba como impacto indirecto aunque P9 y DOM09 la ejecutan | Pasa a impacto directo: 21 directas, 16 indirectas y 7 sin impacto (V2) |

**Cómo se aplicaron:** V6, V8, V11 y V10 se regeneraron en cadena desde la copia del modelo previa a V6, con los mismos generadores y los cambios de arriba. Al final, el modelo sigue con 0 relaciones inválidas, 0 huérfanos y 0 elementos fuera de vistas, y los 23 PNG coinciden con lo que renderiza el modelo.

**No se cambió (decisión del equipo):** la clasificación de seis dominios centrales se mantiene; en el README §5 (V5) se agregó el criterio explícito y el orden de prioridad (DOM05, luego DOM07 y DOM08). Los actores fusionados de V3 («Operadores de flota y operador del metro» y «Fiduciaria») no recuperan el código BA05/BA06 en el nombre para no reintroducir códigos en V4d y V7.
