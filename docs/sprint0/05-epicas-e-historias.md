# Epicas e Historias de Usuario Iniciales - Sprint 0

Estas epicas e historias de usuario fueron construidas a partir de las 8 entrevistas realizadas (Martina, Lucas, Sofia, Nicolas, Tomas, Roberto, Camila, Marta), los 6 mapas de empatia y las 9 user personas. Son a grandes rasgos, para cargar en Jira y refinar durante las plannings. Las estimaciones en story points se definiran via planning poker.

Cada historia indica entre parentesis el entrevistado o user persona que la origino, para trazabilidad.

---

## EP-01: Gestion de Usuarios y Autenticacion

> Como usuario, quiero poder registrarme, iniciar sesion y gestionar mi cuenta para usar la plataforma de forma segura.

### Historias de usuario

**MAT-01: Registro de usuario**
- Como visitante, quiero registrarme con email y contrasena para crear mi cuenta en Matrimillas.
- Criterios de aceptacion:
  - El sistema valida formato de email y longitud minima de contrasena.
  - No se permite registrar un email ya existente.
  - Al registrarse, la cuenta queda activa (o requiere verificacion segun config).
- Origen: Todos los perfiles.

**MAT-02: Login de usuario**
- Como usuario registrado, quiero iniciar sesion con mis credenciales para acceder a mi cuenta.
- Criterios de aceptacion:
  - Se retorna un JWT valido al autenticarse correctamente.
  - Se muestra error claro si las credenciales son incorrectas.
  - El token tiene un tiempo de expiracion configurable.
- Origen: Restriccion tecnica de la catedra (JWT).

**MAT-03: Ver y editar perfil**
- Como usuario, quiero ver y editar mi perfil (nombre, foto) para personalizar mi cuenta.
- Criterios de aceptacion:
  - Se puede cambiar nombre y foto de perfil.
  - Los cambios se reflejan en todos los grupos donde participa.
- Origen: Todos los perfiles.

---

## EP-02: Gestion de Grupos

> Como usuario, quiero crear, unirme y gestionar grupos para organizar las tareas con las personas con las que convivo o comparto espacio.

### Historias de usuario

**MAT-04: Crear un grupo**
- Como usuario, quiero crear un grupo nuevo para empezar a usar Matrimillas con mi pareja/amigos/familia/companeros.
- Criterios de aceptacion:
  - Se define nombre del grupo y configuracion inicial (tipo de aprobacion, limites).
  - El creador queda automaticamente como primer integrante.
  - Se genera un codigo/link de invitacion.
- Origen: Todos los perfiles. Camila: "un grupo de oficina".

**MAT-05: Unirse a un grupo por codigo/link**
- Como usuario, quiero unirme a un grupo existente usando un codigo o link de invitacion para participar.
- Criterios de aceptacion:
  - El codigo/link debe ser valido y no estar expirado.
  - Al unirse, el usuario aparece como integrante activo con saldo en 0.
  - Se notifica al grupo que se sumo alguien nuevo.
- Origen: Regla de negocio #15 (Invitacion por link o codigo).

**MAT-06: Ver integrantes del grupo**
- Como integrante de un grupo, quiero ver la lista de miembros para saber quienes participan.
- Criterios de aceptacion:
  - Se muestra nombre, foto y saldo de cada integrante.
  - Se distingue visualmente al creador del grupo.
- Origen: Lucas, Roberto: "quiero ver como estamos todos".

**MAT-07: Salir de un grupo**
- Como integrante, quiero poder abandonar un grupo voluntariamente.
- Criterios de aceptacion:
  - Se pide confirmacion antes de salir.
  - Si el saldo es negativo, se requiere saldar la deuda o se registra como deuda pendiente.
  - Si el saldo es positivo, los puntos se pierden (o se define politica del grupo).
  - El resto del grupo es notificado.
  - Las acciones pendientes del usuario se cancelan.
- Origen: Roberto: "mis hijos podrian irse en algun momento". Regla de negocio (Salida de un grupo).

**MAT-08: Expulsar a un integrante**
- Como grupo, quiero poder remover a un integrante por votacion para mantener la dinamica sana.
- Criterios de aceptacion:
  - Se inicia una votacion de expulsion.
  - Si la mayoria aprueba, el integrante es removido.
  - Se aplican las mismas reglas de saldo que en la salida voluntaria.
  - El usuario expulsado es notificado.
- Origen: Regla de negocio (Expulsion de un integrante). Lucas: "hay uno que no hace nada".

