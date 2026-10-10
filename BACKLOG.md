# BACKLOG: Parcial 3, recaudo del sistema integrado de transporte

> **Turno de modelo (archivo .archimate):** _libre_  ← escribe tu nombre aquí antes de abrir Archi y vuelve a dejarlo en _libre_ al terminar (ver [CLAUDE.md §7](CLAUDE.md#7-cómo-trabajamos-sin-responsables-fijos)).

## Cómo usar este backlog
- Las tareas están **en orden**. Toma la **primera tarea libre** (`[ ]`) cuyas dependencias estén en `[x]`.
- Estados: `[ ]` libre · `[~] Nombre` en curso · `[x] Nombre` terminada.
- Nadie es dueño de una fase. Si alguien no puede seguir, deja una nota en la tarea, la marca `[ ]` y otra persona la retoma.
- 🧩 = toca el modelo `.archimate` (requiere el turno de modelo). 📝 = solo texto o README, se puede hacer en paralelo.
- `h` es una estimación de horas-persona.

**Calendario (4 personas × 2–5 h/día):**

| Día | Fecha | Meta del día |
|---|---|---|
| 1 | sáb 10 oct | Repositorio listo, entrevista hecha y exportada |
| 2 | dom 11 oct | Hallazgos analizados, V1, V2 y V3 |
| 3 | lun 12 oct | V4, tabla de inclusión y exclusión, contratos, V9 |
| 4 | mar 13 oct | V5, V7, V6 (por dominio) y V8 |
| 5 | mié 14 oct | V11, V10, README completo, ensayo |
| — | **jue 15 oct** | **Entrega y sustentación** |

---

## Día 1 (sáb 10): preparación y Fase 0, entrevista al experto

| ID | Estado | Tarea | Depende de | Entregable | Hecho cuando… | h |
|---|---|---|---|---|---|---|
| T01 | [ ] | Crear el repositorio en GitHub, hacer push de esta estructura e invitar a los 4 integrantes como colaboradores | — | Repositorio remoto | Los 4 pueden clonar y hacer push | 0,5 |
| T02 | [ ] | Los 4 instalan **Archi** (misma versión) y clonan el repositorio | T01 | — | Todos abren Archi | 0,5 c/u |
| T03 | [ ] 🧩 | Crear el modelo vacío `modelo/recaudo.archimate` con las 11 vistas vacías y sus nombres (`V1 Motivación` … `V11 Bounded Context Canvas`) | T02 | Modelo base | Commit con las 11 vistas vacías | 0,5 |
| T04 | [ ] 📝 | Escribir la **instrucción de rol** del experto (quién es, empresa, años de experiencia, qué sabe y qué **no** debe hacer: no diseñar) | T01 | `entrevista/01_instruccion_rol.md` | Revisada por al menos 2 integrantes | 1 |
| T05 | [ ] 📝 | Guion, parte A: **contexto de la organización, proceso E2E, actores, reglas de negocio y excepciones** | T01 | `entrevista/02_guion.md` | Cada bloque tiene preguntas abiertas, de profundización y de validación | 1,5 |
| T06 | [ ] 📝 | Guion, parte B: **indicadores, normatividad, sistemas actuales y el bloque de INTEROPERABILIDAD** (procesos, áreas, sistemas y entidades externas: qué información, en qué dirección y con qué frecuencia) | T01 | `entrevista/02_guion.md` | El bloque cubre las 6 interoperabilidades del enunciado y pregunta por otras | 1,5 |
| T07 | [ ] 📝 | Guion, parte C: **motivación** (interesados, impulsores, evaluaciones, metas, resultados, principios, requerimientos, restricciones) y **capacidades del negocio** (preguntar qué hace la organización, sin pedir el mapa) | T01 | `entrevista/02_guion.md` | Hay preguntas para los 8 elementos de motivación | 1 |
| T08 | [ ] 📝 | **Hacer la entrevista** con la IA usando T04 y el guion completo (T05–T07), con preguntas de repregunta cuando algo quede vago | T04–T07 | Conversación | Se cubrieron todos los bloques | 1,5 |
| T09 | [ ] 📝 | **Exportar la conversación completa** (enlace compartido + texto o PDF) | T08 | `entrevista/03_conversacion.md` | Conversación íntegra en el repositorio | 0,5 |

## Día 2 (dom 11): análisis de hallazgos y Fase 1, motivación, capacidades y E2E

| ID | Estado | Tarea | Depende de | Entregable | Hecho cuando… | h |
|---|---|---|---|---|---|---|
| T10 | [ ] 📝 | **Análisis de hallazgos**: tabla hallazgo → aceptado / descartado / contrastado (con qué fuente: normativa, sitios web de sistemas reales como Metro de Medellín, TransMilenio o MIO) → impacto en el diseño | T09 | `entrevista/04_analisis_hallazgos.md` | Mínimo 20 hallazgos, con al menos 3 descartados o contrastados y justificados | 2 |
| T11 | [ ] 📝 | Inventario de **elementos de motivación** sacados de la entrevista (lista: interesados, impulsores, evaluaciones, metas, resultados, principios, requerimientos, restricciones) | T09 | Borrador en README §2 | Los 8 tipos tienen elementos | 1 |
| T12 | [ ] 🧩 | **V1 Motivación** en Archi: relaciones de influencia, asociación y realización entre los elementos, y cómo la aplicación de recaudo realiza los requerimientos | T11, T03 | `vistas/V1_motivacion.png` | Se lee la cadena interesado → impulsor → evaluación → meta → resultado → requerimiento | 1,5 |
| T13 | [ ] 📝 | Boceto del **mapa de capacidades COMPLETO** de la organización de transporte (estratégicas, misionales y de apoyo, como en la diapositiva 35 de 7_SOA), no solo recaudo | T09 | Boceto (papel o Excalidraw) | Hay ≥ 3 niveles de agrupación y están marcadas las capacidades impactadas | 1,5 |
| T14 | [ ] 🧩 | **V2 Mapa de capacidades** en Archi: capacidades, recursos y cursos de acción, con las **impactadas resaltadas** y una leyenda | T13, T12 | `vistas/V2_mapa_capacidades.png` | Mapa completo y relaciones a V1 (las metas se realizan con cursos de acción y capacidades) | 2 |
| T15 | [ ] 🧩 | **V3 Cadena de valor y proceso E2E**: flujo de valor de la organización → etapa donde opera el recaudo → proceso E2E de recaudo con eventos y actores de negocio | T13, T14 | `vistas/V3_cadena_valor_e2e.png` | Queda claro **dónde** se ubica la aplicación | 1,5 |
| T16 | [ ] 📝 | README §1 (Contexto y entrevista), §2 (Motivación) y §3 (Capacidades y E2E): imagen y **análisis y argumentación** de cada vista | T10, T12, T14, T15 | README.md | Cada vista tiene al menos 1 párrafo de análisis y uno de decisiones | 2 |

## Día 3 (lun 12): Fase 2, descomposición de servicios, contract-first y anticorrupción

| ID | Estado | Tarea | Depende de | Entregable | Hecho cuando… | h |
|---|---|---|---|---|---|---|
| T17 | [ ] 📝 | Descomponer el proceso E2E en **≥ 4 capas** según la diapositiva 28 de 7_SOA: (1) proceso E2E → (2) servicios de negocio de plataforma → (3) servicios de dominio funcional → (4) servicios básicos de subdominio → (5) ACL. Usar las preguntas de la diapositiva 33 | T15 | Tabla borrador | Cada servicio cuelga de uno de la capa superior | 2 |
| T18 | [ ] 📝 | **Tabla de inclusión y exclusión**: cada servicio con *se implementa / no se implementa* y una **justificación explícita** (alcance del enunciado, IoT fuera, servicio de otra área, etc.) | T17 | README §4 | No hay ningún servicio sin justificación | 1,5 |
| T19 | [ ] 📝 | **Servicios externos de la ACL**: tabla externo (proceso interno, sistema legado, proveedor, regulador, dispositivo) → información intercambiada → **dirección** (entra, sale o ambas) → frecuencia o sincronía | T10, T17 | README §4 y §7 | Cubre las 6 interoperabilidades del enunciado y las nuevas que salieron de las capacidades y la entrevista | 1,5 |
| T20 | [ ] 🧩 | **V4 Descomposición de servicios**: servicios de negocio (amarillos) agrupados por capa, con roles, actores, funciones y objetos pasivos. Se distingue visualmente lo que entra y lo que no | T17, T18 | `vistas/V4_descomposicion_servicios.png` | Se ven las capas y la frontera del alcance | 2,5 |
| T21 | [ ] 🧩📝 | **Contract-first**: por cada servicio que se implementa, un objeto de negocio *Contract* con entradas, salidas, errores y requisitos no funcionales. Se modela en V4 (o en una sub-vista V4b) y se documenta en una tabla en el README | T20 | V4/V4b + README §4 | Todos los servicios incluidos tienen contrato | 2 |
| T22 | [ ] 🧩 | **V9 Interoperabilidad y anticorrupción** (capa de aplicación): componentes externos, interfaces, servicios de aplicación de la ACL y flujos con su dirección | T19 | `vistas/V9_interoperabilidad_acl.png` | Coincide 1 a 1 con la tabla de T19 | 1,5 |

## Día 4 (mar 13): Fases 3, 4 y 5, DDD estratégico, táctico y mapa de contextos

| ID | Estado | Tarea | Depende de | Entregable | Hecho cuando… | h |
|---|---|---|---|---|---|---|
| T23 | [ ] 📝 | **Extracción de dominios** con los 3 pasos (estructura organizacional → tormenta de eventos del proceso → puntos de corte), partiendo de V3 y V4 | T20 | Borrador README §5 | Cada dominio tiene sus responsabilidades listadas | 1,5 |
| T24 | [ ] 📝 | **Clasificar** cada dominio en central, de soporte o genérico, **con argumentos** (¿qué diferencia al negocio?, ¿se puede comprar?) | T23 | README §5 | Hay un argumento por dominio | 1 |
| T25 | [ ] 🧩 | **V5 Dominios** (capa de aplicación): agrupaciones y objetos de negocio, con la clasificación visible | T24 | `vistas/V5_dominios.png` | Coincide con T24 | 1 |
| T26 | [ ] 📝 | **Glosario de lenguaje ubicuo**: término, definición, dominio y ejemplo. Resolver los términos ambiguos de [CLAUDE.md §5](CLAUDE.md#5-términos-ambiguos-que-hay-que-resolver-en-el-lenguaje-ubicuo) y dejar explícito **cuando un término cambia de significado entre contextos** | T23 | README §5 | ≥ 25 términos y ≥ 3 términos con doble significado | 2 |
| T27 | [ ] 🧩 | **V7 Lenguaje ubicuo**: representation y significado asociados a los objetos de negocio | T26 | `vistas/V7_lenguaje_ubicuo.png` | Los términos de V7 son los mismos que se usan en las demás vistas | 1 |
| T28 | [ ] 📝 | **DDD táctico** por dominio: entidades vs objetos de valor; agregados con **raíz, límites e invariantes**; **comandos → eventos**. Argumentar el alcance de cada entidad y cada agregado | T24, T26 | README §6 (una tabla por dominio) | Cada agregado tiene ≥ 2 invariantes y su lista de comandos y eventos | 3 |
| T29 | [ ] 🧩 | **V6a…V6n Agregados, comandos y eventos**: **un diagrama por dominio** (objeto de negocio y de datos, proceso de aplicación = comando, evento de aplicación o de negocio) | T28 | `vistas/V6x_agregados_<dominio>.png` | Hay una vista por dominio | 3 |
| T30 | [ ] 📝 | **Mapa de contextos**: listar los bounded contexts y el **patrón de relación** entre cada par y con los externos (C/S, conformista, núcleo compartido, OHS, PL, ACL), con justificación | T24, T19 | README §7 | Es coherente con la ACL de la Fase 2 (T19 y T22) | 1,5 |
| T31 | [ ] 🧩 | **V8 Mapa de contextos** (componentes, interfaces, servicios de aplicación, flujos y relaciones de servicio), con los patrones etiquetados | T30 | `vistas/V8_mapa_contextos.png` | Cada relación tiene su patrón visible | 1,5 |

## Día 5 (mié 14): Fase 6, trazabilidad y cierre

| ID | Estado | Tarea | Depende de | Entregable | Hecho cuando… | h |
|---|---|---|---|---|---|---|
| T32 | [ ] 📝 | **Investigar** cómo representar el Bounded Context Canvas (ddd-crew) en Archi (agrupaciones como celdas, notas, elementos de motivación o aplicación) y **justificar** la elección | — | README §8 (justificación) | Hay una decisión de modelado escrita | 1 |
| T33 | [ ] 🧩 | **V11 Bounded Context Canvas** del contexto **central**, en una sola página: propósito, clasificación estratégica, rol del dominio, lenguaje ubicuo, comunicación entrante y saliente, decisiones de negocio y supuestos | T32, T28, T30 | `vistas/V11_bounded_context_canvas.png` | Cabe en una página y es coherente con V5, V6, V7 y V8 | 2,5 |
| T34 | [ ] 🧩 | **V10 Trazabilidad vertical**: meta (V1) → capacidad (V2) → servicio de negocio (V4) → servicio o componente de aplicación (V8), con realización, influencia, servicio y asignación | T31 | `vistas/V10_trazabilidad.png` | Al menos 2 cadenas completas se pueden seguir de punta a punta | 1,5 |
| T35 | [ ] 🧩 | **Revisión de calidad del modelo**: notación correcta, relaciones válidas (Archi valida), sin elementos huérfanos y nombres según el glosario | T33, T34 | Modelo final | Pasa *Validate Model* en Archi sin errores | 1 |
| T36 | [ ] 📝 | Exportar **todas** las vistas en PNG a `/vistas` y verificar que se vean en el README | T35 | `/vistas/*.png` | Las 11 vistas o más se ven en GitHub | 0,5 |
| T37 | [ ] 📝 | README §6, §7 y §8 con el análisis de cada vista, y **§9 Decisiones y supuestos** | T29, T31, T33 | README.md | Ninguna vista queda sin análisis | 2 |
| T38 | [ ] 📝 | **Índice navegable** con enlaces internos a cada fase y cada vista (probarlos en GitHub) | T37 | README.md | Todos los enlaces funcionan | 0,5 |
| T39 | [ ] 📝 | **Tabla de aportes**: qué construyó cada integrante, verificable con `git shortlog -sn` | T37 | README.md | Coincide con el historial | 0,5 |
| T40 | [ ] 📝 | **Revisión cruzada contra la rúbrica** (checklist de abajo): cada integrante revisa una sección que **no** hizo | T38 | Issues o notas corregidas | Todo el checklist en [x] | 1 c/u |
| T41 | [ ] | **Ensayo de sustentación por sorteo**: 30 min, sorteando las secciones, y repaso del banco de preguntas | T40 | — | Cada integrante explicó al menos 2 secciones que no hizo | 1,5 c/u |

---

## Checklist final de entregables (enunciado §4)
- [ ] README.md con cada vista exportada como imagen, seguida de su análisis y su argumentación
- [ ] Índice al inicio del README con enlaces internos a cada fase y cada vista
- [ ] Modelo fuente `.archimate` en `/modelo`
- [ ] Imágenes de las vistas en `/vistas`
- [ ] `/entrevista` con guion, instrucción de rol, conversación exportada y análisis de hallazgos
- [ ] Tabla de aportes verificable en los commits
- [ ] Vistas V1 a V11 completas (V6, una por dominio)
- [ ] Commits repartidos entre los 4 integrantes

## Checklist contra la rúbrica
| # | Criterio | Peso | Para estar en «Sobresaliente» hace falta… | OK |
|---|---|---|---|---|
| 1 | Entrevista al experto | 10 % | Guion completo por temas **con bloque de interoperabilidad**, y hallazgos analizados, contrastados y **trazados al diseño** | [ ] |
| 2 | Motivación, capacidades y E2E | 10 % | Mapa de capacidades **completo** (no solo recaudo); motivación y E2E coherentes con la app | [ ] |
| 3 | Servicios y anticorrupción | 15 % | **≥ 4 capas**, cada inclusión y exclusión justificada, servicios externos completos | [ ] |
| 4 | Dominios y lenguaje ubicuo | 10 % | Dominios clasificados con argumentos y glosario preciso **usado en todas las vistas** | [ ] |
| 5 | Agregados, comandos y eventos | 15 % | Raíz, límites e invariantes claros; comandos y eventos consistentes por dominio | [ ] |
| 6 | Mapa de contextos | 10 % | Patrones correctos y **consistentes con la ACL** | [ ] |
| 7 | Canvas en ArchiMate | 10 % | Canvas completo en una página, bien resuelto en la herramienta y coherente con el modelo | [ ] |
| 8 | Calidad del modelo | 5 % | Cuatro capas, relaciones horizontales y verticales correctas, trazabilidad de meta a componente | [ ] |
| 9 | Documento en GitHub | 5 % | Índice navegable; cada vista con análisis y argumentación | [ ] |
| 10 | Equipo y sustentación | 10 % | Cualquiera explica cualquier sección; commits repartidos | [ ] |

---

## Banco de preguntas para preparar la sustentación
El profesor pregunta sobre todo **el porqué de las decisiones** y las **interoperabilidades**. Cada integrante debe poder responder:

**Negocio y entrevista**
1. ¿Qué hallazgo de la entrevista descartaron y por qué? ¿Cómo lo contrastaron?
2. ¿Qué meta del negocio justifica la aplicación y qué resultado medible esperan?
3. ¿En qué capacidades impacta la solución y en cuáles no, aunque estén cerca (p. ej. planeación de rutas)?

**Servicios**
4. ¿Por qué ese número de capas? ¿Qué diferencia un servicio de plataforma de uno de dominio?
5. ¿Por qué tal servicio quedó **fuera** del alcance?
6. Muestren el contrato de un servicio: ¿qué recibe, qué devuelve y qué errores maneja?
7. ¿Cómo llegan al sistema las transacciones de los validadores si los dispositivos están fuera del alcance?

**DDD**
8. ¿Por qué el dominio central es ese y no otro?
9. ¿Qué término cambia de significado entre dos contextos?
10. ¿Qué invariante protege tal agregado? ¿Por qué esa entidad está dentro del agregado y no fuera?
11. ¿Qué comando dispara tal evento y quién escucha ese evento?
12. ¿Cómo se calcula el transbordo, y en qué agregado o servicio de dominio vive esa regla? ¿Es una invariante o una política?

**Contextos e interoperabilidad**
13. ¿Por qué la relación con la red de pagos es ACL y no conformista?
14. ¿Qué información sale hacia el área financiera y en qué momento?
15. ¿Cómo se valida el perfil de un estudiante con su institución?
16. ¿Qué pasa si la autoridad de transporte cambia la tarifa?
17. ¿Cómo se trazan desde una meta hasta un componente de aplicación? Muéstrenlo en V10.

**Canvas**
18. ¿Por qué modelaron el canvas con esos elementos de ArchiMate?
