# Trabajo Practico - 2do Cuatrimestre 2026

## Ingenieria del Software I - FIUBA

### Tema: Matrimillas - Economia de puntos entre personas

---

## Matrimillas: Economia de puntos entre personas

**Matrimillas** es una aplicacion pensada para parejas, familias o grupos de amigos que buscan repartir de forma mas transparente la carga de tareas cotidianas. Su funcionamiento se basa en una **economia de puntos** --las "**matrimillas**"--, donde algunas acciones acreditan puntos (cortar el pasto suma 5, por ejemplo) y otras los consumen (salir con amigos cuesta 50). La plataforma ofrece un catalogo de acciones predefinido, que cada grupo puede ampliar con sus propias acciones custom segun su dinamica particular.

El valor de cada accion no es fijo, sino que se define por votacion de todos los usuarios de la plataforma: se promedia lo que vota cada uno y se actualiza cada hora, de forma similar a la cotizacion de una accion bursatil. Sobre ese valor base pueden aplicarse ademas modificadores variables segun el contexto --por ejemplo, que salir a comer valga 10 en general, 5 un viernes y 20 un lunes--. A esto se suma un sistema de transferencias entre usuarios, prestamos, intereses, historial de movimientos, limites y estadisticas de uso.

Para que una accion acredite puntos, quien la realiza debe subir una evidencia (una foto, por ejemplo) que el resto del grupo tiene que aprobar. Es a partir de esta validacion que se despliega el resto de las reglas de negocio, dandole cuerpo y complejidad a la solucion.

---

## Modalidad de Trabajo

Se organizaran en grupos de **6 alumnos**. Trabajaremos dentro del marco **Scrum**, con sprints de 2 semanas. La duracion total del desarrollo sera de 9 semanas: un "sprint 0" de una semana + 4 sprints de 2 semanas.

Durante el sprint 0, todos los miembros del equipo se encargaran de entender el problema mediante herramientas de **product discovery**.

Luego, durante cada sprint, los miembros del grupo deberan rotar entre los siguientes roles:

### Product Owner (PO)
- Refina el backlog: arma historias de usuario y criterios de aceptacion.
- Prioriza historias para el sprint con input del equipo.

### Scrum Master (SM)
- Facilita y lleva a cabo las reuniones: planning, daily, retro.
- Se asegura de que se cumpla el proceso (definition of done, flujo de git, etc.).

### Desarrollador
- Implementa las funcionalidades del sprint, aplicando clean code y la arquitectura definida.

### Tester / QA
- Redacta y ejecuta casos de prueba segun criterios de aceptacion.
- Ejecuta pruebas manuales y automaticas antes de hacer merge.
- Reporta bugs como issues en Jira.
- Verifica la correccion de bugs.

**Aclaraciones:** Todos los miembros del equipo deben desarrollar en todos los sprints, independientemente del rol que tengan. Una misma persona no puede repetir 2 veces el mismo rol durante el tp, a excepcion del rol "desarrollador".

**Ejemplo:**
- Valido: Dev, PO, QA, Dev
- Invalido: PO, Dev, PO, SM

---

## Objetivos

- Validar correctamente el problema en el sprint 0.
- Crear un proyecto en Jira para trabajar en grupo.
- Cargar todas las historias en Jira y estimarlas en story points usando planning poker.
- Armar Documento de Arquitectura preliminar basado en 4+1 y definir atributos de calidad.
- Definir junto al ayudante el alcance a implementar, MVP o Early Testable Product, para trabajar en 4 sprints de 2 semanas.
- Definir flow a utilizar y forma de trabajo en grupo.
- Implementar una version de la API con persistencia en base de datos, basada en el template.
- Armar una coleccion de Postman o Swagger con las invocaciones a cada endpoint de la API.
- Cubrir el 80% del codigo del backend con tests automatizados.
- Modelar e implementar el sistema que sea configurable y facilmente extensible.
- Implementar una UI muy basica que permita usar el sistema.
- Aplicar las tecnicas vistas en la teoria y en la practica.
- Realizar entrega de aceptacion TP con demo a acordar con el ayudante.

---

## Reglas de negocio

Estas reglas de negocio son de caracter obligatorio: cada grupo debe elegir e implementar **15** de esta lista, a su criterio, segun lo que mejor se adapte a su solucion. Cuantas mas reglas de esta lista implementen **mejor se pondera en la nota final**.

Ademas, el grupo puede incorporar **reglas de negocio propias**, surgidas de investigacion propia o de decisiones de diseno que consideren relevantes para el problema. Estas **tambien suman a la evaluacion**, siempre que queden debidamente detalladas y justificadas en el informe final.

### Calculo y valuacion de acciones

