# Conversación exportada

> Tarea T09 del backlog. Entrevista al experto del negocio: Tema 4, recaudo del SIT.

## Método
- **Fecha:** 2026-10-10.
- **IA experta:** Claude (Anthropic), en una sesión **aislada**. No recibió el enunciado, la rúbrica, el backlog ni ningún otro contexto del proyecto: su único contexto fue la [instrucción de rol](01_instruccion_rol.md), a la que se le antepuso la nota técnica «no uses herramientas; responde solo con texto».
- **Entrevistador:** el equipo, siguiendo el [guion](02_guion.md) bloque por bloque.
- Las preguntas conservan la numeración del guion. Las **repreguntas** que surgieron de las respuestas se marcan con `R` (por ejemplo, `R1.a`).
- Las respuestas se transcriben **textualmente**, sin editar.

---

**Entrevistador:** _(instrucción de rol, ver [01_instruccion_rol.md](01_instruccion_rol.md))_

**Experta (Andrea Montoya):**
Buenos días. Soy Andrea Montoya, directora de Recaudo y Tarifas del Ente Gestor del SIT. Llevo unos 15 años en transporte masivo: empecé en conciliación de recaudo, luego pasé por planeación tarifaria y hoy dirijo el área, así que conozco bastante bien cómo se cobra, cómo se integra la tarifa entre buses y metro y cómo se reparte la plata entre los operadores. Cuando quiera, empezamos con su primera pregunta.

---

## Bloque 1. Contexto de la organización

**Entrevistador:**
1.1 ¿Cómo está organizado el ente gestor del SIT y cuál es el papel del área de Recaudo y Tarifas?
1.2 ¿Quiénes participan en el sistema: ente gestor, operadores de flota, operador del metro, proveedor de recaudo, autoridad de transporte…? ¿Qué hace cada uno?
1.3 ¿Cómo es la relación contractual con los operadores? ¿Cómo se les remunera (por pasajero, por kilómetro, mixto)?
1.4 ¿Cuántos pasajeros y validaciones diarias maneja el sistema por modo, aproximadamente?
1.5 Entonces, ¿el recaudo es un proceso del ente gestor y los operadores solo reciben la distribución, es así?

**Experta:**
Con gusto. Voy pregunta por pregunta.

**1.1 Organización del ente gestor y papel de Recaudo y Tarifas**
El ente gestor es una entidad pública, y su cabeza es la Gerencia General. Debajo hay varias direcciones: Operaciones, que controla la flota en vía, la regularidad y las frecuencias; Planeación, que diseña rutas y servicios; Finanzas; Servicio al Cliente; Tecnología; Jurídica y Contratación; y mi área, Recaudo y Tarifas. Hay otras de apoyo, como la administrativa y la de comunicaciones, pero esas son las que más tocan mi trabajo.
Mi área hace cuatro cosas:
- Proponemos la estructura tarifaria: tarifa plena, tarifas especiales y reglas de transbordo. El valor final no lo decido yo; eso se aprueba por acto administrativo con la autoridad de transporte y la Alcaldía.
- Fijamos las reglas de recaudo: medios de pago, recargas, perfiles y bloqueos.
- Supervisamos al proveedor de recaudo.
- Consolidamos, conciliamos y liquidamos el recaudo para que se pueda distribuir.
Somos unas 25 personas, más o menos. Una parte está en conciliación, otra en tarifas y perfiles, y otra en supervisión del contrato de recaudo.

**1.2 Actores del sistema**
- **Ente gestor (nosotros):** planeamos, regulamos y controlamos el sistema. No operamos buses ni trenes.
- **Operadores de flota (privados):** hoy son cuatro concesionarios, aproximadamente. Ponen los buses articulados y los alimentadores, los conductores y el mantenimiento, y prestan el servicio según la programación que les damos.
- **Operador del metro:** es una empresa pública. Opera los trenes y las estaciones de metro y tiene su propio convenio con nosotros, distinto al de los concesionarios.
- **Proveedor de recaudo:** es un tercero. Suministra y mantiene los validadores, los equipos de recarga y la plataforma central de transacciones. También maneja la red de puntos de recarga, propios y aliados. Les aclaro que de la tecnología interna yo no sé; sé qué transacciones nos llegan.
- **Fiducia:** es la entidad financiera que administra el patrimonio autónomo adonde llega la plata del recaudo y desde donde se paga a cada uno.
- **Redes de pago y bancos:** por ellos pasan los pagos con tarjeta débito y crédito sin contacto y algunas recargas digitales.
- **Autoridad de transporte de la ciudad:** expide los actos de tarifa, vigila y es la autoridad frente al usuario y a los operadores en temas regulatorios.
- **Instituciones que certifican perfiles:** colegios, universidades y entidades que certifican discapacidad. Ellas acreditan quién tiene derecho a una tarifa especial.

**1.3 Relación contractual y remuneración**
Con los operadores de flota hay contratos de concesión de largo plazo, del orden de 12 a 20 años según la fase en que entró cada uno. La remuneración es mixta. Se paga principalmente por kilómetro programado y efectivamente recorrido, y hay un componente por pasajero pagado. Además hay descuentos o incentivos por indicadores de calidad: cumplimiento de la programación, estado de la flota y quejas.
Las ponderaciones exactas y las fórmulas las tiene Finanzas con Jurídica, y además cambian según el contrato. No me atrevería a darles porcentajes.
El metro tiene un convenio interadministrativo con reglas propias de reconocimiento.
El proveedor de recaudo tiene su propio contrato y cobra un porcentaje del recaudo más algunos cargos fijos.
Ojo: el dinero no va directo a los operadores. Todo pasa por la fiducia, que paga según una prelación definida en los contratos.

**1.4 Volumen aproximado**
Son cifras aproximadas, de un día hábil típico:
- **Validaciones totales:** unas 550.000 al día.
- **Metro:** cerca de 220.000.
- **Articulados (troncales):** cerca de 200.000.
- **Alimentadores:** cerca de 130.000.
Validación y pasajero no son lo mismo. Mucha gente hace transbordo, entonces un mismo viaje genera dos o tres validaciones. Pasajeros pagos, es decir viajes que generan cobro, serían unos 380.000 a 400.000 al día. Los sábados baja más o menos un 30 % y los domingos casi a la mitad.
Hoy alrededor del 85 % se paga con VAMOS. Los pagos con débito y crédito sin contacto siguen siendo pocos, menos del 5 %, aunque están creciendo. El resto son otros medios que estamos desmontando.

**1.5 ¿El recaudo es del ente gestor y los operadores solo reciben la distribución?**
No exactamente, y quiero corregir eso.
- Nosotros tenemos la titularidad y el control del recaudo: definimos reglas, supervisamos y conciliamos. Pero no recibimos ni manejamos la plata. El dinero de recargas y pagos va a la fiducia, no a una cuenta del ente gestor.
- La operación del recaudo la hace el proveedor de recaudo: validadores, recargas y plataforma.
- Los operadores tampoco son receptores pasivos. Tienen obligaciones que afectan el recaudo, como cuidar los validadores a bordo, reportar fallas y apoyar el control de evasión. También revisan y pueden objetar la liquidación que les presentamos. Ahí hay una conciliación de ida y vuelta con ellos todos los meses.
- Con el metro la cosa es parecida, pero en sus estaciones algunos equipos y procedimientos tienen particularidades propias de su convenio.
En resumen, el recaudo es un proceso compartido. Nosotros lo gobernamos, el proveedor lo opera, la fiducia administra el dinero y los operadores participan en el control y la conciliación.

Quedo atenta al siguiente bloque.

---

## Bloque 2. Proceso E2E de recaudo (con repreguntas del bloque 1)

**Entrevistador:**
Muy claro, gracias. Antes de seguir, dos repreguntas sobre lo que nos dijo:
R1.a Mencionó "otros medios que estamos desmontando". ¿Cuáles son y por qué se desmontan?
R1.b Si la plata va a la fiducia y no al ente gestor, ¿quién le da la orden a la fiducia de cuánto pagarle a cada operador?

Y ahora el bloque 2, proceso E2E de recaudo:
2.1 Descríbanos el recaudo de punta a punta: desde que un usuario consigue su medio de pago hasta que el dinero llega a cada operador.
2.2 ¿Qué pasa exactamente en el momento en que un pasajero valida en un torniquete o en un bus? ¿Qué información queda registrada?
2.3 ¿Cómo y cuándo llegan las transacciones de los validadores al sistema central? ¿En línea, por lotes, al final del día?
2.4 ¿Cómo se emite una tarjeta VAMOS? ¿Dónde se compra, cuánto cuesta y en qué se diferencia una personalizada de una al portador?
2.5 ¿Cómo se recarga una tarjeta y por qué canales (taquillas, puntos externos, app, web)?
2.6 ¿Cómo se paga con débito o crédito? ¿Cuándo se cobra realmente al banco del usuario?
2.7 ¿Cómo se hace la consolidación del recaudo por modo, ruta y operador? ¿Con qué periodicidad?
2.8 ¿Cómo se distribuyen los ingresos entre los operadores y cómo se concilia?
2.9 Si resumo el proceso como: adquirir medio de pago → cargar saldo → validar viaje → aplicar tarifa → consolidar → distribuir y conciliar, ¿falta o sobra algún paso?

**Experta:**
Listo, primero las dos repreguntas y luego el bloque 2.

**R1.a Medios que estamos desmontando**
Son tres, aproximadamente:
1. **La tarjeta de primera generación.** Es la tarjeta sin contacto con la que arrancó el sistema hace unos 12 años. Su tecnología ya no es segura: hemos tenido casos de tarjetas clonadas o con saldo alterado. Además, los fabricantes ya no la producen y no soporta bien los perfiles de tarifa especial. Desde hace un tiempo la cambiamos gratis por VAMOS y respetamos el saldo, y la idea es dejar de aceptarla en una fecha que todavía no está decidida. Quedan unas decenas de miles circulando.
2. **El tiquete de un viaje en papel con código**, que se vende en taquillas del metro. Es caro de producir, se presta para reventa y no permite transbordo integrado.
3. **El pago en efectivo a bordo** en algunas rutas alimentadoras que se integraron hace poco y donde todavía no hay suficientes puntos de recarga cerca. El efectivo es un problema de seguridad para los conductores, abre espacio a la evasión y el pasajero no recibe el beneficio del transbordo.
La razón de fondo es la misma en los tres casos: queremos que todo pase por medios electrónicos que se puedan controlar, integrar tarifariamente y conciliar.

**R1.b ¿Quién le da la orden a la fiducia?**
Nosotros, pero con varios controles:
1. Mi área prepara la **liquidación**. Ahí calculamos cuánto le corresponde a cada actor con base en el recaudo consolidado, los kilómetros que certifica Operaciones, los pasajeros y los indicadores de calidad.
2. **Finanzas** revisa la liquidación, y la **Gerencia General**, como ordenadora, firma la instrucción de giro.
3. La **fiducia** no paga a ciegas. Verifica que la instrucción cumpla el contrato de fiducia, sobre todo el orden de prelación de pagos, y que haya recursos.
4. Existe un **comité fiduciario**, con participación de los concesionarios, donde se revisan los informes y se resuelven diferencias.
En cuanto a la periodicidad, hoy se hacen giros semanales con una liquidación preliminar y un cierre mensual definitivo con ajustes. Eso depende de lo pactado en cada contrato.

**2.1 El recaudo de punta a punta**
Se lo cuento como lo vive la plata:
1. El usuario **consigue su medio de pago**: compra una VAMOS o usa su tarjeta bancaria sin contacto.
2. **Carga saldo** en la VAMOS por algún canal. En ese momento entra el dinero: el canal lo recibe y debe consignarlo en las cuentas de la fiducia en el plazo pactado, que normalmente es de uno o dos días hábiles. Ojo con esto: la plata entra cuando el usuario recarga, no cuando viaja. El saldo que la gente tiene en sus tarjetas es plata recibida por un servicio todavía no prestado.
3. El usuario **valida** en el metro, el articulado o el alimentador. El validador aplica la tarifa en ese mismo momento y descuenta el saldo de la tarjeta.
4. Las transacciones **viajan al sistema central** del proveedor de recaudo.
5. Se **consolida**: ventas por canal de un lado, usos por modo, ruta y operador del otro.
6. Se **concilia**: lo vendido contra lo consignado en la fiducia, y lo usado contra lo reportado.
7. Mi área hace la **liquidación** y se da la instrucción a la fiducia.
8. La fiducia **gira**, en el orden de prelación: primero los costos del sistema, como el proveedor de recaudo y la comisión fiduciaria, y luego operadores de flota y metro.
Con débito y crédito el flujo cambia, se lo explico en la 2.6.

