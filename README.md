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
_Solicitud del usuario, alcance y lo que queda fuera. Resumen de la entrevista y enlaces a [entrevista/](entrevista/): instrucción de rol, guion, conversación y análisis de hallazgos._

## 2. Motivación
### V1 Motivación
![V1 Motivación](vistas/V1_motivacion.png)

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

**Análisis:** _…_  **Capacidades impactadas:** _…_

### V3 Cadena de valor y proceso E2E
![V3 Cadena de valor y proceso E2E](vistas/V3_cadena_valor_e2e.png)

**Análisis:** _…_

## 4. Descomposición de servicios
### V4 Descomposición de servicios
![V4 Descomposición de servicios](vistas/V4_descomposicion_servicios.png)

**Análisis:** _…_

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
| Servicio | Entradas | Salidas | Errores | Requisitos no funcionales |
|---|---|---|---|---|
| | | | | |

#### Servicios externos (capa anticorrupción)

Salieron de las respuestas del bloque 9 de la entrevista. "Entra" y "sale" se miran desde el software. Con esta tabla se arma V9, que debe coincidir con ella.

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

**Análisis:** _…_

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
