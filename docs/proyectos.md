# Gestión de Proyectos

## Introducción
Este proyecto es una aplicación web desarrollada con Django para la gestión de proyectos, tareas, mensajes y colaboración entre usuarios. Se utiliza un entorno virtual con Python 3.11.9 y PostgreSQL como base de datos.

## Estado Actual
- Se configuró un entorno de desarrollo con un entorno virtual en Windows.
- Se instaló PostgreSQL y se configuró como base de datos, creando una base de datos y usuario específicos.
- Se definió un modelo personalizado `Usuario` con campo `rol` y se estableció `AUTH_USER_MODEL = 'TaskFlow.Usuario'`.
- Se creó la aplicación `TaskFlow` con la estructura básica de Django.
- Se implementaron vistas para autenticación (`login`, `logout`, `registro`) y gestión de proyectos:
  - Listado (`/proyectos/`), creación (`/proyectos/crear/`), edición (`/proyectos/editar/<id>/`), y eliminación (`/proyectos/eliminar/<id>/`).
- Se resolvió un error 403 (`PermissionDenied`) ajustando permisos de `is_staff`/`is_superuser` en la base de datos.
- Se creó una plantilla base (`base.html`) y se ajustaron plantillas (`home.html`, `login.html`, `proyecto_list.html`, etc.) para heredar de ella.
- Se implementó la gestión de tareas con un modelo `Tarea` que incluye campos como `nombre`, `descripcion`, `fecha_limite`, `fecha_vencimiento`, `estado`, `usuarios_asignados`, y `asignado_a`.
- Se crearon vistas para listar tareas (`/tareas/`), crear (`/proyectos/<proyecto_id>/tareas/crear/`), editar (`/tareas/editar/<id>/`), y eliminar (`/tareas/eliminar/<id>/`).
- Se ajustó el flujo para mostrar tareas en los detalles de un proyecto (`/proyectos/<id>/`) tras crearlas, resolviendo un problema de redirección inicial.
- Se corrigió un error 404 en `ProyectoDetailView` asegurando que el usuario esté asociado al proyecto, y un error 500 (`TemplateDoesNotExist`) creando `proyectos/proyecto_confirm_delete.html`.

## Problemas Resueltos
- **Error 403:** Restringió el acceso a vistas de administración con `AdminRequiredMixin` y permisos `is_staff`.
- **Error 404 en /proyectos/1/:** Aseguró que el usuario esté en `proyecto.usuarios` o permitió acceso a administradores en `get_queryset`.
- **Error 500 (TemplateDoesNotExist):** Creó la plantilla `proyectos/proyecto_confirm_delete.html` y ajustó `BASE_DIR` en `settings.py`.

## Próximos Pasos
- Añadir validaciones a los formularios (por ejemplo, `fecha_vencimiento` > `fecha_limite`).
- Integrar Bootstrap o CSS personalizado para mejorar el diseño.
- Implementar notificaciones o mensajes entre usuarios.
- Probar el flujo completo con múltiples usuarios y roles.

## Notas Técnicas
- Estructura de carpetas: `templates/proyectos/` y `templates/tareas/` para plantillas específicas.
- Configuración de URLs en `TaskFlow/urls.py` e inclusión en `Sistema/urls.py`.
- Uso de mixins personalizados en `mixins.py` para restricciones de acceso.