**2.2 ¿Qué pasa al validar?**
Con VAMOS, en menos de un segundo, el validador:
- lee la tarjeta y revisa que no esté en la **lista de bloqueo** (perdidas, robadas, fraudulentas);
- revisa el **perfil**, es decir si tiene tarifa especial y si está vigente; por ejemplo, el perfil de estudiante vence al terminar el periodo académico;
- revisa si esta validación es un **transbordo** dentro de la ventana permitida;
- revisa si hay **recargas pendientes** hechas por app o web y, si las hay, las carga en ese momento;
- calcula la tarifa, verifica que el saldo alcance y lo descuenta de la tarjeta;
- abre el torniquete, o en el bus da la luz verde y el sonido.
Queda registrado, que yo sepa:
- número de la tarjeta y tipo de medio;
- perfil tarifario;
- fecha y hora;
- validador, y con eso la estación o el bus;
- ruta y operador, en el caso de los buses;
- tipo de transacción: pago pleno, transbordo, transbordo gratuito o rechazo con su motivo;
- valor cobrado, saldo antes y después, y un consecutivo de la tarjeta.
Los rechazos también quedan, y nos sirven mucho para ver problemas.
Un detalle importante es que el saldo de VAMOS vive en la tarjeta. Por eso el validador puede cobrar aunque en ese momento no tenga conexión.

**2.3 ¿Cómo llegan las transacciones al central?**
Depende del modo:
- **Metro y estaciones de articulados:** casi en línea, porque hay red fija. Llegan en minutos.
- **Buses:** transmiten por datos móviles cuando hay cobertura, más o menos cada pocos minutos. Si no hay señal, el validador las guarda y las descarga cuando recupera conexión o, a más tardar, cuando el bus llega al patio en la noche.
Por contrato, el proveedor tiene que entregar el 100 % de las transacciones de un día en máximo 48 horas, aproximadamente. Lo que llega tarde, por ejemplo de un validador que se dañó y había que recuperar, entra como transacción extemporánea y ajusta el cierre. Esas son una fuente frecuente de diferencias en la conciliación.
Las listas de bloqueo y de recargas pendientes viajan en sentido contrario, del central a los validadores, varias veces al día. Por eso un bloqueo no es inmediato en todos los buses.

**2.4 Emisión de la tarjeta VAMOS**
- **Dónde:** taquillas del metro y de portales, centros de atención al usuario y algunos puntos externos autorizados. Estos últimos solo venden la tarjeta al portador.
- **Costo:** unos $7.000 pesos, aproximadamente. Ese valor es el costo de la tarjeta, no es saldo y no se devuelve.
- **Al portador:** es anónima. Se compra y se usa de una vez. Si se pierde, se pierde el saldo, porque no hay manera de demostrar que es suya.
- **Personalizada:** queda asociada al nombre y la cédula de la persona. Se pide con documento en un centro de atención y el usuario debe autorizar el tratamiento de sus datos personales, por la ley de habeas data. Permite bloquearla si se pierde y pasar el saldo a una tarjeta nueva. Además, es requisito para cualquier tarifa especial: el perfil de estudiante, adulto mayor o movilidad reducida se carga sobre una tarjeta personalizada, después de que la institución correspondiente lo certifica. La reposición por pérdida tiene un costo similar al de la tarjeta nueva.
Hoy más o menos el 45 % de las VAMOS activas son personalizadas. Queremos que sean más.

**2.5 Recargas**
- **Taquillas** en estaciones de metro y portales: efectivo, y en algunas datáfono.
- **Máquinas de autoservicio** en estaciones grandes.
- **Red de puntos externos:** tiendas, droguerías y corresponsales. Son más o menos 1.500 puntos y es el canal más importante en barrios y zonas de alimentadores.
- **App y web:** se paga con PSE o tarjeta. Como el saldo vive en la tarjeta, la recarga queda **pendiente** y se aplica la próxima vez que el usuario valide, o cuando acerque la tarjeta a un equipo de consulta. Eso genera muchas quejas del tipo "pagué y no me aparece el saldo".
Hay un mínimo de recarga, alrededor de $2.000, y un tope de saldo en tarjeta, alrededor de $200.000. Los valores exactos están en la resolución vigente.
Cada canal tiene su propia obligación de consignar y su propia comisión, y eso es parte de lo que conciliamos.

**2.6 Pago con débito o crédito sin contacto**
El usuario pasa su tarjeta bancaria por el validador como si fuera una VAMOS. En ese momento no se le cobra al banco en línea, porque no podemos esperar una autorización bancaria en cada torniquete. El validador revisa que la tarjeta no esté en una **lista de denegación** y lo deja pasar.
Al cierre del día, el sistema agrupa todos los toques de esa tarjeta, aplica las reglas de transbordo y hace **un solo cobro** por el total a través del adquirente, normalmente en la madrugada del día siguiente.
Si el cobro es rechazado, por ejemplo por falta de fondos, esa tarjeta entra a la lista de denegación hasta que la deuda se pague. Ese viaje ya se prestó, entonces asumimos un riesgo, pequeño pero real.
Con tarjeta bancaria solo se paga **tarifa plena**: las tarifas especiales necesitan una VAMOS personalizada. Y ese dinero también llega a la fiducia, descontadas las comisiones de la red y del adquirente.

**2.7 Consolidación**
Hay dos consolidaciones distintas, y conviene no mezclarlas:
- **Ventas:** cuánta plata entró, por canal, punto y medio de pago. Esto se cruza con lo que efectivamente se consignó en la fiducia.
- **Usos:** cuántas validaciones y cuánto valor se consumió, por modo, ruta, operador, estación, franja horaria y tipo de tarifa.
El proveedor entrega reportes diarios y mi equipo los revisa todos los días buscando cosas raras, como un bus sin transacciones o un punto de venta que no consignó. Semanalmente se consolida para la liquidación preliminar. El cierre mensual es el definitivo y toma unos 8 a 10 días hábiles después de terminado el mes.
Para buses también cruzamos con Operaciones los kilómetros recorridos y la programación, porque eso pesa en el pago.

**2.8 Distribución y conciliación**
La distribución sigue el orden de prelación del contrato de fiducia, más o menos así:
1. Costos del sistema: remuneración del proveedor de recaudo y comisión de la fiducia.
2. Aportes a los fondos definidos, por ejemplo uno de contingencia o estabilización, y el porcentaje para la gestión del ente, si aplica en el contrato.
3. Pago a operadores de flota según su fórmula de kilómetros, pasajeros e indicadores.
4. Pago al metro según su convenio.
Si el recaudo no alcanza para cubrir lo que dicen las fórmulas, porque la tarifa al usuario es menor que el costo real, la diferencia se cubre con recursos de la Alcaldía o de los fondos. Eso lo maneja Finanzas.
La conciliación se hace en varias capas:
- **Ventas contra consignaciones:** ¿cada canal consignó lo que vendió?
- **Transacciones del proveedor contra nuestros registros:** ¿cuadran los totales y los consecutivos?
- **Usos contra kilómetros y operación:** ¿lo que liquidamos coincide con lo que se operó?
- **Con cada operador:** les enviamos la liquidación, ellos tienen unos días para objetar y las diferencias se resuelven en mesas técnicas o, si no hay acuerdo, en el comité fiduciario.
También se concilian las devoluciones y los saldos trasladados por bloqueo que salen de Servicio al Cliente.

**2.9 Sobre su resumen del proceso**
Va bien, pero le haría ajustes:
- **Sobra o está mal ubicado "aplicar tarifa" como paso aparte.** La tarifa se aplica en el mismo instante de la validación. Solo con débito y crédito hay un cálculo posterior, en el cobro diferido.
- **Falta la transmisión o recolección de transacciones** de los validadores al central, que con los buses no es inmediata.
- **Falta el cobro diferido al banco** para débito y crédito.
- **Falta el recaudo propiamente dicho:** la consignación de los canales a la fiducia, que es distinta de la recarga.
- **Falta la liquidación y la instrucción de pago**, antes de distribuir. Es un paso con aprobaciones propias.
- **"Cargar saldo" no aplica a todos:** con tarjeta bancaria no hay saldo.
- Yo agregaría un carril paralelo de **excepciones**: bloqueos, devoluciones, transacciones extemporáneas y reclamos. Ahí se nos va mucho del trabajo diario.

Quedo atenta.

---

## Bloques 3 y 4. Actores y reglas de negocio (con repreguntas del bloque 2)

**Entrevistador:**
Excelente, nos ayuda mucho la corrección del resumen. Dos repreguntas y seguimos con los bloques 3 (actores) y 4 (reglas de negocio):
R2.a Dijo que el saldo vive en la tarjeta. Entonces, ¿el sistema central sabe en todo momento cuánto saldo tiene cada tarjeta, o solo lo conoce cuando llegan las transacciones?
R2.b ¿Quién decide qué entra en la lista de bloqueo y en la lista de denegación, y quién puede sacar una tarjeta de esas listas?

Bloque 3, actores:
3.1 ¿Qué tipos de usuarios usan el sistema y en qué se diferencian (residentes, visitantes, estudiantes, adultos mayores, personas con movilidad reducida)?
3.2 ¿Qué personas o áreas internas intervienen en el recaudo y qué hace cada una?
3.3 ¿Quién es el dueño de una tarjeta VAMOS: el pasajero, el titular o el ente gestor?
3.4 ¿El visitante que paga con débito o crédito tiene alguna cuenta o registro en el sistema, o es anónimo?

Bloque 4, reglas de negocio:
4.1 ¿Cómo se define la tarifa de un viaje? ¿Quién la fija y cada cuánto cambia?
4.2 ¿Qué es un transbordo para ustedes? ¿Cuánto tiempo hay, entre qué modos y cuántas veces se puede hacer?
4.3 ¿Cuánto se cobra en un transbordo? ¿Cambia según el modo o según el perfil?
4.4 ¿Cuáles son las condiciones de cada tarifa especial y qué documentos se exigen?
4.5 ¿Cada cuánto se revalida un perfil? ¿Qué pasa cuando vence?
4.6 ¿Hay límites de uso para las tarifas especiales (viajes por día o por mes)?
4.7 ¿Existe saldo negativo o viaje a crédito con la tarjeta VAMOS? ¿Cuál es el saldo máximo?
4.8 ¿Las tarjetas débito y crédito tienen tarifa plena siempre? ¿Aplican transbordos?
4.9 Para confirmar: ¿una validación siempre descuenta una tarifa, salvo que caiga dentro de un transbordo válido?

**Experta:**
Primero las repreguntas y luego los bloques 3 y 4. Recuerden que las cifras son aproximadas y que los valores oficiales están en las resoluciones vigentes.

**R2.a ¿El central sabe el saldo de cada tarjeta en todo momento?**
No en tiempo real. El central lleva un **saldo calculado** de cada tarjeta con las transacciones que le van llegando: recargas, validaciones y ajustes. Para el metro y las estaciones ese saldo está casi al día. Para los buses puede ir atrasado unas horas, o hasta dos días si un validador no descargó a tiempo.
El saldo verdadero en el momento de viajar es el que está en la tarjeta. El del central es una reconstrucción.
Esto tiene consecuencias de negocio:
- Cuando alguien bloquea una tarjeta personalizada por pérdida, no le trasladamos el saldo de inmediato. Esperamos unas 48 horas a que lleguen las transacciones pendientes, y entonces trasladamos el saldo calculado por el central.
- Cuando hay un reclamo del tipo "mi tarjeta dice una cosa y la app otra", casi siempre es este desfase.
- Si encontramos diferencias que no se explican por el desfase, como una tarjeta con más saldo del que debería, eso es señal de posible fraude y lo investigamos.