- **Motor de reglas combinables**: el valor final de una accion no depende solo del valor base, sino de una serie de reglas contextuales que se van aplicando en cadena (dia de la semana, feriado, urgencia declarada por quien pide la accion, racha del grupo, etc.), cada una sumando o multiplicando sobre el resultado de la anterior.
- **Congelamiento de valor**: durante los ultimos 5 minutos de cada hora, la cotizacion de una accion no puede modificarse, para evitar que se manipule justo antes del cierre de la votacion horaria. Cuando se cumple la hora, se recalcula el valor con lo votado y se vuelve abrir para el siguiente ciclo.
- **Combos**: se otorga un bonus adicional cuando se completan varias acciones relacionadas dentro de la misma semana.
- **Bonus por fecha especial**: en fechas puntuales que el grupo defina (cumpleanos, aniversario, feriado especial), ciertas acciones valen un plus fijo sobre su valor habitual.

### Evidencia y aprobacion

- **No autoaprobacion**: quien sube la evidencia de una accion no puede ser quien la aprueba.
- **Aprobacion configurable**: cada grupo define como se aprueba una accion -- alcanza con que la apruebe una sola persona, tienen que estar de acuerdo todos, o decide un "arbitro" que va rotando entre los miembros.
- **Revision ante rechazo**: si una accion es rechazada, se puede pedir que la revise otro integrante del grupo antes de descartar definitivamente.
- **Vencimiento automatico**: una accion pendiente de aprobacion por mas de N dias queda "expirada" -- no acredita puntos ni se rechaza, queda en un estado propio.
- **Tipo de evidencia configurable por accion**: cada accion (del catalogo o custom) define que tipo(s) de evidencia acepta (foto, video, comprobante, ubicacion, ninguna) y si es obligatoria u opcional. Por ejemplo, se podria exigir evidencia obligatoria **solo a partir de cierto valor en puntos**, y dejar las acciones chicas bajo sistema de honor.
- **Plazo de carga de evidencia**: la evidencia debe subirse dentro de un plazo determinado desde que se marca la accion como realizada; pasado ese plazo, la accion no puede acreditarse.
- **Penalizacion por rechazos reiterados**: si a un usuario le rechazan varias evidencias seguidas en un periodo corto, queda temporalmente "bajo revision" (por ejemplo, requiere doble aprobacion hasta recuperar confianza).

### Uso y limites de acciones

- **Cooldown**: una accion no puede acreditarse mas de N veces por dia o por semana, para evitar que se convierta en una fuente ilimitada de puntos.
- **Ciclo de vida de acciones custom**: si una accion custom no se usa durante un periodo de tiempo determinado, se archiva y deja de participar de la votacion global de valores.
- **Acciones colaborativas**: una accion puede requerir la participacion de 2 o mas personas para acreditarse, repartiendo los puntos entre quienes efectivamente colaboraron.

### Economia y saldos

- **Limite de saldo negativo**: existe un tope maximo de puntos que un usuario puede deber.
- **Vencimiento de puntos**: los puntos acumulados y no utilizados caducan luego de un periodo determinado, para incentivar su uso.
- **Conversion entre economias de distintos grupos**: si un usuario pertenece a mas de un grupo, puede convertir matrimillas entre ambos segun una tasa de cambio propia de cada par de grupos.
- **Marketplace de acciones custom entre grupos**: un grupo puede licenciar una accion custom que creo a otro grupo, cobrando una comision cada vez que ese otro grupo la usa. Implica manejar la propiedad de la accion, tasas de comision y liquidacion entre grupos.

### Engagement y experiencia de grupo

- **Favoritos**: cada usuario puede marcar acciones de uso frecuente para registrarlas mas rapido, sin afectar las reglas de negocio en si.
- **Ranking del grupo**: los integrantes pueden ver un leaderboard con el saldo de puntos de cada uno dentro del grupo.

### Roles y administracion

- **Rol de administrador**: un rol de administrador a nivel plataforma, separado de los roles internos de cada grupo (arbitro, aprobador, etc). No pertenece a ningun grupo en particular, sino que opera sobre el sistema.
- **Suspension/reactivacion de usuarios**: el administrador puede suspender o reactivar la cuenta de un usuario (por ejemplo, ante uso indebido o reportes de otros usuarios), bloqueando temporalmente su capacidad de operar en la plataforma.
- **Estadisticas globales**: el administrador puede consultar estadisticas agregadas de uso de la plataforma (grupos activos, acciones mas usadas, volumen de puntos en circulacion, etc.), sin acceder al detalle de movimientos privados de cada grupo.
- **Auditoria de acciones administrativas**: toda accion que realice un administrador (suspender un usuario, modificar el catalogo, etc.) queda registrada en un log auditable, indicando quien la hizo y cuando.

### Ciclo de vida del grupo

