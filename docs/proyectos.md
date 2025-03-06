# Gestión de Proyectos

## Vistas
- **Vistas:** Implementé vistas para listar proyectos (`/proyectos/`) y crear proyectos (`/proyectos/crear/`). Usé `LoginRequiredMixin` para restringir el acceso a usuarios autenticados y `AdminRequiredMixin` para limitar la creación de proyectos a administradores.
- **Estado:** Las vistas ahora funcionan correctamente después de resolver errores de permisos.

## Solucionando Errores de Permisos
Durante el desarrollo, enfrenté un error 403 (`PermissionDenied`) al intentar acceder a `/proyectos/crear/`. Esto ocurrió porque el usuario autenticado no cumplía con los requisitos de `AdminRequiredMixin`. Los pasos para solucionarlo fueron:

- **Causa:** El método `test_func` en `AdminRequiredMixin` verificaba `is_staff` o `is_superuser`, pero el usuario administrador no tenía estos atributos establecidos.
- **Solución:**
# Acceso a la Creación de Proyectos para Administradores

Para permitir que los administradores creen proyectos, fue necesario ajustar los permisos del usuario administrador. Se realizaron los siguientes pasos:

1.  **Acceso a la Shell de Django:**

    Se accedió a la shell interactiva de Django utilizando el comando:

    ```bash
    python manage.py shell
    ```

2.  **Verificación de Atributos del Usuario:**

    Se verificaron los atributos `is_staff` y `is_superuser` del usuario administrador mediante el siguiente código Python:

    ```python
    from django.contrib.auth import get_user_model
    User = get_user_model()
    usuario = User.objects.get(username='tu_usuario_admin')  # Reemplaza 'tu_usuario_admin' con el nombre de usuario real.
    print(usuario.is_staff, usuario.is_superuser)
    ```

3.  **Actualización de Permisos del Usuario:**

    Se actualizaron los permisos del usuario administrador para que tenga acceso completo al sitio, asignando `True` a los atributos `is_staff` y `is_superuser`:

    ```python
    usuario.is_staff = True
    usuario.is_superuser = True
    usuario.save()
    ```

4.  **Verificación del Acceso:**

    Después de reiniciar el servidor de desarrollo, se probó el acceso a la ruta `/proyectos/crear/`. Se confirmó que el usuario administrador ahora podía crear proyectos.

**Alternativa Considerada:**

Se consideró la posibilidad de modificar el `AdminRequiredMixin` para utilizar el campo `rol` del modelo `Usuario` (por ejemplo, `rol == 'admin'`). Sin embargo, se decidió utilizar los atributos `is_staff` y `is_superuser` para mantener la coherencia con las convenciones de permisos de Django.

**Resultado:**

Con estos cambios, los usuarios administradores ahora tienen la capacidad de crear proyectos. Además, el flujo de autenticación (inicio de sesión, cierre de sesión y registro) continúa funcionando correctamente.