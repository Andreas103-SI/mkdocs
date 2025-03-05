# Configuración del Entorno

- **Sistema operativo:** Windows.
- **Python:** Versión 3.11.9 instalada.
- **Entorno virtual:** Creado con `python -m venv .venv` y activado con `.venv\Scripts\activate`.
- **Dependencias:** Instaladas desde `requirements.txt` con `pip install -r requirements.txt`. Incluye Django y otras bibliotecas necesarias.

## Pasos adicionales para asegurar el correcto funcionamiento del entorno virtual

1. **Actualizar pip**:
    ```bash
    python -m pip install --upgrade pip
    ```

2. **Revisar entorno virtual**:
    Asegúrate de que el entorno virtual esté activado correctamente.

3. **Revisar configuración de settings.py**:
    - Verificar `INSTALLED_APPS`.
    - Verificar `DATABASES`.
    - Verificar `TEMPLATES`.

4. **Revisar archivos de registro**:
    Revisa los archivos de registro para obtener más detalles sobre errores o advertencias.

5. **Verificar configuración de URLs**:
    Asegúrate de que todas las rutas URL estén correctamente definidas en los archivos `urls.py`.

6. Para asegurarte de que tu aplicación Django funcione correctamente en un entorno de desarrollo, sigue estos pasos:
     **Configuración de `DEBUG` y `ALLOWED_HOSTS`**:

    Abre el archivo `settings.py` y asegúrate de que las siguientes configuraciones estén establecidas:

    ```python
    # SECURITY WARNING: don't run with debug turned on in production!
    DEBUG = False

    # Allow all hosts (use with caution in development)
    ALLOWED_HOSTS = ['*']
    ```

    **Nota**: `ALLOWED_HOSTS = ['*']` permite que la aplicación acepte solicitudes de cualquier host. Esta configuración es útil en el entorno de desarrollo pero **no** se recomienda para producción debido a razones de seguridad. En producción, especifica los dominios permitidos.
