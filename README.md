# Arquitectura del software de recaudo del sistema integrado de transporte

**Curso:** Arquitectura de Software, UPB · **Profesor:** César López · **Parcial 3**
**Tema 4:** Recaudo del sistema integrado de transporte de una ciudad mediana (alimentadores, articulados y metro; tarjeta VAMOS y débito/crédito).

**Integrantes:** _Nombre 1 · Nombre 2 · Nombre 3 · Nombre 4_

> Plan de trabajo: [BACKLOG.md](BACKLOG.md) · Guía del proyecto: [CLAUDE.md](CLAUDE.md) · Modelo fuente: [modelo/](modelo/)

---

## Índice
1. [Contexto y entrevista](#1-contexto-y-entrevista)
2. [Motivación](#2-motivación) · [V1](#v1-motivación)
3. [Mapa de capacidades y proceso E2E](#3-mapa-de-capacidades-y-proceso-e2e) · [V2](#v2-mapa-de-capacidades) · [V3](#v3-cadena-de-valor-y-proceso-e2e)
4. [Descomposición de servicios](#4-descomposición-de-servicios) · [V4](#v4-descomposición-de-servicios)
5. [Dominios y lenguaje ubicuo](#5-dominios-y-lenguaje-ubicuo) · [V5](#v5-dominios) · [V7](#v7-lenguaje-ubicuo)
6. [Agregados, comandos y eventos](#6-agregados-comandos-y-eventos) · [V6](#v6-agregados-comandos-y-eventos)
7. [Mapa de contextos e interoperabilidad](#7-mapa-de-contextos-e-interoperabilidad) · [V8](#v8-mapa-de-contextos) · [V9](#v9-interoperabilidad-y-anticorrupción)
8. [Bounded Context Canvas](#8-bounded-context-canvas) · [V11](#v11-bounded-context-canvas)
9. [Decisiones y supuestos](#9-decisiones-y-supuestos) · [V10](#v10-trazabilidad-vertical)
10. [Tabla de aportes](#10-tabla-de-aportes)

---

## 1. Contexto y entrevista

El ente gestor de un sistema integrado de transporte (SIT) de una ciudad mediana necesita un software que apoye su proceso de recaudo. El sistema tiene tres modos: buses alimentadores, buses articulados en carriles exclusivos y metro. La gente puede pagar con la tarjeta VAMOS, que es la de la ciudad, o con una tarjeta débito o crédito, pensada sobre todo para los visitantes que no quieren comprar una tarjeta. La idea es que el viaje se pague rápido y con la tarifa que le corresponde a cada persona.

Lo que entra en el alcance:
- Recaudo en los tres modos con los tres medios de pago.
- Gestión de la tarjeta VAMOS: emisión, recargas, consulta de saldo y bloqueo por pérdida.
- Tarifas y perfiles (plena, estudiante de colegio, universitario, adulto mayor y movilidad reducida), incluida la validación de que la persona sí cumple las condiciones de su perfil.
- Aplicación de la tarifa correcta en cada validación, teniendo en cuenta los transbordos.
- Consolidación del recaudo por modo, ruta y operador, como base para repartir los ingresos y conciliar.

Lo que queda por fuera son los validadores, los lectores y todo lo relacionado con IoT. El software recibe las transacciones que generan esos equipos, pero no los gestiona; por eso en el diseño aparecen detrás de una capa anticorrupción.

**La entrevista.** La hicimos con una IA que asumió el papel de Andrea Montoya, directora de Recaudo y Tarifas del ente gestor, con unos 15 años en transporte masivo. La sesión fue aislada: la IA no conocía el enunciado ni la rúbrica, solo la instrucción de rol, y no se le pidió que propusiera capacidades, dominios ni vistas (al final ella misma dijo que eso le tocaba al equipo de arquitectura). Todo el material está en [entrevista/](entrevista/): la [instrucción de rol](entrevista/01_instruccion_rol.md), el [guion](entrevista/02_guion.md) de 11 bloques (el 9 es el de interoperabilidad), la [conversación completa](entrevista/03_conversacion.md) y el [análisis de hallazgos](entrevista/04_analisis_hallazgos.md).

De los 24 hallazgos que analizamos, 16 se aceptaron, 3 se contrastaron con fuentes externas (el Metro de Medellín y la Ley 1581 de 2012) y 5 se descartaron. Estos fueron los que más cambiaron el diseño:
- H07 (descartado): creíamos que toda validación descuenta una tarifa, y la experta nos corrigió. Hay rechazos, credenciales de servicio, tarifas especiales, segundos transbordos y pagos diferidos. Por eso separamos la validación, su resultado, el importe calculado y el movimiento de saldo.
- H04 y H05 (aceptados): las transacciones de los buses pueden llegar hasta 48 horas tarde y el saldo que tiene el sistema central es calculado, no el que está en la tarjeta. De ahí salen las transacciones extemporáneas y las diferencias de saldo.
- H18 (descartado): no se asume que el software reemplace la plataforma del proveedor. Hay que diseñarlo para convivir con ella.
- H14 (descartado): el software no elimina la evasión, solo ayuda a medirla y a dirigir el control. Se limita a indicadores y alertas.
- H21 (descartado): PCI DSS no es una ley colombiana, es un requisito contractual con el adquirente. Se trata como restricción de seguridad.

## 2. Motivación
### V1 Motivación
![V1 Motivación](vistas/V1_motivacion.png)

**Análisis.** La vista junta los 83 elementos del inventario de abajo (15 interesados, 8 impulsores, 12 evaluaciones, 7 metas, 9 resultados, 10 principios, 12 requerimientos y 10 restricciones) y la aplicación de recaudo, con 120 relaciones. Se lee de arriba hacia abajo. A la Gerencia General le importan los hallazgos de la Contraloría, el déficit y el calendario político; al área de Recaudo y Tarifas, el vencimiento del contrato del proveedor, las disputas con operadores y que la liquidación dependa de solo dos personas. Esos impulsores se ven en problemas concretos: el ente depende del proveedor para consultar su propia información (EVA01), la liquidación vive en Excel (EVA02) y los sistemas de recaudo, PQR, flota y finanzas no se hablan entre sí (EVA03). De ahí salen las metas, y la que la experta marcó como la más importante es poder demostrar cuánto dinero entró, por qué concepto y a quién se le pagó. Esa idea une MET01 (control de la información) y MET02 (liquidación y conciliación confiables), y es la que más requerimientos tiene detrás: REQ03 (consolidar, conciliar y liquidar) produce los resultados RES01 a RES03, que son el cierre en máximo 5 días, la diferencia sin explicar en máximo 0,1 % y el 100 % de liquidaciones trazables.

**Decisiones.** Las descripciones y el código de cada elemento (INT01, IMP01, etc.) se copiaron del inventario para que el modelo se pueda leer sin el README. Las cifras de los resultados son indicativas, porque la experta aclaró que la Gerencia todavía no las formaliza. MET07 (integración metropolitana) no tiene un resultado medible en la entrevista, así que la realiza directamente REQ01, el de intercambio de información. Las restricciones de proyecto, como el presupuesto, la contratación pública, los plazos y el tamaño del equipo, afectan a la meta o al resultado de transición (MET06 y RES09) y no a la aplicación, porque el software no las "cumple". Por el contrario, RESC01 y RESC02 (el contrato vigente del proveedor y las tarjetas que ya circulan) sí las realiza la aplicación al interoperar con la plataforma existente. La vista se dejó sin viewpoint porque mezcla motivación con un componente de aplicación. El detalle de cada relación está en [modelo/DECISIONES_MODELO.md](modelo/DECISIONES_MODELO.md).

### Inventario de elementos de motivación

> Inventario de los elementos de motivación identificados en la entrevista al experto del negocio del SIT, organizados en los ocho tipos: interesados, impulsores, evaluaciones, metas, resultados, principios, requerimientos y restricciones.

#### Interesados (Stakeholders)

Personas, áreas y entidades que tienen interés en el software de recaudo y en sus resultados.

| ID | Interesado | Interés o expectativa identificada en la entrevista |
|---|---|---|
| INT01 | Gerencia General | Tener control y transparencia sobre el recaudo y responder con evidencia ante la Alcaldía, el Concejo y los entes de control. |
| INT02 | Recaudo y Tarifas | Reducir la dependencia del proveedor y de Excel, y lograr liquidaciones y conciliaciones confiables, rápidas y trazables. |
| INT03 | Finanzas | Realizar cierres oportunos, disponer de cifras confiables, cobrar los subsidios y controlar la cartera. |
| INT04 | Servicio al Cliente | Consultar la información de tarjetas y usuarios para resolver reclamaciones en menos tiempo. |
| INT05 | Operaciones | Identificar validadores averiados, apoyar la detección de evasión y evitar errores de recaudo por cambios de ruta. |
| INT06 | Planeación | Obtener información confiable y oportuna sobre la demanda y el uso de los servicios. |
| INT07 | Jurídica y oficial de protección de datos | Cumplir las obligaciones legales de protección de datos y contar con evidencia para resolver disputas contractuales. |
| INT08 | Operadores de flota | Conocer cómo se calculan sus pagos, recibirlos oportunamente y reducir las reliquidaciones. |
| INT09 | Operador del metro | Contar con liquidaciones transparentes y oportunas, de acuerdo con su convenio particular. |
| INT10 | Proveedor de recaudo | Mantener la operación contratada y gestionar las solicitudes de información; su posición frente al cambio es ambigua. |
| INT11 | Alcaldía y Secretaría de Hacienda | Conocer el valor de los subsidios, su destinación y los recursos que deben aportar. |
| INT12 | Concejo y entes de control | Verificar la transparencia en el manejo de los recursos públicos. |
| INT13 | Usuarios del sistema | Obtener recargas oportunas, resolver reclamaciones rápidamente y acceder fácilmente a perfiles tarifarios. |
| INT14 | Instituciones certificadoras | Reducir el papeleo y disponer de un formato uniforme para reportar beneficiarios. |
| INT15 | Fiduciaria | Recibir instrucciones de pago claras, completas y debidamente soportadas. |

#### Impulsores (Drivers)

Factores que motivan a la organización a iniciar el proyecto en este momento.

| ID | Impulsor | Descripción |
|---|---|---|
| IMP01 | Vencimiento del contrato del proveedor | El contrato de recaudo vence en aproximadamente tres años y la organización necesita definir su estrategia antes de esa fecha. |
| IMP02 | Hallazgos de la Contraloría | La última auditoría identificó debilidades en la trazabilidad de las liquidaciones y en la dependencia de hojas de cálculo. |
| IMP03 | Disputas con operadores | Existen reclamaciones por diferencias en liquidaciones de años anteriores cuya evidencia fue difícil de reconstruir. |
| IMP04 | Presión financiera | El déficit del sistema está creciendo y la Alcaldía exige reducir la evasión y el fraude en subsidios antes de aportar más recursos. |
| IMP05 | Crecimiento de los pagos bancarios | Aumenta el uso de tarjetas bancarias, lo que exige una gestión más robusta de las transacciones y los cobros. |
| IMP06 | Posible integración metropolitana | Existe la perspectiva de integrar servicios con municipios vecinos, algo que la operación actual podría no soportar adecuadamente. |
| IMP07 | Calendario político | La administración actual termina a finales del próximo año y la Gerencia busca mostrar resultados concretos. |
| IMP08 | Dependencia de personas clave | La liquidación depende de dos personas del equipo, lo que representa un riesgo para la continuidad del proceso. |

#### Evaluaciones (Assessments)

Problemas, debilidades y valoraciones que describen la situación actual del negocio.

| ID | Evaluación | Situación identificada |
|---|---|---|
| EVA01 | Dependencia del proveedor | El ente gestor no tiene acceso directo y oportuno a toda la información detallada del recaudo. |
| EVA02 | Procesos manuales | La liquidación y parte de la conciliación dependen de archivos Excel, con riesgo de errores y poca trazabilidad. |
| EVA03 | Sistemas aislados | Los sistemas de recaudo, PQR, flota y finanzas no están integrados adecuadamente. |
| EVA04 | Diferencias de conciliación | La diferencia sin explicar está entre el 0,2 % y el 0,3 % del recaudo mensual, por encima de la meta del 0,1 %. |
| EVA05 | Atención lenta de PQR | La falta de información integrada retrasa la resolución de reclamaciones de los usuarios. |
| EVA06 | Gestión manual de perfiles | Las instituciones entregan archivos con formatos distintos y los retiros de beneficiarios no siempre se reportan oportunamente. |
| EVA07 | Fuga de subsidios | Algunos usuarios conservan beneficios después de perder el derecho a ellos. |
| EVA08 | Detección tardía de fraude | Las investigaciones dependen de extractos del proveedor y análisis manuales. |
| EVA09 | Cambios operativos poco controlados | Las modificaciones de rutas y tarifas pueden ocasionar errores de configuración y liquidación. |
| EVA10 | Medición insuficiente de evasión | La evasión se estima mediante muestreos realizados pocas veces al año y con poca desagregación. |
| EVA11 | Riesgos de protección de datos | La organización reconoce debilidades en el control de la información personal que debe proteger. |
| EVA12 | Disponibilidad insuficiente de validadores en flota | La disponibilidad actual ronda el 96 %, frente a una meta de al menos el 98 %. |

#### Metas (Goals)

Estados futuros que la organización quiere alcanzar mediante el proyecto.

| ID | Meta | Descripción |
|---|---|---|
| MET01 | Control de la información | Conseguir que el ente gestor tenga control y acceso a la información del recaudo. |
| MET02 | Liquidación y conciliación confiables | Calcular y conciliar los valores con rapidez, precisión y trazabilidad. |
| MET03 | Mejor atención al usuario | Reducir los tiempos de respuesta relacionados con tarjetas, pagos, perfiles y reclamaciones. |
| MET04 | Reducción de pérdidas de recursos | Disminuir las pérdidas asociadas al fraude en perfiles, fallas de validadores y cartera bancaria, y mejorar la medición de la evasión. |
| MET05 | Cumplimiento normativo | Cumplir las obligaciones sobre protección de datos, reportes y control de los recursos. |
| MET06 | Preparación para la transición contractual | Contar con información y procesos bajo control antes de decidir el futuro del contrato del proveedor. |
| MET07 | Preparación para la integración metropolitana | Mejorar la capacidad de intercambio de información y gestión ante una eventual integración con municipios vecinos. |

#### Resultados (Outcomes)

Resultados observables y medibles que permitirían evaluar el éxito del proyecto. Según la entrevista, estas metas son indicativas y todavía no han sido formalizadas por la Gerencia.

| ID | Resultado esperado | Meta propuesta en la entrevista | Plazo indicado |
|---|---|---|---|
| RES01 | Reducir el tiempo del cierre mensual | Pasar de 8–10 días hábiles a un máximo de 5 días hábiles. | 12 meses después de entrar en operación. |
| RES02 | Reducir las diferencias de conciliación sin explicar | Llegar a un máximo del 0,1 %, frente al 0,2–0,3 % actual. | 12 meses. |
| RES03 | Garantizar trazabilidad de liquidaciones | Alcanzar el 100 % de liquidaciones trazables y reconstruibles, sin depender de Excel. | Primer cierre bajo el nuevo esquema. |
| RES04 | Mejorar la atención de PQR | Alcanzar un promedio máximo de 5 días hábiles, frente a los aproximadamente 10 días actuales. | Entre 6 y 12 meses. |
| RES05 | Actualizar oportunamente los perfiles | Reflejar al mes siguiente el retiro de quienes pierdan el derecho al beneficio. | No se especifica un plazo adicional. |
| RES06 | Reducir el fraude en perfiles | Conseguir una disminución medible del fraude asociado a perfiles tarifarios. | Primer año. |
| RES07 | Mejorar la medición de evasión | Medirla mensualmente por ruta y estación, en lugar de hacerlo solo unas pocas veces al año. | No se especifica un plazo. |
| RES08 | Automatizar los reportes | Generar los reportes para entidades de control sin trabajo manual. | No se especifica un plazo. |
| RES09 | Obtener resultados visibles del proyecto | Mostrar resultados concretos y verificables. | Entre 12 y 18 meses y, en todo caso, antes del vencimiento del contrato del proveedor. |

#### Principios (Principles)

Criterios que deben orientar las decisiones y el funcionamiento del software.

| ID | Principio | Aplicación en el negocio |
|---|---|---|
| PRI01 | Equidad tarifaria | Usuarios con el mismo perfil deben recibir el mismo tratamiento tarifario, independientemente del canal, ruta u operador. |
| PRI02 | Legalidad | Las reglas tarifarias deben estar respaldadas por actos administrativos y aplicarse según su vigencia. |
| PRI03 | Transparencia y neutralidad | Los operadores deben liquidarse conforme a sus contratos y poder verificar cómo se calculan sus pagos. |
| PRI04 | Trazabilidad | Cada peso debe poder rastrearse desde la recarga o el viaje hasta el giro correspondiente. |
| PRI05 | Protección de los recursos públicos | El dinero del recaudo debe administrarse mediante el patrimonio autónomo y conforme a las reglas contractuales. |
| PRI06 | Separación de funciones | La persona o área que liquida no debe ser la misma que aprueba ni la que ejecuta el giro. |
| PRI07 | Continuidad del servicio | Las fallas del sistema no deben dejar a los usuarios sin posibilidad de viajar. |
| PRI08 | Protección del usuario frente a errores del sistema | En casos pequeños y razonables, debe darse al usuario el beneficio de la duda según las reglas aplicables. |
| PRI09 | Protección de datos personales | Solo deben tratarse los datos necesarios, con las autorizaciones y medidas de protección correspondientes. |
| PRI10 | Inclusión | Debe existir una alternativa de pago para quienes no tienen cuenta bancaria ni teléfono inteligente. |

#### Requerimientos (Requirements)

Funciones y capacidades que el software debe proporcionar para satisfacer las necesidades del negocio.

| ID | Requerimiento | Descripción |
|---|---|---|
| REQ01 | Gestión de transacciones y ventas | Recibir y consultar la información de transacciones, recargas y ventas de forma completa y oportuna, incluidas las extemporáneas. |
| REQ02 | Gestión de reglas tarifarias | Definir y mantener tarifas, perfiles, transbordos, límites y vigencias, conservando su historial. |
| REQ03 | Consolidación, conciliación y liquidación | Consolidar y conciliar información y liquidar valores por modo, ruta y operador, con trazabilidad y ajustes a periodos cerrados. |
| REQ04 | Cálculo de subsidios | Calcular el valor de los subsidios que deben solicitarse a la Alcaldía. |
| REQ05 | Gestión de usuarios, tarjetas y perfiles | Gestionar titulares, tarjetas, certificaciones, perfiles especiales y vencimientos. |
| REQ06 | Gestión de bloqueos y listas | Registrar las decisiones de bloqueo o desbloqueo, sus responsables y sus motivos. |
| REQ07 | Consulta del historial | Permitir consultar el historial completo de una tarjeta para atender reclamaciones. |
| REQ08 | Gestión de ajustes y devoluciones | Registrar solicitudes, gestionar aprobaciones según el monto y realizar seguimiento a ajustes y devoluciones. |
| REQ09 | Protección de datos | Gestionar autorizaciones y solicitudes de consulta, rectificación y supresión de datos conforme a las obligaciones aplicables. |
| REQ10 | Reportes e indicadores | Generar reportes obligatorios e indicadores para la Gerencia y las entidades correspondientes. |
| REQ11 | Detección de anomalías | Generar alertas sobre comportamientos anómalos y posibles fraudes. |
| REQ12 | Conservación de información histórica | Conservar información durante los periodos exigidos por las normas y los contratos para respaldar auditorías y disputas. |

#### Restricciones (Constraints)

Condiciones legales, contractuales, tecnológicas, financieras y operativas que limitan las alternativas de solución.

| ID | Restricción | Descripción |
|---|---|---|
| RESC01 | Contrato vigente del proveedor | Los validadores, la plataforma de transacciones y los canales de recarga continúan bajo responsabilidad del proveedor, al menos hasta el vencimiento contractual. |
| RESC02 | Tecnología existente | No se pueden reemplazar libremente los validadores ni las tarjetas VAMOS que ya están en circulación. |
| RESC03 | Presupuesto público | El presupuesto requiere aprobación anual. La cifra disponible para el proyecto no está definida en la entrevista. |
| RESC04 | Contratación pública | Las adquisiciones deben cumplir las normas de contratación estatal y sus procedimientos. |
| RESC05 | Cumplimiento normativo | La solución debe considerar la protección de datos personales, los requisitos de seguridad de pagos aplicables, las reglas de la fiducia y los reportes obligatorios. |
| RESC06 | Contratos de concesión y fiducia | El software no puede modificar unilateralmente las fórmulas de remuneración ni la prelación contractual de pagos. |
| RESC07 | Plazos institucionales | El proyecto debe considerar el fin de la administración actual y el vencimiento del contrato del proveedor. |
| RESC08 | Capacidad del equipo | El área de Recaudo y Tarifas es pequeña y no puede abandonar la operación cotidiana durante la implementación. |
| RESC09 | Continuidad operativa | La transición al nuevo sistema no puede detener el servicio de transporte. |
| RESC10 | Calidad de datos históricos | Los datos históricos presentan calidad irregular, lo que puede dificultar la migración, conciliación y reconstrucción de operaciones. |

#### Síntesis

El inventario muestra que el proyecto surge principalmente de la necesidad de recuperar el control de la información del recaudo, mejorar la trazabilidad financiera y reducir la dependencia del proveedor y de procesos manuales.

Los interesados requieren información confiable y oportuna; los impulsores evidencian presiones contractuales, financieras y de auditoría; las evaluaciones describen debilidades actuales; las metas y los resultados establecen mejoras esperadas; y los principios, requerimientos y restricciones delimitan cómo debe desarrollarse e implementarse la solución.

La meta prioritaria expresada por la experta es que el ente gestor pueda demostrar con certeza cuánto dinero entró, por qué concepto y a quién se pagó.

## 3. Mapa de capacidades y proceso E2E
### V2 Mapa de capacidades
![V2 Mapa de capacidades](vistas/V2_mapa_capacidades.png)

**Análisis.** El mapa cubre a todo el ente gestor y no solo al recaudo, como pide la diapositiva 35 de 7_SOA. Tiene 44 capacidades repartidas en 9 grupos, y los colores separan las tres categorías que usó la experta al hablar de las funciones del ente: estratégicas (magenta), misionales (morado) y de apoyo (verde). Las estratégicas son Dirección y estrategia, Gobierno, riesgo y cumplimiento, y Relaciones institucionales. Las misionales son Planeación y operación del transporte, Acceso, tarifas y experiencia del usuario, y Recaudo, conciliación y liquidación. Las de apoyo son Finanzas y administración, Datos y tecnología, y Servicios corporativos. Al lado van 5 recursos (el registro histórico de transacciones y liquidaciones, el equipo de Recaudo y Tarifas, la plataforma central del proveedor, los contratos de operación, recaudo y fiducia, y los sistemas existentes) y 6 cursos de acción que se conectan con las metas de V1.

**Capacidades impactadas.** Cada capacidad trae en su documentación el impacto que le asignamos. De las 44, 20 tienen impacto directo, 17 indirecto y 7 ninguno. Las directas son las que la aplicación ejecuta o automatiza: gestión de usuarios y medios de pago (CAP19), emisión, recarga y ciclo de vida de VAMOS (CAP20), tarifas y transbordos (CAP21), perfiles y elegibilidad (CAP22), toda la cadena desde la recepción de transacciones (CAP25) hasta la liquidación (CAP29), los subsidios (CAP30) y los indicadores (CAP32), además de varias de gobierno y de datos como auditoría y trazabilidad (CAP06), riesgos y fraude (CAP07) y ciberseguridad (CAP39). Las indirectas son las que mejoran porque reciben datos de la aplicación pero no la usan para ejecutarse, por ejemplo la atención de PQR (CAP23), la contabilidad (CAP33) y la tesorería (CAP34). Las que quedan sin impacto, como la supervisión del servicio de validación (CAP17), la gestión de compras y pagos (CAP36) o la comunicación institucional (CAP44), están cerca del recaudo pero fuera de lo que cubre el software.

**Decisiones.** Una capacidad dice qué sabe hacer el ente, no qué área lo hace; por eso la personalización de tarjetas, aunque la ejecuta Servicio al Cliente, cuenta como parte del recaudo. La planeación de rutas queda con impacto indirecto: el software solo consume su catálogo de rutas para aplicar transbordos y liquidar, no diseña rutas. La operación de validadores y dispositivos es IoT y está fuera del alcance, así que ninguna capacidad la hace directa. El recurso de la plataforma del proveedor se marca como externo para no asumir que el ente la poseerá ni que se reemplazará antes de que venza el contrato.

### V3 Cadena de valor y proceso E2E
![V3 Cadena de valor y proceso E2E](vistas/V3_cadena_valor_e2e.png)

**Análisis:** _…_

## 4. Descomposición de servicios
### V4 Descomposición de servicios
![V4 Descomposición de servicios](vistas/V4_descomposicion_servicios.png)

**Análisis.** La vista baja el proceso E2E de recaudo en tres niveles. Arriba está el servicio de extremo a extremo. Debajo hay 10 servicios de plataforma que se implementan, cada uno ligado a los requerimientos de V1 que realiza (por ejemplo, la liquidación a operadores realiza REQ03 y REQ04), y debajo de ellos 19 servicios de dominio funcional. En amarillo está lo que se construye y en gris lo que queda fuera del alcance: seis servicios de plataforma, entre ellos la operación de validadores (IoT), la atención de PQR y la contabilidad y el giro de la fiducia. La cuarta capa, con los 52 servicios básicos que tienen el tamaño para construirse y los 8 que se descartan, está en V4c. La V4d muestra quién hace cada cosa: los roles del ente gestor, las funciones que realizan los servicios de plataforma y los objetos de negocio que manejan.

![V4c Servicios básicos](vistas/V4c_servicios_basicos.png)

![V4d Roles, funciones y objetos](vistas/V4d_roles_funciones_objetos.png)

**Decisiones.** Se usó la relación de agregación entre capas porque un servicio de una capa se compone de los de la inferior sin ser su dueño exclusivo. El servicio de consulta, reportes e indicadores (P10) se dejó como un servicio de plataforma y no como un dominio, porque se alimenta de los demás. La liquidación a operadores (P8) sí se incluye, pero solo aplica las fórmulas de cada contrato y no las decide, porque el software no puede modificar unilateralmente las reglas de remuneración (RESC06).

#### Descomposición del proceso E2E en capas

Partimos del proceso E2E de recaudo, tal como lo corrigió la experta (pregunta 2.9): adquirir el medio de pago, cargar saldo (solo VAMOS), validar, transmitir las transacciones, cobrar al banco de forma diferida (solo tarjeta bancaria), consignar a la fiducia, consolidar, conciliar, liquidar y girar, más un carril de excepciones para bloqueos, devoluciones, transacciones tardías y reclamos. Lo bajamos con las capas de la diapositiva 28 de 7_SOA: (1) proceso E2E, (2) servicios de negocio de plataforma, (3) servicios de dominio funcional, (4) servicios básicos de subdominio, que son los que tienen el tamaño para construirse, y (5) la capa anticorrupción, que aparece en la última tabla de esta sección.

Para decidir en qué capa va cada servicio usamos las preguntas de la diapositiva 33. Por ejemplo, con "determinar la tarifa esperada de un viaje": la responsabilidad es de Recaudo y Tarifas, se usa al verificar cada viaje y al calcular el cobro bancario diferido, los datos los gestiona el procesamiento de transacciones, las reglas las define el tarifario por acto administrativo y el conocimiento está en quien publica ese tarifario. Un servicio de plataforma agrupa varios servicios de dominio que el proceso E2E orquesta; uno de dominio funcional tiene un solo dueño de datos y de reglas.

| Plataforma (L2) | Dominio funcional (L3) | Servicios básicos (L4) | Capacidad en V2 |
|---|---|---|---|
| P1 Gestión de reglas tarifarias | Administración del tarifario | Definir tarifas, reglas de transbordo y límites de uso · Publicar el tarifario · Consultar el tarifario vigente por fecha | CAP21 |
| P2 Gestión de tarjetas y saldos | Ciclo de vida de la tarjeta | Emitir y personalizar la tarjeta · Reponer la tarjeta con traslado de saldo · Retirar las tarjetas de primera generación | CAP19, CAP20 |
|  | Saldo calculado | Registrar recargas · Aplicar movimientos al saldo calculado · Consultar saldo e historial | CAP20 |
| P3 Gestión de usuarios y perfiles | Titulares y datos personales | Registrar el titular y su autorización de datos · Atender solicitudes de consulta, rectificación y supresión | CAP08, CAP19 |
|  | Perfiles tarifarios | Solicitar el perfil · Recibir y validar las certificaciones · Verificar la elegibilidad · Gestionar la vigencia del perfil · Controlar el consumo subsidiado | CAP22 |
| P4 Gestión de listas de control | Decisiones de lista | Registrar una decisión de lista · Levantar una decisión de lista | CAP07 |
|  | Distribución de listas | Publicar la versión de lista · Vigilar la sincronización de los validadores | CAP07, CAP37 |
| P5 Procesamiento de transacciones | Recepción de transacciones | Registrar la transacción · Controlar la completitud | CAP25, CAP26 |
|  | Reconstrucción y verificación del viaje | Asociar la validación a un viaje y reconocer el transbordo · Determinar la tarifa esperada y detectar diferencias · Cerrar el viaje | CAP21, CAP26 |
| P6 Cobro con tarjeta bancaria | Cobro diferido | Generar el cobro diario · Enviar al adquirente y registrar el resultado · Reintentar el cobro | CAP19, CAP30 |
|  | Cartera y contracargos | Gestionar la deuda de la tarjeta · Gestionar los contracargos | CAP30 |
| P7 Consolidación y conciliación | Consolidación | Consolidar los usos · Consolidar las ventas · Incorporar ajustes extemporáneos | CAP27 |
|  | Conciliación | Conciliar por capa · Gestionar las diferencias | CAP28 |
|  | Base de liquidación | Generar la base de liquidación · Aprobar la base de liquidación | CAP27, CAP29 |
| P8 Liquidación a operadores | Esquema de remuneración | Definir y publicar el esquema de un contrato | CAP29 |
|  | Liquidación | Calcular la liquidación · Aprobar la liquidación · Gestionar las objeciones · Preparar la instrucción de giro y registrar el giro | CAP29, CAP34 |
|  | Subsidio | Calcular el subsidio mensual · Presentar el subsidio | CAP30 |
| P9 Ajustes y devoluciones | Gestión de solicitudes | Registrar la solicitud · Aprobar según el monto · Aplicar el ajuste a favor · Solicitar el giro de devolución o el reverso bancario | CAP24 |
| P10 Consulta, reportes e indicadores | Servicio de consulta | Consultar el historial de la tarjeta · Generar los indicadores · Detectar anomalías · Generar los reportes obligatorios | CAP10, CAP32, CAP40 |

#### Tabla de inclusión y exclusión

Los 52 servicios de capa 4 de la tabla de arriba se implementan todos, porque cada uno responde a una necesidad del alcance o de un requerimiento de V1. Abajo justificamos el nivel de plataforma y de dominio, y los servicios que dejamos fuera, incluidos los de capa 4.

| Capa | Servicio | ¿Se implementa? | Justificación |
|---|---|---|---|
| L2 | P1 Gestión de reglas tarifarias | Sí | El alcance pide tarifas y perfiles, y REQ02 lo exige con vigencias e historial. |
| L2 | P2 Gestión de tarjetas y saldos | Sí | El alcance incluye emisión, recargas, consulta de saldo y bloqueo de VAMOS. |
| L2 | P3 Gestión de usuarios y perfiles | Sí | El alcance pide validar que la persona cumple su perfil; además REQ05 y REQ09 (datos personales). |
| L2 | P4 Gestión de listas de control | Sí | La experta quiere que la decisión de bloquear o permitir sea del ente y quede con responsable y motivo (REQ06). |
| L2 | P5 Procesamiento de transacciones | Sí | El enunciado dice que el software recibe las transacciones y aplica la tarifa correcta; REQ01. |
| L2 | P6 Cobro con tarjeta bancaria | Sí | Es el medio de pago de los visitantes y su flujo es distinto al de VAMOS (cobro diferido). |
| L2 | P7 Consolidación y conciliación | Sí | Está en el alcance y es la meta principal de la experta. REQ03. |
| L2 | P8 Liquidación a operadores | Sí | REQ03 y REQ04; en V2 las capacidades de liquidación y subsidios tienen impacto directo. El software aplica las fórmulas de cada contrato pero no las decide (RESC06). |
| L2 | P9 Ajustes y devoluciones | Sí | REQ08; sin esto un reclamo de saldo no se puede cerrar. |
| L2 | P10 Consulta, reportes e indicadores | Sí | REQ07, REQ10 y REQ11; ataca la atención lenta de PQR (EVA05) y la poca medición de evasión (EVA10). |
| L2 | Operación de validadores, lectores y canales de recarga | No | Es IoT y dispositivos, fuera del alcance. La opera el proveedor (RESC01); solo recibimos lo que generan. |
| L2 | Gestión de la flota y los kilómetros recorridos | No | Es de Operaciones. Los kilómetros se consumen para conciliar y liquidar. |
| L2 | Planeación de rutas y servicios | No | Es de Planeación. Se consume el catálogo de rutas y estaciones. |
| L2 | Atención de PQR | No | Está en el sistema de Servicio al Cliente. El software le da el historial de la tarjeta y recibe las solicitudes de ajuste. |
| L2 | Contabilidad, tesorería y giro de la fiducia | No | Son de Finanzas y de la fiducia. El software entrega la liquidación y la instrucción de giro soportada. |
| L2 | Certificación de la condición de cada perfil | No | La hacen colegios, universidades y entidades de salud. El software recibe y valida sus listados. |
| L3 | Todos los de la tabla de capas | Sí | Cada uno tiene un dueño claro de datos y reglas dentro de una plataforma incluida. |
| L4 | Publicar la tabla de tarifas en los validadores | No | Lo ejecuta el proveedor. El software le entrega el tarifario por la capa anticorrupción. |
| L4 | Actualizar las listas dentro del validador | No | Igual: entregamos la versión de lista y el proveedor la distribuye. |
| L4 | Vender tarjetas y recargar en taquillas, tiendas y máquinas | No | Son canales del proveedor. El software solo registra la venta y la consignación. |
| L4 | Detectar la evasión en vía | No | La experta fue clara (H14): el control es físico, de Operaciones y la Policía. El software mide e identifica anomalías. |
| L4 | Autorizar y compensar pagos con tarjeta bancaria | No | Lo hace el adquirente. El software le envía el cobro y recibe el resultado. |
| L4 | Calcular las fórmulas de remuneración de los contratos | No | Las definen Finanzas y Jurídica y cambian por contrato (H02). El software las parametriza pero no las modifica. |
| L4 | Cruce con la Registraduría para detectar fallecidos | No | Hoy no existe ese cruce; queda como mejora futura. |
| L4 | Gestión de credenciales de servicio | No (por decidir) | La experta la mencionó como débil, pero el enunciado no la pide. Es una pregunta abierta del boceto del mapa de capacidades. |

#### Contratos de servicio (contract-first)

Cada servicio básico de la capa 4 tiene su contrato como objeto *Contract* en el modelo (vista V4b), con los mismos datos de esta tabla en su documentación. Los requisitos no funcionales salen de lo que dijo la experta (por ejemplo las 48 horas de llegada de transacciones, la espera de 48 horas para trasladar saldo o la meta de diferencia de conciliación) y de las reglas de protección de datos.

![V4b Contratos de servicio](vistas/V4b_contratos.png)

| Servicio | Entradas | Salidas | Errores | Requisitos no funcionales |
|---|---|---|---|---|
| Definir tarifas, reglas de transbordo y límites de uso | Perfil tarifario, valor o descuento, ventana de transbordo, máximo de transbordos, valor del 1.er y 2.º transbordo, límite mensual de viajes subsidiados y vigencia. | Borrador de tarifario con su número de versión. | Descuento fuera de 0 a 100 %; falta la tarifa plena; vigencia incompleta. | Conserva todas las versiones; registra quién cambió qué y cuándo. |
| Publicar el tarifario | Versión del tarifario, acto administrativo y fecha de vigencia. | Tarifario publicado, inmutable, y entrega al proveedor por la capa anticorrupción. | Sin acto administrativo; vigencia que se traslapa con otra; versión incompleta. | Inmutable una vez publicado; se entrega con días de anticipación a su vigencia. |
| Consultar el tarifario vigente por fecha | Fecha y hora, perfil tarifario. | Tarifa, reglas de transbordo y límites que regían en esa fecha. | Fecha sin tarifario vigente. | Responde con la regla de la fecha de la validación y no con la de llegada de la transacción. |
| Emitir y personalizar la tarjeta | Tipo (al portador o personalizada), documento del titular y su autorización de datos si es personalizada, canal. | Tarjeta emitida con su número y su estado. | Titular sin autorización de datos; tarjeta ya emitida. | Protege los datos personales (Ley 1581 de 2012). |
| Reponer la tarjeta con traslado de saldo | Número de la tarjeta bloqueada e identidad verificada del titular. | Tarjeta nueva y orden de traslado del saldo calculado. | Tarjeta al portador (no se repone); no han pasado las 48 horas de espera. | Espera unas 48 horas para que lleguen las transacciones pendientes. |
| Retirar las tarjetas de primera generación | Número de tarjeta y tarjeta nueva de reemplazo. | Tarjeta retirada y bloqueada, con el saldo respetado. | Tarjeta ya retirada. | Una tarjeta retirada no se puede reactivar. |
| Registrar recargas | Tarjeta, valor, canal y referencia de la venta. | Recarga registrada; si viene de la app o la web queda pendiente de aplicar. | Valor menor a $2.000; saldo que superaría $200.000; tarjeta bloqueada. | Idempotente por la referencia de la venta. |
| Aplicar movimientos al saldo calculado | Transacción con el consecutivo de la tarjeta y su valor. | Saldo calculado actualizado. | Salto de consecutivo (se reporta como diferencia); saldo por debajo de menos una tarifa. | Se aplican en orden de consecutivo; las diferencias se investigan como posible fraude. |
| Consultar saldo e historial | Tarjeta. | Saldo calculado, recargas pendientes, estado y últimos movimientos. | Tarjeta inexistente. | Respuesta en línea para Servicio al Cliente; aclara que el saldo real está en la tarjeta. |
| Registrar el titular y su autorización de datos | Documento, datos de contacto y autorización (del acudiente si es menor). | Titular registrado con autorización vigente. | Menor sin acudiente; autorización incompleta. | Solo los datos necesarios; los de salud con acceso restringido. |
| Atender solicitudes de consulta, rectificación y supresión | Titular y tipo de solicitud. | Respuesta y registro de lo que se hizo. | Titular no verificado; dato que la ley obliga a conservar. | Deja evidencia y respeta los plazos de ley. |
| Solicitar el perfil | Titular, tarjeta personalizada, tipo de perfil y soportes. | Solicitud en verificación. | Tarjeta al portador; el titular ya tiene un perfil activo. | Trazable por titular. |
| Recibir y validar las certificaciones | Listados de las instituciones y certificados. | Certificaciones aceptadas o rechazadas, con su motivo. | Formato no reconocido; titular no encontrado. | Soporta formatos distintos por institución y los picos de enero y julio. |
| Verificar la elegibilidad | Solicitud con su certificación. | Elegible o no, con la vigencia. | Certificación vencida; institución que no responde. | Aplica la regla de cada perfil (edad, matrícula, discapacidad). |
| Gestionar la vigencia del perfil | Perfil, evento (activar, vencer o retirar) y motivo. | Perfil actualizado y novedad para los validadores. | Retiro sin motivo. | Al vencer, la tarjeta sigue a tarifa plena; avisa el vencimiento. |
| Controlar el consumo subsidiado | Validación con tarifa especial. | Contador mensual de viajes subsidiados. | Validación ya contada. | No cuenta los transbordos gratuitos; el límite ronda los 50 viajes al mes. |
| Registrar una decisión de lista | Tarjeta o identificación técnica, lista (bloqueo o denegación), motivo y responsable. | Decisión registrada y orden de publicar. | Sin motivo o sin responsable; bloqueo por pérdida de una tarjeta al portador. | Auditable: nada se borra. |
| Levantar una decisión de lista | Decisión, motivo y quien autoriza. | Decisión levantada y orden de publicar. | Bloqueo por pérdida (no se reversa); quien levanta no tiene permiso. | Solo Recaudo y Tarifas levanta bloqueos por fraude. |
| Publicar la versión de lista | Decisiones nuevas. | Versión numerada entregada al proveedor. | Versión con salto de número. | Inmutable una vez publicada. |
| Vigilar la sincronización de los validadores | Reportes de sincronización por validador. | Validadores desactualizados (más de unas 48 horas) señalados. | Validador que no reporta. | Alerta oportuna a Operaciones. |
| Registrar la transacción | Transacción del validador: medio de pago, perfil, fecha y hora, validador, ruta, operador, tipo, valor, saldo antes y después y consecutivo. | Transacción registrada, o marcada como duplicada o extemporánea. | Transacción incompleta; ruta inexistente. | Idempotente por validador y consecutivo; acepta llegadas de hasta 48 horas. |
| Controlar la completitud | Contadores de cierre del validador y transacciones recibidas. | Informe de completitud por validador y por día. | Contador sin transacciones. | Mide el 99 % recibido en 24 horas y el 100 % en 48 horas. |
| Asociar la validación a un viaje y reconocer el transbordo | Transacción y viaje abierto del medio de pago. | Viaje actualizado; transbordo reconocido o no. | Transbordo en la misma ruta o estación; más de 2 transbordos; fuera de los 90 minutos. | Tolera llegadas desordenadas y reconstruye el viaje. |
| Determinar la tarifa esperada y detectar diferencias | Viaje, perfil y tarifario de la fecha. | Tarifa esperada y diferencia con lo cobrado. | Perfil o tarifario no encontrado. | Usa la regla vigente en la fecha de la validación. |
| Cerrar el viaje | Viaje con la ventana vencida. | Viaje cerrado, listo para el cobro bancario y la consolidación. | Viaje ya cerrado. | Una vez cerrado solo cambia con un ajuste. |
| Generar el cobro diario | Viajes cerrados por identificación técnica de la tarjeta y fecha. | Cobro diario (siempre tarifa plena, con los transbordos aplicados). | Cobro ya generado para esa tarjeta y fecha. | No almacena el número completo de la tarjeta. |
| Enviar al adquirente y registrar el resultado | Cobro diario. | Cobro aprobado o rechazado. | Adquirente no disponible (se acumula y se reintenta); tarjeta inválida. | Envío en la madrugada; PCI DSS a través del adquirente. |
| Reintentar el cobro | Cobro rechazado. | Cobro aprobado o rechazo definitivo. | Se superaron los 3 intentos. | Alrededor de 3 intentos durante algunos días. |
| Gestionar la deuda de la tarjeta | Rechazo definitivo o pago del usuario. | Deuda registrada o saldada, con la orden de denegar o de levantar la denegación. | Pago parcial; deuda ya saldada. | La cartera se castiga tras el plazo; la meta es una cartera no cobrada menor al 1 %. |
| Gestionar los contracargos | Contracargo notificado por el adquirente. | Respuesta con la evidencia de los toques. | Plazo vencido. | Conserva la evidencia de los toques. |
| Consolidar los usos | Transacciones y periodo. | Líneas por modo, ruta, operador y tipo de tarifa. | Transacción de un periodo ya cerrado (entra como ajuste). | Cuadre: la suma de las líneas es igual al total del periodo. |
| Consolidar las ventas | Ventas y consignaciones por canal y punto. | Líneas por canal, punto y medio de pago, con sus diferencias. | Consignación mayor a lo vendido. | Diaria. |
| Incorporar ajustes extemporáneos | Transacción tardía de un periodo cerrado. | Ajuste en el periodo abierto con su periodo de origen. | Sin periodo de origen. | Trazable hasta la transacción original. |
| Conciliar por capa | Capa (ventas contra consignaciones, transacciones contra el proveedor, usos contra kilómetros, con el operador) y periodo. | Diferencias detectadas. | Falta un insumo, por ejemplo los kilómetros. | Meta de diferencia sin explicar del 0,1 % o menos. |
| Gestionar las diferencias | Diferencia, explicación y responsable. | Diferencia explicada o pendiente. | Diferencia sin responsable. | No se cierra un periodo con diferencias sin clasificar. |
| Generar la base de liquidación | Periodo cerrado y conciliado. | Base por modo, ruta y operador con huella de integridad. | Periodo abierto o con diferencias sin clasificar. | Inmutable. |
| Aprobar la base de liquidación | Base y aprobador. | Base aprobada. | El aprobador es quien la generó. | Separación de funciones. |
| Definir y publicar el esquema de un contrato | Contrato, reglas (kilómetros, pasajeros, indicadores), prelación de pagos y vigencia. | Esquema vigente y versionado. | Vigencia que se traslapa; regla sin fuente de dato. | Un esquema vigente no se modifica: cada cambio es una versión con soporte contractual. |
| Calcular la liquidación | Base aprobada, kilómetros certificados, esquema vigente y tipo (preliminar semanal o definitiva mensual). | Liquidación por beneficiario con el origen de cada valor. | Faltan los kilómetros certificados. | Cada valor se reconstruye desde sus insumos, sin depender de Excel. |
| Aprobar la liquidación | Liquidación y aprobador. | Liquidación aprobada. | El aprobador es quien liquidó. | Separación de funciones. |
| Gestionar las objeciones | Objeción del operador y línea objetada. | Objeción registrada y resuelta. | Fuera del plazo. | Suspende solo la línea objetada. |
| Preparar la instrucción de giro y registrar el giro | Liquidación aprobada. | Instrucción soportada para la Gerencia y giro confirmado por la fiducia. | El giro no respeta la prelación de pagos. | Trazable desde el peso pagado hasta su origen. |
| Calcular el subsidio mensual | Periodo de usos cerrado. | Valor a cobrar por viajes con tarifa especial. | Periodo abierto. | Calculado sobre datos cerrados. |
| Presentar el subsidio | Subsidio calculado. | Subsidio presentado a Hacienda. | Subsidio ya presentado (las diferencias van como ajuste). | Inmutable una vez presentado. |
| Registrar la solicitud | Referencia a la PQR, tipo (ajuste a favor, devolución en dinero, reverso bancario o traslado de saldo), monto, causa y evidencias. | Solicitud registrada. | Sin PQR de referencia. | Conserva las evidencias. |
| Aprobar según el monto | Solicitud y aprobador. | Solicitud aprobada o rechazada. | El aprobador no tiene nivel para ese monto; quien registra la solicitud intenta aprobarla. | Hasta $50.000 con causa clara aprueba Servicio al Cliente; el resto, Recaudo y Tarifas. |
| Aplicar el ajuste a favor | Solicitud aprobada. | Ajuste cargado como recarga pendiente de la tarjeta. | Ajuste ya aplicado. | Se aplica una sola vez y entra a la conciliación del mes. |
| Solicitar el giro de devolución o el reverso bancario | Solicitud aprobada y certificación bancaria. | Orden a Finanzas o al adquirente. | Sin certificación bancaria. | Una devolución en dinero tarda de dos a cuatro semanas. |
| Consultar el historial de la tarjeta | Tarjeta y rango de fechas. | Validaciones, recargas, ajustes, rechazos, estado, perfil y viajes subsidiados del mes. | Sin permiso. | Respuesta en línea; no muestra datos personales a quien no los necesita. |
| Generar los indicadores | Periodo y filtros por operador, ruta o modo. | Indicadores de recaudo: evasión estimada, completitud, diferencia de conciliación, cierre y PQR. | Faltan insumos. | Sin armarlos a mano. |
| Detectar anomalías | Validaciones, conteos de pasajeros y saldos. | Alertas: baja validación, diferencias de saldo y perfiles prestados. | Sin datos de comparación. | Ayudan a dirigir el control, no a eliminar la evasión. |
| Generar los reportes obligatorios | Periodo y entidad. | Reporte para DANE, Superintendencias, Ministerio y Contraloría. | Datos incompletos. | Sin trabajo manual; conserva el origen de cada dato. |

#### Servicios externos (capa anticorrupción)

Salieron de las respuestas del bloque 9 de la entrevista. "Entra" y "sale" se miran desde el software. Con esta tabla se armó V9, que coincide con ella fila por fila.

| Externo | Tipo | Información intercambiada | Dirección | Sincronía / frecuencia |
|---|---|---|---|---|
| Validadores y plataforma central del proveedor de recaudo | Dispositivo, sistema legado y proveedor | Entra: transacciones (medio de pago, perfil, fecha y hora, validador, ruta, operador, tipo, valor cobrado, saldo antes y después, consecutivo), eventos del equipo y contadores de cierre. Sale: tarifario con su vigencia, reglas de transbordo y límites, listas de bloqueo y denegación, recargas pendientes y novedades de perfil | Ambas | Metro y estaciones casi en línea; buses por lotes cuando hay conexión, hasta 48 horas. Listas varias veces por hora en estaciones y cada pocas horas en buses |
| Servicio al Cliente (sistema de PQR) | Proceso interno y sistema separado | Sale: historial de la tarjeta, saldo calculado, recargas pendientes, estado, perfil y reglas vigentes. Entra: solicitudes de bloqueo, traslado de saldo, ajuste y devolución, datos de personalización y autorizaciones de datos | Ambas | Caso a caso y en línea; hoy tarda de uno a tres días |
| Finanzas (sistema financiero y contable) | Proceso interno y sistema | Sale: recaudo diario por canal, liquidación preliminar semanal y, cada mes, liquidación definitiva, informe de conciliación, saldo en tarjetas, subsidio, cartera, devoluciones y comisiones. Entra: aprobación de la liquidación y giros de devoluciones ejecutados | Ambas | Diaria, semanal y mensual, por lotes |
| Fiduciaria (portal y cuentas del patrimonio autónomo) | Entidad financiera | Entra: movimientos y saldos de las cuentas recaudadoras y consignaciones por canal, para conciliar ventas contra lo consignado | Entra | Diaria, por consulta del portal o archivo |
| Planeación | Proceso interno | Entra: catálogo de rutas, estaciones y paradas, rutas integradas y asignación de ruta a operador, incluidas las rutas temporales. Sale: validaciones por ruta, estación y franja, secuencias de transbordo sin datos personales y uso por perfil | Ambas | El catálogo cambia pocas veces al mes (las rutas temporales a veces se avisan con 1 o 2 días); la demanda se entrega cada mes |
| Operaciones (sistema de gestión de flota) | Proceso interno y sistema | Entra: kilómetros programados y ejecutados, validadores fuera de servicio y conteos de pasajeros para estimar evasión. Sale: alertas por pocas validaciones en una ruta o estación y validadores sin sincronizar | Ambas | Semanal y mensual para los kilómetros; alertas diarias |
| Adquirente, redes y pasarelas de pago | Entidad financiera y proveedor | Sale: cobro consolidado diario por tarjeta, reversos y respuestas a contracargos. Entra: resultado de los cobros, abonos de la compensación, contracargos, tarjetas reportadas como bloqueadas y recargas en línea confirmadas | Ambas | El cobro se envía en la madrugada; el abono llega entre 1 y 3 días hábiles; los contracargos llegan como evento |
| Canales de recarga (taquillas, tiendas, máquinas, app y web) | Proveedor y terceros | Entra: ventas y recargas por canal y punto, y las consignaciones | Entra | Diaria, a través de los reportes del proveedor |
| Instituciones que certifican perfiles (colegios, Secretaría de Educación, universidades y entidades de discapacidad) | Entidad externa | Entra: listados de matriculados y habilitados, retiros y certificados de discapacidad. Sale: formato uniforme de reporte y avisos de vencimiento | Ambas | Por semestre o año, con picos en enero y julio; hoy llegan en Excel con formatos distintos |
| Autoridad de transporte (Secretaría de Movilidad) | Regulador | Entra: actos de tarifa y decisiones sobre servicios y rutas. Sale: demanda y recaudo, indicadores de calidad, evasión y PQR, y estudio técnico de tarifa | Ambas | Los actos de tarifa salen normalmente en diciembre; los reportes son mensuales o trimestrales |
| Alcaldía y Secretaría de Hacienda | Entidad pública | Sale: cálculo del subsidio (viajes con tarifa especial por la diferencia con la tarifa plena) | Sale | Mensual |
| Operadores de flota y operador del metro | Socio contractual | Sale: liquidación con el soporte de cálculo. Entra: objeciones, novedades de flota (buses nuevos o retirados) y reportes de fallas de validadores | Ambas | Semanal (preliminar) y mensual |
| Entes de control y reportes obligatorios (DANE, Superintendencia de Transporte, Ministerio, Superintendencia de Industria y Comercio, Contraloría) | Regulador | Sale: reportes obligatorios y registro de las bases de datos personales | Sale | Mensual o anual, según el reporte |
| Comunicaciones | Proceso interno | Sale: avisos de perfil vencido, deuda y cambio de tarifa | Sale | Por evento |

Quedan las 6 interoperabilidades que pedía el enunciado (servicio al cliente, financiero, planeación, redes de pago, instituciones que certifican y autoridad de transporte) y 8 que surgieron de la entrevista y del mapa de capacidades: el proveedor y sus validadores, la fiduciaria, Operaciones, los canales de recarga, Hacienda, los operadores, los entes de control y comunicaciones. La experta dijo que la integración más crítica para el día a día es la de los validadores con la plataforma central; en segundo lugar la red de recargas, y en lo financiero la fiducia, porque de ella depende que los operadores reciban su plata.

## 5. Dominios y lenguaje ubicuo

### V5 borrador

## 5. T23 — Extracción de dominios

La extracción de dominios se realiza a partir de la estructura organizacional identificada en la entrevista, la cadena de valor y el proceso E2E representados en V3, y los servicios de negocio agrupados por capas y delimitados por alcance en V4.

El objetivo es agrupar las responsabilidades del negocio en dominios coherentes, identificando sus límites a partir de los eventos del proceso y de los cambios de responsabilidad.

### 5.1. Paso 1: Estructura organizacional

La entrevista identifica las siguientes áreas y actores que participan en el proceso de recaudo:

| Área o actor                          | Responsabilidades                                                                                                                |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Recaudo y Tarifas                     | Definir reglas de recaudo, administrar tarifas y perfiles, supervisar al proveedor, consolidar, conciliar y liquidar el recaudo. |
| Servicio al Cliente                   | Gestionar tarjetas y perfiles registrados, bloqueos, PQR, devoluciones y traslados de saldo.                                     |
| Finanzas y Tesorería                  | Revisar liquidaciones, gestionar información financiera, controlar subsidios y cartera, y preparar reportes contables.           |
| Operaciones                           | Controlar la operación, certificar kilómetros recorridos y reportar novedades de flota y validadores.                            |
| Planeación                            | Diseñar rutas y servicios, estudiar la demanda y proporcionar información que afecta las reglas de integración tarifaria.        |
| Tecnología                            | Gestionar infraestructura e intercambio de información con el proveedor de recaudo.                                              |
| Jurídica                              | Gestionar contratos, actos tarifarios y asuntos relacionados con la protección de datos.                                         |
| Gerencia General                      | Tomar decisiones institucionales y autorizar los pagos según las responsabilidades establecidas.                                 |
| Proveedor de recaudo                  | Operar los validadores, lectores, canales contratados y la plataforma de transacciones.                                          |
| Redes de pago y entidades financieras | Participar en la autorización, procesamiento y liquidación de pagos bancarios.                                                   |
| Operadores del SIT                    | Operar los servicios de transporte, reportar novedades y revisar u objetar liquidaciones.                                        |
| Fiduciaria                            | Custodiar los recursos y ejecutar los giros autorizados.                                                                         |
| Instituciones certificadoras          | Certificar las condiciones de los usuarios que solicitan perfiles tarifarios especiales.                                         |
| Autoridad de transporte y Alcaldía    | Emitir decisiones y actos administrativos que condicionan las tarifas y la operación del sistema.                                |
| Usuario del sistema                   | Utilizar los medios de pago, realizar viajes y solicitar consultas o reclamaciones relacionadas con el recaudo.                  |

La estructura organizacional evidencia que el proceso de recaudo involucra responsabilidades diferenciadas: definición de reglas, administración de medios de pago y perfiles, procesamiento de transacciones, conciliación, liquidación y consulta de información.

Según la frontera definida en V4, la operación de validadores, la gestión de flota y rutas, la atención general de PQR, la contabilidad y tesorería, y la certificación externa de perfiles se mantienen fuera del alcance de implementación. El software consume o intercambia información con estos servicios.

### 5.2. Paso 2: Tormenta de eventos del proceso

A partir del proceso E2E de V3 y de los servicios de negocio de V4, se identifican los siguientes eventos relevantes. Estos representan hechos que ocurren durante el proceso, no funcionalidades del software.

| ID   | Evento de negocio                                                                | Responsabilidad relacionada                  |
| ---- | -------------------------------------------------------------------------------- | -------------------------------------------- |
| EV01 | Se configura una tarifa, un perfil o una vigencia.                               | Gestión de reglas tarifarias.                |
| EV02 | Un usuario obtiene o personaliza un medio de pago.                               | Gestión de tarjetas y saldos.                |
| EV03 | Se registra una recarga o un cambio de saldo.                                    | Gestión de tarjetas y saldos.                |
| EV04 | Se habilita, renueva o vence un perfil tarifario.                                | Gestión de usuarios y perfiles.              |
| EV05 | Se registra una decisión de bloqueo o desbloqueo.                                | Gestión de listas de control.                |
| EV06 | Se encuentra disponible un lote de transacciones en la plataforma del proveedor. | Integración y recepción de transacciones.    |
| EV07 | Se reciben transacciones externas.                                               | Procesamiento de transacciones.              |
| EV08 | Se detecta una transacción duplicada o una inconsistencia temporal.              | Procesamiento de transacciones.              |
| EV09 | Se verifica un viaje y se aplican las reglas tarifarias correspondientes.        | Procesamiento de transacciones.              |
| EV10 | Se consolida el recaudo por modo, ruta, operador y medio de pago.                | Consolidación del recaudo.                   |
| EV11 | Se comparan las ventas, recargas y consignaciones.                               | Conciliación del recaudo.                    |
| EV12 | Se detecta una diferencia de conciliación.                                       | Conciliación del recaudo.                    |
| EV13 | Se resuelve una diferencia y se reprocesan los datos afectados.                  | Conciliación del recaudo.                    |
| EV14 | Se calcula el subsidio y se prepara la liquidación.                              | Liquidación a operadores.                    |
| EV15 | Se aprueba una liquidación y se autoriza una instrucción de pago.                | Liquidación y aprobación de la distribución. |
| EV16 | La fiduciaria confirma la ejecución de un pago.                                  | Integración financiera externa.              |
| EV17 | Se cierra un periodo de recaudo.                                                 | Cierre y reporte de resultados.              |
| EV18 | Se publican informes e indicadores del periodo.                                  | Consulta, reportes e indicadores.            |
| EV19 | Se registra un cobro bancario rechazado o un contracargo.                        | Cobro con tarjeta bancaria.                  |
| EV20 | Se aprueba un ajuste o una devolución.                                           | Ajustes y devoluciones.                      |

Los eventos muestran una secuencia de responsabilidades desde la configuración de las reglas y la recepción de transacciones hasta la consolidación, conciliación, liquidación, autorización de pagos y publicación de resultados.

### 5.3. Paso 3: Identificación de puntos de corte

Los puntos de corte permiten separar responsabilidades que tienen reglas, objetivos o resultados propios. Se identifican a partir de las transiciones entre los procesos de V3 y los servicios agrupados en V4.

| ID   | Punto de corte                                       | Responsabilidad de origen                                                | Responsabilidad de destino                                                      | Justificación                                                                                     |
| ---- | ---------------------------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| PC01 | Configuración tarifaria / procesamiento del viaje    | Definir tarifas, perfiles y vigencias.                                   | Recibir transacciones y aplicar las reglas configuradas.                        | La configuración de reglas es diferente de su aplicación a cada viaje.                            |
| PC02 | Medios de pago / perfiles tarifarios                 | Administrar tarjetas, recargas y saldos.                                 | Gestionar titulares, certificaciones y beneficios tarifarios.                   | El medio de pago y la elegibilidad para un beneficio representan responsabilidades distintas.     |
| PC03 | Gestión de listas / validadores externos             | Registrar decisiones de bloqueo y distribuir listas.                     | Aplicar las listas durante la validación.                                       | La decisión pertenece al negocio; la operación del dispositivo está fuera del alcance.            |
| PC04 | Recepción / procesamiento de transacciones           | Recibir los registros enviados por el proveedor.                         | Validar integridad, controlar duplicados, reconstruir viajes y aplicar tarifas. | La recepción de datos no equivale a su procesamiento completo.                                    |
| PC05 | Procesamiento de viajes / cobro bancario             | Determinar las validaciones y los consumos.                              | Consolidar cobros y gestionar rechazos y contracargos.                          | El cobro bancario tiene estados y reglas diferentes a la validación del viaje.                    |
| PC06 | Consolidación / conciliación                         | Agrupar las transacciones y obtener totales.                             | Comparar ventas, recargas y consignaciones, e investigar diferencias.           | Consolidar información no garantiza que los valores coincidan con los registros financieros.      |
| PC07 | Conciliación / liquidación                           | Determinar y explicar las diferencias del recaudo.                       | Calcular los valores correspondientes a los operadores.                         | La liquidación utiliza información consolidada y conciliada junto con las reglas contractuales.   |
| PC08 | Liquidación / ejecución del pago                     | Calcular, revisar y aprobar la distribución.                             | Ejecutar el giro a través de la fiduciaria.                                     | El software soporta el cálculo y la autorización; la fiduciaria ejecuta la transferencia.         |
| PC09 | Ajustes de recaudo / atención general de PQR         | Registrar y soportar ajustes o devoluciones relacionados con el recaudo. | Gestionar la atención y respuesta al usuario.                                   | La atención general de PQR permanece fuera del alcance, aunque requiere información del software. |
| PC10 | Gestión de perfiles / certificación externa          | Registrar y aplicar perfiles tarifarios.                                 | Verificar y certificar la condición del beneficiario.                           | La certificación corresponde a instituciones externas.                                            |
| PC11 | Datos operativos / liquidación                       | Proporcionar información de rutas, flota y kilómetros recorridos.        | Utilizar los datos para consolidar y liquidar el recaudo.                       | Planeación y Operaciones suministran datos, pero no forman parte del software de recaudo.         |
| PC12 | Procesamiento y liquidación / consulta de resultados | Generar y conservar los datos operativos y financieros.                  | Consultar, consolidar y publicar indicadores e informes.                        | Los reportes consumen información producida por otros procesos.                                   |

### 5.4. Dominios identificados y responsabilidades

A partir de la estructura organizacional, los eventos del proceso y los puntos de corte, se identifican los siguientes dominios candidatos. La agrupación conserva las responsabilidades de V4 y respeta la frontera del alcance definida para el proyecto.

| ID    | Dominio                          | Servicios de V4 relacionados                                         | Responsabilidades del dominio                                                                                                         |
| ----- | -------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| DOM01 | Gestión tarifaria                | Administración del tarifario.                                        | Administrar tarifas, perfiles aplicables, reglas de transbordo y vigencias tarifarias.                                                |
| DOM02 | Gestión de medios de pago        | Ciclo de vida de la tarjeta; saldo calculado.                        | Gestionar tarjetas, recargas, saldos, bloqueos relacionados con el medio de pago y consultas de saldo.                                |
| DOM03 | Gestión de usuarios y perfiles   | Titulares y datos personales; perfiles tarifarios.                   | Gestionar titulares, condiciones de elegibilidad, perfiles especiales, certificaciones recibidas y vigencias.                         |
| DOM04 | Gestión de listas de control     | Decisiones de lista; distribución de listas.                         | Registrar decisiones de bloqueo y desbloqueo, mantener las listas y gestionar su distribución hacia los sistemas externos.            |
| DOM05 | Procesamiento de transacciones   | Recepción de transacciones; reconstrucción y verificación del viaje. | Recibir transacciones, verificar integridad, controlar duplicados y temporalidad, reconstruir viajes y aplicar las reglas tarifarias. |
| DOM06 | Cobro con tarjeta bancaria       | Cobro diferido; cartera y contracargos.                              | Consolidar consumos bancarios, registrar estados de cobro, gestionar rechazos y hacer seguimiento a cartera y contracargos.           |
| DOM07 | Consolidación y conciliación     | Consolidación; conciliación.                                         | Consolidar el recaudo por modo, ruta, operador y medio de pago; comparar registros y gestionar diferencias.                           |
| DOM08 | Liquidación a operadores         | Base de liquidación; esquema de remuneración; liquidación; subsidio. | Aplicar reglas contractuales, calcular liquidaciones, determinar subsidios y preparar la distribución para su aprobación.             |
| DOM09 | Ajustes y devoluciones           | Gestión de solicitudes.                                              | Gestionar solicitudes de ajuste y devolución, registrar aprobaciones y conservar la trazabilidad de los cambios económicos.           |
| DOM10 | Consulta, reportes e indicadores | Servicio de consulta.                                                | Permitir consultas autorizadas, generar reportes e indicadores y presentar resultados del recaudo.                                    |

### 5.5. Relación con la frontera del alcance

Los siguientes servicios participan en el proceso, pero permanecen fuera del alcance de implementación establecido en V4:

| Servicio externo                                        | Tratamiento                                                                                                                                |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Operación de validadores, lectores y canales de recarga | El proveedor opera los dispositivos y canales; el software recibe e intercambia información.                                               |
| Gestión de flota y kilómetros recorridos                | Operaciones proporciona los datos necesarios para el cálculo y la liquidación.                                                             |
| Planeación de rutas y servicios                         | Planeación suministra las rutas, los servicios y la información operativa correspondiente.                                                 |
| Atención general de PQR                                 | Servicio al Cliente gestiona los casos y consulta la información del recaudo para responder al usuario.                                    |
| Contabilidad, tesorería y giro de la fiducia            | Finanzas y la fiduciaria conservan sus responsabilidades; el software proporciona datos y soportes para la liquidación y el pago.          |
| Certificación de perfiles                               | Las instituciones correspondientes certifican la condición de los beneficiarios; el software consume y administra la información recibida. |

### 5.6. Resultado de la extracción

La T23 identifica diez dominios candidatos para organizar las responsabilidades del software de recaudo del SIT. La extracción se basa en la estructura organizacional, los eventos del proceso E2E y los puntos de corte entre responsabilidades.

Los dominios permiten diferenciar la gestión de reglas y medios de pago, el procesamiento de transacciones, la conciliación financiera, la liquidación y la consulta de resultados. También mantienen explícita la separación entre las funciones implementadas por el software y los servicios externos que participan en el proceso.


### V5 Dominios
![V5 Dominios](vistas/V5_dominios.png)



| Dominio | Clasificación | Argumento |
|---|---|---|
| | | |

### V7 Lenguaje ubicuo
![V7 Lenguaje ubicuo](vistas/V7_lenguaje_ubicuo.png)

| Término | Definición | Dominio/contexto | Ejemplo |
|---|---|---|---|
| | | | |

## 6. Agregados, comandos y eventos
### V6 Agregados, comandos y eventos
_Un diagrama por dominio._

#### V6a _Dominio…_
![V6a](vistas/V6a_agregados_dominio.png)

| Agregado (raíz) | Entidades / objetos de valor | Invariantes | Comandos | Eventos |
|---|---|---|---|---|
| | | | | |

## 7. Mapa de contextos e interoperabilidad
### V8 Mapa de contextos
![V8 Mapa de contextos](vistas/V8_mapa_contextos.png)

| Contexto A | Contexto B | Patrón | Justificación |
|---|---|---|---|
| | | | |

### V9 Interoperabilidad y anticorrupción
![V9 Interoperabilidad y anticorrupción](vistas/V9_interoperabilidad_acl.png)

**Análisis.** La vista tiene los 14 externos de la tabla de servicios externos, uno por fila, con la dirección de cada intercambio escrita en el flujo ("Entra" y "Sale" se miran desde la aplicación). Ocho tienen una capa anticorrupción (los componentes cuyo nombre empieza por ACL): la plataforma del proveedor, el sistema de PQR, el sistema financiero, la fiduciaria, el adquirente y las redes de pago, los canales de recarga, las instituciones que certifican perfiles y el sistema de flota de Operaciones. En todos esos casos el modelo del otro lado es ajeno o no lo controlamos (formatos de Excel distintos, plataforma del proveedor, códigos del adquirente), y no queremos que contamine el lenguaje de la aplicación; la ACL traduce en los dos sentidos. Con los otros seis la relación es directa: Planeación y la autoridad de transporte son conformistas (adoptamos su catálogo de rutas y sus actos de tarifa tal como vienen), y a Hacienda, los operadores, los entes de control y la propia autoridad el software les entrega lo suyo por una sola interfaz de reportes y liquidación, que es el lenguaje publicado del lado nuestro. Comunicaciones solo recibe avisos.

**Decisiones.** La integración más crítica, según la experta, es la de los validadores con la plataforma central, por eso es la que tiene el flujo en ambos sentidos con más detalle (transacciones hacia arriba, tarifario y listas hacia abajo). La vista tiene que coincidir con el mapa de contextos (V8) cuando se haga: un externo con ACL aquí debe aparecer con ese patrón allá.

## 8. Bounded Context Canvas
### V11 Bounded Context Canvas
![V11 Bounded Context Canvas](vistas/V11_bounded_context_canvas.png)

**Cómo lo resolvimos en ArchiMate (componente investigativo):** _…_

## 9. Decisiones y supuestos
### V10 Trazabilidad vertical
![V10 Trazabilidad vertical](vistas/V10_trazabilidad.png)

**Decisiones de diseño:** _…_
**Supuestos:** _…_

## 10. Tabla de aportes
| Integrante | Aportes (tareas del backlog) | Commits |
|---|---|---|
| | | |
