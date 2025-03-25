# Paradigmas API

## Definición de API  (Application Programming Interfaces - Interfaz de Programación de Aplicaciones) 
Una API es una interfaz que establece cómo se deben gestionar las solicitudes y respuestas mediante:  
✔ **Métodos**  
✔ **Endpoints**  
✔ **Tipos de datos**  
✔ **Protocolos**  

## ¿Qué es un Paradigma?  
Un **paradigma** es un modelo o enfoque que define cómo estructurar, diseñar o resolver un problema en un contexto específico.  

## ¿Qué es un Paradigma de API?  
Un **paradigma de API** es un conjunto de principios y enfoques para diseñar correctamente una API.  

✔ La API **expone** (pone a disposición) ciertos datos o funciones del backend para que otras aplicaciones puedan utilizarlos.  
✔ Permite que las aplicaciones interactúen con el backend **sin conocer su implementación interna**.  

---

# **Paradigma de Solicitud - Respuesta**  
**Ejemplos**: REST, RPC, SOAP, GraphQL.  

✔ Usa **protocolos web** como HTTP para manejar la comunicación cliente-servidor.  
✔ Se definen **endpoints** (URLs específicas) donde los clientes envían solicitudes para acceder o modificar recursos.  
✔ Los clientes envían **solicitudes HTTP** a los endpoints para obtener datos o realizar acciones en el servidor.  
✔ El servidor **procesa la solicitud** y devuelve una respuesta en **JSON** o **XML**.  

---

# **REST (Representational State Transfer - Transferencia de estado representacional)**  
✔ **La API más popular en el mercado**  
✔ Exponen datos como **recursos** y usan HTTP para realizar **operaciones CRUD**  
✔ Usa **JSON**  
✔ Permite que cualquier cliente (web, móvil, etc.) consuma la API sin importar la tecnología del backend  
✔ **Altamente escalable**  

**REST trabaja con entidades y recursos** (usuarios, productos, pedidos).  

### **Ejemplo de API REST**  
Obtener información de un usuario  
```http
GET /usuarios/123 HTTP/1.1
Host: api.ejemplo.com
Accept: application/json
```
Respuesta del servidor
```json
{
  "id": 123,
  "nombre": "Juan Pérez",
  "email": "juan@example.com",
  "edad": 25
}
```
### **Métodos HTTP en REST**  
| Método  | Descripción                     |
|---------|---------------------------------|
| **GET**    | Obtener un recurso           |
| **POST**   | Crear y guardar un nuevo recurso |
| **PUT**    | Modificar un recurso         |
| **DELETE** | Eliminar un recurso          |

### **Códigos de Estado HTTP**  
| Código  | Significado                   |
|---------|--------------------------------|
| **2XX** | Éxito                         |
| **3XX** | Recurso movido                 |
| **4XX** | Error del lado del cliente     |
| **5XX** | Error del lado del servidor    |

---

# **RPC (Remote Procedure Call - Llamada de Procedimiento Remoto)**  
✔ **API más simple**  
✔ Un cliente ejecuta un **bloque de código en otro servidor**  
✔ Mientras que REST se enfoca en **recursos**, RPC se enfoca en **acciones**  
✔ **Eficiente** y permite **llamadas directas a funciones**  
✔ **NO depende de HTTP**, puede usar:  
| Tecnología               | Descripción                                      |
|--------------------------|--------------------------------------------------|
| **Apache Thrift**        | Soporte para múltiples lenguajes de programación. |
| **gRPC** (Google Remote Procedure Call) | Ideal para microservicios debido a su alto rendimiento. |
| **Message Queue (MQ) + RPC** | Utilizado para sistemas de colas y comunicación asíncrona. |


**RPC trata con acciones y procedimientos** (*crearUsuario, eliminarUsuario*).  

### **Reglas básicas en RPC**  
1. Los **endpoints contienen el nombre de la operación** que se va a ejecutar.  
2. Las llamadas a la API se realizan con el **verbo HTTP más apropiado**:
### **Métodos HTTP en RPC**  
| Método  | Descripción                     |
|---------|---------------------------------|
| **GET**    | Para solicitudes de solo lectura |
| **POST**   | Para las demás operaciones |

### **Ejemplo de API RPC**  
Llamada a un procedimiento remoto para crear un usuario
```http
POST /rpc HTTP/1.1
Host: api.ejemplo.com
Content-Type: application/json

{
  "method": "crearUsuario",
  "params": {
    "nombre": "Juan Pérez",
    "email": "juan@example.com",
    "edad": 25
  }
}
```
Respuesta del servidor
```json
{
  "id": 123,
  "mensaje": "Usuario creado exitosamente"
}
```
# **GraphQL**  
✔ **Desarrollado por Facebook en 2012**  
✔ **Trabaja con una sola petición** (a diferencia de REST, que puede requerir múltiples llamadas)  
✔ El **cliente tiene control sobre la estructura y el contenido de la respuesta**  
✔ **Autodocumentado** desde el desarrollo  

