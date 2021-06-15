##  API de Integración

Bienvenido a la documentación de nuestra api de integración. Aquí encontrarás todo lo necesario para integrarse a nuestro ecommerce, con un desglosamiento de todas sus peticiones y múltiples ejemplos para comprender sus distintas URIs.

En esta documentación nos encontraremos con varios directorios, los cuales (a excepción del primero, en el que se contienen la petición de autenticación) harán referencia cada uno a un recurso de nuestra API en concreto. Dentro de cada uno de estos directorios habrán distintas requests con sus métodos HTTP (GET, POST, PUT, DELETE). Éstas contendrán una gama de peticiones de dicho tipo HTTP con distintos parámetros.

El orden del consumo de los endpoints viene dado por el número de los directorios que contiene esta documentación, empezando por "1. Tiendas y canales de venta.", seguido por "2. Listas" y así consecutivamente hasta el último "3. Productos.".
##### LINK PUBLICO DE LA COLECCIÓN: https://www.getpostman.com/collections/fc82d00b525f8178367a

![](https://s3-us-west-2.amazonaws.com/api.v3.documentation/xmart_integration.jpeg)

#### DIAGRAMA DE LA ESTRUCTURA GENERAL DE LOS ENDPOINTS.

![](https://s3-us-west-2.amazonaws.com/api.v3.documentation/json_overview_v3_api_listing.png)


#### VERSIONAMIENTO
|Versión| Fecha |Descripción|Autor(es)|
|--|--|--|--|
| Versión 1 | 26/06/2020 |Creación del documento| Alex Guamán|
| Versión 1.0.1 | 29/06/2020 |Actualización de ejemplos para creación de listas, cambio de nombre para el path de listas (sección 2).| Alex Guamán|
| Versión 1.0.2 | 07/07/2020 |- Documentación para el proceso de creación de clientes oAuth (sección autenticación).<br> - Soporte para información adicional en modifiers, modifiers options y products (sección 1).<br>- Soporte mostrar u ocultar modifiers (sección 1).<br>- Documentación para creación y asignacion de bodegas a tiendas.<br>- Documentación para creación y actualización de stock de productos.| Alex Guamán|
| Versión 1.0.3 | 08/07/2020 |- Actualización del proceso de creación de clientes oAuth (sección autenticación).<br> - Las cadenas ahora se conocerán como marcas.<br>- Ejemplos descargables para zonas de cobertura, ciudades, sectores, marcas.<br>| Alex Guamán|
| Versión 1.0.4 | 10/07/2020 |- **Cambio de path** para el proceso de autenticación (sección autenticación).<br> - **Cambio Content-Type de autenticación** el body debe ser de tipo **JSON** anteriormente era de tipo "application/x-www-form-urlencoded" (sección autenticación).<br> - Es obligatorio el envío de dos **nuevos headers  (Platform: oauth y client-version: 3)**  a todas las peticiones excepto autenticación.<br>| Alex Guamán|
| Versión 1.0.5 **OBLIGATORIO !!!**| 27/07/2020 |- Se añadió el parámetro **vendorId** en la creación de listas (sección 2.)<br>| Alex Guamán|
| Versión 1.0.6 | 27/07/2020 |- Se añadió documentación sobre errores de validación y estados de respuesta.<br>| Alex Guamán|
| Versión 1.0.7 | 31/07/2020 |- Se añadió documentación sobre venta cruzada (cross selling).<br>- Ahora es posible definir la posición de los modificadores en productos.<br>| Alex Guamán|
| Versión 1.0.8 | 01/09/2020 |- Se actualizó los tipos de modificadores. <br>| Alex Guamán|
| Versión 1.0.9 | 20/10/2020 |- Éndpoint para obtener informe de sincronización. <br>- Soporte para activación e inactivación programada de tiendas y productos. <br>| Alex Guamán|
| Versión 1.0.10 | 12/01/2020 |- Lista de canales estandarizados.| Alex Guamán|
| Versión 1.0.11 | 12/22/2020 |- Soporte para channelReferenceName para el endpoint de resumen de sincronización.| Alex Guamán|
| Versión 1.0.12 | 12/22/2020 |- Documentación para configuración de botones de pago (sección 1).| Alex Guamán|
| Versión 1.0.13 | 12/30/2020 |- Soporte para listas relacionadas a nivel de canales de venta (sección 1).| Alex Guamán|