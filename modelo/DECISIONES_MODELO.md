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
