# WordPress Docker Local Development Environment (English)

This project provides a Docker Compose setup to run a WordPress local development environment easily and portably.

## ✨ Key Features

*   **Portable:** The entire environment, including WordPress files and the MySQL database, is stored within the project folder (`./www/` for WordPress, `./data/` for the database). This makes it easy to create backups, share the environment, or move it between different machines.
*   **Isolated:** Uses Docker to ensure the development environment does not interfere with other local or system configurations.
*   **Easy to Use:** Start all services with a simple command (`docker-compose up -d`) and stop them with (`docker-compose down`).
*   **phpMyAdmin Included:** Easily access the database through phpMyAdmin for visual management.
*   **Pre-configured:** A ready-to-use WordPress environment with a basic setup.

## 📋 Prerequisites

Ensure you have installed:
*   [Docker](https://www.docker.com/get-started)
*   [Docker Compose](https://docs.docker.com/compose/install/) (usually included with Docker Desktop)

## 📁 Project Structure

*   `docker-compose.yml`: Main Docker Compose configuration file that defines the services (WordPress, MySQL, phpMyAdmin).
*   `./data/`: Contains the MySQL database files. This folder is created by Docker when starting the services and is ignored by Git thanks to the `.gitignore` file.
*   `./www/`: Contains WordPress core files, themes, plugins, and uploaded files. This folder is created by Docker and is also ignored by Git.
*   `./apache-config.conf`: Additional configuration file for Apache (used by WordPress and phpMyAdmin containers, e.g., for `ServerName`).
*   `.gitignore`: Specifies files and folders that Git should ignore (like `./data/` and `./www/`).

## 🚀 Usage

1.  **Clone the Repository (if applicable) or Download the Files:**
    If you have uploaded this project to a Git repository:
    ```bash
    git clone <REPOSITORY_URL>
    cd <PROJECT_DIRECTORY_NAME>
    ```
    Otherwise, just make sure you have `docker-compose.yml` and `apache-config.conf` in your working directory.

2.  **Start the Services:**
    Navigate to the project's root directory (where the `docker-compose.yml` file is located) and run:
    ```bash
    docker-compose up -d
    ```
    This will download the necessary Docker images (if it's the first time) and create and start the containers in the background (`-d`).

3.  **Access the Services:**
    *   **WordPress:** Open your browser and go to `http://localhost` (or `http://localhost:80`).
        *   The first time, you will be guided through the WordPress installation process.
        *   Use the following database connection details during WordPress installation (these are defined in `docker-compose.yml`):
            *   Database Name: `wordpress`
            *   User: `wordpress`
            *   Password: `wordpress`
            *   Database Host: `db` (this is the name of the database service in `docker-compose.yml`)
            *   Table Prefix: `dockwp_` (pre-configured in `docker-compose.yml`)
    *   **phpMyAdmin:** Open your browser and go to `http://localhost:8080`.
        *   Server: `db`
        *   User: `root`
        *   Password: `password` (this is the `MYSQL_ROOT_PASSWORD` defined in `docker-compose.yml`)

4.  **Stop the Services:**
    To stop all containers associated with this project, run in the same directory:
    ```bash
    docker-compose down
    ```
    This will stop and remove the containers. Data in `./data/` and `./www/` will persist on your local system as they are mapped as volumes.

## 🔧 Customization

You can customize the configuration by editing the `docker-compose.yml` file:

*   **Database Credentials:** Modify the `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD` environment variables under the `db` service. Remember to also update the `WORDPRESS_DB_USER`, `WORDPRESS_DB_PASSWORD` variables in the `wordpress` service.
*   **WordPress/MySQL/phpMyAdmin Versions:** Change the image tags (e.g., `wordpress:latest`, `mysql:5.7`, `phpmyadmin/phpmyadmin:latest`).
*   **Ports:** Adjust port mappings if you have conflicts. For example, if port `8080` is already in use, you can change `8080:80` to `8081:80` for phpMyAdmin. The same applies to WordPress port `80`.

### Note on Environment Variables and `.env` File

This setup uses generic credentials directly in the `docker-compose.yml` file to simplify the startup of a local development environment. A separate `.env` file for environment variables is not used to keep the configuration as straightforward as possible for this purpose. If you need greater security or credential customization for a production or shared environment, consider adapting the configuration to use an `.env` file.

---

## 🙏 Acknowledgements

Special thanks to Oscar García ([@opobla](https://github.com/opobla)) for introducing me to the power of Docker.

---

Enjoy your portable and easy-to-manage local WordPress development environment!

---
---

# Entorno de Desarrollo Local de WordPress con Docker (Español)

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

### Nota sobre Variables de Entorno y Archivo `.env`

Esta configuración utiliza credenciales genéricas directamente en el archivo `docker-compose.yml` para simplificar la puesta en marcha de un entorno de desarrollo local. No se utiliza un archivo `.env` separado para las variables de entorno con el fin de mantener la configuración lo más directa posible para este propósito. Si necesitas una mayor seguridad o personalización de las credenciales para un entorno de producción o compartido, considera adaptar la configuración para usar un archivo `.env`.

---

## 🙏 Agradecimientos

Un agradecimiento especial a Oscar García ([@opobla](https://github.com/opobla)) por darme a conocer el poder de Docker.

---

¡Disfruta de tu entorno de desarrollo local de WordPress portable y fácil de gestionar!