**En GraphQL, el cliente puede especificar exactamente qué información necesita en su consulta.**  

### **Ejemplo de API GraphQL**  
Consulta de usuario en GraphQL: en **GraphQL**, el cliente puede solicitar exactamente los datos que necesita. 
```graphql
query ($id: String!) {  
  user(login: $id) {  
    name  
    company  
    createdAt  
  }  
}
```
Respuesta del servidor
```json
{
  "data": {
    "user": {
      "name": "Juan Pérez",
      "company": "TechCorp",
      "createdAt": "2024-03-24T12:00:00Z"
    }
  }
}
```
# **Comparación de Paradigmas API: Solicitud - Respuesta**


## **REST vs RPC vs GraphQL: Pros y Contras**

| Característica      | REST                                       | RPC                                        | GraphQL                                   |
|--------------------|-------------------------------------------|-------------------------------------------|-------------------------------------------|
| **Pros**           | Estandarización en métodos, argumentos y códigos de estado. <br> Utiliza características de HTTP. <br> Fácil de mantener y escalar. | Simple y fácil de entender. <br> Bajo consumo de ancho de banda. <br> Alto rendimiento. | Reduce múltiples viajes de ida y vuelta. <br> Evita versionado. <br> Introspección incorporada. |
| **Contras**        | Cargas útiles grandes. <br> Múltiples viajes de ida y vuelta en HTTP. | Difícil de descubrir. <br> Estándar limitado. <br> Puede generar una explosión de funciones. | Requiere análisis adicional de consultas. <br> Optimización del backend compleja. <br> Puede ser innecesariamente complejo para APIs simples. |
| **¿Cuándo usarlo?** | Para APIs que realizan operaciones CRUD. | Para APIs que exponen múltiples acciones. | Cuando se necesita flexibilidad en consultas y mantener consistencia. |

---

## **Características Principales**

| Característica       | REST                                          | RPC                                             | GraphQL                                        |
|---------------------|---------------------------------------------|----------------------------------------------|----------------------------------------------|
| **¿Qué es?**        | Expone datos como recursos y usa métodos HTTP estándar para CRUD. | Expone métodos basados en acciones, donde los clientes pasan el nombre del método y argumentos. | Un lenguaje de consulta para APIs, donde los clientes definen la estructura de la respuesta. |
| **Ejemplos de servicios** | Stripe, GitHub, Twitter, Google         | Slack, Flickr                               | Facebook, GitHub, Yelp                      |
| **Ejemplo de uso**  | `GET /users/<id>`                            | `GET users.get?id=<id>`                     | ```graphql query ($id: String!) { user(login: $id) { name company createdAt } }``` |
| **Uso de verbos HTTP** | `GET`, `POST`, `PUT`, `PATCH`, `DELETE`    | `GET`, `POST`                               | `GET`, `POST`                               |

---

## **GraphQL vs REST** 

| Característica              | **GraphQL**                                      | **REST**                                     |
|----------------------------|------------------------------------------------|---------------------------------------------|
| **Rendimiento**             | Más rápido al evitar múltiples llamadas de red. | Puede requerir varias llamadas de red para obtener toda la información. |
| **Complejidad de consulta** | Flexible pero puede volverse compleja si hay muchas relaciones de datos. | Consultas simples gracias a endpoints separados. |
| **Popularidad**             | En crecimiento. | Muy popular y ampliamente adoptado. |
| **Soporte y comunidad**     | En expansión. | Comunidad establecida y amplia documentación. |
| **Curva de aprendizaje**    | Pronunciada debido a su sintaxis y flexibilidad. | Sencilla y basada en estándares conocidos. |
| **Carga de archivos**       | No compatible de forma nativa. | Compatible. |
| **Caché web**               | Requiere librerías externas. | Integrado en la arquitectura HTTP. |
| **Caso de uso recomendado** | Múltiples microservicios y aplicaciones móviles. | Aplicaciones simples y basadas en recursos. |

---

# **Paradigma Basado en Eventos** 
Un paradigma basado en eventos es un modelo de programación donde el flujo de ejecución se determina por eventos, como interacciones del usuario, mensajes o cambios de estado.
## Problema con las APIs de Solicitud-Respuesta
Con las APIs de solicitud-respuesta, para servicios con datos que cambian constantemente, la respuesta puede volverse obsoleta rápidamente.

Esto sucede porque en una API de solicitud-respuesta (como REST o RPC), el cliente recibe los datos en el momento de la solicitud, pero si los datos en el servidor cambian después de esa respuesta, el cliente no se entera automáticamente.

### Polling
Los desarrolladores usan "polling" para consultar la API periódicamente y detectar cambios en los datos.

- **Polling con baja frecuencia**: Las aplicaciones pueden perder eventos.
- **Polling con alta frecuencia**: Se desperdician muchos recursos.

---

