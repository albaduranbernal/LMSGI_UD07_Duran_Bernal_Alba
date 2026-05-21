# Manual Técnico de Explotación - WillmanTech S.L.
**Cumplimiento Normativo: Estándar Internacional ISO/IEC/IEEE 26514:2022**
-----------------------------------------------------------------------------------------------------------------------------------

## 1. Introducción y Arquitectura
El sistema de gestión empresarial (ERP/CRM) de WillmanTech S.L. está diseñado bajo una arquitectura de microservicios contenerizados mediante Docker. Esta topología garantiza el aislamiento de dependencias, portabilidad y un escalado eficiente de los módulos integrados: Ventas, Facturación, Inventario y CRM.

### Topología Lógica del Despliegue
El entorno consta de dos contenedores principales interconectados mediante una red virtual interna aislada:
* **Contenedor Web/App (ERP):** Expone el core de la aplicación y gestiona las peticiones HTTP/HTTPS.
* **Contenedor SGBD:** Almacena de manera persistente las bases de datos relacionales en un entorno aislado.

----------------------------------------------------------------------------------------------------------------------------------

## 2. Guía de Instalación y Reinstalación
Para levantar la infraestructura tecnológica desde cero en entornos de staging o producción, ejecute el siguiente procedimiento guiado:

### Requisitos y Dependencias del SGBD
* Docker Engine y Docker Compose 
* SGBD Relacional: **PostgreSQL v15** (configurado con UTF-8 e integridad referencial estricta).

### Variables de Entorno Requeridas 
Antes del despliegue, configure el archivo de variables del sistema:

DB_USER=willman_admin
DB_PASSWORD=Secure_Crypto_Pass_2026!
DB_NAME=willmantech_prod
ERP_PORT=8069

-------------------------------------------------------------------------------------------------------------------------------
### Procedimiento de Backup
## 1. Clonar el repositorio de infraestructura e ingresar al directorio
cd /opt/willmantech-erp

## 2. Construir e iniciar los microservicios en segundo plano (detached mode)
docker-compose up -d --build

## 3. Verificar el correcto estado de ejecución de los contenedores
docker -compose ps

-------------------------------------------------------------------------------------------------------------------------------
### Comando de Restauración 

## 1. Limpieza y recreación de la base de datos destino
docker exec -it willmantech-db dropdb -U willman_admin willmantech_prod
docker exec -it willmantech-db createdb -U willman_admin willmantech_prod


## 2. Restauración del volcado binario de datos
docker exec -i willmantech-db pg_restore -U willman_admin -d willmantech_prod -v /backups/willmantech_destino.backup