**R2.b ¿Quién decide las listas de bloqueo y de denegación?**
*Lista de bloqueo (VAMOS):*
- **Por solicitud del titular.** Solo aplica a tarjetas personalizadas, porque una al portador no tiene a quién verificar. El usuario lo pide por la línea, la app, la web o un centro de atención, y Servicio al Cliente lo registra después de verificar su identidad. Ese bloqueo no se reversa: si la tarjeta aparece, igual queda inservible y el saldo ya se pasó a la nueva.
- **Por fraude o anomalía.** Lo decide mi área, normalmente a partir de alertas del proveedor de recaudo o de nuestra propia revisión. Solo mi área, después de investigar, puede autorizar que una tarjeta bloqueada por sospecha vuelva a funcionar.
- **Por desmonte de tecnología.** Las tarjetas de primera generación que ya fueron cambiadas se bloquean, para que no se usen dos veces.
*Lista de denegación (tarjetas bancarias):*
- Entra **automáticamente** cuando el cobro diferido es rechazado. También entran las tarjetas que las redes de pago reportan como bloqueadas.
- Sale **automáticamente** cuando el usuario paga la deuda pendiente por el portal web.
- Mi área autoriza excepciones manuales. Por ejemplo, si el rechazo fue por un error del adquirente y no del usuario.
Servicio al Cliente recibe el caso, pero no decide sacar una tarjeta de una lista. Esa decisión es nuestra.

**3.1 Tipos de usuarios**
Los perfiles tarifarios son de la persona, no del viaje.
- **Usuario frecuente residente, tarifa plena:** la gran mayoría. Usa VAMOS, personalizada o al portador, y viaja casi a diario por trabajo o estudio.
- **Usuario ocasional residente:** viaja de vez en cuando y muchas veces usa una VAMOS al portador con poco saldo. También empieza a usar su tarjeta bancaria.
- **Visitante o turista:** no conoce el sistema ni quiere comprar tarjeta. Para él pensamos el pago con débito y crédito. Siempre paga tarifa plena.
- **Estudiante de colegio:** tiene tarifa especial con perfil certificado por la institución y la Secretaría de Educación.
- **Universitario:** tiene tarifa especial con condiciones socioeconómicas. Lo veo en detalle en la 4.4.
- **Adulto mayor:** tarifa especial por edad.
- **Persona con movilidad reducida o con discapacidad certificada:** tarifa especial. Además requiere atención particular en la infraestructura, pero esa parte la ve Operaciones.
Aparte están los **usuarios de servicio**: funcionarios del ente gestor y de los operadores en ejercicio de sus funciones, y la Policía uniformada. Tienen credenciales que validan sin cobro, pero esas validaciones quedan registradas. No son usuarios comerciales.

**3.2 Personas y áreas internas que intervienen en el recaudo**
- **Recaudo y Tarifas (mi área):** estudios y propuestas tarifarias, administración de perfiles, supervisión del contrato del proveedor de recaudo, consolidación, conciliación, liquidación, investigación de fraude y gestión de las listas.
- **Servicio al Cliente:** personalización de tarjetas, registro de perfiles una vez certificados, bloqueos, PQR, devoluciones y traslados de saldo. Atiende al usuario, pero aplica las reglas que definimos nosotros.
- **Finanzas:** relación con la fiducia, tesorería, revisión de la liquidación, manejo de los recursos de la Alcaldía que cubren subsidios y déficit, y reportes contables, incluido el saldo de las tarjetas como obligación con los usuarios.
- **Operaciones:** certifica los kilómetros y la operación real, y reporta buses o estaciones con validadores fuera de servicio. Sus datos pesan en el pago a operadores.
- **Planeación:** diseña rutas y servicios, lo cual afecta los transbordos posibles. También hace los estudios de demanda que usamos para tarifas.
- **Tecnología:** maneja el intercambio de información con el proveedor de recaudo y los datos internos. No opera los validadores.
- **Jurídica:** contratos, resoluciones de tarifa y temas de protección de datos personales. Ahí está el oficial de protección de datos.
- **Gerencia General:** ordena los pagos y lleva las propuestas tarifarias a la Alcaldía.
- **Control Interno:** audita todo esto periódicamente.

**3.3 ¿Quién es dueño de la tarjeta VAMOS?**
Hay que separar tres cosas:
- **El plástico y el chip** son del sistema. Así lo dicen las condiciones de uso: el usuario paga los $7.000 por el derecho a usarla, no la compra como propiedad. Por eso podemos bloquearla o retirarla si hay fraude.
- **El saldo** es del usuario: del **titular** si la tarjeta es personalizada, o de quien la tenga si es al portador.
- **El pasajero** es quien viaja, y no siempre es el titular. Una VAMOS personalizada con tarifa plena se puede prestar en la práctica; no lo controlamos. Una tarjeta con **tarifa especial** es personal e intransferible, y si encontramos que la usa otra persona podemos quitarle el perfil.

**3.4 ¿El visitante con débito o crédito tiene registro?**
Para nosotros es prácticamente anónimo. No sabemos su nombre ni recibimos datos del banco. Lo que el sistema maneja es una identificación técnica de la tarjeta, que no es el número completo, con la cual se agrupan sus viajes del día para cobrar.
Hay un portal opcional donde la persona puede consultar sus viajes y pagar una deuda si la tarjeta quedó en denegación. Si se registra ahí, ya nos entrega algunos datos y los manejamos bajo la política de protección de datos. Pero registrarse no es obligatorio para viajar.

**4.1 ¿Cómo se define la tarifa?**
Hoy hay una **tarifa plena única de alrededor de $3.200** para cualquier modo: alimentador, articulado o metro. Antes había tarifas distintas por modo, y la unificación simplificó mucho las cosas para el usuario.
Mi área hace el estudio técnico con Finanzas, considerando el costo del sistema, la inflación, la demanda y la capacidad de pago de la gente. La Gerencia lo lleva a la Alcaldía, y el valor se fija por decreto o resolución con la autoridad de transporte.
Normalmente cambia **una vez al año**, en enero, y suele ajustarse cerca de la inflación. Pero es una decisión política: hay años en que se congela y el faltante lo cubre la Alcaldía.

**4.2 ¿Qué es un transbordo?**
Para nosotros, un transbordo es una validación que se hace dentro de los **90 minutos** siguientes a la primera validación pagada, en un servicio diferente.
- Se permite entre cualquier par de modos: alimentador con articulado, articulado con metro y alimentador con metro. También entre dos rutas de bus distintas.
- **No** se permite en la misma ruta ni en la misma estación de entrada. Si vuelve a validar ahí, se cobra como viaje nuevo, para evitar que la tarjeta se preste para que pasen dos personas.
- Se pueden hacer **hasta dos transbordos** en la ventana, es decir tres tramos.
- Ojo: si cambia de línea de metro o de troncal sin salir del área paga, no hay validación. Eso no cuenta como transbordo para el sistema porque ni siquiera se registra.

**4.3 ¿Cuánto cuesta un transbordo?**
- **Primer transbordo:** $0.
- **Segundo transbordo:** un valor pequeño, alrededor de $400.
No cambia según el modo, porque la tarifa es única. Tampoco cambia según el perfil: el usuario con tarifa especial tiene las mismas reglas de transbordo. Él paga su tarifa reducida en el primer tramo y el primer transbordo le sale gratis igual que a todos.

**4.4 Condiciones de cada tarifa especial**
Valores aproximados:
- **Estudiantes de colegio:** alrededor de 50 % de descuento. Deben estar matriculados en un colegio de la ciudad y ser menores de 19 años. El colegio reporta a los estudiantes y la Secretaría de Educación valida. El estudiante presenta documento de identidad y la tarjeta se personaliza.
- **Universitarios:** alrededor de 25 % de descuento. Para pregrado en instituciones con convenio y para estratos 1, 2 y 3. Se exige certificado de matrícula vigente, que la institución envía, y un soporte de estrato, como una factura de servicios públicos.
- **Adultos mayores:** alrededor de 30 % de descuento, desde los 62 años, aproximadamente. Basta la cédula; la edad la verificamos nosotros.
- **Personas con discapacidad o movilidad reducida:** alrededor de 50 % de descuento. Se exige el certificado de discapacidad expedido según la normatividad del Ministerio de Salud. El tema del acompañante está en discusión y todavía no está decidido.
La diferencia entre la tarifa plena y la especial la cubre la Alcaldía como subsidio, y Finanzas la gestiona.

**4.5 Revalidación de perfiles**
- **Colegio:** cada año. El perfil vence al final del año escolar y se renueva con el nuevo reporte de matrícula.
- **Universitarios:** cada semestre.
- **Adultos mayores:** no vence.
- **Discapacidad:** según la vigencia del certificado. Si es permanente no se revalida; si es temporal, vence con el certificado.
Cuando un perfil vence, la tarjeta **sigue funcionando a tarifa plena**: no se bloquea y el saldo queda intacto. El validador muestra un mensaje y algunas instituciones avisan, pero no tenemos una notificación automática al usuario. De ahí vienen bastantes quejas en enero y en julio.

**4.6 Límites de uso**
Sí:
- **Estudiantes de colegio y universitarios:** alrededor de **50 viajes subsidiados al mes**. Desde el viaje 51 pagan tarifa plena hasta el mes siguiente. Los transbordos gratuitos no cuentan dentro de ese límite.
- **Adultos mayores y personas con discapacidad:** hoy no tienen límite mensual.
- **Para todos los perfiles especiales:** no se puede validar dos veces en el mismo punto en un lapso corto, de unos 10 minutos. Así se evita que alguien deje pasar a otra persona con su descuento.

**4.7 Saldo negativo y saldo máximo**
Sí existe un **viaje de emergencia**. Si una VAMOS no tiene saldo suficiente, el validador deja pasar **un solo viaje** y el saldo queda negativo hasta por una tarifa. En la siguiente recarga se descuenta lo que se debe. Mientras tenga saldo negativo, no se permite otro viaje.
Hay un detalle: con una tarjeta al portador ese saldo negativo a veces no se recupera nunca, porque la tarjeta se bota. Es una pérdida pequeña que tenemos medida.
El **saldo máximo** es alrededor de $200.000.

**4.8 Débito y crédito**
Siempre **tarifa plena**, sin excepción, porque no hay perfil asociado.
Los **transbordos sí aplican**, con las mismas reglas, y se calculan en el cobro diferido al final del día. Por ejemplo, si el visitante tomó alimentador y luego metro dentro de los 90 minutos, al día siguiente se le cobra una sola tarifa.
No hay viaje de emergencia, porque el riesgo ya está en el cobro diferido.

**4.9 ¿Una validación siempre descuenta una tarifa, salvo un transbordo válido?**
No siempre. Hay varias excepciones:
- El **segundo transbordo** no es gratis, y tampoco es una tarifa completa.
- Las **validaciones rechazadas** (tarjeta bloqueada, sin saldo, en denegación, o pasaje dentro de los 10 minutos en el mismo punto) no descuentan nada, aunque quedan registradas.
- Las **credenciales de servicio** validan sin cobrar.
- Con **tarjeta bancaria** no se descuenta nada en el momento; el cobro se calcula después.
- Con **tarifa especial** se descuenta la tarifa reducida, no la plena, salvo que ya haya pasado el límite del mes.
- El **viaje de emergencia** descuenta, pero deja el saldo negativo.
Y al revés, hay viajes sin validación: los cambios de línea dentro del área paga y los niños pequeños que entran con un adulto sin pagar. Para los niños hay un límite de estatura que define la resolución.

Quedo atenta.

---

## Bloques 5 y 6. Excepciones e indicadores (con repreguntas del bloque 4)

**Entrevistador:**
Muy completo, gracias. Dos repreguntas y pasamos a excepciones (bloque 5) e indicadores (bloque 6):
R4.a Usted habla de "viaje", "validación", "tramo" y "transbordo". Para que no nos confundamos: ¿cómo define cada uno? ¿Un viaje con dos transbordos es un viaje o son tres?
R4.b Cuando se cambia la tarifa en enero, ¿qué pasa con las validaciones que llegan tarde al central pero ocurrieron en diciembre? ¿Con cuál tarifa se liquidan?

