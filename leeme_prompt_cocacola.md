Perfecto — voy a dejarte **todo hecho**: primero la **estructura de carpetas** y después **todos los procedimientos y archivos** (comandos, `models.py`, `views.py`, templates, `urls.py`, `admin.py`, etc.) para que el proyecto **UIII_Cocacola_1299** con Django funcione en el puerto **8036**. Seguí tu instrucción: **primero la estructura de carpetas**.

# Estructura de carpetas 

```
UIII_Cocacola_1299/
├─ .venv/                       # entorno virtual (oculto)
├─ backend_cocacola/            # proyecto Django (carpeta del proyecto)
│  ├─ backend_cocacola/
│  │  ├─ __init__.py
│  │  ├─ settings.py
│  │  ├─ urls.py
│  │  ├─ asgi.py
│  │  └─ wsgi.py
│  ├─ manage.py
│  └─ db.sqlite3                # (después de migrate)
├─ app_cocacola/                # aplicación Django
│  ├─ migrations/
│  │  └─ __init__.py
│  ├─ templates/
│  │  ├─ base.html
│  │  ├─ header.html
│  │  ├─ navbar.html
│  │  ├─ footer.html
│  │  ├─ inicio.html
│  │  └─ cliente/
│  │     ├─ agregar_cliente.html
│  │     ├─ ver_cliente.html
│  │     ├─ actualizar_cliente.html
│  │     └─ borrar_cliente.html
│  ├─ __init__.py
│  ├─ admin.py
│  ├─ apps.py
│  ├─ models.py
│  ├─ tests.py
│  ├─ urls.py
│  └─ views.py
├─ static/                      # (opcional) css, js, img locales
│  ├─ css/
│  ├─ js/
│  └─ img/
└─ README.md
```

---

# Procedimientos paso a paso (comandos y explicaciones)

> Asumo que usas Windows (PowerShell) o macOS/Linux; si necesitas comandos específicos para otro shell dímelo y lo adapto. No repetiré preguntas: procedo según lo pedido.

### 1) Crear carpeta del proyecto

Abre tu Explorador y crea la carpeta:

```
UIII_Cocacola_1299
```

### 2) Abrir VS Code sobre la carpeta

Desde el Explorador: `Abrir con VS Code` sobre la carpeta `UIII_Cocacola_1299`
O desde terminal:

```bash
cd /ruta/a/UIII_Cocacola_1299
code .
```

### 3) Abrir terminal en VS Code

Menú `Terminal > New Terminal`. Asegúrate de estar en la raíz `UIII_Cocacola_1299`.

### 4) Crear carpeta entorno virtual `.venv` desde terminal de VS Code

Windows (PowerShell):

```powershell
python -m venv .venv
```

macOS / Linux:

```bash
python3 -m venv .venv
```

### 5) Activar el entorno virtual

Windows (PowerShell):

```powershell
.venv\Scripts\Activate.ps1
# O si falla: .venv\Scripts\activate
```

macOS / Linux:

```bash
source .venv/bin/activate
```

(Al activarlo verás `(.venv)` al inicio del prompt.)

### 6) Activar intérprete de Python en VS Code

En VS Code: `Ctrl+Shift+P` → `Python: Select Interpreter` → elegir `./.venv` (asegúrate que aparezca la ruta del `.venv`).

### 7) Instalar Django

Con el entorno activado:

```bash
pip install django==4.2
# (o la versión que prefieras)
```

### 8) Crear proyecto `backend_cocacola` sin duplicar carpeta

En la raíz `UIII_Cocacola_1299` ejecuta:

```bash
django-admin startproject backend_cocacola
```

Si ya estás dentro de `backend_cocacola` y no querés carpeta extra, usa:

```bash
# Alternativa (cuando quieres crear proyecto en la carpeta actual):
django-admin startproject backend_cocacola .
```

(Usa la forma anterior si ya estás dentro de la carpeta destino; la instrucción estándar crea la carpeta `backend_cocacola` por ti.)

### 9) Ejecutar servidor en el puerto 8036

Primero crea la app (paso 11). Luego:

```bash
cd backend_cocacola
python manage.py runserver 8036
```

### 10) Copiar y pegar el link en el navegador

En el navegador abre:

```
http://127.0.0.1:8036/
```

(O `http://localhost:8036/`)

### 11) Crear la aplicación `app_cocacola`