**MAT-09: Disolver un grupo**
- Como ultimo integrante de un grupo, quiero poder disolverlo cuando ya no tiene sentido.
- Criterios de aceptacion:
  - Si queda un solo integrante, puede disolver el grupo.
  - Los saldos se cancelan.
  - Las acciones custom del grupo se archivan.
- Origen: Regla de negocio (Disolucion de un grupo).

---

## EP-03: Catalogo de Acciones

> Como usuario, quiero poder ver, votar y crear acciones para definir que actividades suman o restan puntos en mi grupo.

### Historias de usuario

**MAT-10: Ver catalogo de acciones predefinidas**
- Como integrante de un grupo, quiero ver las acciones disponibles en el catalogo para saber que puedo registrar.
- Criterios de aceptacion:
  - Se muestra nombre, descripcion, valor actual y tipo (suma/resta puntos).
  - Se puede filtrar y buscar por nombre.
  - El catalogo incluye categorias: limpieza, cocina, compras, organizacion/gestion, cuidado de personas.
- Origen: Todos. Marta/Sofia/Camila: las tareas de cuidado y gestion deben estar.

**MAT-11: Votar el valor de una accion**
- Como usuario, quiero votar cuanto creo que vale una accion para influir en su cotizacion.
- Criterios de aceptacion:
  - Cada usuario puede emitir un voto por accion (valor numerico).
  - No se puede votar durante los ultimos 5 minutos de cada hora (congelamiento).
  - Al cumplirse la hora, el valor se recalcula como promedio de los votos.
- Origen: Lucas: "no deberia valer lo mismo sacar la basura que limpiar todo". Sofia: "el valor depende de la situacion".

**MAT-12: Crear accion custom del grupo**
- Como integrante, quiero proponer una accion custom para adaptar el catalogo a la dinamica de mi grupo.
- Criterios de aceptacion:
  - Se define nombre, descripcion, tipo de evidencia requerida y categoria.
  - La accion queda disponible solo para el grupo que la creo.
  - Participa de la votacion global de valores.
- Origen: Lucas: "hay cosas especificas que solo nosotros hacemos". Camila: "reponer insumos de la oficina".

**MAT-13: Marcar acciones como favoritas**
- Como usuario, quiero marcar acciones frecuentes como favoritas para acceder a ellas mas rapido.
- Criterios de aceptacion:
  - Se muestra una seccion de favoritos al inicio.
  - Se puede agregar/quitar de favoritos con un toque.
- Origen: Marta: necesita flujo minimo. Sofia/Martina: la rapidez de registro es critica para la adopcion.

**MAT-14: Ciclo de vida de acciones custom**
- Como sistema, quiero archivar acciones custom que no se usan para mantener el catalogo limpio.
- Criterios de aceptacion:
  - Si una accion custom no se usa en N dias (configurable), se archiva automaticamente.
  - La accion archivada deja de participar en la votacion global.
  - Se puede reactivar manualmente.
- Origen: Regla de negocio (Ciclo de vida de acciones custom).

---

## EP-04: Registro y Aprobacion de Acciones

> Como usuario, quiero registrar acciones realizadas y que sean aprobadas por el grupo para que se acrediten los puntos.

### Historias de usuario

**MAT-15: Registrar una accion realizada**
- Como integrante, quiero registrar que realice una accion para que se me acrediten los puntos correspondientes.
- Criterios de aceptacion:
  - Se selecciona la accion del catalogo (o de favoritos).
  - Se sube la evidencia si es requerida segun la configuracion de la accion.
  - La accion queda en estado "pendiente de aprobacion".
  - El registro debe poder hacerse en menos de 3 toques desde favoritos.
- Origen: Todos. Martina/Sofia/Camila: "si registrar lleva mucho tiempo, la dejo de usar".

**MAT-16: Subir evidencia de una accion**
- Como integrante, quiero subir evidencia de que realice la accion, segun lo que la accion requiera.
- Criterios de aceptacion:
  - Se acepta el tipo de evidencia configurado (foto, video, comprobante, ubicacion, ninguna).
  - Para acciones de bajo valor, la evidencia puede ser opcional ("sistema de honor").
  - La evidencia debe subirse dentro del plazo establecido; pasado el plazo, la accion no puede acreditarse.
- Origen: Martina: "para tareas chicas no quiero foto". Tomas: "una foto esta bien, es hasta divertido". Marta: "en familia con confianza alcanza".

