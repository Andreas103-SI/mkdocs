# Mejoras en Plantillas y Diseño

En esta sección se documentan las mejoras realizadas en las plantillas de TaskFlow, incluyendo la estilización de las plantillas HTML, la creación de un archivo CSS personalizado, y la optimización de la experiencia de usuario con un diseño responsivo.

## Creación de un Archivo CSS Personalizado (`style.css`)

Se creó un archivo `style.css` para centralizar los estilos personalizados del proyecto, permitiendo su reutilización en todas las plantillas. Este archivo se encuentra en `static/css/style.css`.

- **Ubicación**: `static/css/style.css`
- **Contenido principal**:
  - Estilos generales para el cuerpo (`body`), contenido principal (`main`), y footer (`footer`).
  - Estilos para la barra de navegación (`navbar`), incluyendo sombras, transiciones y badge para notificaciones.
  - Estilos para componentes reutilizables como tarjetas (`.card`), alertas (`.alert`), y botones personalizados (`.btn-custom`).
  - Ajustes de responsividad con media queries para pantallas pequeñas y medianas.

## Actualización de `base.html`

Se modificó la plantilla base (`base.html`) para implementar un diseño estilizado y responsivo usando Bootstrap 5 y el archivo `style.css`.

- **Ubicación**: `templates/base.html`
- **Cambios principales**:
  - Incorporación de Bootstrap 5 y Font Awesome para íconos.
  - Creación de una barra de navegación responsiva con un badge para notificaciones no leídas.
  - Uso de `style.css` para estilos personalizados, eliminando estilos en línea.
  - Estructura con `flex` para mantener el footer al final de la página.
  - Context processor para mostrar el conteo de notificaciones no leídas en todas las páginas.

## Mejoras en Plantillas Específicas

Se estilizaron las siguientes plantillas para mejorar la experiencia de usuario, utilizando Bootstrap 5 y los estilos definidos en `style.css`:

### 1. `notificaciones_list.html`
- **Ubicación**: `templates/notificaciones_list.html`
- **Cambios**:
  - Diseño con tarjeta (`card`) para la lista de notificaciones.
  - Botón "Marcar como leída" estilizado con `btn-custom`.
  - Manejo de mensajes de éxito/error con alertas de Bootstrap.
  - Formato de fecha (`d/m/Y H:i`) y diseño responsivo.

### 2. `no_permission.html`
- **Ubicación**: `templates/no_permission.html`
- **Cambios**:
  - Diseño centrado con tarjeta (`card`).
  - Título en rojo (`text-danger`) para resaltar el acceso denegado.
  - Botón "Volver a la lista de proyectos" estilizado con `btn-secondary`.

### 3. `proyecto_confirm_delete.html`
- **Ubicación**: `templates/proyecto_confirm_delete.html`
- **Cambios**:
  - Diseño centrado con tarjeta (`card`).
  - Título en rojo (`text-danger`) para resaltar la acción de eliminación.
  - Botones "Confirmar" (`btn-danger`) y "Cancelar" (`btn-secondary`) alineados.

### 4. `proyecto_detail.html`
- **Ubicación**: `templates/proyecto_detail.html`
- **Cambios**:
  - Sección de detalles del proyecto en una tarjeta (`card`).
  - Secciones separadas para tareas y mensajes con botones estilizados (`btn-custom`, `btn-success`, `btn-primary`).
  - Botón "Eliminar Proyecto" movido al lado de "Volver a Proyectos" usando `d-flex`.
  - Diseño responsivo con espaciado adecuado.

### 5. `proyecto_form.html`
- **Ubicación**: `templates/proyecto_form.html`
- **Cambios**:
  - Formulario en una tarjeta (`card`) con campos renderizados manualmente.
  - Manejo de mensajes de éxito/error con alertas.
  - Botones "Crear Proyecto" (`btn-custom`) y "Cancelar" (`btn-secondary`) alineados con `d-flex`.

### 6. `proyecto_list.html`
- **Ubicación**: `templates/proyecto_list.html`
- **Cambios**:
  - Lista de proyectos en una tarjeta (`card`) con diseño de lista.
  - Botón "Ver Detalles" estilizado con `btn-custom`.
  - Botones "Crear Proyecto" (`btn-success`) y "Volver al Inicio" (`btn-secondary`) alineados con `d-flex`.

