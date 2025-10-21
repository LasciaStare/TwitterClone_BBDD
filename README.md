# Bases de Datos - Laboratorio 03: Aplicación de Gestión de Posts y Comentarios

Este repositorio contiene el desarrollo de una aplicación para la gestión de posts y comentarios, implementada como parte del Laboratorio 03 de la asignatura de Bases de Datos. El objetivo principal es afianzar los conocimientos en diseño y modelamiento de bases de datos relacionales.

## 🚀 Tecnologías Utilizadas

*   **Lenguaje de Programación:** Python
*   **Framework:** Django
*   **Motor de Base de Datos:** SQLite

## 📦 Estructura del Proyecto

El proyecto incluye un diseño detallado de la base de datos y scripts para su creación:

1.  **Diagrama Entidad-Relación (ERD):** Visualización de las entidades principales (Usuarios, Posts, Comentarios, Tipos de Post) y sus relaciones.
2.  **Modelo Relacional:** Especificación de tablas, atributos, tipos de datos, claves primarias y foráneas, y restricciones de integridad.
3.  **Script SQL:** Un script para la creación de las tablas de la base de datos.

## 💡 Funcionalidades de la Aplicación

La aplicación ofrece un menú interactivo con las siguientes funcionalidades principales:

*   **Operaciones CRUD para Usuarios:** Crear, ver, actualizar y eliminar usuarios.
*   **Operaciones CRUD para Posts:** Crear, ver, actualizar y eliminar posts (con eliminación en cascada de comentarios).
*   **Operaciones CRUD para Comentarios:** Añadir, ver, actualizar y eliminar comentarios.
*   **Operaciones CRUD para Tipos de Posts:** Crear, ver, actualizar y eliminar tipos de post.
*   **Búsqueda de Posts:** Buscar posts por tipo, tema, autor y palabras clave.
*   **Visualización de Posts Completos:** Ver el contenido completo de un post y todos sus comentarios asociados.
*   **Listado de Usuarios y Cantidad de Posts:** Un listado que muestra cada usuario y el número total de posts que ha publicado.


### Restricciones Implementadas

*   Un post solo puede ser editado o eliminado por su autor.
*   Un comentario solo puede ser editado o eliminado por su autor.

## 🤝 Integrantes del Grupo

*   Juan Aguirre
*   Luis Cabarcas
*   Andres España
*   Jose Menco
*   Camilo Vargas

## Arquitectura y estructura de carpetas

```
Project/
├── blog/               # App principal (posts, comentarios, likes, hashtags)
│   ├── management/     # Comandos custom (p. ej. carga de datos dummy)
│   ├── templates/      # Vistas HTML (home, detalle, formularios, etc.)
│   ├── static/blog/    # CSS, JS (likes.js) e imágenes
│   └── serializers.py  # Exposición de entidades vía DRF
├── users/              # App para perfiles, registro y autenticación adicional
│   ├── templates/users/ # Formularios de registro, login, perfil, cambio de contraseña
│   └── forms.py         # Formularios personalizados (registro/edición)
├── django_project/     # Configuración global de Django (settings, urls)
├── media/              # Archivos subidos por los usuarios
├── staticfiles/        # Carpeta generada por `collectstatic`
├── requirements.txt    # Dependencias del proyecto
└── manage.py           # Punto de entrada de Django
```

## Requisitos previos

- Python 3.10 o superior
- Pip y `venv` habilitados
- SQLite (incluida por defecto con Python)
- (Opcional) Node/npm si se desea gestionar assets adicionales

## Instalación y puesta en marcha

1. **Clonar el repositorio**

    ```bash
    git clone https://github.com/LasciaStare/TwitterClone_BBDD.git
    cd TwitterClone_BBDD/Project
    ```

2. **Crear y activar entorno virtual** (PowerShell en Windows)

    ```powershell
    python -m venv .venv
    .\.venv\Scripts\Activate
    ```

3. **Instalar dependencias**

    ```powershell
    pip install --upgrade pip
    pip install -r requirements.txt
    ```

4. **Aplicar migraciones**

    ```powershell
    python manage.py migrate
    ```

5. **Crear superusuario (opcional pero recomendado)**

    ```powershell
    python manage.py createsuperuser
    ```

6. **Ejecutar el servidor de desarrollo**

    ```powershell
    python manage.py runserver
    ```

    Visita <http://127.0.0.1:8000/> en tu navegador y autentícate para acceder al feed.

## Uso de la aplicación

### Autenticación y perfiles
- Registro mediante formulario (`/register/`).
- Login (`/login/`) y logout (`/logout/`).
- Búsqueda de usuarios desde la barra de búsqueda interna.
- Página “Mi perfil” para actualizar nombre de usuario, email, cambiar contraseña y eliminar la cuenta definitivamente.

### Publicaciones y hashtags
- Crea publicaciones con el botón “Nuevo post”.
- Los hashtags se detectan automáticamente y permiten filtrar el feed (`/?type=hashtag`).
- Las publicaciones pueden editarse o borrarse por sus autores.

### Comentarios y likes
- Los comentarios se gestionan desde la página de detalle de cada post.
- El botón de “Me gusta” funciona sin recargar la página gracias a `likes.js`; si el usuario no ha iniciado sesión, se redirige al login.

### Búsquedas
- El campo superior realiza búsquedas tanto por hashtag (con o sin `#`) como por texto libre en contenido y usuarios.

## API REST integrada

La aplicación expone endpoints básicos mediante Django REST Framework:

- `GET /l/users/` – listado de usuarios autenticado
- `GET /l/groups/` – listado de grupos
- `GET | POST | DELETE /api/posts` – listado, creación y eliminación masiva de posts (requiere autenticación)

Para interactuar con la API, autentícate mediante la sesión de Django o usa tokens si añades un backend adicional.

## Gestión de datos de ejemplo

Existe un comando personalizado para poblar la base de datos con posts de prueba:

```powershell
python manage.py create_dummy_data
```

Puedes modificar el comando en `blog/management/commands/create_dummy_data.py` para ajustar la cantidad de entradas.

## Ejecución de pruebas

La suite de tests básicos se ejecuta con:

```powershell
python manage.py test
```

El comando crea una base de datos temporal, verifica modelos y vistas fundamentales, y luego limpia los datos.

## Buenas prácticas y seguridad

- Mantén actualizado el archivo `requirements.txt` y aplica parches de seguridad.
- Si despliegas en producción, configura variables de entorno (`SECRET_KEY`, `DEBUG`, `ALLOWED_HOSTS`) y ejecuta `python manage.py collectstatic`.
- Usa HTTPS en producción y un backend de correo real para la recuperación de contraseñas.
- Revisa los permisos de archivos subidos en `media/` y configura un almacenamiento apropiado (S3, Azure Blob, etc.).

## 🗓️ Fecha del Laboratorio

26 de septiembre de 2025

---
