# CLAUDE.md: guía del proyecto (Parcial 3, Arquitectura de Software)

> Este archivo sirve de guía para el equipo y para cualquier asistente de IA que trabaje en el repositorio.
> El plan de trabajo, paso a paso, está en [BACKLOG.md](BACKLOG.md).

## 1. Qué estamos haciendo

**Diseño de la arquitectura de una aplicación empresarial con ArchiMate y DDD.** Profesor: César López. Vale el **25 %** de la nota del curso.
Entrega: este repositorio en GitHub más una sustentación presencial de 40 min (30 de presentación y 10 de preguntas), grabada en Teams. Al empezar, el profesor sortea **quién presenta cada sección**, así que todos tenemos que dominar todo el diseño.

### Tema 4: recaudo del sistema integrado de transporte de una ciudad mediana

> «Operamos el sistema integrado de transporte de la ciudad, con tres modos: buses alimentadores (satélites), buses articulados en carriles exclusivos y metro. Necesitamos un software que apoye el proceso de recaudo, que está ligado directamente a la operación, y que permita a residentes y visitantes pagar su viaje de forma ágil y con la tarifa que les corresponde».

**Dentro del alcance**
- Recaudo en los **3 modos** (alimentador, articulado y metro) con **3 medios de pago**: la tarjeta **VAMOS** de la ciudad y las tarjetas **débito** y **crédito** (para visitantes que no quieren comprar tarjeta).
- Gestión de la tarjeta VAMOS: **emisión, recargas, consulta de saldo y bloqueo por pérdida**.
- Tarifas y perfiles: **tarifa plena** y tarifas especiales para estudiantes de colegio, universitarios, adultos mayores y personas con movilidad reducida, incluida la **validación de que el usuario cumple las condiciones de su perfil**.
- Aplicación de la **tarifa correcta en cada validación**, teniendo en cuenta la integración entre modos (**transbordos**).
- **Consolidación del recaudo por modo, ruta y operador**, como base para la distribución de ingresos y la conciliación.

**Fuera del alcance**
- Los validadores, lectores y demás dispositivos, y todo lo relacionado con IoT. El software **recibe las transacciones** que generan esos equipos, pero no los gestiona. Esto se modela como un sistema externo detrás de la capa anticorrupción.

**Interoperabilidades por explorar** (hay que confirmarlas, ampliarlas o descartarlas en la entrevista):
servicio al cliente (PQR y devoluciones) · financiero (registro contable de recaudos e ingresos) · planeación de rutas y de la operación · redes de pago y entidades financieras · entidades que certifican perfiles (colegios, universidades, etc.) · autoridad de transporte de la ciudad · las que aparezcan al analizar las capacidades.

## 2. Reglas del curso que no se pueden romper

1. **La IA es solo el experto del negocio durante la entrevista, después, una herramienta para el equipo.** En la entrevista **no se le puede pedir** que proponga el mapa de capacidades, los dominios, los agregados, el mapa de contextos ni las vistas ArchiMate. Después del apartado de la entrevista, si será posible pedirle a la IA recomendaciones sobre el mapa de capacidades, los dominios, los agregados, el mapa de contextos y las vistas ArchiMate. Esto se hace para que la entrevista sea lo más natural posible y que luego si se pueda trabajar de acuerdo a lo que la IA nos dijo en la entrevista.
2. Hay que guardar como evidencia **la instrucción de rol, la conversación completa exportada y el análisis de hallazgos** (aceptados, descartados o contrastados, y cómo influyeron en el diseño).
3. **Un único modelo ArchiMate** con varias vistas, que use las capas de Estrategia, Motivación, Negocio y Aplicación, con relaciones horizontales y verticales que permitan **trazar cada componente de aplicación hasta la meta y la capacidad** que lo justifican.
4. **Commits repartidos:** cada integrante hace commit con su propia cuenta. La tabla de aportes se verifica contra el historial.
5. Llegar tarde a la sustentación cuesta **−0,1 por minuto**.

## 3. Mapa fase → vista → diapositivas → rúbrica