Bloque 5, excepciones:
5.1 ¿Cuáles son los problemas más frecuentes en el recaudo?
5.2 ¿Qué pasa si la tarjeta no tiene saldo suficiente al validar? (más allá del viaje de emergencia que ya nos explicó)
5.3 ¿Cómo funciona el bloqueo por pérdida? ¿Qué pasa con el saldo? ¿Cuánto tarda en aplicarse en los validadores?
5.4 ¿Qué pasa si un validador queda sin conexión? ¿Se aceptan viajes y cómo se cobran después?
5.5 ¿Qué pasa si se rechaza el pago con débito o crédito después de que el pasajero ya pasó?
5.6 ¿Cómo se manejan los dobles cobros, las devoluciones y los reclamos por saldo?
5.7 ¿Qué fraudes o usos indebidos se han visto (perfiles prestados, tarjetas clonadas)?
5.8 ¿Esas excepciones las resuelve Recaudo o se trasladan a otra área?

Bloque 6, indicadores:
6.1 ¿Con qué indicadores mide la gerencia que el recaudo funciona bien?
6.2 ¿Qué metas tienen hoy en esos indicadores (evasión, tiempo de validación, cuadre de conciliación, PQR)?
6.3 ¿Cuál de esos indicadores es el más crítico hoy?

**Experta:**
Primero las dos repreguntas y luego los bloques 5 y 6. Repito que las cifras son aproximadas.

**R4.a Viaje, validación, tramo y transbordo**
- **Validación:** cada vez que una tarjeta o medio de pago se acerca a un validador y queda un registro. Puede ser exitosa o rechazada. Es lo que más contamos, porque es lo que el sistema registra.
- **Tramo:** cada uso de un servicio, desde que la persona se sube a un bus o entra al metro hasta que se baja. Casi todos los tramos empiezan con una validación, pero no todos. Cuando alguien cambia de línea de metro o de troncal sin salir del área paga, hace un tramo nuevo sin validar.
- **Transbordo:** una validación exitosa que, por caer dentro de la ventana de 90 minutos en un servicio distinto, se liga a la validación pagada anterior. No se cobra como tarifa nueva: cuesta $0 o el valor reducido del segundo transbordo.
- **Viaje:** para recaudo y tarifas, es la cadena que empieza con una validación pagada y sigue con sus transbordos. Es lo que llamamos un **pasajero pago**.
Entonces, un viaje con dos transbordos es **un viaje**, con **tres validaciones** y al menos **tres tramos**, o más si además cambió de línea dentro del área paga.
Una advertencia: en Planeación "viaje" a veces significa otra cosa. Ellos hablan del desplazamiento origen-destino de las encuestas de movilidad, que puede incluir caminar o tomar otro medio. Cuando hablen con ellos, conviene confirmar.

**R4.b Cambio de tarifa y validaciones que llegan tarde**
Manda la **fecha y hora en que ocurrió la validación**, no la fecha en que llegó al central.
- Los validadores reciben la nueva tabla de tarifas con días de anticipación y con una fecha de vigencia programada. A las 00:00 del día del cambio empiezan a cobrar la nueva tarifa.
- Una validación del 30 de diciembre que llega el 2 de enero se cobró con la tarifa de diciembre, porque así la descontó el validador, y se liquida en el periodo de diciembre.
- Si diciembre ya estaba cerrado, entra como **ajuste extemporáneo** en la liquidación siguiente, pero identificada como de diciembre.
- El caso feo es un validador que no se actualizó a tiempo y siguió cobrando la tarifa vieja en enero. Al usuario no le cobramos la diferencia después. Quién asume esa diferencia depende de la causa: si fue falla del proveedor, el contrato le permite al ente gestor descontársela, pero cada caso lo revisa Jurídica.
- El saldo de las tarjetas está en pesos, no en viajes. Con la nueva tarifa, el mismo saldo simplemente alcanza para menos viajes.

**5.1 Problemas más frecuentes**
En orden aproximado de lo que más nos ocupa:
1. **Evasión:** gente que se cuela o entra por la puerta trasera de los buses. No es una falla del recaudo como tal, pero es la mayor fuga de ingresos.
2. **Validadores fuera de servicio en buses.** Cuando no funciona el validador, la gente viaja sin pagar.
3. **Recargas por app o web que el usuario no ve aplicadas**, porque todavía no ha validado.
4. **Transacciones extemporáneas** que descuadran los cierres.
5. **Puntos de recarga que consignan tarde o incompleto.**
6. **Quejas por perfiles vencidos**, sobre todo en enero y julio.
7. **Diferencias de saldo** reclamadas por usuarios, como un doble descuento o "me cobraron sin pasar".

**5.2 Tarjeta sin saldo suficiente**
- El validador **rechaza**, muestra "saldo insuficiente" y la validación queda registrada como rechazada.
- Si el usuario ya usó su viaje de emergencia y tiene saldo negativo, también se rechaza.
- Si la validación cae como **primer transbordo**, que cuesta $0, pasa aunque no tenga saldo, porque no hay nada que cobrar. El segundo transbordo sí necesita saldo para su valor.
- En una estación, la persona puede recargar en la taquilla o en la máquina. En un bus alimentador no se puede recargar a bordo, entonces se tiene que bajar. En la práctica, a veces el conductor la deja pasar. Eso está prohibido y cuenta como evasión.

**5.3 Bloqueo por pérdida**
- Solo aplica a **tarjetas personalizadas**. Una al portador no se puede bloquear por pérdida porque no sabemos de quién es.
- El titular reporta por la línea, la app, la web o en un centro de atención. Se verifica su identidad y el bloqueo queda registrado en el central **de inmediato**.
- **Llegada a los validadores:** a las estaciones, en minutos u horas. A los buses puede tardar **hasta unas 24 horas**, porque algunos solo actualizan listas cuando se conectan o llegan al patio.
- **Saldo:** esperamos unas 48 horas a que lleguen todas las transacciones. Lo que se haya usado con la tarjeta perdida antes de que el bloqueo llegara al validador lo asume el usuario, según las condiciones de uso. El saldo restante se traslada a la tarjeta nueva y aparece cuando la valida por primera vez.
- La tarjeta nueva tiene costo de reposición, alrededor de $7.000. Si tenía perfil especial, el perfil se traslada sin repetir la certificación, siempre que siga vigente.

**5.4 Validador sin conexión**
Hay que distinguir entre **sin conexión** y **dañado**.
*Sin conexión:*
- Con **VAMOS** funciona normal, porque el saldo está en la tarjeta. Las transacciones se guardan y se envían después.
- El riesgo es que el validador trabaja con listas desactualizadas. Puede dejar pasar una tarjeta recién bloqueada o no aplicar una recarga web reciente.
- Las **tarjetas bancarias** también se aceptan con la última lista de denegación que tenga el validador, y se cobran al día siguiente como siempre. El riesgo de no cobrar es un poco mayor.
*Dañado:*
- No se cobra. La gente viaja gratis.
- El operador debe reportarlo y Operaciones lo registra.
- Si el proveedor no cumple los tiempos de reparación, tiene descuentos según su contrato.
- Si el daño destruye la memoria con transacciones no enviadas, esas transacciones se pierden. La plata ya está en la fiducia, porque se recaudó al recargar, y el saldo ya salió de la tarjeta, pero no sabemos a qué ruta ni a qué operador asignar esos viajes. El saldo calculado del central queda más alto que el real, y eso aparece después como diferencia de conciliación. Es poco, pero pasa.

**5.5 Rechazo del cobro bancario después del viaje**
- La tarjeta entra a la **lista de denegación** y no puede volver a viajar hasta pagar.
- El sistema **reintenta el cobro** varias veces durante algunos días, unos tres intentos.
- El usuario puede pagar la deuda en el portal. Al pagar, sale automáticamente de la lista.
- Si nunca paga, después de un tiempo esa cartera se castiga como pérdida. Es alrededor del 0,5 % del valor de los viajes con tarjeta bancaria; es baja.

**5.6 Dobles cobros, devoluciones y reclamos de saldo**
- **Doble cobro con VAMOS:** la regla de los 10 minutos en el mismo punto evita la mayoría. Cuando ocurre por una falla del validador, el usuario hace la PQR, Servicio al Cliente revisa las transacciones y, si el caso es claro, se carga un **ajuste a favor** como recarga pendiente. Los casos dudosos o de montos altos los revisa mi área.
- **Doble cobro con tarjeta bancaria:** se hace un **reverso** a través del adquirente.
- **Devoluciones de saldo en dinero:** son excepcionales. Proceden, por ejemplo, por fallecimiento del titular, con solicitud de los herederos, o cuando el usuario se va de la ciudad y la tarjeta es personalizada. Requieren aprobación y las gira Finanzas desde la fiducia. Para la tarjeta dañada no se devuelve plata: si el chip se puede leer o es personalizada, el saldo se pasa a otra tarjeta.
- **Plazos:** por ley tenemos 15 días hábiles para responder una PQR. Internamente la meta es menor.
- Todos estos ajustes y devoluciones entran a la conciliación del mes.

**5.7 Fraudes y usos indebidos**
- **Perfiles prestados:** el más común. Por ejemplo, la tarjeta de estudiante la usa el papá, o la del adulto mayor la usa un nieto. Lo detectamos con los controles en estaciones y por patrones raros, como una tarjeta de colegio que viaja a las 11 de la noche todos los días.
- **Venta de tarjetas con perfil:** personas que sacan el perfil y venden la tarjeta.
- **Clonación y alteración de saldo** en las tarjetas de primera generación. Es una de las razones para desmontarlas.
- **Reventa y falsificación de tiquetes de papel.**
- **Puntos de recarga** que recargan sin recibir el pago o que no consignan lo vendido.
- **Conductores** en rutas alimentadoras con efectivo que cobran y no registran.
- **Uso indebido de credenciales de servicio** por personas que ya no tienen derecho.
- Y la **evasión**, que no es fraude con un medio de pago, pero es el uso indebido más grande.

**5.8 ¿Quién resuelve las excepciones?**
Depende del tipo:
- **Servicio al Cliente:** recibe todo lo que viene del usuario y resuelve lo que está claro con las reglas que fijamos: ajustes pequeños, bloqueos y traslados de saldo.
- **Recaudo y Tarifas:** resuelve lo que requiere criterio. Eso incluye ajustes grandes o dudosos, investigaciones de fraude, retiro de perfiles, sacar tarjetas de las listas, diferencias de conciliación y extemporáneas.
- **Proveedor de recaudo:** corrige las fallas técnicas, pero mi área lo supervisa.
- **Operaciones:** maneja la evasión en vía y en estaciones, con el personal de control y la Policía. También los reportes de validadores dañados en flota.
- **Finanzas:** gira las devoluciones en dinero.
- **Jurídica:** se encarga de las denuncias penales por fraude y de las sanciones contractuales.

**6.1 Indicadores**
Los que más mira la Gerencia:
- **Tasa de evasión**, como porcentaje de la demanda.
- **Disponibilidad de validadores**, en estaciones y en flota.
- **Completitud y oportunidad de las transacciones:** porcentaje recibido en 24 y en 48 horas.
- **Diferencia de conciliación**, como porcentaje del recaudo sin explicar.
- **Oportunidad de consignación de los canales.**
- **Tiempo del cierre mensual.**
- **PQR de recaudo:** cantidad por cada 100.000 validaciones y tiempo de respuesta.
- **Participación de medios electrónicos** en el total.
- **Cartera no cobrada** con tarjetas bancarias.
- **Tiempo de validación:** este se lo medimos al proveedor.