Desde la carpeta `backend_cocacola` (la que contiene `manage.py`):

```bash
python manage.py startapp app_cocacola
```

---

# Archivos importantes y su contenido

> **Nota importante**: Dijiste "por lo pronto solo trabajar con Cliente, dejar pendiente Proveedor y Producto". Para evitar dependencias en las migraciones, **el `models.py` que te doy ahora contiene solo el modelo `Cliente`**. Al final incluyo los bloques comentados de `Proveedor` y `Producto` para que los añadas cuando quieras.

### `app_cocacola/models.py`

```python
from django.db import models

# ==========================================
# MODELO: CLIENTE
# ==========================================
class Cliente(models.Model):
    nombre = models.CharField(max_length=50)
    apellido = models.CharField(max_length=50)
    direccion = models.CharField(max_length=255)
    telefono = models.CharField(max_length=20)
    email = models.EmailField(max_length=100)
    fecha_registro = models.DateField(auto_now_add=True)
    preferencia = models.CharField(max_length=100, blank=True, null=True)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"

# ==========================================
# (PROVEEDOR y PRODUCTO quedan pendientes - abajo hay plantillas comentadas)
"""
class Proveedor(models.Model):
    nombre_empresa = models.CharField(max_length=100)
    contacto = models.CharField(max_length=100)
    telefono = models.CharField(max_length=20)
    correo = models.EmailField(max_length=100)
    direccion = models.CharField(max_length=200)
    pais = models.CharField(max_length=50)
    tipo_producto_suministro = models.CharField(max_length=100)

    def __str__(self):
        return self.nombre_empresa

class Producto(models.Model):
    nombre_producto = models.CharField(max_length=100)
    categoria = models.CharField(max_length=100)
    precio_unitario = models.DecimalField(max_digits=10, decimal_places=2)
    stock_actual = models.IntegerField()
    fecha_fabricacion = models.DateField()
    fecha_vencimiento = models.DateField()
    cliente = models.ForeignKey(Cliente, on_delete=models.CASCADE)
    proveedor = models.ForeignKey(Proveedor, on_delete=models.CASCADE)

    def __str__(self):
        return self.nombre_producto
"""
```

---

### 12.5) Procedimiento para realizar las migraciones

Desde `backend_cocacola` (carpeta con `manage.py`):

```bash
python manage.py makemigrations app_cocacola
python manage.py migrate
```

Si agregas modelos después: repetir `makemigrations` y `migrate`.

---

### 14) `app_cocacola/views.py` — funciones para Cliente (inicio, CRUD)

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Cliente
from django.urls import reverse
from django.utils import timezone

def inicio_cocacola(request):
    return render(request, 'inicio.html')

# Agregar cliente (muestra formulario y procesa POST)
def agregar_cliente(request):
    if request.method == 'POST':
        nombre = request.POST.get('nombre', '').strip()
        apellido = request.POST.get('apellido', '').strip()
        direccion = request.POST.get('direccion', '').strip()
        telefono = request.POST.get('telefono', '').strip()
        email = request.POST.get('email', '').strip()
        preferencia = request.POST.get('preferencia', '').strip()
        Cliente.objects.create(
            nombre=nombre,
            apellido=apellido,
            direccion=direccion,
            telefono=telefono,
            email=email,
            preferencia=preferencia
        )
        return redirect('ver_cliente')
    return render(request, 'cliente/agregar_cliente.html')

# Ver clientes
def ver_cliente(request):
    clientes = Cliente.objects.all().order_by('-fecha_registro')
    return render(request, 'cliente/ver_cliente.html', {'clientes': clientes})

# Mostrar formulario de actualización
def actualizar_cliente(request, cliente_id):
    cliente = get_object_or_404(Cliente, id=cliente_id)
    return render(request, 'cliente/actualizar_cliente.html', {'cliente': cliente})

# Procesar actualización
def realizar_actualizacion_cliente(request, cliente_id):
    if request.method == 'POST':
        cliente = get_object_or_404(Cliente, id=cliente_id)
        cliente.nombre = request.POST.get('nombre', cliente.nombre).strip()
        cliente.apellido = request.POST.get('apellido', cliente.apellido).strip()
        cliente.direccion = request.POST.get('direccion', cliente.direccion).strip()
        cliente.telefono = request.POST.get('telefono', cliente.telefono).strip()
        cliente.email = request.POST.get('email', cliente.email).strip()
        cliente.preferencia = request.POST.get('preferencia', cliente.preferencia).strip()
        cliente.save()
    return redirect('ver_cliente')

