# Manual Técnico de Explotación - WillmanTech S.L.
**Cumplimiento Normativo: Estándar Internacional ISO/IEC/IEEE 26514:2022**


## 1. Introducción y Arquitectura
El sistema de gestión empresarial (ERP/CRM) de WillmanTech S.L. está diseñado bajo una arquitectura de microservicios contenerizados mediante **Docker**. Esta topología garantiza el aislamiento de dependencias, portabilidad y un escalado eficiente de los módulos integrados: Ventas, Facturación, Inventario y CRM.

### Topología Lógica del Despliegue (`docker-compose.yml`)
El entorno consta de dos contenedores principales interconectados mediante una red virtual interna aislada:
* **Contenedor Web/App (ERP):** Expone el core de la aplicación y gestiona las peticiones HTTP/HTTPS.
* **Contenedor SGBD:** Almacena de manera persistente las bases de datos relacionales en un entorno aislado.



## 2. Guía de Instalación y Reinstalación
Para levantar la infraestructura tecnológica desde cero en entornos de staging o producción, ejecute el siguiente procedimiento guiado:


