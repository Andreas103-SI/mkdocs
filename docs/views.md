# Vista de Lista de Tareas (`TareaListView`)

La clase `TareaListView` es una vista basada en clases (CBV) de Django que hereda de `LoginRequiredMixin` y `ListView`. Esta vista se utiliza para mostrar una lista de tareas asociadas a un proyecto específico o todas las tareas disponibles, dependiendo de la URL y los permisos del usuario. Está diseñada para filtrar las tareas según si el usuario es superusuario/staff o un usuario normal autenticado, asegurando que solo vea las tareas asignadas a él.

## Código Fuente

A continuación se muestra el código completo de `TareaListView` con comentarios explicativos:

```python
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic import ListView
from django.db import models
from django.shortcuts import get_object_or_404
from .models import Tarea, Proyecto

class TareaListView(LoginRequiredMixin, ListView):
    """
    Vista para listar las tareas asociadas a un proyecto específico o todas las tareas disponibles.
    Requiere que el usuario esté autenticado (LoginRequiredMixin).
    
    Atributos:
        model (Tarea): El modelo asociado a esta vista.
        template_name (str): La plantilla a renderizar ('tareas/tarea_list.html').
        context_object_name (str): El nombre del contexto para las tareas en la plantilla ('tareas').
    """
    
    model = Tarea
    template_name = 'tareas/tarea_list.html'
    context_object_name = 'tareas'

    def get_queryset(self):
        """
        Obtiene el conjunto de datos de tareas a mostrar.
        
        Retorna:
            QuerySet: Un conjunto de tareas filtradas según el proyecto y los permisos del usuario.
        
        Lógica:
        - Si `proyecto_id` está presente en la URL, filtra las tareas por ese proyecto.
        - Si el usuario es superusuario o staff, muestra todas las tareas del proyecto.
        - Si el usuario es autenticado (pero no staff), filtra las tareas donde el usuario sea
          el `asignado_a` o esté en `usuarios_asignados`.
        - Si no hay `proyecto_id`, devuelve un QuerySet vacío.
        """
        proyecto_id = self.kwargs.get('proyecto_id')
        print(f"Proyecto ID: {proyecto_id}")  # Depuración
        print(f"Usuario autenticado: {self.request.user}, Autenticado: {self.request.user.is_authenticated}")  # Depuración
        
        if proyecto_id:
            if self.request.user.is_superuser or self.request.user.is_staff:
                print("Usuario es superusuario o staff, mostrando todas las tareas.")
                tareas = Tarea.objects.filter(proyecto_id=proyecto_id)
            elif self.request.user.is_authenticated:
                print(f"Filtrando tareas para usuario ID: {self.request.user.id}")  # Depuración
                q1 = models.Q(asignado_a=self.request.user)
                q2 = models.Q(usuarios_asignados=self.request.user)
                try:
                    print("Q1 creado:", q1)  # Depuración
                    print("Q2 creado:", q2)  # Depuración
                    tareas = Tarea.objects.filter(proyecto_id=proyecto_id).filter(q1 | q2)
                except Exception as e:
                    print(f"Error al crear el filtro: {e}")
                    tareas = Tarea.objects.none()
            else:
                print("Usuario no autenticado, devolviendo queryset vacío.")
                tareas = Tarea.objects.none()
            print(f"Tareas encontradas: {list(tareas)}")  # Depuración
            return tareas
        print("Proyecto ID no proporcionado, devolviendo queryset vacío.")
        return Tarea.objects.none()

    def get_context_data(self, **kwargs):
        """
        Agrega datos adicionales al contexto para la plantilla.
        
        Args:
            **kwargs: Argumentos adicionales pasados al contexto.
        
        Retorna:
            dict: El contexto actualizado con 'proyecto_id' y 'proyecto'.
        
        Lógica:
        - Si `proyecto_id` está presente, intenta obtener el objeto Proyecto correspondiente.
        - Si no existe el proyecto, establece 'proyecto' como None.
        - Si no hay `proyecto_id`, 'proyecto' también será None.
        """
        context = super().get_context_data(**kwargs)
        proyecto_id = self.kwargs.get('proyecto_id')
        context['proyecto_id'] = proyecto_id
        if proyecto_id:
            try:
                context['proyecto'] = get_object_or_404(Proyecto, id=proyecto_id)
            except Proyecto.DoesNotExist:
                context['proyecto'] = None
        else:
            context['proyecto'] = None
        return context



## Explicación

### Propósito
`TareaListView` se utiliza para mostrar una lista de tareas en la URL `/tareas/` (sin filtro de proyecto) o `/proyectos/<int:proyecto_id>/tareas/` (filtrado por proyecto). Requiere autenticación mediante `LoginRequiredMixin`, lo que redirige a la página de inicio de sesión si el usuario no está autenticado.

### Funcionalidad Clave
**Filtrado de tareas:**
- Si el usuario es superusuario o staff, ve todas las tareas del proyecto especificadas.
- Si es un usuario normal autenticado, solo ve las tareas donde sea el `asignado_a` o esté en `usuarios_asignados`.
- Usa objetos `Q` para combinar condiciones lógicas (OR) en el filtro.

**Contexto adicional:**
- Proporciona `proyecto_id` y `proyecto` al contexto para que la plantilla pueda mostrar detalles del proyecto asociado (si aplica).

### Dependencias
- `LoginRequiredMixin`: Para requerir autenticación.
- `ListView`: Para manejar la lista genérica de objetos.
- `models.Q`: Para consultas complejas con condiciones lógicas.
- `get_object_or_404`: Para obtener el objeto `Proyecto` de forma segura.

### Uso
Acceda a `/proyectos/1/tareas/` para ver las tareas del proyecto con ID 1. La plantilla `tareas/tarea_list.html` renderiza la lista de tareas y muestra enlaces para editar o eliminar.

### Notas de depuración
Los mensajes impresos están incluidos para depurar el flujo (proyecto ID, autenticación, filtros, etc.). Estos se pueden eliminar en producción.

### Mejoras futuras
- Agregar paginación para manejar grandes listas de tareas.
- Incluir filtros adicionales (por estado, fecha, etc.) en el queryset.
- Optimizar las consultas con `select_related` o `prefetch_related` para relaciones como `usuarios_asignados`.