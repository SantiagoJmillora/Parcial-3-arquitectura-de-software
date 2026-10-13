# T13: boceto del mapa de capacidades del ente gestor del SIT

Boceto para pasar a Archi en la **V2 Mapa de capacidades** (T14). Cubre **todo** el ente gestor, no solo el recaudo, como en la diapositiva 35 de 7_SOA.

**Fuente:** entrevista, bloque 1 (1.1, 1.2), bloque 3 (3.2), bloque 9 (9.8) y bloque 11 (11.1 a 11.4). La experta describió las funciones tal como las viven; la organización en capacidades, niveles e impacto es **decisión del equipo** (ella lo dejó explícito al cierre de la entrevista).

## 1. Criterios

- **Una capacidad no es un área.** La capacidad dice *qué* sabe hacer la organización, no *quién* lo hace. Por ejemplo, la personalización de tarjetas la ejecuta Servicio al Cliente, pero con reglas de Recaudo y Tarifas; por eso queda dentro de *Recaudo*.
- **Niveles:**
  - **Nivel 0, categoría:** estratégicas, misionales (razón de ser) y de apoyo. Sigue la clasificación de la experta en 11.2.
  - **Nivel 1:** capacidad de negocio.
  - **Nivel 2:** sub-capacidad.
  - **Nivel 3:** solo en la rama de *Recaudo*, que es donde está la aplicación y donde hace falta más detalle.
- **Impacto** (resaltado en la V2, con leyenda):

| Marca | Impacto | Criterio |
|---|---|---|
| 🔴 | **Directo** | La aplicación de recaudo soporta o automatiza la capacidad (realiza algún REQ de la V1) |
| 🟡 | **Indirecto** | La capacidad mejora porque recibe datos o servicios de la aplicación (11.3), pero la aplicación no la ejecuta |
| ⚪ | **Sin impacto** | Fuera del alcance de la aplicación |

## 2. Mapa

### Nivel 0: capacidades estratégicas

| Código | Nivel 1 | Nivel 2 | Impacto | Justificación |
|---|---|---|---|---|
| E1 | **Planeación del sistema** | | 🟡 | |
| E1.1 | | Diseño de rutas y servicios | ⚪ | La aplicación **consume** las rutas para aplicar transbordos y liquidar, pero no diseña rutas (fuera del alcance) |
| E1.2 | | Estudios de demanda | 🟡 | Recibe datos de validaciones más confiables (11.3) |
| E1.3 | | Planeación de la expansión | ⚪ | Nuevas troncales y obras: no dependen del recaudo |
| E2 | **Política tarifaria** | | 🟡 | La experta la ubica como estratégica (11.2): «Recaudo y Tarifas tiene un pie en cada lado» |
| E2.1 | | Estudios técnicos tarifarios | 🟡 | Usan datos de demanda, recaudo y subsidios de la aplicación |
| E2.2 | | Adopción de actos tarifarios | ⚪ | La decide la Alcaldía con la autoridad de transporte; la aplicación solo configura el resultado (ver M3.2) |
| E3 | **Sostenibilidad financiera** | | 🟡 | |
| E3.1 | | Financiación de subsidios y déficit | 🟡 | El cálculo de subsidios (M3.4.4) soporta el cobro a Hacienda |
| E3.2 | | Planeación presupuestal | ⚪ | |
| E4 | **Relación institucional** | | 🟡 | |
| E4.1 | | Relación con Alcaldía, Concejo, autoridad de transporte y Ministerio | 🟡 | Reportes automatizados (RES08) |
| E4.2 | | Integración metropolitana | 🟡 | La aplicación debe poder intercambiar información con otros municipios (MET07), aunque la integración no está decidida |

### Nivel 0: capacidades misionales (razón de ser: «que la gente se mueva bien y pague justo»)

