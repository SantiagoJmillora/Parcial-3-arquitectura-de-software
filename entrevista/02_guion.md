# Guion de la entrevista

> Tareas T05, T06 y T07 del backlog. Tipos de pregunta: **(A)** abierta · **(P)** profundización · **(V)** validación.
> Durante la entrevista se agregan **repreguntas** según las respuestas; en la conversación exportada quedan marcadas como `R`.
> Por regla del enunciado, **no** se le pide al experto que proponga el mapa de capacidades, los dominios, los agregados, el mapa de contextos ni las vistas.

## Parte A (T05)

### 1. Contexto de la organización
- 1.1 (A) ¿Cómo está organizado el ente gestor del SIT y cuál es el papel del área de Recaudo y Tarifas?
- 1.2 (A) ¿Quiénes participan en el sistema: ente gestor, operadores de flota, operador del metro, proveedor de recaudo, autoridad de transporte…? ¿Qué hace cada uno?
- 1.3 (P) ¿Cómo es la relación contractual con los operadores? ¿Cómo se les remunera (por pasajero, por kilómetro, mixto)?
- 1.4 (P) ¿Cuántos pasajeros y validaciones diarias maneja el sistema por modo, aproximadamente?
- 1.5 (V) Entonces, ¿el recaudo es un proceso del ente gestor y los operadores solo reciben la distribución, es así?

### 2. Proceso E2E de recaudo
- 2.1 (A) Descríbanos el recaudo de punta a punta: desde que un usuario consigue su medio de pago hasta que el dinero llega a cada operador.
- 2.2 (P) ¿Qué pasa exactamente en el momento en que un pasajero valida en un torniquete o en un bus? ¿Qué información queda registrada?
- 2.3 (P) ¿Cómo y cuándo llegan las transacciones de los validadores al sistema central? ¿En línea, por lotes, al final del día?
- 2.4 (P) ¿Cómo se emite una tarjeta VAMOS? ¿Dónde se compra, cuánto cuesta y en qué se diferencia una personalizada de una al portador?
- 2.5 (P) ¿Cómo se recarga una tarjeta y por qué canales (taquillas, puntos externos, app, web)?
- 2.6 (P) ¿Cómo se paga con débito o crédito? ¿Cuándo se cobra realmente al banco del usuario?
- 2.7 (P) ¿Cómo se hace la consolidación del recaudo por modo, ruta y operador? ¿Con qué periodicidad?
- 2.8 (P) ¿Cómo se distribuyen los ingresos entre los operadores y cómo se concilia?
- 2.9 (V) Si resumo el proceso como: adquirir medio de pago → cargar saldo → validar viaje → aplicar tarifa → consolidar → distribuir y conciliar, ¿falta o sobra algún paso?

### 3. Actores
- 3.1 (A) ¿Qué tipos de usuarios usan el sistema y en qué se diferencian (residentes, visitantes, estudiantes, adultos mayores, personas con movilidad reducida)?
- 3.2 (A) ¿Qué personas o áreas internas intervienen en el recaudo y qué hace cada una?
- 3.3 (P) ¿Quién es el dueño de una tarjeta VAMOS: el pasajero, el titular o el ente gestor?
- 3.4 (V) ¿El visitante que paga con débito o crédito tiene alguna cuenta o registro en el sistema, o es anónimo?

### 4. Reglas de negocio
- 4.1 (A) ¿Cómo se define la tarifa de un viaje? ¿Quién la fija y cada cuánto cambia?
- 4.2 (P) ¿Qué es un transbordo para ustedes? ¿Cuánto tiempo hay, entre qué modos y cuántas veces se puede hacer?
- 4.3 (P) ¿Cuánto se cobra en un transbordo? ¿Cambia según el modo o según el perfil?
- 4.4 (P) ¿Cuáles son las condiciones de cada tarifa especial y qué documentos se exigen?
- 4.5 (P) ¿Cada cuánto se revalida un perfil? ¿Qué pasa cuando vence?
- 4.6 (P) ¿Hay límites de uso para las tarifas especiales (viajes por día o por mes)?
- 4.7 (P) ¿Existe saldo negativo o viaje a crédito con la tarjeta VAMOS? ¿Cuál es el saldo máximo?
- 4.8 (P) ¿Las tarjetas débito y crédito tienen tarifa plena siempre? ¿Aplican transbordos?
- 4.9 (V) Para confirmar: ¿una validación siempre descuenta una tarifa, salvo que caiga dentro de un transbordo válido?

### 5. Excepciones
- 5.1 (A) ¿Cuáles son los problemas más frecuentes en el recaudo?
- 5.2 (P) ¿Qué pasa si la tarjeta no tiene saldo suficiente al validar?
- 5.3 (P) ¿Cómo funciona el bloqueo por pérdida? ¿Qué pasa con el saldo? ¿Cuánto tarda en aplicarse en los validadores?
- 5.4 (P) ¿Qué pasa si un validador queda sin conexión? ¿Se aceptan viajes y cómo se cobran después?
- 5.5 (P) ¿Qué pasa si se rechaza el pago con débito o crédito después de que el pasajero ya pasó?
- 5.6 (P) ¿Cómo se manejan los dobles cobros, las devoluciones y los reclamos por saldo?
- 5.7 (P) ¿Qué fraudes o usos indebidos se han visto (perfiles prestados, tarjetas clonadas)?
- 5.8 (V) ¿Esas excepciones las resuelve Recaudo o se trasladan a otra área?

## Parte B (T06)