- **Invitacion por link o codigo**: para sumarse a un grupo, un usuario necesita un link de invitacion o un codigo que le comparta alguien que ya pertenezca a ese grupo; no hay alta libre a un grupo existente.
- **Creacion de un grupo**: cualquier usuario puede crear un grupo nuevo, convirtiendose automaticamente en su primer integrante y definiendo la configuracion inicial.
- **Salida de un grupo**: un integrante puede abandonar un grupo voluntariamente; hay que definir que pasa con su saldo.
- **Disolucion de un grupo**: si el grupo se disuelve (o queda sin integrantes), hay que definir que pasa con los saldos pendientes de cada uno y con las acciones custom que ese grupo haya creado.
- **Expulsion de un integrante**: el grupo puede remover a un integrante (por votacion o decision del arbitro), con las mismas consideraciones de saldo que la salida voluntaria.

### Notificaciones

- **Notificacion de aprobacion/rechazo**: cuando se aprueba o rechaza una accion, la persona que subio la evidencia recibe una notificacion con el resultado.
- **Notificacion de solicitud de aprobacion**: cuando alguien sube evidencia que requiere aprobacion, se notifica a quien tiene que aprobar.
- **Resumen periodico del grupo**: cada integrante recibe un resumen con la actividad del grupo, acciones, ranking, y cambios de cotizacion.
- **Recordatorio de evidencia pendiente**: si una accion le queda poco tiempo antes de vencer su plazo de carga de evidencia, se notifica a quien la marco como realizada.
- **Alerta de saldo negativo**: cuando el saldo de un usuario se acerca al limite maximo de deuda permitido, el sistema le envia un aviso.

---

## Herramientas a utilizar / Restricciones

- Jira
- Java
- Unit testing
- Git / GitLab
- Docker / Docker-Compose
- Auth: Para consumir la API, el cliente debera autenticarse primero para obtener un JWT, que luego enviara como token en las llamadas siguientes.

---

## Entorno

Se debera desarrollar el trabajo practico sobre la base entregada por la catedra. Los desarrollos realizados deberan pasar el pipeline de CI/CD.

Cada grupo tendra asignada una URL del tipo `https://grupo-xx.tp1.ingsoft1.fiuba.ar/`

---

## Cronograma

| Sprint | Periodo | Evento |
|--------|---------|--------|
| Sprint 0 | 14-sep al 21-sep | Revision de avance: 21-sep |
| Sprint 1 | 21-sep al 7-oct | Demo sprint 1: 7-oct |
| Sprint 2 | 7-oct al 21-oct | Demo sprint 2: 21-oct |
| Sprint 3 | 21-oct al 4-nov | Demo sprint 3: 4-nov |
| Sprint 4 | 4-nov al 18-nov | Demo sprint 4: 18-nov |
| Demo final | - | Aceptacion TP: 25-nov o 30-nov |

---

## Entregables

### Sprint 0

- Resultados de las entrevistas.
- Mapas de empatia de las personas afectadas por el problema.
- User personas de las personas afectadas por el problema.
- Conclusiones sobre el problema relevado y propuesta de solucion.
- Primeras epicas e historias de usuario, a grandes rasgos. Tablero de Jira armado y listo para trabajar.
- (Opcional) Alguna idea sobre como se ve la solucion propuesta. Wireframes, flujos, etc.

### Cada sprint

#### Product Owner

| Entregable | Donde queda | Se corrige verificando que... |
|-----------|-------------|-------------------------------|
| Meta del sprint | Jira | Sea una oracion concreta y todas las historias del sprint aporten a ella. |
| Historias de usuario del sprint | Jira | Sigan el formato "Como... quiero... para...", tengan criterios de aceptacion claros, estimacion en story points y responsables asignados. |
| Backlog priorizado | Jira | El orden refleje prioridad real (no orden de carga) y las epicas esten vinculadas a sus historias. |
| Registro de cambios de alcance | Documentacion del grupo | Este escrito que se saco o agrego respecto de lo planificado y por que. |

*Recuerde que el PO tambien es desarrollador*

#### Scrum Master

| Entregable | Donde queda | Se corrige verificando que... |
|-----------|-------------|-------------------------------|
| Acta de planning | Documentacion del grupo (una por sprint) | Incluya fecha, asistentes, meta acordada, historias comprometidas y capacidad estimada. |
| Registro de dailies | Documentacion del grupo | Haya un registro breve de cada daily con los bloqueos identificados. |
| Registro de impedimentos | Documentacion del grupo | Cada impedimento tenga fecha de deteccion, responsable y fecha de resolucion (o estado abierto). |
| Burndown del sprint | Documentacion del grupo (uno por sprint) | Exista, sea consistente con el tablero y el SM pueda explicar los desvios. |
| Team velocity | Documentacion del grupo | |
| Retrospectiva | Documentacion del grupo (una por sprint) | Tenga acciones de mejora concretas con responsable, y una verificacion explicita de si se cumplieron las acciones del sprint anterior. |
| Cumplimiento del proceso | Repositorio | Los PRs respeten el flujo de Git acordado y la definition of done que el equipo definio. |