| Código | Nivel 1 | Nivel 2 | Nivel 3 | Impacto | Justificación |
|---|---|---|---|---|---|
| M1 | **Gestión y control de la operación** | | | 🟡 | |
| M1.1 | | Programación de servicios | | ⚪ | |
| M1.2 | | Control en vía y estaciones | | ⚪ | |
| M1.3 | | Gestión de novedades de flota y equipos | | 🟡 | Recibe alertas de validadores fuera de servicio o sin transmitir (H12) |
| M1.4 | | Medición de la calidad del servicio | | ⚪ | |
| M1.5 | | Control de la evasión | | 🟡 | La aplicación da indicadores por ruta y estación (RES07), pero el control es físico y operativo (H14 descartado) |
| M2 | **Gestión de concesiones y convenios** | | | 🟡 | |
| M2.1 | | Supervisión de operadores de flota y metro | | 🟡 | Liquidación transparente y verificable (PRI03) |
| M2.2 | | Supervisión del proveedor de recaudo | | 🟡 | Ya no depende de los extractos del proveedor (EVA01) |
| M2.3 | | Aplicación de incentivos, descuentos y sanciones | | ⚪ | Las fórmulas son de Finanzas y Jurídica; la aplicación solo entrega los datos de pasajeros |
| M3 | **Recaudo** | | | 🔴 | Capacidad central del proyecto |
| M3.1 | | Gestión de medios de pago | | 🔴 | |
| M3.1.1 | | | Emisión y personalización de tarjetas VAMOS | 🔴 | Alcance del enunciado |
| M3.1.2 | | | Recarga de tarjetas | 🔴 | La aplicación registra y concilia las recargas; la red de puntos la opera el proveedor |
| M3.1.3 | | | Consulta de saldo e historial | 🔴 | Alcance del enunciado y REQ07 |
| M3.1.4 | | | Bloqueo por pérdida, listas y traslado de saldo | 🔴 | Alcance del enunciado y REQ06 |
| M3.1.5 | | | Gestión de pagos con tarjetas bancarias | 🔴 | Débito y crédito: consolidación de viajes, cobro diferido y deuda (H10) |
| M3.1.6 | | | Logística de tarjetas físicas | ⚪ | Inventario y distribución: hoy es del proveedor (11.4) |
| M3.2 | | Gestión de tarifas y perfiles | | 🔴 | |
| M3.2.1 | | | Configuración de reglas tarifarias y de transbordo | 🔴 | REQ02, con vigencias e historial |
| M3.2.2 | | | Validación de perfiles tarifarios | 🔴 | Verificar que el usuario cumple las condiciones con la institución certificadora (enunciado) |
| M3.2.3 | | | Gestión de vigencias y revalidación de perfiles | 🔴 | RES05 y EVA07 (fuga de subsidios) |
| M3.2.4 | | | Gestión de credenciales de servicio | ⚪ | Mencionada en 11.4 como débil, pero no está en el enunciado. **Pendiente de decidir** |
| M3.3 | | Procesamiento de validaciones | | 🔴 | |
| M3.3.1 | | | Recepción de transacciones de validación | 🔴 | Incluye las tardías y las duplicadas (H04, H11) |
| M3.3.2 | | | Aplicación de la tarifa y los transbordos | 🔴 | Alcance del enunciado |
| M3.3.3 | | | Operación de validadores y dispositivos | ⚪ | IoT fuera del alcance: el proveedor la opera |
| M3.4 | | Consolidación, conciliación y liquidación | | 🔴 | |
| M3.4.1 | | | Consolidación del recaudo por modo, ruta y operador | 🔴 | Alcance del enunciado |
| M3.4.2 | | | Conciliación de ventas, recargas y consignaciones | 🔴 | Incluye las comisiones de los canales de recarga (H22 y 11.4) |
| M3.4.3 | | | Liquidación a operadores | 🔴 | REQ03 |
| M3.4.4 | | | Cálculo de subsidios | 🔴 | REQ04 |
| M3.5 | | Control del recaudo | | 🔴 | |
| M3.5.1 | | | Detección de fraude y anomalías | 🔴 | REQ11 |
| M3.5.2 | | | Indicadores y reportes del recaudo | 🔴 | REQ10 |
| M4 | **Atención al usuario** | | | 🟡 | |
| M4.1 | | Gestión de PQR | | 🟡 | El sistema de PQR es de Servicio al Cliente; la aplicación le da el historial de la tarjeta (H15) |
| M4.2 | | Ajustes y devoluciones | | 🔴 | REQ08: la aplicación registra el ajuste de saldo y su aprobación según el monto |
| M4.3 | | Centros de atención | | ⚪ | |
| M4.4 | | Información al usuario (app y web) | | 🟡 | Consumen saldo y recargas de la aplicación |

### Nivel 0: capacidades de apoyo

| Código | Nivel 1 | Nivel 2 | Impacto | Justificación |
|---|---|---|---|---|
| A1 | **Gestión financiera** | | 🟡 | La experta no la clasificó en 11.2. El equipo la deja en apoyo porque ejecuta (tesorería, contabilidad); lo estratégico está en E3 |
| A1.1 | | Administración fiduciaria y tesorería | 🟡 | Recibe instrucciones de pago soportadas por la liquidación |
| A1.2 | | Contabilidad | 🟡 | Registro contable de recaudos e ingresos; el saldo de las tarjetas es una obligación con los usuarios (H03) |
| A1.3 | | Gestión de cartera | 🟡 | Deudas de tarjetas bancarias denegadas |
| A2 | **Gestión jurídica y contractual** | | 🟡 | |
| A2.1 | | Contratación | ⚪ | |
| A2.2 | | Protección de datos personales | 🟡 | La aplicación implementa autorizaciones y consultas (REQ09); la responsabilidad legal sigue en Jurídica |
| A2.3 | | Defensa en disputas contractuales | 🟡 | Evidencia histórica reconstruible (REQ12) |
| A3 | **Gestión de tecnología** | | 🟡 | |
| A3.1 | | Intercambio de información con terceros | 🟡 | La capa anticorrupción de la aplicación cambia cómo se integra con el proveedor y la banca |
| A3.2 | | Seguridad e infraestructura TI | ⚪ | Transversal |
| A4 | **Control interno y relación con entes de control** | | 🟡 | Reportes respaldados y trazables (IMP02) |
| A5 | **Comunicaciones y cultura ciudadana** | | ⚪ | |
| A6 | **Infraestructura física** | | ⚪ | Estaciones, portales, patios y carriles. La experta la pone en apoyo para el día a día (11.2) |
| A7 | **Seguridad** | | ⚪ | Coordinación con la Policía |
| A8 | **Gestión humana, administrativa y de compras** | | ⚪ | |