### 6. Indicadores
- 6.1 (A) ¿Con qué indicadores mide la gerencia que el recaudo funciona bien?
- 6.2 (P) ¿Qué metas tienen hoy en esos indicadores (evasión, tiempo de validación, cuadre de conciliación, PQR)?
- 6.3 (V) ¿Cuál de esos indicadores es el más crítico hoy?

### 7. Normatividad
- 7.1 (A) ¿Qué normas regulan el recaudo, las tarifas y los subsidios?
- 7.2 (P) ¿Qué exigencias hay sobre datos personales de los usuarios y sobre pagos con tarjeta (PCI, por ejemplo)?
- 7.3 (P) ¿Qué reportes hay que entregar obligatoriamente y a quién?
- 7.4 (V) ¿Los subsidios a perfiles especiales los financia el sistema o una entidad externa?

### 8. Sistemas actuales
- 8.1 (A) ¿Qué sistemas usan hoy para el recaudo y qué problemas tienen?
- 8.2 (P) ¿Qué funciones se hacen hoy manualmente o en hojas de cálculo?
- 8.3 (V) ¿Qué es lo que más esperan resolver con el nuevo software?

### 9. Interoperabilidad (bloque obligatorio)
> Para cada externo: **qué información, en qué dirección, con qué frecuencia y qué pasa si falla**.

**9.1 Validadores y dispositivos (fuera del alcance, fuente de transacciones)**
- 9.1.1 (A) ¿Qué datos envía un validador por cada transacción y qué datos necesita recibir (listas de bloqueo, tarifas, perfiles)?
- 9.1.2 (P) ¿Con qué frecuencia se actualizan las listas que reciben los validadores?

**9.2 Servicio al cliente (PQR y devoluciones)**
- 9.2.1 (A) ¿Qué información necesita Servicio al Cliente de Recaudo, y qué le devuelve?
- 9.2.2 (P) ¿Cómo se aprueba y se ejecuta una devolución de saldo o de un cobro?

**9.3 Financiero**
- 9.3.1 (A) ¿Qué le entrega Recaudo a Finanzas y con qué periodicidad?
- 9.3.2 (P) ¿Cómo se registra contablemente un recaudo, una recarga y un ingreso? ¿Cuándo se reconoce el ingreso?

**9.4 Planeación de rutas y de la operación**
- 9.4.1 (A) ¿Qué información de recaudo usa Planeación y qué le envía Planeación a Recaudo (rutas, paradas, tablas de operadores)?
- 9.4.2 (P) Cuando se crea o se cambia una ruta, ¿cómo se entera el recaudo?

**9.5 Redes de pago y entidades financieras**
- 9.5.1 (A) ¿Con qué actores financieros interactúan (adquirente, franquicias, bancos, pasarela de recargas, fiduciaria)?
- 9.5.2 (P) ¿Cómo se autorizan y se liquidan los pagos con tarjeta débito o crédito y cuándo llega el dinero?
- 9.5.3 (P) ¿Dónde se custodia el dinero del recaudo y cómo se gira a los operadores?

**9.6 Entidades que certifican perfiles**
- 9.6.1 (A) ¿Cómo se comprueba que alguien es estudiante, adulto mayor o persona con movilidad reducida? ¿Quién lo certifica?
- 9.6.2 (P) ¿Ese intercambio se hace hoy de forma digital o con documentos físicos?

**9.7 Autoridad de transporte**
- 9.7.1 (A) ¿Qué le reporta Recaudo a la autoridad de transporte y qué recibe de ella?
- 9.7.2 (P) ¿Cómo se aplica un cambio de tarifa decretado?

**9.8 Otros**
- 9.8.1 (A) ¿Con qué otras áreas, sistemas o entidades intercambia información el recaudo que no hayamos mencionado?
- 9.8.2 (V) De todas estas integraciones, ¿cuál es la más crítica para la operación diaria?

## Parte C (T07)

### 10. Motivación
- 10.1 (A) **Interesados:** ¿quiénes tienen interés en que este software exista y qué espera cada uno?
- 10.2 (A) **Impulsores:** ¿qué está empujando a la organización a hacer este proyecto ahora?
- 10.3 (P) **Evaluaciones:** ¿qué problemas o debilidades concretas tiene la situación actual?
- 10.4 (A) **Metas:** ¿qué quiere lograr la organización con esto?
- 10.5 (P) **Resultados:** ¿qué resultado medible consideraría un éxito y en qué plazo?
- 10.6 (A) **Principios:** ¿qué principios o criterios deben respetarse siempre (por ejemplo, equidad tarifaria o transparencia con los operadores)?
- 10.7 (P) **Requerimientos:** ¿qué debe permitir hacer el software sí o sí?
- 10.8 (P) **Restricciones:** ¿qué limitaciones hay (presupuesto, normas, contratos vigentes, tecnología existente, plazos)?
- 10.9 (V) Si tuviera que escoger una sola meta como la más importante, ¿cuál sería?

### 11. Qué hace la organización (insumo para las capacidades)
- 11.1 (A) Más allá del recaudo, ¿cuáles son todas las grandes funciones que realiza el ente gestor?
- 11.2 (P) ¿Qué funciones son estratégicas, cuáles son la razón de ser del sistema y cuáles son de apoyo?
- 11.3 (V) ¿Cuáles de esas funciones se verían afectadas o mejoradas con el nuevo software de recaudo?
- 11.4 (A) Cierre: ¿hay algo importante del recaudo que no le hayamos preguntado?