*Recuerde que el SM tambien es desarrollador*

#### Desarrollador

| Entregable | Donde queda | Se corrige verificando que... |
|-----------|-------------|-------------------------------|
| Commits | GitLab | Sean atomicos, con mensaje descriptivo y referencien la historia de Jira (ej. MAT-12: ...). |
| Pull requests | GitLab | Cada PR corresponda a una historia, tenga descripcion, pase el pipeline y tenga al menos una revision aprobada de otro integrante. |
| Funcionalidad en produccion | URL del grupo | Todo lo marcado como "Done" en Jira este desplegado y funcione en la demo. |
| Decisiones de diseno documentadas | Repositorio (ADRs o seccion del README) | Toda decision relevante (patron aplicado, cambio de arquitectura) tiene un registro corto: contexto, decision, alternativas descartadas. |

#### Tester / QA

| Entregable | Donde queda | Se corrige verificando que... |
|-----------|-------------|-------------------------------|
| Casos de prueba | Documentacion del grupo o Jira | Cada historia del sprint tenga sus casos, trazables a los criterios de aceptacion. |
| Tests automatizados | Repositorio | Cada historia "Done" tenga tests que la respalden y el coverage del backend se mantenga o suba respecto del sprint anterior. |
| Reporte de ejecucion | Documentacion del grupo (uno por sprint) | Indique que casos se ejecutaron, con que resultado, y el coverage al cierre del sprint. |
| Bugs reportados | Jira | Tengan pasos para reproducir, resultado esperado vs. obtenido y severidad. |

*Recuerde que el Tester tambien es desarrollador*

#### Equipo en conjunto

| Entregable | Donde queda | Se corrige verificando que... |
|-----------|-------------|-------------------------------|
| Incremento del producto | Ambiente de produccion | Todo lo demostrado corra sobre la URL del grupo, no en branches ni ambientes locales. |
| Demo | Fecha del cronograma | Cualquier integrante pueda presentar y responder preguntas sobre cualquier parte del trabajo. |
| README actualizado | Repositorio | Permita levantar el proyecto localmente siguiendo solo las instrucciones, e indique donde esta la documentacion del grupo. |

---

## Final del TP

- Informe final con:
  - Analisis del problema: Todo el relevamiento del sprint 0.
  - Arquitectura: basada en 4+1 y atributos de calidad.
  - Modalidad de trabajo, flow a usar para los commits.
  - Documentacion que fueron generando en los sprints (reuniones, metricas, velocidad del equipo).
  - Post-mortem (cosas a mejorar, potenciales adiciones, etc).
  - Conclusiones: Hablar un poco de algunas decisiones de diseno (porque hicimos tal cosa asi y no de otra forma, porque decidimos que esto es lo mejor, etc).
- Trabajo finalizado (basado en lo acordado con cada ayudante), desplegado en ambiente de produccion.

---

## Criterios de correccion

### Sprint 0
- Asistencia obligatoria para la revision de avance al final del sprint 0.
- Cada integrante del equipo debe contribuir al product discovery. Se haran preguntas individuales y se evaluaran sus respuestas.

### Cada sprint
- La asistencia a demos/reviews es obligatoria para todos los integrantes del grupo. Maximo una falta sobre el total de 4 demos.
- Cada demo debe ser presentada sobre el ambiente de produccion. No se aceptan funcionalidades dispersas sobre diferentes branches o ambientes.
- Cada integrante del equipo debe contribuir al progreso del trabajo practico. Se haran preguntas individuales y se evaluaran los entregables segun el rol correspondiente.
- Cada integrante del equipo debe poder presentar en las demos y estar al tanto del estado del trabajo practico.
- **Jira:**
  - Todas las historias deben estar bien definidas, tener criterios de aceptacion claros, estimacion y asignacion a un responsable.
  - El tablero debe reflejar el estado real del trabajo en todo momento.
- **Codigo:**
  - Se deben aplicar buenas practicas de codigo limpio y principios SOLID.
  - Donde corresponda, aplicar patrones de diseno.
  - Los commits deben ser atomicos y con mensajes descriptivos.
- **Tests:**
  - Toda funcionalidad completa debe tener tests que la respalden.
- **Documentacion:**
  - El README debe estar actualizado e incluir instrucciones para levantar el proyecto localmente.
  - Se deben documentar las decisiones arquitectonicas relevantes.
