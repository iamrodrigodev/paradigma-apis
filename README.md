# 🌍 Paradigmas de API

## 📌 Definición de API (Application Programming Interfaces)  
Una **API** es una interfaz que establece cómo gestionar solicitudes y respuestas mediante:  
✔ **Métodos**  
✔ **Endpoints**  
✔ **Tipos de datos**  
✔ **Protocolos**  

---

## 🤔 ¿Qué es un Paradigma?  
Un **paradigma** es un modelo o enfoque que define cómo estructurar, diseñar o resolver un problema en un contexto específico.  

## 🔄 ¿Qué es un Paradigma de API?  
Un **paradigma de API** es un conjunto de principios y enfoques para diseñar correctamente una API.  

✔ La API **expone** (pone a disposición) ciertos datos o funciones del backend para que otras aplicaciones puedan utilizarlos.  
✔ Permite que las aplicaciones interactúen con el backend **sin conocer su implementación interna**.  

---

# 🔄 Paradigma de Solicitud - Respuesta  
**Ejemplos**: REST, RPC, SOAP, GraphQL.  

✔ Usa **protocolos web** como HTTP para manejar la comunicación cliente-servidor.  
✔ Se definen **endpoints** (URLs específicas) donde los clientes envían solicitudes para acceder o modificar recursos.  
✔ Los clientes envían **solicitudes HTTP** a los endpoints para obtener datos o realizar acciones en el servidor.  
✔ El servidor **procesa la solicitud** y devuelve una respuesta en **JSON** o **XML**.  

---

# 🌐 REST (Representational State Transfer)  
✔ **La API más popular en el mercado**  
✔ Exponen datos como **recursos** y usan HTTP para realizar **operaciones CRUD**  
✔ Usa **JSON**  
✔ Permite que cualquier cliente (web, móvil, etc.) consuma la API sin importar la tecnología del backend  
✔ **Altamente escalable**  

### 📌 Ejemplo de API REST  
```http
GET /usuarios/123 HTTP/1.1
Host: api.ejemplo.com
Accept: application/json
```
📨 **Respuesta del servidor**  
```json
{
  "id": 123,
  "nombre": "Juan Pérez",
  "email": "juan@example.com",
  "edad": 25
}
```

### 🔹 Métodos HTTP en REST  
| Método  | Descripción                     |
|---------|---------------------------------|
| **GET**    | Obtener un recurso           |
| **POST**   | Crear y guardar un nuevo recurso |
| **PUT**    | Modificar un recurso         |
| **DELETE** | Eliminar un recurso          |

### 📊 Códigos de Estado HTTP  
| Código  | Significado                   |
|---------|--------------------------------|
| **2XX** | ✅ Éxito                         |
| **3XX** | 🔀 Recurso movido                 |
| **4XX** | ⚠️ Error del lado del cliente     |
| **5XX** | ❌ Error del lado del servidor    |

---

# 🔗 RPC (Remote Procedure Call)  
✔ **API más simple**  
✔ Un cliente ejecuta un **bloque de código en otro servidor**  
✔ Mientras que REST se enfoca en **recursos**, RPC se enfoca en **acciones**  
✔ **Eficiente** y permite **llamadas directas a funciones**  
✔ **NO depende de HTTP**, puede usar:  

| 🛠️ Tecnología  | 📌 Descripción |
|---------------|--------------|
| **Apache Thrift**  | Soporte para múltiples lenguajes de programación. |
| **gRPC** (Google RPC) | Ideal para microservicios debido a su alto rendimiento. |
| **Message Queue (MQ) + RPC** | Utilizado para sistemas de colas y comunicación asíncrona. |

### 📌 Ejemplo de API RPC  
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
📨 **Respuesta del servidor**  
```json
{
  "id": 123,
  "mensaje": "Usuario creado exitosamente"
}
```

---

# 🚀 GraphQL  
✔ **Desarrollado por Facebook en 2012**  
✔ **Trabaja con una sola petición** (a diferencia de REST, que puede requerir múltiples llamadas)  
✔ El **cliente tiene control sobre la estructura y el contenido de la respuesta**  
✔ **Autodocumentado** desde el desarrollo  

### 📌 Ejemplo de API GraphQL  
```graphql
query ($id: String!) {  
  user(login: $id) {  
    name  
    company  
    createdAt  
  }  
}
```
📨 **Respuesta del servidor**  
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

---

# 📡 Paradigma Basado en Eventos  
### ❌ Problema con las APIs de Solicitud-Respuesta  
✔ Las respuestas pueden quedar obsoletas rápidamente.  
✔ Se usa "Polling" para actualizar datos, pero consume muchos recursos.  

| 🔄 Tipo de Polling  | 📌 Descripción  |
|--------------------|--------------|
| **Baja frecuencia** | ⚠️ Puede perder eventos. |
| **Alta frecuencia** | ❌ Desperdicio de recursos. |

---

# 🔔 WebHooks  
✔ Envían datos en **tiempo real** a una URL específica.  
✔ Usado por **Slack, Stripe, GitHub y Zapier**.  

---

# 📶 WebSockets  
✔ Protocolo **full-dúplex** sobre TCP.  
✔ Comunicación bidireccional en tiempo real.  

---

# 📡 Comparación: WebHooks vs WebSockets vs HTTP Streaming  

| Característica      | WebHooks 📩 | WebSockets 🔄 | HTTP Streaming 📡 |
|--------------------|------------|--------------|-----------------|
| **Funcionamiento**  | Notificación de eventos vía HTTP | Comunicación bidireccional sobre TCP | Conexión de larga duración sobre HTTP |
| **Ejemplos de uso** | Slack, Stripe, GitHub | Slack, Trello, Blockchain | Twitter, Facebook |
| **Pros**           | Fácil implementación. | Comunicación en tiempo real. | Transmisión continua sobre HTTP. |
| **Contras**        | Puede fallar y requerir reintentos. | Requiere conexiones persistentes. | Difícil comunicación bidireccional. |

---
