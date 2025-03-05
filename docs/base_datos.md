# Configuración de la Base de Datos

- **Herramienta:** Conectado a pgAdmin4 para gestionar la base de datos PostgreSQL.
- **Cambio en `BASE_DIR`:** Originalmente estaba como `Path(__file__).resolve().parent.parent`, pero no funcionaba. Lo cambié a:
  ```python
  BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))