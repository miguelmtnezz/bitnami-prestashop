# bitnami-prestashop
Repositorio practica Prestashop

Este repositorio trata de la utilizacion de la herramienta de Docker Compose, pero pra instalar una aplicacion Prestashop. La estructura de este repositorio
 sigue siendo igual que la del repositiorio anterior lo unico que cambiamos la imagenes de Worpress y MySQL por Prestashop y la utilizacion del servicio de Base 
 Datos como sería MariaDB:
 
 ```
 services:
  prestashop:
    image: bitnami/prestashop:1.7
    environment:
      - PRESTASHOP_FIRST_NAME=${PRESTASHOP_FIRST_NAME}
      - PRESTASHOP_LAST_NAME=${PRESTASHOP_LAST_NAME}
      - PRESTASHOP_PASSWORD=${PRESTASHOP_PASSWORD}
      - PRESTASHOP_EMAIL=${PRESTASHOP_EMAIL}
      - PRESTASHOP_HOST=${PRESTASHOP_HOST}
      - PRESTASHOP_ENABLE_HTTPS=${PRESTASHOP_ENABLE_HTTPS}
      - PRESTASHOP_COUNTRY=${PRESTASHOP_COUNTRY}
      - PRESTASHOP_LANGUAGE=${PRESTASHOP_LANGUAGE}
      - PRESTASHOP_DATABASE_HOST=${PRESTASHOP_DATABASE_HOST}
      - PRESTASHOP_DATABASE_NAME=${MYSQL_DATABASE}
      - PRESTASHOP_DATABASE_USER=${MYSQL_USER}
      - PRESTASHOP_DATABASE_PASSWORD=${MYSQL_PASSWORD}
    restart: always
    volumes:
      - prestashop_data:/bitnami/prestashop
    depends_on:
      - mariadb
    networks:
      - frontend_network
      - backend_network
  
  mariadb:
    image: mariadb:10.4
    environment:
      - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
      - MYSQL_DATABASE=${MYSQL_DATABASE}
      - MYSQL_USER=${MYSQL_USER}
      - MYSQL_PASSWORD=${MYSQL_PASSWORD}
    restart: always
    volumes:
      - mariadb_data:/var/lib/mysql
    networks:
      - backend_network
    security_opt:
      - seccomp:unconfined
 ```
 
 En el configuramos los volumenes e interfaces y variables de configuracion que estaran asociadas al fichero .env que se encuentra en este mismo
  repositorio para la configuracion de conexion y creacion de la Base de Datos y credenciales de acceso para la misma y la aplicacion.
  
  ```
  # Configuración de acceso a la base de datos
MYSQL_ROOT_PASSWORD=password
MYSQL_DATABASE=prestashop_db
MYSQL_USER=prestashop_user
MYSQL_PASSWORD=prestashop_password

# Configuración de PrestaShop
PRESTASHOP_FIRST_NAME=Usuario
PRESTASHOP_LAST_NAME=Apellido
PRESTASHOP_PASSWORD=admin_password
PRESTASHOP_EMAIL=admin@mail.es
PRESTASHOP_HOST=practica16iaw.ddns.net
PRESTASHOP_ENABLE_HTTPS=yes
PRESTASHOP_COUNTRY=es
PRESTASHOP_LANGUAGE=es
PRESTASHOP_DATABASE_HOST=mariadb
  ```
