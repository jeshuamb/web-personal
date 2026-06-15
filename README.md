# Web Personal - Jesús Marín

Portafolio web personal construido con Django 6.0.5. Incluye página de perfil, sección acerca de, galería de proyectos y página de contacto.

## Estructura del proyecto

Dos aplicaciones Django:

- **core** -- Páginas estáticas: inicio, acerca de y contacto. Sin modelos, solo vistas que renderizan templates.
- **portfolio** -- Gestión de proyectos. Incluye el modelo `Project` con título, descripción, imagen, link opcional y marcas de tiempo. Los proyectos se ordenan del más reciente al más antiguo y se administran desde el panel de Django admin.

Los templates usan Bootstrap 4, Font Awesome 4 y un tema Clean Blog. El layout base está en `base.html` con bloques para título, imagen de fondo, encabezados y contenido que cada página extiende.

## Requisitos

- Python 3.10+
- Django 6.0.5
- MySQL (probado en 8.x)
- Pillow (para subida de imágenes)
- mysqlclient (o PyMySQL como alternativa)

Debe existir una base de datos MySQL llamada `webpersonaldb`. La conexión por defecto apunta a `127.0.0.1:3306` con usuario `root`.

## Instalación

```bash
# Crear y activar un entorno virtual
python -m venv venv
venv\Scripts\activate   # Windows
# source venv/bin/activate   # Linux / macOS

# Instalar dependencias
pip install -r requirements.txt

# Configurar la conexión a la base de datos en webpersonal/settings.py
# si tus credenciales de MySQL son distintas a las que vienen por defecto.

# Crear la base de datos
mysql -u root -p -e "CREATE DATABASE webpersonaldb CHARACTER SET utf8mb4;"

# Ejecutar migraciones
python manage.py migrate

# Crear un superusuario para el panel de administración
python manage.py createsuperuser

# Iniciar el servidor de desarrollo
python manage.py runserver
```

El sitio estará disponible en `http://127.0.0.1:8000/`.

## Configuración

Todos los ajustes están en `webpersonal/settings.py`:

| Ajuste | Valor por defecto |
|---|---|
| `DEBUG` | `True` |
| `LANGUAGE_CODE` | `es` |
| `TIME_ZONE` | `UTC` |
| `DATABASES` | MySQL, `webpersonaldb` |
| `MEDIA_ROOT` | `BASE_DIR / media` |
| `ALLOWED_HOSTS` | `127.0.0.1`, `localhost`, IPs locales |

Antes de desplegar, cambiar `DEBUG = False` y actualizar `ALLOWED_HOSTS`.

## Páginas

| URL | Vista | Descripción |
|---|---|---|
| `/` | `core.views.home` | Página de inicio con resumen del perfil |
| `/about-me/` | `core.views.about` | Biografía y antecedentes |
| `/portfolio/` | `portfolio.views.portfolio` | Galería de proyectos con imágenes y descripciones |
| `/contact/` | `core.views.contact` | Información de contacto |
| `/admin/` | Admin de Django | Gestión de proyectos y usuarios |

## Administrar proyectos

Ingresar a `/admin/` con la cuenta de superusuario. El modelo Project tiene estos campos:

- **Título** -- obligatorio, máximo 200 caracteres
- **Descripción del Proyecto** -- texto largo
- **Imagen** -- se sube a `media/projects/`
- **Link de GitHub** -- opcional, campo URL
- **Fecha de Creación** -- se asigna automáticamente, solo lectura en admin
- **Fecha de Modificación** -- se asigna automáticamente, solo lectura en admin

## Licencia

Proyecto personal. Sin licencia especificada.

## Vista de Web Personal

### Página de perfil

![Perfil](assets/perfil.png)

### Página de Acerca de 

![TaskMaster](assets/about.png)

### Portafolio de proyectos

![Portafolio](assets/portafolio.png)

### Página de contacto

![Contacto](assets/contacto.png)