**MAT-17: Aprobar o rechazar una accion**
- Como integrante del grupo, quiero aprobar o rechazar la accion de otro para validar que fue realizada.
- Criterios de aceptacion:
  - No se puede autoaprobar (quien sube no puede aprobar).
  - Se respeta el tipo de aprobacion configurado por el grupo (una persona, todos, arbitro rotativo).
  - Al aprobarse, se acreditan los puntos al valor vigente en ese momento.
  - Al rechazarse, se puede pedir revision a otro integrante.
- Origen: Reglas de negocio #5, #6. Tomas: "mi hermana no puede aprobarse sola".

**MAT-18: Penalizacion por rechazos reiterados**
- Como sistema, quiero que un usuario con multiples rechazos recientes quede "bajo revision" temporalmente.
- Criterios de aceptacion:
  - Si un usuario acumula N rechazos en un periodo, sus siguientes acciones requieren doble aprobacion.
  - El estado "bajo revision" se levanta automaticamente despues de M dias sin rechazos.
  - Se notifica al usuario que entro en este estado.
- Origen: Regla de negocio (Penalizacion por rechazos reiterados).

**MAT-19: Vencimiento automatico de acciones pendientes**
- Como sistema, quiero que las acciones pendientes de aprobacion por mas de N dias expiren automaticamente.
- Criterios de aceptacion:
  - Pasado el plazo configurado, la accion pasa a estado "expirada".
  - No acredita ni descuenta puntos.
  - Se notifica al usuario que la registro.
- Origen: Regla de negocio #7. Nadie quiere pendientes eternos.

---

## EP-05: Economia de Puntos

> Como usuario, quiero ver mi saldo, el historial de movimientos y el ranking del grupo para tener visibilidad de mi contribucion.

### Historias de usuario

**MAT-20: Ver saldo de puntos**
- Como integrante, quiero ver mi saldo actual de matrimillas para saber cuantos puntos tengo disponibles.
- Criterios de aceptacion:
  - Se muestra el saldo total.
  - Se indica visualmente si estoy cerca del limite de saldo negativo.
- Origen: Nicolas: "seria una forma rapida de saber como estoy". Todos.

**MAT-21: Ver historial de movimientos**
- Como integrante, quiero ver el historial de mis acreditaciones y debitos para entender como se compone mi saldo.
- Criterios de aceptacion:
  - Se muestra fecha, accion, puntos, estado y quien aprobo/rechazo.
  - Se puede filtrar por periodo y por tipo (acreditacion/debito).
- Origen: Todos. Marta: "que se vea lo que hice".

**MAT-22: Ver ranking del grupo**
- Como integrante, quiero ver un leaderboard con los saldos de todos para tener visibilidad de la situacion del grupo.
- Criterios de aceptacion:
  - Se ordena por saldo de mayor a menor.
  - Se muestra nombre, foto y saldo de cada integrante.
  - Se destaca visualmente mi posicion.
- Origen: Lucas, Nicolas, Tomas: lo pidieron explicitamente. Roberto: "que los numeros hablen solos".

**MAT-23: Limite de saldo negativo**
- Como sistema, quiero impedir que un usuario supere el tope de deuda para mantener la economia equilibrada.
- Criterios de aceptacion:
  - Al intentar una accion que llevaria el saldo por debajo del limite configurado, se rechaza.
  - Se envia alerta cuando el saldo se acerca al limite (ej: al 80%).
- Origen: Regla de negocio #12.

---

## EP-06: Motor de Reglas y Valuacion

> Como sistema, quiero aplicar reglas contextuales al valor de las acciones para que reflejen el esfuerzo real segun el contexto.

### Historias de usuario

**MAT-24: Aplicar modificadores por dia de la semana**
- Como sistema, quiero que el valor de ciertas acciones varie segun el dia para reflejar el esfuerzo contextual.
- Criterios de aceptacion:
  - Se pueden configurar multiplicadores por dia de la semana para cada accion.
  - El modificador se aplica sobre el valor base votado.
  - El usuario puede ver el valor modificado antes de registrar.
- Origen: Consigna: "que salir a comer valga 10 en general, 5 un viernes y 20 un lunes". Sofia: "una misma tarea puede ser mas complicada segun la situacion".

**MAT-25: Aplicar bonus por fecha especial**
- Como integrante, quiero que en fechas especiales las acciones valgan mas para reconocer el esfuerzo extra.
- Criterios de aceptacion:
  - El grupo puede definir fechas especiales (cumpleanos, aniversario, feriados).
  - Se aplica un plus fijo configurable sobre el valor habitual.
  - Se muestra visualmente que una fecha especial esta activa.
