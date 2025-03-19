# Proyecto MkDocs

Este proyecto utiliza MkDocs para generar documentación estática a partir de archivos Markdown.

## Instalación

Para instalar las dependencias necesarias, ejecuta:

```sh
pip install mkdocs
```

## Uso

Para generar la documentación y servirla localmente, ejecuta:

```sh
mkdocs serve
```

Esto iniciará un servidor local en `http://127.0.0.1:8000/` donde podrás ver la documentación.

## Estructura del Proyecto

- `docs/`: Contiene los archivos Markdown de la documentación.
- `mkdocs.yml`: Archivo de configuración de MkDocs.

## Despliegue

Para desplegar la documentación en GitHub Pages, ejecuta:

```sh
mkdocs gh-deploy
```

## Contribuir

Si deseas contribuir a este proyecto, por favor sigue estos pasos:

1. Haz un fork del repositorio.
2. Crea una nueva rama (`git checkout -b feature/nueva-funcionalidad`).
3. Realiza tus cambios y haz commit (`git commit -am 'Añadir nueva funcionalidad'`).
4. Sube tus cambios (`git push origin feature/nueva-funcionalidad`).
5. Abre un Pull Request.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo `LICENSE` para más detalles.
