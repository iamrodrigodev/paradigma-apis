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

- La API **expone** (pone a disposición) ciertos datos o funciones del backend para que otras aplicaciones puedan utilizarlos.  
- Permite que las aplicaciones interactúen con el backend **sin conocer su implementación interna**.  

---

# **Paradigma de Solicitud - Respuesta**  
**Ejemplos**: REST, RPC, SOAP, GraphQL.  

- Usa **protocolos web** como HTTP para manejar la comunicación cliente-servidor.  
- Se definen **endpoints** (URLs específicas) donde los clientes envían solicitudes para acceder o modificar recursos.  
- Los clientes envían **solicitudes HTTP** a los endpoints para obtener datos o realizar acciones en el servidor.  
- El servidor **procesa la solicitud** y devuelve una respuesta en **JSON** o **XML**.  

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