# WebHooks
- Simplemente es una URL que acepta una solicitud HTTP `POST` (o `GET`, `PUT` o `DELETE`).
- Permite recibir actualizaciones en **tiempo real**.
- Varios proveedores de API, como **Slack, Stripe, GitHub y Zapier**, los soportan.

## Polling vs WebHook
| Característica      | Polling                                      | WebHook                                  |
|--------------------|--------------------------------------------|-----------------------------------------|
| **Funcionamiento**  | El cliente consulta la API periódicamente. | El servidor envía datos automáticamente cuando hay cambios. |
| **Eficiencia**      | Ineficiente, genera muchas solicitudes innecesarias. | Eficiente, solo envía datos cuando es necesario. |
| **Frecuencia**      | Depende del intervalo definido por el cliente. | En tiempo real o casi en tiempo real. |
| **Carga en el servidor** | Alta, debido a múltiples solicitudes repetitivas. | Baja, ya que solo se envían datos cuando ocurre un evento. |
| **Implementación**  | Fácil, solo requiere hacer solicitudes HTTP periódicas. | Más compleja, requiere configurar un endpoint que reciba los datos. |
| **Ejemplos de uso** | Consultar actualizaciones de pedidos o notificaciones. | Notificaciones de pago (Stripe), eventos en repositorios (GitHub). |

## Consideraciones de WebHooks
- **Fallos**: Garantizar la entrega mediante reintentos.
- **Firewalls**: Las aplicaciones detrás de firewalls pueden enviar datos, pero recibirlos puede ser complicado.
- **Ruido**: Demasiados WebHooks en poco tiempo pueden generar ruido.

## Casos de Uso de WebHooks
- Una tienda en línea notificando a tu aplicación de facturación sobre una venta.
- Un proveedor de pagos notificando a los comerciantes sobre un pago.
- Sistemas de control de versiones notificando a los miembros del equipo sobre un commit en un repositorio.
- Sistemas de monitoreo alertando a los administradores sobre un error o actividad inusual en un sistema.

---

# WebSockets
- Utilizado para establecer un canal de comunicación bidireccional mediante una única conexión **TCP** (Transport Control Protocol).
- Permite una comunicación **full-dúplex**, lo que significa que el servidor y el cliente pueden comunicarse simultáneamente.

## Beneficio en APIs empresariales
Algunos desarrolladores empresariales que usan las APIs de **Slack** prefieren **WebSockets** en lugar de WebHooks, ya que pueden recibir eventos de la API de Slack de forma segura sin necesidad de exponer un endpoint HTTP WebHook en Internet.

## Pros y Contras de WebSockets
| Pros                                        | Contras                                  |
|---------------------------------------------|------------------------------------------|
| Comunicación bidireccional de baja latencia | Los clientes son responsables de las conexiones |
| Reducción de la sobrecarga de solicitudes HTTP | Desafíos de escalabilidad               |

---

# HTTP Streaming
- El servidor mantiene abierta una solicitud específica del cliente para enviar datos continuamente en la misma respuesta.

## Métodos para transmitir datos en **HTTP Streaming**:
1. **Transfer-Encoding: chunked**  
   - Indica que los datos llegarán en fragmentos delimitados por saltos de línea.
   - Fácil de procesar para los desarrolladores.

2. **Eventos enviados por el servidor (SSE - Server-Sent Events)**  
   - Ideal para clientes en navegadores, ya que pueden usar la API estándar **EventSource**.

## Uso de HTTP Streaming en Twitter
**Twitter** usa **HTTP Streaming** para enviar tweets en tiempo real a través de una única conexión, evitando la necesidad de hacer polling continuo a su API.

---

# Comparación: WebHooks vs WebSockets vs HTTP Streaming

| Característica      | WebHooks                                   | WebSockets                                | HTTP Streaming                             |
|--------------------|------------------------------------------|------------------------------------------|------------------------------------------|
| **¿Qué es?**      | Notificación de eventos vía callback HTTP | Conexión bidireccional de streaming sobre TCP | Conexión de larga duración sobre HTTP |
| **Ejemplos de servicios** | Slack, Stripe, GitHub, Zapier, Google | Slack, Trello, Blockchain | Twitter, Facebook |
| **Pros**          | Fácil comunicación entre servidores. <br> Usa protocolo HTTP. | Comunicación bidireccional en tiempo real. <br> Soporte nativo en navegador. <br> Puede evitar firewalls. | Puede transmitir sobre HTTP. <br> Soporte nativo en navegador. <br> Puede evitar firewalls. |
| **Contras**       | No funciona a través de firewalls ni en navegadores. <br> Manejar fallos, reintentos y seguridad es complicado. | Necesita mantener una conexión persistente. <br> No es HTTP. | La comunicación bidireccional es difícil. <br> Se requieren reconexiones para recibir diferentes eventos. |
| **¿Cuándo usarlo?** | Para activar eventos en tiempo real en el servidor. | Para comunicación bidireccional en tiempo real entre navegadores y servidores. | Para comunicación unidireccional sobre HTTP. |
