# PréstamoLab CTMA

Aplicación móvil educativa para la consulta y trazabilidad de préstamos de equipos y herramientas en ambientes de formación.

## Tabla de contenido

- [Actividad 1 – Descubrimiento y Product Goal](#actividad-1--descubrimiento-y-product-goal)
- [Actividad 2 – Historias de usuario y criterios de aceptación](#actividad-2--historias-de-usuario-y-criterios-de-aceptación)
- [Actividad 3 – Riesgos y priorización de pruebas](#actividad-3--riesgos-y-priorización-de-pruebas)
- [Actividad 4 – Sprint Planning](#actividad-4--sprint-planning)

---

## Actividad 1 – Descubrimiento y Product Goal

### 1.1 Visión del producto

**Problema**

En los ambientes de formación existen diferentes equipos y herramientas que los aprendices e instructores necesitan utilizar temporalmente para realizar prácticas. Actualmente, cuando el control de estos préstamos se realiza de manera manual, puede ser difícil conocer qué equipos están disponibles, cuáles ya fueron solicitados y cuáles tienen una devolución pendiente.

PréstamoLab CTMA busca mejorar la consulta y trazabilidad de estos préstamos mediante una aplicación móvil educativa que permita visualizar los equipos disponibles, realizar solicitudes y consultar el estado de estas durante la ejecución de la aplicación.

**Usuarios**

- **Solicitante demo**: representa a un aprendiz o instructor que consulta los recursos disponibles y registra una solicitud de préstamo.
- **Gestor simulado**: representa conceptualmente a quien puede realizar cambios en el estado de una solicitud durante las pruebas. En este primer incremento no requiere autenticación real.
- **Instructor**: facilita los datos de laboratorio, observa el proceso y valida las evidencias desarrolladas por el equipo.

**Necesidades**

El usuario necesita poder:

- Consultar los equipos y herramientas disponibles.
- Ver la información detallada de cada equipo.
- Registrar una solicitud de préstamo.
- Indicar el ambiente o destino, propósito y duración estimada.
- Recibir validaciones cuando los datos no cumplan las reglas establecidas.
- Consultar sus solicitudes.
- Conocer el estado de cada solicitud.
- Cancelar una solicitud cuando todavía se encuentre en el estado permitido.
- Evitar que un mismo equipo sea solicitado varias veces por error.

Estas necesidades corresponden al alcance funcional mínimo definido para el incremento.

**Restricciones**

- La aplicación será un prototipo educativo, no un sistema institucional real.
- No se deben utilizar datos personales reales.
- No es necesario implementar autenticación.
- Los datos se mantendrán mediante un repositorio simulado compartido durante la ejecución.
- No se requiere implementar una operación logística real de préstamos.
- Se trabaja únicamente con el alcance funcional definido para el MVP.
- Los identificadores inexistentes deben manejarse sin que la aplicación se cierre abruptamente.

**Valor esperado**

El valor principal de PréstamoLab CTMA es facilitar la consulta de los recursos disponibles y mejorar el seguimiento de las solicitudes de préstamo dentro de un entorno educativo.

Además, el proyecto permitirá que el usuario tenga mayor claridad sobre la disponibilidad de los equipos y el estado de sus solicitudes, evitando situaciones como solicitudes duplicadas o préstamos sobre equipos que ya no están disponibles.

### 1.2 Mapa de actores

| Actor | Interacción con el sistema |
|---|---|
| Solicitante demo | Consulta el catálogo, visualiza detalles, registra solicitudes, consulta sus solicitudes y puede cancelar una solicitud permitida. |
| Gestor simulado | Representa cambios de estado utilizados durante las pruebas del sistema. |
| Instructor | Facilita los datos de prueba, observa el proceso y valida las evidencias del proyecto. |

### 1.3 Product Goal

> Mejorar la consulta, disponibilidad y trazabilidad de los préstamos de equipos y herramientas de formación, permitiendo a los usuarios conocer los recursos disponibles, registrar solicitudes válidas y realizar seguimiento a su estado de manera clara y organizada.

Este Product Goal está alineado con el objetivo general planteado para PréstamoLab CTMA: mejorar la trazabilidad y consulta de préstamos de recursos de formación mediante una experiencia móvil.

---

## Actividad 2 – Historias de usuario y criterios de aceptación

### HU-01 – Consultar catálogo de equipos

**Historia de usuario**

Como solicitante demo, quiero consultar el catálogo de equipos disponibles y no disponibles para conocer qué recursos puedo solicitar para una práctica.

**Criterios de aceptación**

- **CA-01.1**: Dado que existen equipos registrados en el repositorio, cuando el usuario ingresa al catálogo, entonces debe visualizar el nombre, la categoría y el estado de disponibilidad de cada equipo.
- **CA-01.2**: La disponibilidad del equipo debe mostrarse mediante texto o información adicional y no depender únicamente del color.
- **CA-01.3**: Cuando el estado de un equipo cambie después de crear o cancelar una solicitud, el catálogo debe reflejar el estado actualizado.

### HU-02 – Consultar detalle de un equipo

**Historia de usuario**

Como solicitante demo, quiero consultar el detalle de un equipo para conocer su información y decidir si deseo solicitarlo.

**Criterios de aceptación**

- **CA-02.1**: Dado un equipoId válido, cuando el usuario selecciona un equipo desde el catálogo, entonces debe visualizar el detalle correspondiente al equipo seleccionado.
- **CA-02.2**: La navegación debe utilizar el identificador del equipo como argumento.
- **CA-02.3**: Dado un equipoId inexistente, cuando el usuario intenta acceder al detalle, entonces la aplicación debe mostrar un estado recuperable y no cerrarse abruptamente.

### HU-03 – Registrar solicitud de préstamo

**Historia de usuario**

Como solicitante demo, quiero registrar una solicitud de préstamo para un equipo disponible para poder utilizarlo temporalmente en una práctica.

**Criterios de aceptación**

- **CA-03.1**: Dado un equipo en estado DISPONIBLE, cuando el usuario diligencia correctamente el formulario y pulsa Guardar, entonces se debe crear una solicitud en estado SOLICITADA.
- **CA-03.2**: Después de crear la solicitud, el equipo debe cambiar su estado a RESERVADO.
- **CA-03.3**: Solo se debe crear una solicitud por cada acción válida de guardado.
- **CA-03.4**: La solicitud creada debe aparecer en la sección Mis solicitudes.

### HU-04 – Validar los datos de la solicitud

**Historia de usuario**

Como solicitante demo, quiero recibir validaciones en el formulario para asegurarme de que la información de mi solicitud cumple con las reglas antes de guardarla.

**Criterios de aceptación**

- **CA-04.1**: El campo de ambiente o destino debe ser obligatorio.
- **CA-04.2**: Si el ambiente o destino está vacío, la solicitud no debe guardarse y los demás datos diligenciados deben conservarse.
- **CA-04.3**: El propósito debe contener entre 10 y 180 caracteres.
- **CA-04.4**: La duración estimada debe estar entre 1 y 8 horas.
- **CA-04.5**: Cuando exista un error, el sistema debe mostrar un mensaje específico y comprensible para el usuario.

Estas validaciones corresponden a las reglas RN-02, RN-03 y RN-04.

### HU-05 – Evitar solicitudes sobre equipos no disponibles

**Historia de usuario**

Como solicitante demo, quiero que el sistema controle la disponibilidad del equipo para evitar solicitar un recurso que ya se encuentre reservado o prestado.

**Criterios de aceptación**

- **CA-05.1**: Solo se debe permitir crear una solicitud cuando el equipo se encuentre en estado DISPONIBLE.
- **CA-05.2**: Si el equipo está en estado RESERVADO, la solicitud debe ser rechazada.
- **CA-05.3**: Si el equipo está en estado PRESTADO, la solicitud también debe ser rechazada.

Esta historia responde a la regla RN-01.

### HU-06 – Evitar solicitudes duplicadas

**Historia de usuario**

Como solicitante demo, quiero que una doble pulsación del botón Guardar no cree solicitudes duplicadas para el mismo equipo.

**Criterios de aceptación**

- **CA-06.1**: Dado un formulario válido y un equipo disponible, cuando el usuario pulsa Guardar dos veces rápidamente, entonces solo debe crearse una solicitud.
- **CA-06.2**: El equipo debe quedar en estado RESERVADO.
- **CA-06.3**: En la lista de solicitudes solo debe existir una solicitud activa para esa acción.

### HU-07 – Consultar mis solicitudes

**Historia de usuario**

Como solicitante demo, quiero consultar mis solicitudes para conocer cuáles préstamos he registrado y cuál es su estado actual.

**Criterios de aceptación**

- **CA-07.1**: Cuando existan solicitudes registradas, el usuario debe poder visualizarlas en la pantalla Mis solicitudes.
- **CA-07.2**: Cada solicitud debe permitir identificar al menos el equipo asociado y su estado.
- **CA-07.3**: Cuando el usuario seleccione una solicitud, debe poder navegar a su detalle utilizando solicitudId.

### HU-08 – Cancelar una solicitud

**Historia de usuario**

Como solicitante demo, quiero cancelar una solicitud que todavía esté pendiente para liberar nuevamente el equipo.

**Criterios de aceptación**

- **CA-08.1**: Dado que una solicitud se encuentra en estado SOLICITADA, cuando el usuario selecciona Cancelar, entonces la solicitud debe cambiar a estado CANCELADA.
- **CA-08.2**: Después de cancelar una solicitud, la disponibilidad del equipo debe actualizarse de forma coherente.
- **CA-08.3**: Una solicitud que ya se encuentre en estado CANCELADA no debe poder cancelarse nuevamente.
- **CA-08.4**: En el MVP, no se debe permitir cancelar una solicitud que se encuentre en un estado diferente de SOLICITADA.

### HU-09 – Mantener los datos durante la ejecución

**Historia de usuario**

Como usuario de la aplicación, quiero que la información de equipos y solicitudes se mantenga actualizada mientras utilizo las diferentes pantallas para que los datos sean coherentes durante toda la ejecución.

**Criterios de aceptación**

- **CA-09.1**: Las pantallas deben consultar una fuente de datos compartida.
- **CA-09.2**: Cuando se cree una solicitud, el cambio debe verse reflejado tanto en el catálogo como en la lista de solicitudes.
- **CA-09.3**: La aplicación debe utilizar un repositorio simulado compartido durante la ejecución.

### Product Backlog inicial

| ID | Historia / necesidad | Prioridad | Riesgo |
|---|---|---|---|
| PB-01 | Consultar catálogo de equipos y disponibilidad | Alta | Alto |
| PB-02 | Consultar detalle de un equipo | Alta | Medio |
| PB-03 | Registrar solicitud de préstamo | Alta | Alto |
| PB-04 | Validar ambiente, propósito y duración | Alta | Alto |
| PB-05 | Evitar solicitudes sobre equipos no disponibles | Alta | Alto |
| PB-06 | Evitar duplicación por doble pulsación | Alta | Alto |
| PB-07 | Consultar mis solicitudes y su detalle | Media | Medio |
| PB-08 | Cancelar solicitud en estado SOLICITADA | Media | Medio |
| PB-09 | Mantener consistencia mediante repositorio compartido | Alta | Alto |

> **Decisión del proyecto**: se mantienen estas historias porque cubren todo el flujo principal del MVP. En la Actividad 4 (Sprint Planning) se seleccionan cuáles entran realmente en el mini-Sprint.

---

## Actividad 3 – Riesgos y priorización de pruebas

### 3.1 Matriz de riesgos

| ID | Riesgo | Probabilidad | Impacto | Nivel | Estrategia de cobertura |
|---|---|---|---|---|---|
| R-01 | Se crean dos solicitudes activas para el mismo equipo debido a una doble pulsación en Guardar. | Alta | Alta | Crítico | Ejecutar prueba de doble pulsación y verificar que solo exista una solicitud. |
| R-02 | El sistema permite registrar datos inválidos o fuera de los límites establecidos. | Alta | Media | Alto | Aplicar partición de equivalencia y valores límite sobre propósito y duración. |
| R-03 | Un equipoId o solicitudId inexistente provoca un cierre abrupto de la aplicación. | Media | Alta | Alto | Realizar pruebas negativas con identificadores inexistentes y verificar un estado recuperable. |
| R-04 | Después de crear una solicitud, el catálogo no actualiza correctamente el estado del equipo. | Media | Alta | Alto | Ejecutar el flujo completo de creación y comprobar la consistencia entre catálogo, detalle y solicitudes. |
| R-05 | Se permite solicitar un equipo que se encuentra RESERVADO o PRESTADO. | Media | Alta | Alto | Realizar pruebas de decisión utilizando equipos en diferentes estados. |
| R-06 | La cancelación permite transiciones de estado no válidas. | Media | Media | Medio | Aplicar pruebas de transición de estados para solicitudes SOLICITADA, CANCELADA y otros estados utilizados. |
| R-07 | La interfaz pierde información o acciones importantes cuando se aumenta el tamaño de fuente. | Media | Media | Medio | Probar la aplicación con fuente aumentada a 1.5× y verificar que los mensajes y botones continúen siendo utilizables. |

### 3.2 Relación entre riesgos y casos de prueba

| Riesgo | Caso o casos relacionados | Cobertura |
|---|---|---|
| R-01 – Solicitudes duplicadas | TC-13 | Doble pulsación en Guardar. |
| R-02 – Datos inválidos | TC-04 a TC-11 | Límites del propósito y duración. |
| R-03 – ID inexistente | TC-03 | Navegación negativa y estado recuperable. |
| R-04 – Estado no actualizado | TC-14, TC-15 y regresión | Verificación de consistencia entre solicitudes y disponibilidad. |
| R-05 – Equipo no disponible | TC-12 | Decisión según estado del equipo. |
| R-06 – Transición inválida | TC-15 y TC-16 | Cancelación válida e inválida. |
| R-07 – Problemas de accesibilidad | TC-18 | Fuente aumentada y contenido utilizable. |

### 3.3 Decisión de priorización de pruebas

**🔴 Prioridad crítica**

- Evitar solicitudes duplicadas.
- Mantener la disponibilidad coherente del equipo.
- Impedir solicitudes sobre equipos no disponibles.

**🟠 Prioridad alta**

- Validar correctamente propósito, destino y duración.
- Controlar IDs inexistentes sin cerrar la aplicación.

**🟡 Prioridad media**

- Controlar las transiciones de estado durante la cancelación.
- Comprobar accesibilidad básica con fuente aumentada.

### 3.4 Base de pruebas

- **Historias de usuario**: HU-01 a HU-09.
- **Criterios de aceptación**: definidos en la Actividad 2.
- **Reglas de negocio**: RN-01 a RN-09.
- **Riesgos**: R-01 a R-07.
- **Técnicas de caja negra**: partición de equivalencia, valores límite, tabla de decisión, transición de estados y casos de uso.

---

## Actividad 4 – Sprint Planning

### 4.1 Sprint Goal

> Permitir que el usuario consulte los equipos disponibles y registre una solicitud de préstamo válida, manteniendo la disponibilidad actualizada y demostrando el funcionamiento mediante pruebas reproducibles.

### 4.2 Selección de PBIs para el Sprint

| ID | PBI | Prioridad | ¿Entra al Sprint? | Justificación |
|---|---|---|---|---|
| PB-01 | Consultar catálogo de equipos y disponibilidad | Alta | ✅ Sí | Es necesario para iniciar el flujo principal. |
| PB-02 | Consultar detalle de un equipo | Alta | ✅ Sí | Permite seleccionar y conocer el equipo antes de solicitarlo. |
| PB-03 | Registrar solicitud de préstamo | Alta | ✅ Sí | Es una funcionalidad central del Sprint Goal. |
| PB-04 | Validar ambiente, propósito y duración | Alta | ✅ Sí | Evita guardar solicitudes que incumplan las reglas. |
| PB-05 | Evitar solicitudes sobre equipos no disponibles | Alta | ✅ Sí | Protege la regla principal de disponibilidad. |
| PB-06 | Evitar duplicación por doble pulsación | Alta | ✅ Sí | Reduce el riesgo crítico identificado como R-01. |
| PB-07 | Consultar mis solicitudes y su detalle | Media | ❌ Pendiente | Aporta valor, pero no es indispensable para cumplir el objetivo principal de este Sprint. |
| PB-08 | Cancelar solicitud en estado SOLICITADA | Media | ❌ Pendiente | Puede desarrollarse en un incremento posterior. |
| PB-09 | Mantener consistencia mediante repositorio compartido | Alta | ✅ Sí | Es necesario para mantener los cambios entre las pantallas durante la ejecución. |

**PBIs seleccionados: 7** → PB-01, PB-02, PB-03, PB-04, PB-05, PB-06 y PB-09.

### 4.3 Sprint Backlog

| PBI | Actividades principales |
|---|---|
| PB-01 – Catálogo | Crear modelo de Equipo, cargar datos sintéticos, crear repositorio y diseñar pantalla de catálogo. |
| PB-02 – Detalle | Configurar navegación mediante equipoId, recuperar el equipo desde el repositorio y manejar IDs inexistentes. |
| PB-03 – Solicitud | Crear modelo SolicitudPrestamo, diseñar formulario y registrar una solicitud válida. |
| PB-04 – Validaciones | Validar ambiente obligatorio, propósito entre 10 y 180 caracteres y duración entre 1 y 8 horas. |
| PB-05 – Disponibilidad | Comprobar el estado del equipo antes de crear una solicitud y rechazar equipos no disponibles. |
| PB-06 – Duplicación | Evitar que una doble pulsación cree dos solicitudes para el mismo equipo. |
| PB-09 – Consistencia | Utilizar un repositorio InMemory compartido y actualizar el estado del equipo después de una solicitud. |
| Calidad | Diseñar casos de prueba, ejecutar pruebas y registrar resultados reales. |
| Documentación | Actualizar README, decisiones técnicas y evidencias. |

### 4.4 Plan accionable del mini-Sprint

**1. Modelado**

- Crear `Equipo`.
- Crear `SolicitudPrestamo`.
- Crear los enums para estados y categorías.
- Definir las reglas de validación.

**2. Capa de datos**

- Crear la interfaz `PrestamoRepository`.
- Crear `InMemoryPrestamoRepository`.
- Cargar equipos sintéticos.
- Implementar operaciones para consultar equipos y crear solicitudes.

**3. Gestión del estado**

- Crear `PrestamoUiState`.
- Crear el ViewModel.
- Exponer el estado de solo lectura.
- Centralizar las acciones y validaciones fuera de los composables.

**4. Navegación**

Crear las rutas principales:

```
Catálogo → Detalle del equipo → Solicitud
```

utilizando:

- `EquipoDetalle/{equipoId}`
- `Solicitar/{equipoId}`

**5. Interfaz**

- Pantalla de catálogo.
- Tarjetas de equipos.
- Pantalla de detalle.
- Formulario de solicitud.
- Mensajes específicos de validación.
- Indicadores de disponibilidad que no dependan únicamente del color.

**6. Pruebas**

- Preparar datos sintéticos.
- Diseñar los casos de prueba.
- Ejecutar los casos seleccionados.
- Registrar resultados PASS, FAIL o BLOCKED.
- Guardar las evidencias reales.

> Una prueba no ejecutada no puede reportarse como PASS y los casos impedidos deben registrarse como BLOCKED con su causa.

### 4.5 Riesgos e impedimentos iniciales

| ID | Riesgo o impedimento | Posible consecuencia | Acción inicial |
|---|---|---|---|
| RI-01 | Falta de experiencia con navegación en Compose | Errores al enviar y recuperar IDs. | Implementar primero una navegación mínima y probar IDs válidos e inexistentes. |
| RI-02 | Estado compartido mal gestionado | Catálogo y solicitudes muestran información inconsistente. | Utilizar un único repositorio InMemory compartido. |
| RI-03 | Validaciones dentro de la UI | Dificultad para reutilizar y probar las reglas. | Crear funciones o lógica desacoplada. |
| RI-04 | Doble pulsación en Guardar | Solicitudes duplicadas. | Controlar el estado de guardado y validar nuevamente antes de crear. |
| RI-05 | Tiempo limitado | Algunas funcionalidades podrían quedar incompletas. | Priorizar los 7 PBIs seleccionados según el Sprint Goal. |
| RI-06 | Pruebas sin datos preparados | Casos BLOCKED o evidencia incompleta. | Preparar desde el inicio los datos sintéticos y estados necesarios. |

### 4.6 Definition of Done

- [ ] El proyecto compila y puede ejecutarse en el ambiente definido.
- [ ] Los criterios de aceptación seleccionados están implementados.
- [ ] La UI no modifica directamente la fuente de datos.
- [ ] El ViewModel expone UiState o StateFlow de solo lectura.
- [ ] La navegación transporta identificadores y controla IDs inexistentes.
- [ ] Se ejecutaron los casos de prueba acordados y los resultados registrados son reales.
- [ ] Los defectos críticos o altos tienen una decisión explícita.
- [ ] Las correcciones relevantes tienen confirmación y pruebas de regresión.
- [ ] Git y el README están actualizados.
- [ ] El incremento puede demostrarse y cada integrante puede explicar cómo funciona.