# Borrar cliente (confirmación)
def borrar_cliente(request, cliente_id):
    cliente = get_object_or_404(Cliente, id=cliente_id)
    if request.method == 'POST':
        cliente.delete()
        return redirect('ver_cliente')
    return render(request, 'cliente/borrar_cliente.html', {'cliente': cliente})
```

---

### 15) Carpeta `templates` dentro de `app_cocacola`

Crea `app_cocacola/templates/` y las subcarpetas indicadas (`cliente/`).

### 16) Archivos HTML a crear

A continuación te doy contenido listo para pegar.

#### `app_cocacola/templates/base.html`

```html
<!doctype html>
<html lang="es">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Sistema de Administración Coca Cola</title>
    <!-- Bootstrap CSS (CDN) -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body class="d-flex flex-column min-vh-100">
    {% include 'header.html' %}
    {% include 'navbar.html' %}
    <main class="container my-4">
      {% block content %}{% endblock %}
    </main>
    {% include 'footer.html' %}
    <!-- Bootstrap JS (CDN) -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

#### `app_cocacola/templates/header.html`

```html
<header class="bg-light py-2 border-bottom">
  <div class="container d-flex align-items-center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/9/94/Coca-Cola_logo.svg" alt="Logo" style="height:40px; margin-right:10px;">
    <h1 class="h5 mb-0">Sistema de Administración Coca Cola</h1>
  </div>
</header>
```

(La imagen es desde la red; puedes reemplazarla con una local en `static/img/` si prefieres.)

#### `app_cocacola/templates/navbar.html`

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container">
    <a class="navbar-brand" href="{% url 'inicio_cocacola' %}">Coca Cola</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMain">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navMain">
      <ul class="navbar-nav me-auto">
        <li class="nav-item">
          <a class="nav-link" href="{% url 'inicio_cocacola' %}">Inicio</a>
        </li>

        <!-- Cliente (submenú) -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="clienteMenu" role="button" data-bs-toggle="dropdown">
            <i class="bi bi-people-fill"></i> Cliente
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="{% url 'agregar_cliente' %}">Agregar Cliente</a></li>
            <li><a class="dropdown-item" href="{% url 'ver_cliente' %}">Ver Cliente</a></li>
          </ul>
        </li>

        <!-- Proveedor -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="proveedorMenu" role="button" data-bs-toggle="dropdown">
            <i class="bi bi-truck"></i> Proveedor
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Proveedor</a></li>
            <li><a class="dropdown-item" href="#">Ver Proveedor</a></li>
          </ul>
        </li>

        <!-- Producto -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="productoMenu" role="button" data-bs-toggle="dropdown">
            <i class="bi bi-box-seam"></i> Producto
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Producto</a></li>
            <li><a class="dropdown-item" href="#">Ver Producto</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</nav>

<!-- Bootstrap icons -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css">
```

> Nota: pediste íconos en las opciones principales (no en submenús) — añadí `bootstrap-icons`.

#### `app_cocacola/templates/footer.html`

```html
<footer class="mt-auto bg-light border-top py-3">
  <div class="container text-center">
    <small>© {{ now|date:"Y" }} - Creado por Alumna Ximena Reyes, CBTis 128. Todos los derechos reservados.</small>
  </div>
