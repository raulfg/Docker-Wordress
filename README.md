# WordPress Docker Local Development Environment

Este proyecto proporciona una configuración de Docker Compose para ejecutar un entorno de desarrollo local de WordPress de forma sencilla y portable.

## ✨ Características Principales

*   **Portable:** Todo el entorno, incluyendo los archivos de WordPress y la base de datos MySQL, se almacena dentro de la carpeta del proyecto (`./www/` para WordPress, `./data/` para la base de datos). Esto facilita la creación de copias de seguridad, compartir el entorno o moverlo entre diferentes máquinas.
*   **Aislado:** Utiliza Docker para asegurar que el entorno de desarrollo no interfiera con otras configuraciones locales o del sistema.
*   **Fácil de Usar:** Inicia todos los servicios con un simple comando (`docker-compose up -d`) y detenlos con (`docker-compose down`).
*   **phpMyAdmin Incluido:** Accede fácilmente a la base de datos a través de phpMyAdmin para una gestión visual.
*   **Pre-configurado:** Un entorno de WordPress listo para usar con una configuración básica.

## 📋 Requisitos Previos

Asegúrate de tener instalados:
*   [Docker](https://www.docker.com/get-started)
*   [Docker Compose](https://docs.docker.com/compose/install/) (generalmente se incluye con Docker Desktop)

## 📁 Estructura del Proyecto

*   `docker-compose.yml`: Archivo principal de configuración de Docker Compose que define los servicios (WordPress, MySQL, phpMyAdmin).
*   `./data/`: Contiene los archivos de la base de datos MySQL. Esta carpeta es creada por Docker al iniciar los servicios y está ignorada por Git gracias al archivo `.gitignore`.
*   `./www/`: Contiene los archivos del núcleo de WordPress, temas, plugins y archivos subidos. Esta carpeta es creada por Docker y también está ignorada por Git.
*   `./apache-config.conf`: Archivo de configuración adicional para Apache (utilizado por los contenedores de WordPress y phpMyAdmin, por ejemplo, para `ServerName`).
*   `.gitignore`: Especifica los archivos y carpetas que Git debe ignorar (como `./data/` y `./www/`).

## 🚀 Uso

1.  **Clonar el Repositorio (si aplica) o Descargar los Archivos:**
    Si has subido este proyecto a un repositorio Git:
    ```bash
    git clone <URL_DEL_REPOSITORIO>
    cd <NOMBRE_DEL_DIRECTORIO_DEL_PROYECTO>
    ```
    Si no, simplemente asegúrate de tener `docker-compose.yml` y `apache-config.conf` en tu directorio de trabajo.

2.  **Iniciar los Servicios:**
    Navega al directorio raíz del proyecto (donde se encuentra el archivo `docker-compose.yml`) y ejecuta:
    ```bash
    docker-compose up -d
    ```
    Esto descargará las imágenes de Docker necesarias (si es la primera vez) y creará e iniciará los contenedores en segundo plano (`-d`).

3.  **Acceder a los Servicios:**
    *   **WordPress:** Abre tu navegador y ve a `http://localhost` (o `http://localhost:80`).
        *   La primera vez, serás guiado a través del proceso de instalación de WordPress.
        *   Utiliza las siguientes credenciales para la conexión a la base de datos durante la instalación de WordPress (estas están definidas en `docker-compose.yml`):
            *   Nombre de la base de datos: `wordpress`
            *   Usuario: `wordpress`
            *   Contraseña: `wordpress`
            *   Host de la base de datos: `db` (este es el nombre del servicio de la base de datos en `docker-compose.yml`)
            *   Prefijo de tabla: `dockwp_` (preconfigurado en `docker-compose.yml`)
    *   **phpMyAdmin:** Abre tu navegador y ve a `http://localhost:8080`.
        *   Servidor: `db`
        *   Usuario: `root`
        *   Contraseña: `password` (es la `MYSQL_ROOT_PASSWORD` definida en `docker-compose.yml`)

4.  **Detener los Servicios:**
    Para detener todos los contenedores asociados a este proyecto, ejecuta en el mismo directorio:
    ```bash
    docker-compose down
    ```
    Esto detendrá y eliminará los contenedores. Los datos en `./data/` y `./www/` persistirán en tu sistema local, ya que están mapeados como volúmenes.

## 🔧 Personalización

Puedes personalizar la configuración editando el archivo `docker-compose.yml`:

*   **Credenciales de la Base de Datos:** Modifica las variables de entorno `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD` bajo el servicio `db`. Recuerda actualizar también las variables `WORDPRESS_DB_USER`, `WORDPRESS_DB_PASSWORD` en el servicio `wordpress`.
*   **Versión de WordPress/MySQL/phpMyAdmin:** Cambia las etiquetas de las imágenes (ej. `wordpress:latest`, `mysql:5.7`, `phpmyadmin/phpmyadmin:latest`).
*   **Puertos:** Ajusta los mapeos de puertos si tienes conflictos. Por ejemplo, si el puerto `8080` ya está en uso, puedes cambiar `8080:80` a `8081:80` para phpMyAdmin. Lo mismo aplica para el puerto `80` de WordPress.

---

### Nota sobre Variables de Entorno y Archivo `.env`

Esta configuración utiliza credenciales genéricas directamente en el archivo `docker-compose.yml` para simplificar la puesta en marcha de un entorno de desarrollo local. No se utiliza un archivo `.env` separado para las variables de entorno con el fin de mantener la configuración lo más directa posible para este propósito. Si necesitas una mayor seguridad o personalización de las credenciales para un entorno de producción o compartido, considera adaptar la configuración para usar un archivo `.env`.

---

¡Disfruta de tu entorno de desarrollo local de WordPress portable y fácil de gestionar!