### 7. `proyecto_update.html`
- **Ubicación**: `templates/proyecto_update.html`
- **Cambios**:
  - Formulario en una tarjeta (`card`) con campos renderizados manualmente.
  - Manejo de mensajes de éxito/error con alertas.
  - Botones "Guardar Cambios" (`btn-custom`) y "Cancelar" (`btn-secondary`) alineados con `d-flex`.

### 8. `comentario_form.html`
- **Ubicación**: `templates/tareas/comentario_form.html`
- **Cambios**:
  - Formulario en una tarjeta (`card`) con campos renderizados manualmente.
  - Manejo de mensajes de éxito/error con alertas.
  - Botones "Enviar Comentario" (`btn-custom`) y "Volver a Tarea" (`btn-secondary`) alineados con `d-flex`.

### 9. `tarea_confirm_delete.html`
- **Ubicación**: `templates/tarea_confirm_delete.html`
- **Cambios**:
  - Diseño centrado con tarjeta (`card`).
  - Título en rojo (`text-danger`) para resaltar la acción de eliminación.
  - Botones "Confirmar Eliminación" (`btn-danger`) y "Cancelar" (`btn-secondary`) alineados.

### 10. `tarea_detalle.html`
- **Ubicación**: `templates/tarea_detalle.html`
- **Cambios**:
  - Detalles de la tarea y comentarios en tarjetas separadas (`card`).
  - Formato de fecha (`d/m/Y H:i`) para comentarios.
  - Botón "Agregar Comentario" (`btn-custom`) y "Volver a Tareas" (`btn-secondary`).

### 11. `tarea_form.html`
- **Ubicación**: `templates/tarea_form.html`
- **Cambios**:
  - Formulario en una tarjeta (`card`) con campos renderizados manualmente.
  - Título dinámico ("Crear Tarea" o "Editar Tarea") según el contexto.
  - Botones "Crear Tarea"/"Guardar Cambios" (`btn-custom`) y "Volver a Tareas" (`btn-secondary`) alineados con `d-flex`.

### 12. `tarea_list.html`
- **Ubicación**: `templates/tarea_list.html`
- **Cambios**:
  - Lista de tareas en una tarjeta (`card`) con diseño de lista.
  - Comentarios anidados con formato de fecha (`d/m/Y H:i`).
  - Botones "Agregar Comentario" (`btn-custom`), "Crear Tarea" (`btn-success`), y "Volver a Proyectos" (`btn-secondary`).

### 13. `mensaje_form.html`
- **Ubicación**: `templates/mensajes/mensaje_form.html`
- **Cambios**:
  - Formulario en una tarjeta (`card`) con campos renderizados manualmente.
  - Campos condicionales (`usuario_receptor` y `grupo`) mostrados dinámicamente con JavaScript (sin recarga de página).
  - Manejo de mensajes de éxito/error con alertas.
  - Botones "Enviar Mensaje" (`btn-custom`) y "Volver a Mensajes" (`btn-secondary`) alineados con `d-flex`.

### 14. `mensaje_reply_form.html`
- **Ubicación**: `templates/mensajes/mensaje_reply_form.html`
- **Cambios**:
  - Mensaje original destacado en una tarjeta (`card`) con fecha formateada.
  - Formulario de respuesta en una tarjeta (`card`) con campos renderizados manualmente.
  - Campos condicionales (`usuario_receptor` y `grupo`) mostrados dinámicamente con JavaScript (sin recarga de página).
  - Manejo de mensajes de éxito/error con alertas.
  - Botones "Enviar Respuesta" (`btn-custom`) y "Volver a Mensajes" (`btn-secondary`) alineados con `d-flex`.

## Notas Adicionales
- Todas las plantillas ahora son responsivas gracias a Bootstrap 5 y los ajustes en `style.css`.
- Se implementó un context processor para mostrar el conteo de notificaciones no leídas en todas las páginas.
- Los formularios incluyen manejo de errores y mensajes de éxito/error para mejorar la experiencia de usuario.