**6.2 Metas**
| Indicador | Meta | Hoy |
|---|---|---|
| Evasión | por debajo del 8 % | alrededor del 11 % |
| Disponibilidad de validadores en estaciones | ≥ 99 % | se cumple |
| Disponibilidad de validadores en flota | ≥ 98 % | alrededor del 96 % |
| Tiempo de validación | menos de medio segundo | se cumple |
| Transacciones recibidas en 24 horas | ≥ 99 % | se cumple casi siempre |
| Transacciones recibidas en 48 horas | 100 % | se cumple casi siempre |
| Diferencia de conciliación sin explicar | ≤ 0,1 % del recaudo mensual | entre 0,2 % y 0,3 % |
| Cierre mensual | ≤ 10 días hábiles | se cumple casi siempre, a veces con correcciones posteriores |
| Respuesta a PQR | 8 días hábiles (meta interna) | alrededor de 10 días en promedio |
| Cartera bancaria no cobrada | menos del 1 % | se cumple |
En respuesta a PQR, el límite legal es de 15 días hábiles, y en los picos de enero y julio nos acercamos peligrosamente a ese límite.

**6.3 El más crítico hoy**
La **evasión**, sin duda. Con un 11 % de evasión hablamos de unos 45.000 a 50.000 viajes diarios sin pagar. A la tarifa actual son del orden de **$150 millones de pesos al día**, aproximadamente. Ninguna otra excepción se le acerca.
Hay dos detalles importantes. La evasión no sale de los datos del recaudo, porque quien se cuela no valida. Se estima con conteos y muestreos que hacen Operaciones y Planeación. Y la controlan sobre todo Operaciones y la Policía. A nosotros nos toca medir el impacto en ingresos.
En segundo lugar pondría la **disponibilidad de validadores en flota**, porque cada validador dañado es evasión forzada, y la **diferencia de conciliación**, porque genera discusiones con los operadores todos los meses.

Quedo atenta.

---

## Bloques 7 y 8. Normatividad y sistemas actuales (con repregunta del bloque 6)

**Entrevistador:**
Gracias, Andrea. Una repregunta y seguimos con normatividad (bloque 7) y sistemas actuales (bloque 8):
R6.a Dijo que la evasión es el mayor problema pero que la controlan Operaciones y la Policía. Entonces, ¿qué esperaría usted concretamente del nuevo software de recaudo frente a la evasión, si es que espera algo?

Bloque 7, normatividad:
7.1 ¿Qué normas regulan el recaudo, las tarifas y los subsidios?
7.2 ¿Qué exigencias hay sobre datos personales de los usuarios y sobre pagos con tarjeta (PCI, por ejemplo)?
7.3 ¿Qué reportes hay que entregar obligatoriamente y a quién?
7.4 ¿Los subsidios a perfiles especiales los financia el sistema o una entidad externa?

Bloque 8, sistemas actuales:
8.1 ¿Qué sistemas usan hoy para el recaudo y qué problemas tienen?
8.2 ¿Qué funciones se hacen hoy manualmente o en hojas de cálculo?
8.3 ¿Qué es lo que más esperan resolver con el nuevo software?

**Experta:**
Respondo la repregunta y los bloques 7 y 8. Una aclaración antes: de normatividad le doy lo que manejo en el día a día, pero el listado exacto con artículos y vigencias lo tiene Jurídica. Mejor valídenlo con ellos.

**R6.a ¿Qué espero del nuevo software frente a la evasión?**
No espero que el software acabe con la evasión. Quien se cuela no pasa por ningún validador, así que eso se controla en la puerta, con infraestructura, personal y Policía.
Sí espero que nos ayude a **verla y a dirigir el control**. En concreto:
- **Comparar** las validaciones con los conteos de pasajeros que hacen Operaciones y Planeación, por ruta, estación y franja horaria, para estimar la evasión con más frecuencia que hoy. Hoy la medimos con muestreos unas pocas veces al año.
- **Alertas** cuando un bus o una estación registra muchas menos validaciones de lo esperado para su ruta y hora. Puede ser un validador dañado, un conductor que deja subir sin pagar o evasión fuerte.
- **Saber rápido qué validadores están fuera de servicio** y desde cuándo, para cuantificar cuánto se dejó de recaudar y cobrarle al proveedor lo que corresponda.
- **Medir el efecto de las campañas de control:** si se pusieron controladores en una estación, ¿subieron las validaciones?
Cómo se haga eso técnicamente le corresponde al equipo de arquitectura. Yo le digo qué necesito saber como negocio.

**7.1 Normas que regulan recaudo, tarifas y subsidios**
De lo que manejo:
- **Ley 86 de 1989:** marco de los sistemas de transporte masivo. Establece el principio de que la tarifa debe cubrir los costos de operación, lo que llamamos autosostenibilidad tarifaria. Leyes posteriores lo flexibilizaron, sobre todo el Plan Nacional de Desarrollo de 2015, que abrió fuentes de financiación distintas de la tarifa y fondos para subsidiar la demanda.
- **Ley 105 de 1993 y Ley 336 de 1996:** marco general del transporte. Fijan la competencia de las autoridades locales para fijar tarifas y el Estatuto Nacional de Transporte.
- **Ley 310 de 1996:** cofinanciación de la Nación a los sistemas de transporte masivo.
- **Decreto 1079 de 2015:** decreto único reglamentario del sector transporte. Ahí está buena parte de la reglamentación de los sistemas integrados, incluido el tema del sistema de recaudo, control e información.
- **A nivel local:** los decretos o resoluciones de la Alcaldía que fijan cada año la tarifa y las tarifas especiales; los acuerdos del Concejo que crean los subsidios y el fondo de estabilización; y los actos de la autoridad de transporte.
- **Contratos:** los de concesión, el del proveedor de recaudo y el de fiducia. No son normas, pero en la práctica mandan igual en el día a día.
- **Perfiles especiales:** influyen las normas de discapacidad, como la Ley 1618 de 2013, y las de protección del adulto mayor. Los descuentos concretos de esta ciudad salen de los actos locales.

**7.2 Datos personales y pagos con tarjeta**
*Datos personales:*
- Aplica la **Ley 1581 de 2012** de protección de datos personales y su reglamentación. Las exigencias son:
  - Necesitamos **autorización previa** del titular, con finalidades claras, para personalizar una tarjeta o asignar un perfil.
  - El titular tiene derecho a conocer, actualizar, rectificar y pedir la supresión de sus datos, y a revocar la autorización.
  - Debemos tener una **política de tratamiento** publicada y las bases de datos inscritas en el registro de la **Superintendencia de Industria y Comercio**.
- Hay **datos sensibles**: el certificado de discapacidad es información de salud y requiere protección reforzada.
- Hay **datos de menores**: los estudiantes de colegio son niños y adolescentes, y el tratamiento debe respetar su interés superior. Normalmente la autorización la da el acudiente.
- El **historial de viajes** dice dónde estuvo una persona y a qué hora. Lo cuidamos mucho. Si la Fiscalía o la Policía lo pide, solo se entrega con el soporte legal que corresponda, y eso lo revisa Jurídica.
*Pagos con tarjeta:*
- El estándar **PCI DSS** no es una ley colombiana. Lo exigen las redes de pago y el adquirente por contrato.
- El proveedor de recaudo y el adquirente deben estar certificados. Como ente gestor, no debemos guardar ni ver los números completos de las tarjetas bancarias. Por eso trabajamos con una identificación técnica, como les conté.
- La **fiducia** está vigilada por la Superintendencia Financiera, y eso también impone reglas sobre cómo se manejan los recursos.

**7.3 Reportes obligatorios**
Los que conozco, aproximadamente:
- **DANE:** reporte mensual de pasajeros y recaudo para la encuesta de transporte urbano. Lo preparamos con Planeación.
- **Superintendencia de Transporte:** información financiera y de operación en los formatos y plazos que ellos definen.
- **Ministerio de Transporte:** información de seguimiento de demanda y operación, asociada a la cofinanciación de la Nación.
- **Contraloría municipal y entes de control:** información del recaudo y del manejo de los recursos cuando la piden, y en la rendición de cuentas anual.
- **Alcaldía y Concejo:** informes de recaudo, subsidios y déficit, especialmente para el presupuesto y el cálculo del subsidio.
- **Superintendencia de Industria y Comercio:** registro y actualización de las bases de datos personales.
- **Contractuales:** liquidaciones a operadores, informes al comité fiduciario e informes de supervisión del contrato de recaudo. No son ante una autoridad, pero son obligatorios por contrato.
Las periodicidades exactas de algunos de estos las tienen Jurídica y Planeación. No me quiero equivocar.

**7.4 ¿Quién financia los subsidios?**
Una **entidad externa**: la Alcaldía, con recursos del presupuesto municipal. Una parte viene de fuentes como el cobro por estacionamiento en vía pública. Los operadores no los financian, y tampoco salen de la tarifa de los demás usuarios.
Funciona así:
1. Mi área calcula cada mes el valor del subsidio: las validaciones con tarifa especial multiplicadas por la diferencia frente a la tarifa plena.
2. Finanzas lo presenta a la Secretaría de Hacienda.
3. La Alcaldía gira esos recursos a la fiducia.
El problema es que el giro a veces llega tarde, y mientras tanto la fiducia tiene menos caja para pagar a los operadores.
La Nación ha cofinanciado sobre todo infraestructura. Si la Nación participa o no en la operación es un tema que se ha discutido en los últimos años, y eso lo sabe mejor Finanzas.

**8.1 Sistemas actuales y sus problemas**
- **Plataforma central del proveedor de recaudo:** recibe las transacciones y administra tarjetas, listas, recargas y reportes. Es de ellos, no nuestra. Los problemas:
  - Dependemos del proveedor para casi cualquier consulta que no esté en los reportes estándar. Un reporte nuevo puede tardar semanas.
  - No tenemos acceso fácil a los datos detallados.
  - Cuando el contrato se termine, no tenemos claro qué información nos queda.
- **Sistema de PQR de Servicio al Cliente:** está separado. Para resolver un reclamo de saldo, el asesor tiene que pedirle al proveedor o a mi área el historial de la tarjeta. Por eso las respuestas se demoran.
- **Sistema de gestión de flota de Operaciones:** de ahí salen los kilómetros recorridos. No conversa con el recaudo, y cruzamos la información a mano.
- **Sistema financiero y contable de Finanzas,** más el **portal de la fiducia,** donde vemos movimientos y saldos de las cuentas.
- **Perfiles especiales:** las instituciones nos mandan archivos en formatos distintos, cada una a su manera.
El problema general es que **cada pieza está aislada**. Nadie tiene una vista completa de una tarjeta con su usuario, sus viajes, sus recargas y sus reclamos.

**8.2 Lo que hoy se hace a mano o en hojas de cálculo**
- **La liquidación a operadores.** Es un libro de Excel grande y delicado, que dominan dos personas de mi equipo. Si una de ellas se enferma en cierre de mes, tenemos un problema.
- **La conciliación de ventas contra consignaciones de los canales**, en buena parte.
- **El seguimiento de las transacciones extemporáneas** y de los ajustes a periodos cerrados.
- **El cálculo del subsidio** que se cobra a la Alcaldía.
- **La recepción y validación de los listados de las instituciones** antes de cargar perfiles.
- **El seguimiento de las objeciones de los operadores**, por correo y en actas.
- **Los indicadores para la Gerencia** y buena parte de los reportes a entidades. Se arman juntando reportes de varios sistemas.
- **Las investigaciones de fraude:** se piden extractos al proveedor y se analizan en Excel.

**8.3 Lo que más esperamos resolver**
Hablo desde el negocio:
1. **Tener control de nuestra información de recaudo** sin depender del proveedor para cada consulta.
2. **Una liquidación y una conciliación confiables y trazables.** Que cualquiera pueda ver de dónde sale cada peso que se le paga a un operador, que el cierre sea más rápido y que no dependa de dos personas.
3. **Una vista completa de la tarjeta y del usuario** para Servicio al Cliente, para responder un reclamo en días y no en semanas.
4. **Que la gestión de perfiles con las instituciones sea ordenada:** que ellas reporten de forma uniforme y que los vencimientos se avisen.
5. **Detectar fraude y anomalías a tiempo**, incluido lo que le dije de la evasión.
6. **Indicadores y reportes oportunos** sin armarlos a mano.
Ahora, qué alcance tiene exactamente el nuevo software (si reemplaza la plataforma del proveedor, si convive con ella, o qué parte queda en manos del tercero) es una decisión que todavía no está tomada en la Gerencia. Lo que sí está claro es que los validadores siguen con el tercero.