- Origen: Regla de negocio #4. Roberto: "en Navidad todo lleva el doble de esfuerzo".

**MAT-26: Congelamiento de valor**
- Como sistema, quiero congelar la cotizacion durante los ultimos 5 minutos de cada hora para evitar manipulacion.
- Criterios de aceptacion:
  - Durante los ultimos 5 minutos de cada hora, no se aceptan votos nuevos.
  - Al cumplirse la hora, se recalcula el valor con los votos existentes.
  - Se muestra indicador de "votacion cerrada" cuando esta congelado.
- Origen: Regla de negocio #2.

**MAT-27: Sistema de combos**
- Como integrante, quiero recibir un bonus cuando completo varias acciones relacionadas en la misma semana.
- Criterios de aceptacion:
  - Se definen grupos de acciones que forman un combo (ej: "limpieza completa" = bano + cocina + pisos).
  - Al completar todas las acciones del combo en una semana, se otorga un bonus adicional.
  - Se muestra progreso del combo en la UI.
- Origen: Regla de negocio #3. Tomas: motivacion por logros/rachas.

**MAT-28: Cooldown de acciones**
- Como sistema, quiero limitar cuantas veces se puede acreditar una accion por dia/semana para evitar abusos.
- Criterios de aceptacion:
  - Cada accion tiene un cooldown configurable (N veces por dia o por semana).
  - Al alcanzar el limite, el usuario ve un mensaje indicando cuando podra registrar nuevamente.
- Origen: Regla de negocio #10. Sin esto, se podria registrar "barrer" 20 veces por dia.

---

## EP-07: Acciones Colaborativas

> Como usuario, quiero poder registrar acciones realizadas en equipo para repartir los puntos equitativamente.

### Historias de usuario

**MAT-29: Registrar accion colaborativa**
- Como integrante, quiero registrar una accion que hicimos entre varios para repartir los puntos.
- Criterios de aceptacion:
  - Se seleccionan los participantes de la accion.
  - Los puntos se dividen equitativamente entre los participantes.
  - Cada participante debe confirmar su participacion antes de que se acrediten.
  - Si un participante no confirma en N dias, se acredita solo a quienes confirmaron.
- Origen: Regla de negocio #11. Tomas: "limpiamos el jardin entre los dos". Lucas: tareas que hacen juntos.

---

## EP-08: Notificaciones

> Como usuario, quiero recibir notificaciones sobre eventos relevantes para estar al tanto sin tener que revisar la app constantemente.

### Historias de usuario

**MAT-30: Notificacion de aprobacion/rechazo**
- Como integrante, quiero recibir una notificacion cuando mi accion es aprobada o rechazada.
- Criterios de aceptacion:
  - Se envia notificacion con el resultado (aprobado/rechazado) y los puntos acreditados.
  - Si fue rechazada, se indica el motivo y la opcion de pedir revision.
- Origen: Regla de negocio (Notificacion de aprobacion/rechazo). Todos quieren saber el resultado.

**MAT-31: Notificacion de solicitud de aprobacion**
- Como integrante aprobador, quiero recibir una notificacion cuando alguien sube evidencia que necesita mi aprobacion.
- Criterios de aceptacion:
  - Se notifica a quien(es) debe(n) aprobar segun la configuracion del grupo.
  - La notificacion incluye la accion, quien la registro y link directo para aprobar/rechazar.
- Origen: Regla de negocio (Notificacion de solicitud de aprobacion).

**MAT-32: Resumen periodico del grupo**
- Como integrante, quiero recibir un resumen periodico con la actividad del grupo.
- Criterios de aceptacion:
  - Se envia semanalmente (configurable).
  - Incluye: ranking actual, acciones mas realizadas, cambios de cotizacion relevantes, actividad de cada integrante.
- Origen: Camila: "un resumen mensual seria perfecto para las reuniones de gastos". Roberto: "que los numeros hablen solos".

**MAT-33: Recordatorio de evidencia pendiente**
- Como integrante, quiero recibir un aviso cuando me queda poco tiempo para subir evidencia de una accion.
- Criterios de aceptacion:
  - Se notifica cuando queda menos del 25% del plazo de carga.
  - Se indica la accion y el tiempo restante.
- Origen: Regla de negocio (Recordatorio de evidencia pendiente).

