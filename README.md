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

#### Tabla de inclusión y exclusión
| Capa | Servicio | ¿Se implementa? | Justificación |
|---|---|---|---|
| | | | |

#### Contratos de servicio (contract-first)
| Servicio | Entradas | Salidas | Errores | Requisitos no funcionales |
|---|---|---|---|---|
| | | | | |

#### Servicios externos (capa anticorrupción)
| Externo | Tipo | Información intercambiada | Dirección | Sincronía/frecuencia |
|---|---|---|---|---|
| | | | | |

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
