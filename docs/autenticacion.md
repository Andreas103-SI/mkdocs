# Autenticación de Usuarios

- **Modelo de usuario personalizado:** Configuré `AUTH_USER_MODEL = 'TaskFlow.Usuario'` en `settings.py` para usar un modelo `Usuario` en la app `TaskFlow`.
- **Vistas:** Creé vistas para login, logout y registro copiando código estándar de Django (por ejemplo, `LoginView`, `LogoutView` y una vista personalizada para registro).
- **URLs:** Configuré las URLs en `urls.py` para autenticación (ejemplo: `/accounts/login/`, `/accounts/logout/`, `/accounts/register/`).