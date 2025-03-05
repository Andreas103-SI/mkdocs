# Errores y Soluciones

- **Errores encontrados:**
  - `[05/Mar/2025 10:53:18] "GET /accounts/login/?next=/proyectos/ HTTP/1.1" 404 179`: La URL de login no se encuentra.
  - `[05/Mar/2025 10:53:55] "GET /proyectos/ HTTP/1.1" 302 0`: Redirección a login, pero falla porque login no está definido.
  - `[05/Mar/2025 10:54:26] "GET /proyectos/crear/ HTTP/1.1" 302 0`: Igual que arriba, redirección fallida.
- **Solución pendiente:** Configurar correctamente la URL de login y verificar las vistas.