Quedo atenta.

---

## Bloque 9. Interoperabilidad (con repregunta del bloque 8)

**Entrevistador:**
Gracias. Una repregunta y pasamos al bloque más importante para nosotros, el 9 de interoperabilidad. Para cada externo nos interesa: qué información se intercambia, en qué dirección, con qué frecuencia y qué pasa si falla.
R8.a Dijo que no está decidido si el nuevo software reemplaza o convive con la plataforma del proveedor. Para efectos de esta conversación, si el proveedor siguiera operando validadores y su plataforma de transacciones, ¿qué funciones le gustaría a usted que el ente gestor tuviera bajo su control directo?

9.1 Validadores y dispositivos (del tercero):
9.1.1 ¿Qué datos envía un validador por cada transacción y qué datos necesita recibir (listas de bloqueo, tarifas, perfiles)?
9.1.2 ¿Con qué frecuencia se actualizan las listas que reciben los validadores?
9.2 Servicio al cliente (PQR y devoluciones):
9.2.1 ¿Qué información necesita Servicio al Cliente de Recaudo, y qué le devuelve?
9.2.2 ¿Cómo se aprueba y se ejecuta una devolución de saldo o de un cobro?
9.3 Financiero:
9.3.1 ¿Qué le entrega Recaudo a Finanzas y con qué periodicidad?
9.3.2 ¿Cómo se registra contablemente un recaudo, una recarga y un ingreso? ¿Cuándo se reconoce el ingreso?
9.4 Planeación de rutas y de la operación:
9.4.1 ¿Qué información de recaudo usa Planeación y qué le envía Planeación a Recaudo (rutas, paradas, tablas de operadores)?
9.4.2 Cuando se crea o se cambia una ruta, ¿cómo se entera el recaudo?
9.5 Redes de pago y entidades financieras:
9.5.1 ¿Con qué actores financieros interactúan (adquirente, franquicias, bancos, pasarela de recargas, fiduciaria)?
9.5.2 ¿Cómo se autorizan y se liquidan los pagos con tarjeta débito o crédito y cuándo llega el dinero?
9.5.3 ¿Dónde se custodia el dinero del recaudo y cómo se gira a los operadores?
9.6 Entidades que certifican perfiles:
9.6.1 ¿Cómo se comprueba que alguien es estudiante, adulto mayor o persona con movilidad reducida? ¿Quién lo certifica?
9.6.2 ¿Ese intercambio se hace hoy de forma digital o con documentos físicos?
9.7 Autoridad de transporte:
9.7.1 ¿Qué le reporta Recaudo a la autoridad de transporte y qué recibe de ella?
9.7.2 ¿Cómo se aplica un cambio de tarifa decretado?
9.8 Otros:
9.8.1 ¿Con qué otras áreas, sistemas o entidades intercambia información el recaudo que no hayamos mencionado?
9.8.2 De todas estas integraciones, ¿cuál es la más crítica para la operación diaria?

**Experta:**
Respondo la repregunta y luego el bloque 9, integración por integración. Como siempre, las cifras y frecuencias son aproximadas. Los detalles técnicos de cómo viajan los datos los conoce el proveedor; yo le cuento qué pasa desde el negocio.

**R8.a Si el proveedor sigue con validadores y transacciones, ¿qué quisiera bajo control directo?**
Hablo de control de negocio, no de cómo se construye:
1. **Las reglas tarifarias:** tarifas, perfiles, transbordos, límites y vigencias. Hoy las definimos nosotros, pero el proveedor las configura a su manera. Quisiéramos definirlas, aprobarlas y tener evidencia de qué regla estaba vigente en cada momento.
2. **La gestión de usuarios y perfiles:** quién es titular de qué tarjeta, qué perfil tiene y hasta cuándo. Para la ley de datos personales, el **responsable** del tratamiento es el ente gestor; el proveedor es un **encargado**. Hoy en la práctica es al revés: los datos están en su plataforma.
3. **Las decisiones sobre las listas:** quién entra y quién sale por bloqueo, fraude o deuda. El proveedor las distribuye, pero la decisión debe ser nuestra y quedar registrada.
4. **Una copia completa y oportuna de todas las transacciones**, para tener nuestro propio saldo calculado y nuestras propias consultas.
5. **La consolidación, la conciliación y la liquidación.** Eso no debería depender de reportes del proveedor.
6. **La atención al usuario sobre su tarjeta:** historial, saldo, ajustes y devoluciones.
7. **Los indicadores y el control del contrato del proveedor:** disponibilidad, oportunidad y completitud.
Sobre los canales de recarga, no tengo una posición definida todavía. Hoy los contrata el proveedor, y si eso cambia o no lo decide la Gerencia con Jurídica.

### 9.1 Validadores y dispositivos (del tercero)

**9.1.1 ¿Qué envían y qué reciben los validadores?**
*Envían, por cada transacción:*
- identificación y tipo del medio de pago (VAMOS o la identificación técnica de la tarjeta bancaria);
- perfil, fecha y hora;
- validador, estación o bus, ruta y operador;
- tipo de transacción (pago, transbordo, rechazo con motivo, recarga pendiente aplicada);
- valor cobrado, saldo antes y después, y consecutivo de la tarjeta.
*Envían además, sin ser transacciones de viaje:*
- **eventos del equipo**: encendido, apagado, fallas, alarmas y manipulación;
- **contadores de cierre** por validador, que nos sirven para comprobar que llegó todo;
- en estaciones, las **recargas y consultas** hechas en máquinas y taquillas.
*Reciben:*
- la **tabla de tarifas** con su fecha de vigencia y las **reglas de transbordo y de límites**;
- la **lista de bloqueo** de VAMOS y la **lista de denegación** de tarjetas bancarias;
- las **recargas pendientes y ajustes** que se escriben en la tarjeta cuando la persona valida;
- las **novedades de perfil**, como un perfil retirado por fraude. El perfil y su vencimiento quedan grabados en la tarjeta al personalizarla; lo que viaja son los cambios;
- la **configuración del bus**: a qué operador pertenece y qué ruta está haciendo. Este es un punto delicado, porque si el bus queda configurado con la ruta equivocada, todas sus validaciones se asignan mal;
- la hora sincronizada.

**9.1.2 Frecuencia de actualización de las listas**
- **Metro y estaciones:** varias veces por hora, casi en línea.
- **Buses:** cada vez que tienen conexión, normalmente cada pocas horas. Como mínimo, todas las noches en el patio.
- **Tarifas y reglas:** se envían con días de anticipación y se activan en la fecha programada.
*Si falla:*
- Un validador con listas viejas deja pasar tarjetas bloqueadas o en mora y no aplica recargas web. Eso último genera quejas inmediatamente.
- Si falla el envío de transacciones, aparecen las extemporáneas y los descuadres.
- Hoy nos enteramos tarde de los validadores que llevan días sin actualizar. Quisiera que cualquier validador que pase de unas 48 horas sin sincronizar quede señalado.

### 9.2 Servicio al Cliente

**9.2.1 ¿Qué necesita Servicio al Cliente y qué devuelve?**
*Necesita de Recaudo, para atender un caso:*
- historial de la tarjeta: validaciones, recargas, ajustes y rechazos;
- saldo calculado y recargas pendientes de aplicar;
- estado de la tarjeta: bloqueos, perfil y vigencia, viajes subsidiados usados en el mes;
- para tarjeta bancaria: viajes, cobros y deuda;
- las reglas vigentes, para explicarle al usuario por qué le cobraron lo que le cobraron.
*Nos devuelve:*
- solicitudes de bloqueo y de traslado de saldo;
- solicitudes de ajuste o devolución;
- datos de personalización y autorizaciones de datos personales;
- reportes de posible fraude que llegan por denuncia;
- la estadística de PQR por tipo, que nos sirve para detectar problemas.
*Frecuencia:* caso a caso, durante todo el día. Lo ideal es en el momento. Hoy el asesor pide la información por correo o tiquete al proveedor o a mi área, y la respuesta tarda de uno a tres días.
*Si falla:* no se puede responder a tiempo, las PQR se vencen y quedamos expuestos a quejas ante la Superintendencia de Transporte y la de Industria y Comercio.

**9.2.2 Aprobación y ejecución de una devolución**
1. El usuario radica la PQR.
2. Servicio al Cliente verifica las transacciones y aplica las reglas.
3. **Ajustes pequeños, hasta unos $50.000 y con causa clara:** los aprueba Servicio al Cliente. Se cargan a la tarjeta como ajuste pendiente y aparecen en la siguiente validación.
4. **Montos mayores, casos dudosos o sospechas de fraude:** los aprueba mi área.
5. **Devoluciones en dinero:** las aprueba mi área. Finanzas instruye a la fiducia para que transfiera a la cuenta bancaria del usuario, y para eso se pide una certificación bancaria. Tardan de dos a cuatro semanas.
6. **Cobros dobles con tarjeta bancaria:** mi área le pide al proveedor el reverso a través del adquirente.
7. Todo queda registrado para la conciliación del mes y se le informa al usuario en la respuesta de la PQR.

### 9.3 Finanzas

**9.3.1 ¿Qué le entrega Recaudo a Finanzas?**
- **Diario:** recaudo por canal y lo que debería entrar a la fiducia, para que tesorería haga seguimiento.
- **Semanal:** liquidación preliminar para los giros.
- **Mensual, en el cierre:**
  - liquidación definitiva por operador y metro;
  - informe de conciliación con las diferencias explicadas y las pendientes;
  - saldo total en tarjetas;
  - valor del subsidio a cobrar a la Alcaldía;
  - cartera de tarjetas bancarias;
  - devoluciones y ajustes;
  - comisiones de canales, del proveedor y bancarias.
- **Anual:** proyecciones de demanda y recaudo para el presupuesto y para el estudio de tarifa.
*Si falla:* se atrasan los giros a los operadores y se arma un problema contractual en días.

**9.3.2 Registro contable y reconocimiento del ingreso**
Aquí tengo que ser cuidadosa: no soy contadora. Esto lo define Contabilidad, bajo el marco que aplica a entidades públicas en Colombia. Lo que yo entiendo es:
- **La recarga no es ingreso.** El dinero entra a la fiducia, pero se le debe un servicio al usuario. El saldo en las tarjetas se registra como una **obligación** con los usuarios.
- **El ingreso se reconoce cuando se presta el viaje**, es decir con la validación.
- **Tarjeta bancaria:** el viaje genera el ingreso y una **cuenta por cobrar** hasta que el banco paga. Si no se cobra, va a cartera y eventualmente se castiga.
- **El plástico de la tarjeta** es ingreso cuando se vende.
- Ojo: el dinero está en un **patrimonio autónomo** y buena parte le pertenece a los operadores según sus contratos. Qué parte se registra como ingreso del ente gestor y qué parte no, es un tema contable que maneja Finanzas.
- Hay un tema **sin decidir**: los saldos de tarjetas que no se usan hace años. Qué se hace con esa plata está en discusión con Jurídica y Finanzas.

### 9.4 Planeación

**9.4.1 ¿Qué intercambian Planeación y Recaudo?**
*Planeación usa de Recaudo:*
- validaciones por ruta, estación, parada y franja horaria;
- secuencias de transbordo, con las que estiman cómo se mueve la gente entre servicios. Las reciben sin datos personales;
- uso por perfil;
- efecto de los cambios de tarifa en la demanda.
*Planeación envía a Recaudo:*
- el **catálogo de rutas**: código, tipo de servicio, operador asignado y fecha de vigencia;
- **estaciones y paradas**;
- qué rutas están integradas;
- las **asignaciones de ruta a operador**.
Los kilómetros programados y ejecutados vienen de Operaciones, no de Planeación.
*Frecuencia:* el catálogo cambia unas pocas veces al mes. La información de demanda la piden mensualmente, y en los estudios grandes piden bases más detalladas.

