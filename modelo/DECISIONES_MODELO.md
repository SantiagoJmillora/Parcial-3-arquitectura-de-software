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
| Colores | Los de ArchiMate por defecto | CLAUDE.md §6 |

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

## 4. Pendientes para las siguientes vistas
- **V2:** reutilizar MET01–MET07 y relacionarlas con capacidades y cursos de acción (T14).
- **V10:** escoger al menos 2 cadenas meta → capacidad → servicio → componente. Candidatas: MET02 (liquidación y conciliación confiables) y MET04 (reducción de pérdidas).

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

**Colores de V4, V4b, V4c, V4d y V9:** siguen la paleta de la presentación de TOGAF (`10_Arquitectura_Empresarial_TOGAF`) y no la de Archi por defecto. Negocio `#FEFF99` (amarillo), aplicación `#F0FFFF` (celeste muy claro), estrategia `#FBE0A7`, motivación `#ADB0FF` y tecnología `#CDFFCC`. Se guardan como color de relleno de cada objeto en la vista. En gris (`#D9D9D9`) van los servicios y los externos que quedan fuera del alcance. V1 y V2 conservan sus colores, y V2 usa colores propios por categoría (estratégica, misional y de apoyo). Esto se aparta de lo que dice CLAUDE.md §6 ("los de ArchiMate por defecto"), así que el equipo debe decidir si todas las vistas usan esta paleta.

## 6. V5 Dominios (T25)

**Contenido nuevo:** 11 elementos (los 10 dominios como elemento *Grouping* y el objeto de negocio «Solicitud de consulta») y 30 relaciones. Los dominios (DOM01 a DOM10) y su clasificación son los de README §5.4 y §5.5 (T23 y T24); la vista no los cambia.

| Relación | Desde | Hacia | Para qué |
|---|---|---|---|
| Agregación | Dominio | Objeto de negocio | Los conceptos principales del dominio. Los objetos de negocio son los que ya creó V4d, así que V4 y V5 comparten elementos |
| Asociación | Dominio | Servicio de plataforma de V4 (P1 a P10) | Cada dominio se apoya en el servicio de plataforma que corresponde (DOM01 con P1, DOM02 con P2, etc.). Está en el modelo pero no se dibuja |

**Decisiones:**
- Los dominios son el elemento *Grouping* (el enunciado pide «agrupación» en V5). Las franjas de la vista (centrales, de soporte, genérico) son *Group* visuales, como pide la convención de este archivo.
- El color de cada dominio sale de su clasificación (central rojo, de soporte azul, genérico gris), no de su capa. Los objetos de negocio usan el amarillo de la paleta de TOGAF.
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

**Contenido nuevo:** 105 elementos de aplicación (10 raíces `AG-DOMxx`, 2 entidades, 53 objetos de valor, 20 comandos `CMD-DOMxx` y 20 eventos `EVT-DOMxx`) y 130 relaciones. Una vista por dominio; V6a reutiliza la vista vacía original y las otras nueve se crearon a continuación.

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
| Servicio | Servicio de aplicación | Componente que lo consume | Las 21 relaciones de README §7.2; el nombre es el patrón (C/S + PL u OHS + PL) |
| Composición | Contexto BC01, BC02 o BC07 | Interfaz «API pública … (OHS)» | El servicio abierto de §7.4 |
| Flujo | Componente de contexto | Componente de contexto | Eventos de las políticas de V6; el nombre es «evento: …» |

**Decisiones:**
- Nombres de los componentes: «Contexto de …», para no confundirlos con el *Grouping* del dominio de V5. El código `BCxx` va en la propiedad `ID`.
- Colores: el de la clasificación del dominio en V5 (central `#F8CBAD`, de soporte `#BDD7EE`, genérico `#D9D9D9`); servicios e interfaces `#F0FFFF`; externos `#E7E6E6`.
- Los externos se conectan al contenedor con los flujos de V9; los que tienen ida y vuelta se dibujan con un quiebre para que no se encimen.
