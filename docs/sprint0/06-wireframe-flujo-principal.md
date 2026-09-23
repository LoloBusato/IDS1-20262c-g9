# Wireframe de Sprint 0 - flujo principal de Matrimillas

> Approach inicial de cómo se podría ver la interfaz. Obviamente va a variar en el tiempo

## Archivo

[Abrir el flujo mobile principal](https://www.figma.com/design/mz92G3vgpkBBqEI6f0NNon/Matrimillas?node-id=10-7) · [Abrir creación de grupo mobile](https://www.figma.com/design/mz92G3vgpkBBqEI6f0NNon/Matrimillas?node-id=46-117) · [Abrir la versión web de PC](https://www.figma.com/design/mz92G3vgpkBBqEI6f0NNon/Matrimillas?node-id=29-117)

En Figma, usar **Presentar** desde cualquiera de los tres puntos de inicio: flujo principal mobile, creación de grupo mobile o landing web. Los recorridos principales son clickeables; otros controles visibles son ilustrativos y todavía no tienen comportamiento prototipado. Las pantallas están organizadas en filas dentro de la misma página de Figma.

## Qué muestra

| Paso | Pantalla | Acción principal |
|---|---|---|
| 1 | Grupo Casa | Felipe ve el contexto del grupo y elige registrar una acción. |
| 2 | Catálogo | Elige «Cocinar» entre las acciones frecuentes. |
| 3 | Registro | Agrega contexto o evidencia opcional y envía la acción. |
| 4 | Pendiente | Los puntos aún no se acreditan; el prototipo cambia de actor. |
| 5 | Vista de Martina | Otra integrante revisa y aprueba la acción. |
| 6 | Vista de Felipe | Se acredita el movimiento y se actualiza el saldo. |

La secuencia sirve para explicar **registrar → esperar aprobación → acreditar → ver saldo**, no para definir todas las reglas del producto. El cambio de Felipe a Martina se hace mediante un botón de simulación para que una sola persona pueda recorrer ambas perspectivas.

## Trazabilidad con épicas e historias

Cada pantalla representa total o parcialmente historias ya incluidas en `05-epicas-e-historias.md`:

| Pantalla o momento | Épica | Historias relacionadas | Alcance representado |
|---|---|---|---|
| Landing pública | EP-01 · Gestión de Usuarios y Autenticación | MAT-01, MAT-02 | Relación indirecta: la landing sugiere el ingreso al producto, pero la demo omite registro y login. |
| Grupo Casa | EP-02 · Gestión de Grupos; EP-05 · Economía de Puntos | MAT-06, MAT-20 | Contexto del grupo y saldo individual. La lista completa de integrantes no está prototipada. |
| Catálogo | EP-03 · Catálogo de Acciones | MAT-10 | Selección de una acción predefinida y visualización de un valor ilustrativo. |
| Registro y evidencia | EP-04 · Registro y Aprobación de Acciones | MAT-15, MAT-16 | Registro de la acción y evidencia opcional. |
| Estado pendiente | EP-04 · Registro y Aprobación de Acciones | MAT-15, MAT-19 | Estado pendiente; el vencimiento automático no está prototipado. |
| Revisión de Martina | EP-04 · Registro y Aprobación de Acciones | MAT-17 | Aprobación por otra persona. Rechazo y otras políticas de aprobación quedan fuera del recorrido. |
| Saldo e historial | EP-05 · Economía de Puntos | MAT-20, MAT-21 | Actualización del saldo y un movimiento reciente. |

La creación y la invitación pertenecen a **EP-02 · Gestión de Grupos** y se relacionan principalmente con **MAT-04 · Crear un grupo**, **MAT-05 · Unirse a un grupo por código/link** y **MAT-06 · Ver integrantes del grupo**. También dependen de MAT-01/MAT-02 si se decide que solo una persona autenticada puede crear o aceptar una invitación. La rama de quien crea ya está dibujada en Figma; la rama de quien recibe una invitación sigue pendiente.

## Flujo mobile: crear e invitar a un grupo

El recorrido de quien crea está prototipado como una hipótesis para discutir; no es una decisión aprobada. Parte de una sesión ya iniciada para no mezclar MAT-01/MAT-02 con MAT-04.

| Paso | Pantalla mobile | Acción principal |
|---|---|---|
| C1 | Primer ingreso sin grupos | Elegir **Crear grupo**. **Unirme** es ilustrativo en este recorrido. |
| C2 | Nombre del grupo | Escribir un nombre reconocible y continuar. |
| C3 | Configuración inicial | Revisar valores predeterminados y continuar. |
| C4 | Revisión | Confirmar la creación. |
| C5 | Grupo creado e invitación | Ver link/código y entrar al grupo o posponer la invitación. |
| C6 | Inicio del grupo nuevo | Ver al creador como primer integrante y volver a la invitación. |

### Rama de quien crea

1. En el primer ingreso, la persona elige entre **Crear un grupo** y **Unirme con código o link**.
2. Para crear, informa un nombre y completa una configuración inicial breve. Conviene ofrecer valores predeterminados y permitir modificar opciones avanzadas después.
3. Al confirmar, el grupo se crea y la persona pasa a ser automáticamente su primer integrante.
4. Se muestra una pantalla de éxito con un link y un código que se pueden copiar o compartir, además de la opción **Invitar más tarde**.
5. La persona llega al inicio del grupo, donde puede volver a consultar sus integrantes y compartir una invitación.

### Rama de quien recibe una invitación - pendiente de prototipar

1. La persona abre el link o escribe el código desde **Unirme a un grupo**.
2. Si todavía no inició sesión, se conserva la invitación mientras se registra o ingresa.
3. Antes de incorporarla, se muestra una vista previa mínima: nombre del grupo, quién compartió la invitación y una confirmación explícita para unirse.
4. Con una invitación vigente, la persona se incorpora y llega al inicio del grupo. Con una invitación inválida, revocada o vencida, recibe un error accionable y puede ingresar otro código.

Para un primer corte, la alternativa más simple es que un link o código vigente permita ingresar luego de la confirmación, sin una segunda aprobación del grupo.

### Decisiones a discutir que surgen después de ver el modelo

- quiénes pueden generar o revocar invitaciones;
- si la invitación vence, es de un solo uso o admite varios ingresos;
- qué configuración inicial se solicita y cuáles son sus valores predeterminados;
- si el creador obtiene algún rol interno especial o solo es el primer integrante;
- qué información del grupo puede ver una persona antes de unirse;
- si el ingreso genera notificaciones y cuál es el saldo inicial;
- si una persona puede pertenecer a varios grupos y cómo cambia entre ellos.

El backlog actual agrega expiración, saldo inicial en cero y notificación al grupo dentro de MAT-05, las cuales son decisiones razonables.

## Versión web de PC

El wireframe desktop explora cómo podría comenzar una experiencia web, además del flujo interno ya representado en mobile. La primera pantalla es una **landing pública** que explica la propuesta y ofrece «Explorar demo». Ese botón entra directamente al grupo ficticio «Casa»: no implica que el registro, el onboarding o las invitaciones estén diseñados.

| Paso | Pantalla web | Acción clickeable |
|---|---|---|
| 1 | Landing pública | Explorar demo. |
| 2 | Grupo y catálogo | Elegir «Cocinar». |
| 3 | Registrar acción | Enviar para aprobación. |
| 4 | Acción pendiente | Ver la perspectiva de Martina. |
| 5 | Martina aprueba | Aprobar acción. |
| 6 | Saldo actualizado | Volver al grupo. |

Cada marco mide 1280 × 800 px. La versión web aprovecha el ancho para mostrar catálogo, saldo y contexto de aprobación en columnas; no reemplaza ni modifica los wireframes mobile. Es una exploración de plataforma, no una decisión del equipo de desarrollar web, mobile o ambas.

## Supuestos representados para poder probar el flujo

- Se muestra una experiencia mobile de 390 × 844 px y una web desktop de 1280 × 800 px.
- El flujo principal parte de un grupo ya creado; el flujo adicional representa cómo lo crea una persona que ya inició sesión. El registro/login y la aceptación de una invitación siguen fuera del prototipo.
- El ejemplo usa una aprobación por otro integrante antes de acreditar puntos. **La cantidad y política de aprobaciones siguen siendo hipótesis**, no una regla acordada.
- Se presenta evidencia fotográfica como opcional para esta acción. Hay que validar cuándo sería necesaria o incómoda y si se configura por grupo o tipo de acción.
- «Cocinar» vale 20 puntos en el ejemplo y el saldo cambia de 120 a 140. Esos números son únicamente datos ficticios para hacer visible el efecto; no se propone fijarlos como valores del catálogo.
- El catálogo, los textos y los nombres son material de simulación. No representan resultados de entrevistas ni una decisión final del equipo.