**9.4.2 Cuando se crea o se cambia una ruta, ¿cómo se entera Recaudo?**
Hoy es así:
1. Se expide el acto de cambio de ruta.
2. Planeación nos envía un correo, a nosotros y al proveedor, con unas dos semanas de anticipación si todo sale bien.
3. El proveedor configura la nueva ruta en su plataforma y en los validadores.
4. Nosotros actualizamos los parámetros de la liquidación en el Excel.
*Si falla:*
- Los buses validan con el código de ruta viejo y los viajes se asignan a la ruta o al operador equivocado. Toca reliquidar, y los operadores reclaman.
- Una ruta nueva que no se configuró como integrada hace que se cobre el transbordo a la gente.
Lo peor son las **rutas temporales** por obras, eventos o emergencias, que a veces se avisan con uno o dos días.

### 9.5 Redes de pago y entidades financieras

**9.5.1 Actores financieros**
- **Adquirente:** procesa los cobros a tarjetas débito y crédito.
- **Franquicias** como Visa y Mastercard: ponen las reglas, pero nos relacionamos con ellas a través del adquirente, no directamente.
- **Bancos emisores:** indirectamente, cuando hay rechazos o contracargos.
- **Pasarelas de pago** de la app y la web: PSE y pago con tarjeta para las recargas en línea.
- **Redes de puntos de recarga:** las tiendas y droguerías trabajan a través de empresas de redes de pago y corresponsales.
- **Transportadora de valores:** recoge el efectivo de las taquillas.
- **Bancos donde están las cuentas recaudadoras** de la fiducia.
- **La fiduciaria.**

**9.5.2 Autorización y liquidación de pagos con tarjeta bancaria**
- **Autorización:** en el toque, el validador verifica que la tarjeta sea válida y que no esté en la lista de denegación. No espera al banco. Tengo entendido que en el primer uso del día se hace una verificación con el banco, pero el detalle técnico es del proveedor y del adquirente.
- **Cobro:** en la madrugada siguiente se envía al adquirente el cobro consolidado del día de cada tarjeta, con los transbordos aplicados.
- **Llegada del dinero:** después de la compensación, el abono a la cuenta de la fiducia llega en uno a tres días hábiles, descontada la comisión. Esa comisión ronda el 1,5 % a 2 % del valor.
- **Contracargos:** si un usuario desconoce un cobro ante su banco, el adquirente nos notifica y tenemos un plazo para responder con la evidencia de los toques.
*Si falla el adquirente:* los cobros se acumulan y se reintentan cuando se restablece el servicio. Mientras tanto, la gente sigue viajando y el riesgo de no cobrar crece.

**9.5.3 Custodia del dinero y giros**
- Todo el recaudo se custodia en el **patrimonio autónomo** que administra la fiduciaria, en cuentas bancarias a su nombre. Nunca en cuentas del ente gestor ni de los operadores.
- **Taquillas:** la transportadora de valores recoge el efectivo y lo consigna.
- **Puntos externos:** consignan a través de su red, en el plazo pactado.
- **Pagos en línea y bancarios:** se abonan directamente.
- **Subsidios de la Alcaldía:** se transfieren también a la fiducia.
- **Giros:** con la instrucción aprobada, la fiducia verifica y transfiere a las cuentas registradas de cada beneficiario, en el orden de prelación. También alimenta las subcuentas, como el fondo de contingencia.
*Si no alcanza la plata:* se paga según la prelación, y lo que falte queda pendiente hasta que lleguen recursos, normalmente el subsidio atrasado de la Alcaldía.

### 9.6 Entidades que certifican perfiles

**9.6.1 ¿Cómo se comprueba cada perfil?**
- **Estudiantes de colegio:** el colegio reporta a la Secretaría de Educación, y la Secretaría valida contra el sistema nacional de matrícula y nos envía el listado de habilitados.
- **Universitarios:** cada institución con convenio nos envía cada semestre el listado de matriculados. El estrato lo verificamos con el soporte que trae el estudiante.
- **Adultos mayores:** verificamos la cédula en el centro de atención. No tenemos cruce con la Registraduría, entonces no nos enteramos cuando un beneficiario fallece. Se han visto tarjetas de personas fallecidas que siguen usando otros.
- **Personas con discapacidad:** presentan el certificado de discapacidad expedido según la reglamentación del Ministerio de Salud. Lo revisamos en el centro de atención. En algunos casos dudosos consultamos con la Secretaría de Salud.

**9.6.2 ¿Digital o físico?**
Es una mezcla:
- **Instituciones y Secretaría de Educación:** archivos de Excel por correo, cada uno con un formato distinto. Mi equipo los revisa y los acomoda antes de cargarlos.
- **Adultos mayores y discapacidad:** documentos físicos en el centro de atención, que se escanean.
*Frecuencia:* hay picos fuertes en enero y en julio. Los retiros casi nunca nos llegan: un estudiante que se sale del colegio en abril sigue con su perfil hasta fin de año, y eso es una fuga.
*Si falla o se atrasa:* en enero miles de estudiantes pagan tarifa plena, se disparan las PQR y hay presión política de padres y concejales.

### 9.7 Autoridad de transporte

Una aclaración: en esta ciudad la autoridad de transporte es la Secretaría de Movilidad, que es distinta del ente gestor.

**9.7.1 ¿Qué se reporta y qué se recibe?**
*Le reportamos:*
- demanda y recaudo;
- indicadores de calidad, de evasión y de PQR;
- el estudio técnico de tarifa cuando hay ajuste.
*Recibimos:*
- los actos de tarifa;
- las decisiones sobre servicios y rutas que requieren su aval;
- requerimientos de información y, a veces, solicitudes por quejas de ciudadanos.
*Frecuencia:* reportes periódicos, en general mensuales o trimestrales, y requerimientos puntuales.

**9.7.2 ¿Cómo se aplica un cambio de tarifa decretado?**
1. Entre octubre y noviembre hacemos el estudio y la Gerencia presenta la propuesta.
2. La Alcaldía expide el acto, normalmente en diciembre.
3. Le entregamos al proveedor la nueva tabla de tarifas con fecha de vigencia. Él la configura y hacemos pruebas.
4. Se envía a los validadores con anticipación y se activa a las 00:00 del día de vigencia.
5. Comunicaciones avisa a los usuarios y se actualizan los avisos en estaciones y puntos.
6. Ajustamos los parámetros de liquidación y del cálculo del subsidio.
7. El primer día monitoreamos qué validadores no tomaron la nueva tarifa.
*El riesgo:* cuando el acto sale en la última semana de diciembre, quedan muy pocos días para configurar y probar.

### 9.8 Otros

**9.8.1 Otras áreas, sistemas o entidades**
- **Operadores de flota y metro:** reciben las liquidaciones y presentan objeciones. Nos reportan fallas de validadores y novedades de flota, como buses nuevos o retirados que hay que dar de alta o de baja.
- **Operaciones:** kilómetros, programación, eventos de operación y datos del sistema de gestión de flota.
- **Secretaría de Hacienda:** cobro y giro del subsidio.
- **Comunicaciones:** campañas y avisos sobre tarifas, perfiles y cambios.
- **Policía:** evasión y denuncias de fraude.
- **Control Interno y Contraloría:** auditorías.
- **DANE, Superintendencias y Ministerio:** los reportes que ya mencioné.
- **Tecnología:** seguridad e infraestructura.
- **Canales de consulta al usuario,** como la app y la web, donde la gente consulta saldo y recargas.
- **Hacia el futuro:** los municipios vecinos del área metropolitana quieren que sus buses se integren con la tarifa. Eso no está decidido, pero ya se habla.

**9.8.2 La integración más crítica para el día a día**
La de **validadores con la plataforma central**: transacciones hacia arriba y listas y tarifas hacia abajo. Si eso falla, no cobramos bien, no sabemos qué pasó y todo lo demás se cae detrás, porque no hay consolidación, ni liquidación, ni respuesta a PQR.
En segundo lugar, la **red de recargas**. Si se cae un lunes a las 6 de la mañana, la gente no puede cargar, se cuela o se queda afuera, y eso es caos en las estaciones.
En lo financiero, la más crítica es la **fiducia**, porque de ella depende que los operadores reciban su plata. Pero esa falla se siente en días, no en minutos.

Quedo atenta.

---

## Bloques 10 y 11. Motivación y qué hace la organización

**Entrevistador:**
Muchísimas gracias, ese bloque nos aclara muchísimo. Vamos a los dos últimos: motivación (bloque 10) y qué hace la organización (bloque 11). Para el bloque 11, por favor descríbanos las funciones de la organización tal como ustedes las viven; no le pedimos que nos arme ningún mapa ni modelo.

Bloque 10, motivación:
10.1 Interesados: ¿quiénes tienen interés en que este software exista y qué espera cada uno?
10.2 Impulsores: ¿qué está empujando a la organización a hacer este proyecto ahora?
10.3 Evaluaciones: ¿qué problemas o debilidades concretas tiene la situación actual?
10.4 Metas: ¿qué quiere lograr la organización con esto?
10.5 Resultados: ¿qué resultado medible consideraría un éxito y en qué plazo?
10.6 Principios: ¿qué principios o criterios deben respetarse siempre (por ejemplo, equidad tarifaria o transparencia con los operadores)?
10.7 Requerimientos: ¿qué debe permitir hacer el software sí o sí?
10.8 Restricciones: ¿qué limitaciones hay (presupuesto, normas, contratos vigentes, tecnología existente, plazos)?
10.9 Si tuviera que escoger una sola meta como la más importante, ¿cuál sería?

Bloque 11, qué hace la organización:
11.1 Más allá del recaudo, ¿cuáles son todas las grandes funciones que realiza el ente gestor?
11.2 ¿Qué funciones son estratégicas, cuáles son la razón de ser del sistema y cuáles son de apoyo?
11.3 ¿Cuáles de esas funciones se verían afectadas o mejoradas con el nuevo software de recaudo?
11.4 Cierre: ¿hay algo importante del recaudo que no le hayamos preguntado?

**Experta:**
Con gusto, cerramos con los bloques 10 y 11. En el 11 le describo lo que hacemos como lo vivimos. Cómo se organiza eso en un modelo le corresponde al equipo de arquitectura.

### Bloque 10, motivación

**10.1 Interesados y qué espera cada uno**
- **Gerencia General:** control y transparencia del recaudo. Poder responderle a la Alcaldía, al Concejo y a los entes de control sin quedar en evidencia.
- **Recaudo y Tarifas (mi área):** dejar de depender del proveedor y del Excel. Que la liquidación y la conciliación sean confiables, rápidas y trazables.
- **Finanzas:** cierres a tiempo, cifras confiables para la contabilidad, cobro oportuno del subsidio y control de la cartera.
- **Servicio al Cliente:** ver la información de la tarjeta y del usuario para resolver en días, no en semanas.
- **Operaciones:** saber qué validadores fallan y dónde hay posible evasión, y que los cambios de ruta no rompan el recaudo.
- **Planeación:** datos de demanda confiables y oportunos.
- **Jurídica y el oficial de protección de datos:** cumplir la ley de datos personales con el ente gestor como responsable real, y tener evidencia sólida para disputas con operadores.
- **Operadores de flota:** transparencia sobre cómo se calcula lo que reciben, pagos a tiempo y menos reliquidaciones. Algunos pueden desconfiar al principio, porque más trazabilidad también significa más control sobre ellos.
- **Metro:** lo mismo, con su propio convenio.
- **Proveedor de recaudo:** su posición es ambigua. Puede verlo como una amenaza a su negocio o como un alivio, porque dejaría de atender tantas solicitudes de información.
- **Alcaldía y Secretaría de Hacienda:** certeza sobre cuánto subsidio están pagando y para quién.
- **Concejo y entes de control:** transparencia en el uso de recursos públicos.
- **Usuarios:** que las recargas se reflejen rápido, que los reclamos se resuelvan pronto y que obtener o renovar un perfil sea fácil.
- **Instituciones que certifican:** menos papeleo y un formato único para reportar.
- **Fiduciaria:** instrucciones claras y soportadas.

