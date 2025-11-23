# 🐳 Entorno de Desarrollo BBDD con Docker Compose (MVE)

Este repositorio contiene un **Entorno Mínimo Viable (MVE)** para desarrollo de bases de datos, fácil de configurar y ejecutar. Utiliza **MySQL 8.0** como motor de base de datos y **phpMyAdmin** para la gestión visual.

---

## 🚀 Requisitos Previos

* **Docker** instalado en tu máquina.
* **Docker Compose** instalado (generalmente incluido en Docker Desktop).

---

## 🛠️ Configuración e Instalación

### 1. Estructura del Proyecto
Crea un archivo llamado `docker-compose.yml` en la raíz de tu proyecto y pega el siguiente contenido:

```yaml
version: '3.8'

services:
  # 1. Servicio de Base de Datos: MySQL
  db:
    image: mysql:8.0
    container_name: mysql-dev-bbdd
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword   # ¡IMPORTANTE! Cambiar en producción
      MYSQL_DATABASE: mi_bbdd_dev
      MYSQL_USER: devuser
      MYSQL_PASSWORD: devpassword
    volumes:
      - db_data:/var/lib/mysql
    ports:
      - "3306:3306"

  # 2. Servicio de Gestión de Base de Datos: phpMyAdmin
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: phpmyadmin-dev-gui
    restart: always
    environment:
      PMA_HOST: db
      PMA_PORT: 3306
      MYSQL_ROOT_PASSWORD: rootpassword
    ports:
      - "8080:80"
    depends_on:
      - db

volumes:
  db_data:

Si aún no lo has hecho, clona este repositorio en tu máquina local:

```bash
git clone [URL_DEL_REPOSITORIO]
cd [NOMBRE_DEL_REPOSITORIO]