**Conteo:** 4 + 4 + 8 capacidades de nivel 1; 3 niveles bajo la categoría en la rama de Recaudo. Impacto directo: M3 completo y M4.2.

## 3. Recursos (se asignan a capacidades)

| Recurso | Asignado a | Fuente |
|---|---|---|
| Parque de tarjetas VAMOS | M3.1 | 3.3: el plástico y el chip son del sistema |
| Actos administrativos tarifarios | E2, M3.2 | 4.1 |
| Registro de transacciones del recaudo | M3.3, M3.4, M3.5 | H19: hoy lo tiene el proveedor |
| Patrimonio autónomo (fiducia) | M3.4, A1.1 | 1.2 y 1.5 |
| Contratos de concesión y convenios | M2, M3.4.3 | 1.3 |
| Plataforma central del proveedor de recaudo | M3.3 | 1.2 (recurso externo, vía la capa anticorrupción) |
| Equipo de Recaudo y Tarifas | M3 | 1.1: unas 25 personas |
| Certificaciones de las instituciones | M3.2.2 | 9.6 |

## 4. Cursos de acción (los realizan capacidades; ellos realizan metas de la V1)

| Curso de acción | Lo realizan | Realiza | Fuente |
|---|---|---|---|
| CA1 Disponer de una copia propia y completa de las transacciones del recaudo | M3.3, A3.1 | MET01 Control de la información | EVA01, H19 |
| CA2 Automatizar la consolidación, conciliación y liquidación con trazabilidad | M3.4, M3.5.2 | MET02 Liquidación y conciliación confiables | EVA02, H22 |
| CA3 Integrar el recaudo con atención al usuario, finanzas, operación y planeación | M4.1, M4.2, A1, M1.3 | MET03 Mejor atención al usuario, MET07 Preparación para la integración metropolitana | EVA03, EVA05 |
| CA4 Validar perfiles contra las instituciones y monitorear anomalías | M3.2.2, M3.2.3, M3.5.1 | MET04 Reducción de pérdidas de recursos | EVA06, EVA07, EVA08 |
| CA5 Incorporar la protección de datos y los reportes regulatorios desde el diseño | A2.2, M3.5.2, A4 | MET05 Cumplimiento normativo | H20, EVA11 |
| CA6 Interoperar con la plataforma del proveedor en lugar de reemplazarla | A3.1, M2.2 | MET06 Preparación para la transición contractual | H18 (descartado: no se reemplaza obligatoriamente) |

## 5. Relaciones para la V2 (todas válidas en Archi 5.10)

| Desde | Relación | Hacia |
|---|---|---|
| Capacidad de nivel 1 | composición | Capacidad de nivel 2 (y nivel 2 → nivel 3) |
| Recurso | asignación | Capacidad |
| Capacidad | realización | Curso de acción |
| Curso de acción | realización | Meta (reutilizar MET01–MET07 de la V1, **no crear nuevas**) |

## 6. Propuesta de disposición en Archi

- Tres grandes **grupos visuales** horizontales: *Estratégicas* (arriba), *Misionales* (centro, la más grande) y *Apoyo* (abajo).
- Las capacidades de nivel 2 y 3 van **anidadas** dentro de la de nivel 1. En Archi el anidamiento debe respaldarse con la relación de composición, y al anidar Archi lo pregunta.
- **Resaltado:** 🔴 con relleno de color fuerte (por ejemplo naranja) y borde grueso, 🟡 con relleno claro, ⚪ con el color por defecto de estrategia. La leyenda va en una nota dentro de la vista.
- Recursos a la izquierda, cursos de acción y metas a la derecha, para que la vista no se cargue sobre el mapa.

## 7. Preguntas abiertas para el equipo

1. ¿Las **credenciales de servicio** (M3.2.4) entran al alcance? Hoy quedan ⚪ porque el enunciado no las menciona.
2. ¿Mantenemos la **gestión financiera** en apoyo (decisión del equipo) o la subimos a misional?
3. Si la V2 queda muy cargada, se puede hacer una **V2b** solo con recursos y cursos de acción, y dejar en la V2 el mapa con las capacidades impactadas.