**10.2 Impulsores, ¿por qué ahora?**
- **El contrato del proveedor de recaudo vence en unos tres años.** Tenemos que decidir qué hacer y no queremos llegar a esa fecha sin control de nuestra información.
- **Hallazgos de la Contraloría** en la última auditoría sobre la trazabilidad de la liquidación y la dependencia de hojas de cálculo.
- **Disputas con operadores.** Un concesionario tiene una reclamación formal por diferencias en liquidaciones de años anteriores, y nos costó mucho reconstruir la evidencia.
- **Presión financiera:** el déficit del sistema crece. La Alcaldía exige reducir la evasión y el fraude en subsidios antes de poner más plata.
- **Crecimiento de los pagos con tarjeta bancaria** y la perspectiva de integración con municipios vecinos, que la operación actual no aguantaría bien.
- **El calendario político:** la administración actual termina a finales del próximo año, y la Gerencia quiere mostrar resultados concretos.
- **El riesgo de personas clave:** la liquidación depende de dos personas.

**10.3 Problemas y debilidades de la situación actual**
- La información está en manos del proveedor y no tenemos acceso directo ni oportuno.
- La liquidación y la conciliación se hacen en Excel, sin trazabilidad, con riesgo de errores y concentradas en pocas personas.
- Los sistemas están aislados: recaudo, PQR, flota y finanzas no conversan.
- Los cierres son lentos y las diferencias de conciliación están por encima de la meta.
- Las PQR se resuelven lento porque falta información.
- La gestión de perfiles es manual, con formatos distintos y sin retiros oportunos. Hay fuga de subsidio.
- Detectamos el fraude tarde y a mano.
- Los cambios de ruta y de tarifa no tienen un procedimiento controlado.
- La evasión se mide poco y sin desagregación.
- Como responsables, tenemos debilidades frente a la protección de datos personales.

**10.4 Metas**
- Que el ente gestor tenga **control y propiedad de la información** del recaudo.
- **Liquidar y conciliar** de forma confiable, rápida y trazable.
- **Mejorar la atención al usuario** en todo lo relacionado con tarjetas y pagos.
- **Reducir la fuga de recursos**: fraude en perfiles, validadores fuera de servicio, cartera bancaria y medición de la evasión.
- **Cumplir** con datos personales, reportes y entes de control sin esfuerzos heroicos.
- **Estar preparados** para la decisión sobre el contrato del proveedor y para la integración metropolitana.

**10.5 Resultados medibles y plazos**
Son metas indicativas. La Gerencia todavía no las ha formalizado.
| Resultado | Meta | Plazo |
|---|---|---|
| Cierre mensual | ≤ 5 días hábiles (hoy 8 a 10) | 12 meses después de entrar en operación |
| Diferencia de conciliación sin explicar | ≤ 0,1 % (hoy entre 0,2 % y 0,3 %) | 12 meses |
| Liquidaciones trazables y reconstruibles | 100 %, sin Excel | primer cierre en el nuevo esquema |
| Respuesta a PQR de recaudo | ≤ 5 días hábiles en promedio (hoy alrededor de 10) | 6 a 12 meses |
| Retiro de perfiles que perdieron el derecho | reflejado al mes siguiente | — |
| Fraude detectado en perfiles | disminución medible | primer año |
| Medición de evasión | mensual, por ruta y estación (hoy pocas veces al año) | — |
| Reportes a entidades de control | sin trabajo manual | — |
Lo ideal es tener resultados visibles en 12 a 18 meses y, en todo caso, antes del vencimiento del contrato del proveedor.

**10.6 Principios que deben respetarse siempre**
- **Equidad tarifaria:** las mismas reglas para todos los usuarios con el mismo perfil, sin importar el canal, la ruta o el operador.
- **Legalidad:** ninguna regla tarifaria se aplica sin acto administrativo que la soporte, y siempre con su vigencia.
- **Transparencia y neutralidad con los operadores:** todos se liquidan con las mismas reglas de su contrato, y cada uno puede verificar cómo se llegó a su cifra.
- **Trazabilidad:** todo peso tiene que poder seguirse, desde la recarga o el viaje hasta el giro.
- **El dinero es público y está en la fiducia:** nadie maneja el recaudo por fuera del patrimonio autónomo.
- **Separación de funciones:** quien liquida no aprueba ni gira.
- **Continuidad del servicio:** una falla de sistemas no puede dejar a la gente sin poder viajar.
- **El usuario no paga los errores del sistema:** en casos pequeños y razonables, se le da el beneficio de la duda.
- **Protección de datos:** solo los datos necesarios, con autorización, y cuidado especial con menores, información de salud e historial de viajes.
- **Inclusión:** siempre debe haber una forma de pagar para quien no tiene cuenta bancaria ni teléfono inteligente.

**10.7 ¿Qué debe permitir el software sí o sí?**
Desde el negocio:
1. Tener **toda la información de transacciones, recargas y ventas**, completa y oportuna, incluidas las extemporáneas.
2. **Definir y mantener las reglas tarifarias** (tarifas, perfiles, transbordos, límites) con sus vigencias y su historial.
3. **Consolidar, conciliar y liquidar** por modo, ruta y operador, con trazabilidad completa y ajustes a periodos cerrados.
4. **Calcular el subsidio** a cobrar a la Alcaldía.
5. **Gestionar usuarios, tarjetas y perfiles**, incluidas las certificaciones de las instituciones y los vencimientos.
6. **Decidir y registrar los bloqueos y las listas**, con quién decidió y por qué.
7. **Consultar el historial completo** de una tarjeta para atender a un usuario.
8. **Gestionar ajustes y devoluciones** con aprobaciones según el monto.
9. **Cumplir la protección de datos:** autorizaciones, consultas, rectificaciones y supresión.
10. **Generar los reportes obligatorios** y los indicadores.
11. **Alertar sobre anomalías y posibles fraudes.**
12. **Conservar la información histórica** por los años que exijan las normas y los contratos, para soportar disputas.

**10.8 Restricciones**
- **Contrato vigente del proveedor:** los validadores, la plataforma de transacciones y los canales de recarga siguen con él al menos hasta su vencimiento. Jurídica está revisando las cláusulas sobre propiedad de la información y la entrega de datos.
- **Tecnología existente:** no se pueden cambiar los validadores ni las tarjetas VAMOS en circulación.
- **Presupuesto:** es público, con aprobación anual. Si el proyecto pasa de un año fiscal, necesita autorizaciones especiales. No tengo la cifra; eso lo manejan Finanzas y la Gerencia.
- **Contratación pública:** cualquier compra se rige por las normas de contratación estatal, y eso toma tiempo.
- **Normas:** protección de datos, PCI por medio del adquirente, reglas de la fiducia y reportes obligatorios.
- **Contratos de concesión y de fiducia:** las reglas de remuneración y la prelación de pagos no las cambia el software.
- **Plazos:** el fin de la administración y el vencimiento del contrato del proveedor.
- **Personas:** mi área es pequeña y no puede parar la operación para la implementación.
- **Continuidad:** la operación no se puede detener durante la transición.
- **Datos históricos:** su calidad es irregular.

**10.9 La meta más importante**
Que el ente gestor sepa con certeza, y pueda demostrar, **cuánto dinero entró, por qué, y a quién se le pagó**: control y trazabilidad del recaudo de punta a punta. Casi todo lo demás se desprende de ahí.

### Bloque 11, qué hace la organización

**11.1 Grandes funciones del ente gestor**
Así las vivimos:
- **Planear el sistema:** diseñar rutas y servicios, estudiar la demanda y planear la expansión, como nuevas troncales o la integración metropolitana.
- **Gestionar y controlar la operación:** programar los servicios, controlar en vía y en estaciones que se cumpla la programación, manejar incidentes y medir la calidad del servicio.
- **Gestionar las concesiones y convenios:** supervisar el cumplimiento de los operadores de flota, del metro y del proveedor de recaudo, y aplicar incentivos, descuentos y sanciones.
- **Recaudo y tarifas:** lo que les he contado en toda esta conversación.
- **Gestión financiera:** fiducia, presupuesto, subsidios, financiación del déficit, relación con Hacienda y con la Nación, y contabilidad.
- **Atención al usuario:** PQR, centros de atención, personalización de tarjetas e información al usuario.
- **Infraestructura:** desarrollar y mantener estaciones, portales, patios, carriles y paraderos, normalmente a través de contratos.
- **Comunicaciones y cultura ciudadana:** campañas, información de cambios y campañas contra la evasión.
- **Relación institucional:** con la Alcaldía, el Concejo, la autoridad de transporte, el Ministerio y los municipios vecinos.
- **Seguridad:** coordinación con la Policía.
- **Gestión jurídica y contractual.**
- **Tecnología.**
- **Gestión humana, administrativa y de compras.**
- **Control interno y relación con los entes de control.**

**11.2 Estratégicas, razón de ser y apoyo**
Esta es mi visión; otra área podría ponerlo un poco distinto.
- **Estratégicas:** planear el sistema, la política tarifaria y la sostenibilidad financiera, y la relación institucional, incluida la integración metropolitana. Ahí se define hacia dónde va el sistema.
- **Razón de ser:** que la gente se mueva bien y pague justo. Eso incluye gestionar y controlar la operación, gestionar las concesiones, la operación del recaudo y la atención al usuario.
- **Apoyo:** jurídica, gestión humana, administrativa y compras, tecnología, comunicaciones y control interno. La infraestructura la pondría también en apoyo para el día a día, aunque en los proyectos de expansión es estratégica.
Fíjese que Recaudo y Tarifas tiene un pie en cada lado. La **política tarifaria** es estratégica, mientras que **recaudar, conciliar y liquidar** es parte de la razón de ser.

**11.3 ¿Cuáles se verían afectadas o mejoradas?**
- **Recaudo y tarifas:** es la que más cambia.
- **Gestión financiera:** cierres más rápidos, cobro del subsidio mejor soportado, mejor control de cartera y cifras más confiables para la contabilidad.
- **Atención al usuario:** respuestas más rápidas y mejor información.
- **Gestión de concesiones:** la liquidación transparente mejora la relación con los operadores y la supervisión del proveedor de recaudo.
- **Gestión y control de la operación:** datos de validadores fuera de servicio y de posible evasión, y mejor coordinación en los cambios de ruta.
- **Planeación:** mejores datos de demanda.
- **Jurídica:** mejor cumplimiento en datos personales y evidencia para disputas.
- **Control interno y relación con los entes de control:** reportes más fáciles y respaldados.
También hay efectos de corto plazo que no son mejoras: carga de trabajo en la transición, capacitación, ajuste de procedimientos y una relación más tensa con el proveedor mientras se define su futuro.

**11.4 Cierre: lo que no me han preguntado**
Hay algunas cosas que yo no dejaría por fuera:
- **Los saldos de tarjetas inactivas.** Es plata que está en la fiducia y que, en términos prácticos, nadie va a usar. Qué se hace con ella todavía no se ha decidido.
- **La logística de las tarjetas físicas:** inventario, distribución a puntos de venta y tarjetas dañadas. Hoy la maneja el proveedor, pero si cambian las cosas alguien tiene que hacerla.
- **La remuneración de los canales de recarga** y sus comisiones, que también se concilian.
- **Las credenciales de servicio:** quién las tiene, quién las autoriza y cuándo se retiran. Hoy están poco controladas.
- **La contingencia:** qué hacemos si se cae la plataforma central un día completo. Hay un plan informal, pero no está escrito como debería.
- **El calendario:** los picos de enero y julio por perfiles y cambio de tarifa, y los cierres de mes. Ninguna implementación debería coincidir con esas fechas.
- **El histórico:** los contratos duran hasta 20 años y las disputas pueden llegar a tribunales de arbitramento. Hay que conservar y poder reconstruir información de muchos años atrás.
- **Temas en discusión que no están decididos:** tarifas diferenciales por horario, topes de gasto diario o semanal, que le darían al usuario un beneficio por viajar mucho, y la integración tarifaria metropolitana. No son reglas hoy, pero conviene que sepan que se están discutiendo.

Fue un gusto. Si necesitan profundizar en algún tema, sobre todo conciliación y liquidación, quedo a disposición. Para lo contable y lo jurídico, les recomiendo validar con Finanzas y Jurídica.

---
_Fin de la entrevista. La experta no propuso en ningún momento capacidades, dominios, agregados, contextos ni vistas; en dos ocasiones (R6.a y bloque 11) indicó explícitamente que eso le corresponde al equipo de arquitectura._