</footer>
```

> Para que `now` funcione, activa el context processor `django.template.context_processors.request` (viene por defecto); si no, puedes usar `{{ ""|date:"Y" }}`.

#### `app_cocacola/templates/inicio.html`

```html
{% extends 'base.html' %}
{% block content %}
  <div class="row">
    <div class="col-md-8">
      <h2>Bienvenido al Sistema de Administración Coca Cola</h2>
      <p>Este sistema permite administrar clientes (Agregar, Ver, Actualizar y Borrar). Proveedores y Productos quedan pendientes por ahora.</p>
    </div>
    <div class="col-md-4">
      <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Coca-Cola_company_logo.svg/320px-Coca-Cola_company_logo.svg.png" class="img-fluid" alt="Coca Cola">
    </div>
  </div>
{% endblock %}
```

(Imagen desde la red; reemplaza por local si prefieres.)

---

### 21) Crear subcarpeta `cliente` y los templates (archivos HTML)

#### `app_cocacola/templates/cliente/agregar_cliente.html`

```html
{% extends 'base.html' %}
{% block content %}
  <h3>Agregar Cliente</h3>
  <form method="post" action="{% url 'agregar_cliente' %}">
    {% csrf_token %}
    <div class="mb-3">
      <label class="form-label">Nombre</label>
      <input type="text" name="nombre" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Apellido</label>
      <input type="text" name="apellido" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Dirección</label>
      <input type="text" name="direccion" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Teléfono</label>
      <input type="text" name="telefono" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Correo</label>
      <input type="email" name="email" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Preferencia</label>
      <input type="text" name="preferencia" class="form-control">
    </div>
    <button class="btn btn-success" type="submit">Guardar</button>
    <a href="{% url 'ver_cliente' %}" class="btn btn-secondary">Volver</a>
  </form>
{% endblock %}
```

#### `app_cocacola/templates/cliente/ver_cliente.html`

```html
{% extends 'base.html' %}
{% block content %}
  <h3>Clientes</h3>
  <a href="{% url 'agregar_cliente' %}" class="btn btn-primary mb-3">Agregar Cliente</a>
  <table class="table table-striped">
    <thead>
      <tr>
        <th>Id</th>
        <th>Nombre</th>
        <th>Apellido</th>
        <th>Teléfono</th>
        <th>Correo</th>
        <th>Fecha registro</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      {% for c in clientes %}
      <tr>
        <td>{{ c.id }}</td>
        <td>{{ c.nombre }}</td>
        <td>{{ c.apellido }}</td>
        <td>{{ c.telefono }}</td>
        <td>{{ c.email }}</td>
        <td>{{ c.fecha_registro }}</td>
        <td>
          <a href="{% url 'actualizar_cliente' c.id %}" class="btn btn-sm btn-warning">Editar</a>
          <a href="{% url 'borrar_cliente' c.id %}" class="btn btn-sm btn-danger">Borrar</a>
        </td>
      </tr>
      {% empty %}
      <tr><td colspan="7">No hay clientes registrados.</td></tr>
      {% endfor %}
    </tbody>
  </table>
{% endblock %}
```

#### `app_cocacola/templates/cliente/actualizar_cliente.html`

```html
{% extends 'base.html' %}
{% block content %}
  <h3>Actualizar Cliente</h3>
  <form method="post" action="{% url 'realizar_actualizacion_cliente' cliente.id %}">
    {% csrf_token %}
    <div class="mb-3">
      <label class="form-label">Nombre</label>
      <input type="text" name="nombre" value="{{ cliente.nombre }}" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Apellido</label>
      <input type="text" name="apellido" value="{{ cliente.apellido }}" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Dirección</label>
      <input type="text" name="direccion" value="{{ cliente.direccion }}" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Teléfono</label>
      <input type="text" name="telefono" value="{{ cliente.telefono }}" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Correo</label>
      <input type="email" name="email" value="{{ cliente.email }}" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Preferencia</label>
      <input type="text" name="preferencia" value="{{ cliente.preferencia }}" class="form-control">
    </div>
    <button class="btn btn-success" type="submit">Guardar cambios</button>
    <a href="{% url 'ver_cliente' %}" class="btn btn-secondary">Cancelar</a>
  </form>
{% endblock %}
```

#### `app_cocacola/templates/cliente/borrar_cliente.html`

```html
{% extends 'base.html' %}
{% block content %}
  <h3>Eliminar Cliente</h3>
  <p>¿Deseas eliminar al cliente <strong>{{ cliente.nombre }} {{ cliente.apellido }}</strong>?</p>
  <form method="post">
    {% csrf_token %}
    <button type="submit" class="btn btn-danger">Sí, eliminar</button>
    <a href="{% url 'ver_cliente' %}" class="btn btn-secondary">No, regresar</a>
  </form>
{% endblock %}
```

---

### 24) `app_cocacola/urls.py` (rutas de la app)

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_cocacola, name='inicio_cocacola'),
    path('cliente/agregar/', views.agregar_cliente, name='agregar_cliente'),
    path('cliente/ver/', views.ver_cliente, name='ver_cliente'),
    path('cliente/actualizar/<int:cliente_id>/', views.actualizar_cliente, name='actualizar_cliente'),
    path('cliente/actualizar/realizar/<int:cliente_id>/', views.realizar_actualizacion_cliente, name='realizar_actualizacion_cliente'),
    path('cliente/borrar/<int:cliente_id>/', views.borrar_cliente, name='borrar_cliente'),
]
```

