# Configuración de la Base de Datos

- **Herramienta:** Conectado a pgAdmin4 para gestionar la base de datos PostgreSQL.
- **Cambio en `BASE_DIR`:** Originalmente estaba como `Path(__file__).resolve().parent.parent`, pero no funcionaba. Lo cambié a:
  ```python
  BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

# pgAdmin 4  
pgAdmin 4 es una herramienta de administración de bases de datos PostgreSQL de código abierto. Permite gestionar bases de datos, ejecutar consultas SQL y visualizar esquemas.  

# DBeaver Community  
DBeaver Community es una herramienta de administración de bases de datos multiplataforma y gratuita. Permite conectarse a diversas bases de datos, incluyendo PostgreSQL, y generar diagramas Entidad-Relación (DER).  

## Instalación de DBeaver y Conexión a PostgreSQL  

### Descarga DBeaver Community  
1. Ve al sitio web oficial de DBeaver: [dbeaver.io/download/](https://dbeaver.io/download/)  
2. Descarga el instalador de Windows (.exe) para una instalación sencilla.  

### Instala DBeaver  
1. Ejecuta el instalador descargado y sigue las instrucciones en pantalla.  

### Abre DBeaver y crea una nueva conexión  
1. En el menú **"Base de datos"**, selecciona **"Nueva conexión de base de datos"**.  
2. Elige **"PostgreSQL"** como tipo de base de datos.  
3. Introduce los detalles de tu conexión:  
   - **Host**: `localhost` (o la dirección de tu servidor PostgreSQL)  
   - **Puerto**: `5432` (por defecto)  
   - **Base de datos**: El nombre de tu base de datos  
   - **Usuario**: Tu usuario de PostgreSQL  
   - **Contraseña**: Tu contraseña  
4. Haz clic en **"Probar conexión"** para verificar y luego en **"Finalizar"**.  


### Descarga de controladores  
Si DBeaver te pide descargar los controladores JDBC de PostgreSQL, acepta la descarga.  

## Generación del Diagrama Entidad-Relación (DER)  

### Expande la conexión  
1. En el panel **"Navegador de base de datos"**, expande tu conexión PostgreSQL.  
2. Expande **"Bases de datos"**, luego tu base de datos y **"Esquemas" -> "public"**.  

### Crea las tablas (si es necesario)  
1. Si no tienes las tablas creadas, abre un nuevo **"Script SQL"** y pega el script SQL con las definiciones de tus tablas.  
2. Ejecuta el script para crear las tablas.  

### Genera el DER  
1. Haz clic derecho en el esquema **"public"** y selecciona **"Ver Diagrama ER"**.  
2. DBeaver generará el DER automáticamente.  

### Personaliza y exporta el DER (opcional)  
- Organiza las tablas arrastrándolas.  
- Cambia la apariencia con las opciones de formato.  
- Exporta el diagrama como imagen (**clic derecho -> "Exportar diagrama"**).  

## Ejemplo de Diagrama Entidad-Relación (DER)  
![Diagrama Entidad-Relación generado con DBeaver]

## Consideraciones  
- Las tablas de unión para relaciones muchos a muchos se crean automáticamente en Django, no necesitas modelos explícitos para ellas.  
- Las migraciones de Django sincronizan los cambios entre tus modelos y la base de datos.  
- DBeaver refleja los cambios realizados en la base de datos, ya sea por migraciones o directamente.  
