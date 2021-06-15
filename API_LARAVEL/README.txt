# Introduction
Esta API es capaz de gestionar recursos de Tipo Project, cada Project tiene asociada información que lo define y una serie de recursos Task.
Cada Task esta asociada a un Project.

# Overview
Esta es una API dummy para ser consumida por el cliente desarrollado en este :
[Repositorio](https://github.com/fenix15100/LaraReactNotes)

# Authentication
La API esta protejida via JWT, antes de poder usar las llamadas de esta API hay que registrarse en ella a traves de la llamada "Register in API" una vez hecho esto usar la llamada "Login in API" para obtener el TOKEN JWT, todas las demás llamadas de esta API deberán ser enviadas con un Header "Authentication" =>Bearer <token>

# Error Codes
## 400 Bad Request (Malformed request)
## 500 Internal Server Error (Error in Server o BBDD)
## 404 Not Found (Resource not found)

Puedes reutilizar esta API para usarla en cualquier cliente que desarrolles para hacer pruebas de concepto.

Enjoy!.