| Fase | Producto | Vista ArchiMate | Capa | Diapositivas de referencia | Criterio de la rúbrica (peso) |
|---|---|---|---|---|---|
| 0 | Entrevista al experto: guion, rol, conversación y análisis | — | — | — | 1. Entrevista (10 %) |
| 1 | Motivación | **V1** Motivación | Motivación | — | 2. Motivación, capacidades y E2E (10 %) |
| 1 | Mapa de capacidades (impactadas resaltadas) | **V2** Mapa de capacidades | Estrategia | 7_SOA: 32–35 | 2 |
| 1 | Cadena de valor y proceso E2E | **V3** Cadena de valor y E2E | Negocio | 7_SOA: 21 | 2 |
| 2 | Descomposición en ≥ 4 capas, tabla de inclusión y exclusión, contratos | **V4** Descomposición de servicios | Negocio | 7_SOA: 20–28, 39–47 | 3. Servicios y anticorrupción (15 %) |
| 2/5 | Servicios externos y ACL | **V9** Interoperabilidad y anticorrupción | Aplicación | 7_SOA: 25, 28 | 3 y 6 |
| 3 | Dominios: central, de soporte y genérico | **V5** Dominios | Aplicación | 9_DDD: 7–15 | 4. Dominios y lenguaje ubicuo (10 %) |
| 3 | Lenguaje ubicuo (glosario) | **V7** Lenguaje ubicuo | Negocio (representation) | 9_DDD: 28–30 | 4 |
| 4 | Entidades, objetos de valor, agregados, comandos y eventos | **V6** (una por dominio) | Aplicación | 9_DDD: 16–24, 31–33, 39–41 | 5. Agregados, comandos y eventos (15 %) |
| 5 | Mapa de contextos delimitados con patrones | **V8** Mapa de contextos | Aplicación | 9_DDD: 25–27 | 6. Mapa de contextos (10 %) |
| 6 | Bounded Context Canvas del contexto central | **V11** Canvas | Libre, justificada | 9_DDD: 34–35 (ddd-crew) | 7. Canvas (10 %) |
| — | Trazabilidad meta → capacidad → servicio → componente | **V10** Trazabilidad vertical | Todas | — | 8. Calidad del modelo (5 %) |
| — | README con índice y análisis por vista | — | — | — | 9. Documento GitHub (5 %) |
| — | Sustentación | — | — | — | 10. Equipo y sustentación (10 %) |

### Elementos ArchiMate de referencia por vista (según el enunciado)
- **V1:** interesado, impulsor, evaluación, meta, resultado, principio, requerimiento, restricción.
- **V2:** capacidad, recurso, curso de acción.
- **V3:** flujo de valor, proceso, evento y actor de negocio.
- **V4:** servicio de negocio (amarillo), proceso, función, agrupación, rol, actor y objetos pasivos (los **contratos**, contract-first).
- **V5:** agrupación, objeto de negocio.
- **V6:** objeto de negocio y de datos, evento de negocio y de aplicación, proceso de aplicación.
- **V7:** significado, representación, objeto de negocio.
- **V8:** componente, interfaz y servicio de aplicación, flujo, relación de servicio.
- **V9:** interfaz de aplicación, flujo, servicio, componente externo.
- **V10:** relaciones de realización, influencia, servicio y asignación.
- **V11:** a elección del equipo, con justificación.
> Se pueden usar otros elementos siempre que se **justifique** en el README por qué representan mejor el concepto.

## 4. Conceptos clave de las diapositivas (resumen)

**Jerarquía de servicios SOA (7_SOA, diapositiva 28, ejemplo de citas médicas).** Las capas, de mayor a menor, son:
1. **Proceso de negocio E2E**: la secuencia completa (por ejemplo: adquirir medio de pago → cargar saldo → validar viaje → aplicar tarifa → consolidar → distribuir).
2. **Servicio de negocio de plataforma**: unidades grandes que el proceso orquesta.
3. **Servicio de dominio funcional**.
4. **Servicio básico de subdominio funcional**: el tamaño adecuado para construir.
5. **Capa anticorrupción (ACL)**: aísla a los externos para que no contaminen la semántica del dominio.
(La capa de infraestructura, con autenticación, permisos, auditoría y notificaciones, es transversal.)

**Contract-first (diapositivas 44–47):** antes de implementar se define, por servicio, qué recibe, qué devuelve, la semántica de errores y los requisitos no funcionales. En ArchiMate se modela con **objetos pasivos de negocio / contract** asociados a cada servicio.

**Preguntas para identificar servicios (diapositiva 33):** ¿quién es responsable de la función?, ¿dónde se usa?, ¿quién gestiona los datos?, ¿quién define las reglas?, ¿qué paso tiene el conocimiento?

**DDD:**
- Extracción de dominios en 3 pasos (Van Ingen): estructura organizacional → tormenta de ideas del proceso (triggers, eventos, bifurcaciones) → puntos de corte para delimitar subdominios.
- Clasificación: **central** (core: diferencia al negocio), **de soporte** (necesario pero no diferenciador), **genérico** (se puede comprar o tercerizar).
- **Entidad**: tiene identidad y estado que cambia. **Objeto de valor**: inmutable y sin identidad (p. ej. `Dinero`, `Tarifa aplicada`, `Ventana de transbordo`).
- **Agregado**: raíz con punto de acceso único, límite de consistencia transaccional e **invariantes** que protege (por ejemplo, «el saldo nunca queda negativo más allá del cupo permitido», o «una tarjeta bloqueada no puede validar»).
- **Comandos** (intención, en imperativo: `RecargarTarjeta`) → **Eventos** (hecho, en pasado: `TarjetaRecargada`).
- Diferenciar **invariantes** (dentro del agregado) de **políticas** (coordinación, en servicios o eventos de dominio).
- **Patrones del mapa de contextos:** cliente-proveedor, conformista, núcleo compartido, servicio abierto (OHS), lenguaje publicado (PL) y capa anticorrupción (ACL).
- **Bounded Context Canvas (ddd-crew):** nombre, propósito, clasificación estratégica (core/soporte/genérico; tipo de modelo de negocio; evolución), roles del dominio, comunicación entrante y saliente (consultas, comandos, eventos y colaboradores), lenguaje ubicuo, decisiones de negocio, supuestos y preguntas abiertas.