---

### 25) Agregar `app_cocacola` en `backend_cocacola/settings.py`

En `INSTALLED_APPS` añade la app:

```python
INSTALLED_APPS = [
    # apps por defecto...
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # tu app
    'app_cocacola',
]
```

Configura `TEMPLATES` y `STATIC` por defecto (Django ya trae configuración por defecto útil).

---

### 26) Configurar `backend_cocacola/urls.py` para enlazar la app

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_cocacola.urls')),  # rutas de la app en la raíz
]
```

---

### 27) `app_cocacola/admin.py` — registrar modelo Cliente

```python
from django.contrib import admin
from .models import Cliente

@admin.register(Cliente)
class ClienteAdmin(admin.ModelAdmin):
    list_display = ('id', 'nombre', 'apellido', 'telefono', 'email', 'fecha_registro')
    search_fields = ('nombre', 'apellido', 'email', 'telefono')
```

Luego:

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser   # crear usuario admin si quieres acceder a /admin/
```

---

### 28) Por lo pronto solo trabajar con Cliente

Ya lo implementamos así: modelos, vistas y plantillas solo para `Cliente`. `Proveedor` y `Producto` están listos como comentario para agregarlos cuando quieras.

---

### 29) Estética: colores suaves, modernos y HTML sencillo

Usé Bootstrap con `bg-primary` y colores suaves en layout. Si querés una paleta rosada (como en otros proyectos tuyos), dime y la adapto con CSS custom en `static/css/styles.css`.

---

### 30) No validar entrada de datos

Las vistas usan `request.POST` sin validaciones extras (tal como pediste).

---

### 31) Al inicio crear la estructura completa de carpetas y archivos

La estructura y todos los archivos clave fueron provistos arriba; pégalos en los archivos indicados y crea las carpetas.

---

### 32) Proyecto totalmente funcional

Resumen de pasos finales para dejarlo funcional:

1. Activar `.venv`.
2. `pip install django`
3. `django-admin startproject backend_cocacola`
4. `cd backend_cocacola`
5. `python manage.py startapp app_cocacola`
6. Crear los archivos `models.py`, `views.py`, `urls.py` de la app con los contenidos provistos.
7. Crear carpeta `templates` y archivos HTML con los contenidos provistos.
8. Añadir `app_cocacola` a `INSTALLED_APPS` en `backend_cocacola/settings.py`
9. En `backend_cocacola/urls.py` incluir la app (`path('', include('app_cocacola.urls'))`)
10. Migraciones:

```bash
python manage.py makemigrations
python manage.py migrate
```

11. Crear superusuario (opcional para admin):

```bash
python manage.py createsuperuser
```

12. Ejecutar servidor en puerto 8036:

```bash
python manage.py runserver 8036
```

13. Abrir en el navegador: `http://127.0.0.1:8036/`

---

### 33) Finalmente ejecutar servidor en el puerto 8036

Repetido para que no se pierda:

```bash
python manage.py runserver 8036
```

---

## Comentarios finales y recomendaciones rápidas

* **Migraciones**: si decides descomentar `Proveedor` y `Producto` más tarde, primero agrégalos al `models.py` y luego `makemigrations` y `migrate`. Ten cuidado con las relaciones FK: si `Producto` referencia `Proveedor` y `Cliente`, asegúrate que ambos modelos existan antes de migrar.
* **Imagenes desde la red**: usé imágenes públicas para `header` e `inicio`. Si prefieres usar imágenes locales, colócalas en `static/img/` y referencia con `{% static 'img/tuimagen.png' %}` (recuerda configurar `STATIC_URL` y `{% load static %}` en templates).
* **Estilo**: si querés una paleta específica (p. ej. rosada), puedo generar `static/css/styles.css` y modificar `base.html` para cargarlo.
* **No forms.py**: cumplido — usamos campos HTML y `request.POST`.

---

Si querés, ahora mismo (en este mismo mensaje) puedo:

* Generarte el archivo `settings.py` modificado con `STATIC`/`TEMPLATES` listos,
* O crear los archivos completos en un ZIP descargable.
  No necesito preguntar más: dime cuál de las dos opciones prefieres y lo preparo inmediatamente.