**MAT-34: Alerta de saldo negativo**
- Como integrante, quiero recibir un aviso cuando mi saldo se acerca al limite de deuda.
- Criterios de aceptacion:
  - Se envia alerta cuando el saldo llega al 80% del limite negativo.
  - Se sugiere realizar acciones para mejorar el saldo.
- Origen: Regla de negocio (Alerta de saldo negativo).

---

## EP-09: Administracion de la Plataforma

> Como administrador, quiero gestionar usuarios y el catalogo global para mantener la plataforma funcionando correctamente.

### Historias de usuario

**MAT-35: Panel de administrador**
- Como administrador, quiero acceder a un panel para gestionar la plataforma.
- Criterios de aceptacion:
  - Acceso separado del flujo de usuario normal.
  - Se pueden ver estadisticas globales: grupos activos, acciones mas usadas, volumen de puntos en circulacion.
  - No se puede acceder al detalle de movimientos privados de cada grupo.
- Origen: Regla de negocio (Estadisticas globales). User persona: Admin.

**MAT-36: Suspender/reactivar usuario**
- Como administrador, quiero poder suspender o reactivar usuarios para actuar ante abusos.
- Criterios de aceptacion:
  - La suspension bloquea todas las operaciones del usuario en la plataforma.
  - Se puede reactivar en cualquier momento.
  - La accion queda registrada en el log de auditoria con quien, cuando y por que.
- Origen: Regla de negocio (Suspension/reactivacion de usuarios).

**MAT-37: Auditoria de acciones administrativas**
- Como plataforma, quiero registrar toda accion del administrador en un log auditable.
- Criterios de aceptacion:
  - Cada accion admin se registra con: quien, cuando, que hizo, sobre quien/que.
  - El log es consultable por el administrador.
  - No se pueden borrar entradas del log.
- Origen: Regla de negocio (Auditoria de acciones administrativas).

---

## Resumen de Epicas

| ID | Epica | Historias | Sprint tentativo |
|----|-------|:-:|:-:|
| EP-01 | Gestion de Usuarios y Autenticacion | 3 (MAT-01 a 03) | Sprint 1 |
| EP-02 | Gestion de Grupos | 6 (MAT-04 a 09) | Sprint 1 |
| EP-03 | Catalogo de Acciones | 5 (MAT-10 a 14) | Sprint 1-2 |
| EP-04 | Registro y Aprobacion de Acciones | 5 (MAT-15 a 19) | Sprint 2 |
| EP-05 | Economia de Puntos | 4 (MAT-20 a 23) | Sprint 2 |
| EP-06 | Motor de Reglas y Valuacion | 5 (MAT-24 a 28) | Sprint 3 |
| EP-07 | Acciones Colaborativas | 1 (MAT-29) | Sprint 3 |
| EP-08 | Notificaciones | 5 (MAT-30 a 34) | Sprint 3-4 |
| EP-09 | Administracion de la Plataforma | 3 (MAT-35 a 37) | Sprint 4 |
| **Total** | | **37 historias** | |

---

## Trazabilidad: Historias por entrevistado

Para verificar que todos los perfiles estan representados en las historias:

| Entrevistado | Historias donde influyo directamente |
|---|---|
| **Martina** (pareja, 24) | MAT-15 (registro rapido), MAT-16 (evidencia opcional para cosas chicas), MAT-13 (favoritos) |
| **Lucas** (amigos, 27) | MAT-11 (valor diferenciado), MAT-12 (acciones custom), MAT-22 (ranking), MAT-08 (expulsion) |
| **Sofia** (familia, 32) | MAT-10 (catalogo con cuidado/gestion), MAT-24 (modificadores contextuales), MAT-16 (evidencia configurable) |
| **Nicolas** (amigos, 23) | MAT-22 (ranking), MAT-29 (compensar tareas), MAT-20 (ver saldo) |
| **Tomas** (adolescente, 16) | MAT-22 (ranking), MAT-27 (combos), MAT-16 (foto divertida), MAT-29 (colaborativas) |
| **Roberto** (padre, 55) | MAT-32 (resumen periodico), MAT-25 (bonus fechas), MAT-07 (salida de grupo) |
| **Camila** (oficina, 29) | MAT-12 (acciones custom oficina), MAT-32 (resumen mensual), MAT-10 (tareas de gestion) |
| **Marta** (mayor, 68) | MAT-13 (favoritos), MAT-10 (tareas de cuidado), MAT-16 (sin evidencia, confianza) |
| **Admin** | MAT-35, MAT-36, MAT-37 |