## 5. Términos ambiguos que hay que resolver en el lenguaje ubicuo

Estos términos pueden tener más de un significado según el contexto. El glosario (V7) debe dejar explícito qué significan en cada uno:
- **Viaje** vs **Validación** vs **Transbordo**: ¿un viaje es la validación al entrar o el trayecto completo con sus transbordos?
- **Tarifa**: el valor configurado en el pliego tarifario vs el valor efectivamente cobrado en una validación.
- **Saldo**: el saldo de la tarjeta (prepago) vs el saldo pendiente de un operador en la liquidación.
- **Usuario / Pasajero / Titular / Cliente**: quién viaja, quién es dueño de la tarjeta y quién pone una PQR.
- **Perfil**: perfil tarifario (estudiante, adulto mayor…) vs perfil de usuario del sistema.
- **Operador**: el operador de transporte (dueño de flota o ruta) vs el operador de recaudo.
- **Transacción**: el evento crudo que manda el validador vs la transacción de pago en una red financiera.

## 6. Convenciones del repositorio

```
/README.md               documento principal (índice + vistas + análisis)
/BACKLOG.md              plan de tareas
/CLAUDE.md               esta guía
/modelo/recaudo.archimate  modelo ArchiMate único (herramienta: Archi)
/modelo/DECISIONES_MODELO.md  decisiones y convenciones de modelado (leer antes de tocar el modelo)
/vistas/V#_nombre.png     imágenes exportadas de cada vista
/entrevista/             rol, guion, conversación y análisis
```
- **Herramienta:** [Archi](https://www.archimatetool.com/), gratuita. Todos deben usar la misma versión.
- **Nombres de vistas en Archi:** `V1 Motivación`, `V2 Mapa de capacidades`, …, `V11 Bounded Context Canvas`. Para V6, una por dominio: `V6a …`, `V6b …`.
- **Imágenes:** `vistas/V1_motivacion.png`, `vistas/V6a_agregados_<dominio>.png`, etc. Se exportan desde Archi en PNG (escala 100–200 %).
- **Colores:** los de ArchiMate por defecto (estrategia en marrón claro, negocio en amarillo, aplicación en azul, motivación en morado). Las capacidades **impactadas** se resaltan con un color o un borde, y la leyenda va en la vista.
- **Mismo nombre en todas partes:** el término que se fije en el glosario es el que se usa en todas las vistas y en el README (la rúbrica lo evalúa).

## 7. Cómo trabajamos (sin responsables fijos)

- El [BACKLOG.md](BACKLOG.md) está **ordenado**. Cada persona toma **la siguiente tarea libre cuyas dependencias estén cerradas**.
- Para tomar una tarea, se cambia su estado a `[~] Nombre`, se hace commit y push enseguida (así nadie la toma dos veces). Al terminar, se marca `[x] Nombre`.
- Commits pequeños y frecuentes, con el formato `T07: V2 mapa de capacidades - capacidades misionales`.
- Siempre hacer `git pull` antes de empezar.

### Turno de modelo (muy importante)
El archivo `.archimate` es un XML grande y **los merges simultáneos lo corrompen**. Regla:
1. Solo **una persona a la vez** edita `modelo/recaudo.archimate`. Para pedir el turno, se escribe el nombre en la línea **«Turno de modelo»** al inicio del BACKLOG, con commit y push.
2. Antes de abrir Archi se hace `git pull`. Al terminar: guardar, exportar las imágenes que se tocaron, hacer commit y push, y **liberar el turno**.
3. Mientras tanto, los demás avanzan en tareas que no tocan el modelo: redacción del README, tablas, análisis, glosario en texto y bocetos en papel o Excalidraw para pasarlos luego al modelo.

## 8. Instrucciones para asistentes de IA en este repositorio
- Se puede proponer y generar el diseño, eso si, siempre con confirmación del equipo de trabajo. Es importante **revisar, señalar inconsistencias, explicar conceptos y dar formato**
- Responder en español.
- No agregar coautoría ni firmas de IA en commits, PRs ni archivos.
