# 🌍 Paradigmas API

## 📌 Definición de API (Application Programming Interfaces - Interfaz de Programación de Aplicaciones) 
Una API es una interfaz que establece cómo se deben gestionar las solicitudes y respuestas mediante:  
✔ **Métodos**  
✔ **Endpoints**  
✔ **Tipos de datos**  
✔ **Protocolos**  

## ❓ ¿Qué es un Paradigma?  
Un **paradigma** es un modelo o enfoque que define cómo estructurar, diseñar o resolver un problema en un contexto específico.  

## 🔍 ¿Qué es un Paradigma de API?  
Un **paradigma de API** es un conjunto de principios y enfoques para diseñar correctamente una API.  

✔ La API **expone** (pone a disposición) ciertos datos o funciones del backend para que otras aplicaciones puedan utilizarlos.  
✔ Permite que las aplicaciones interactúen con el backend **sin conocer su implementación interna**.  

---

# 🚀 **Paradigma de Solicitud - Respuesta**  
**Ejemplos**: REST, RPC, SOAP, GraphQL.  

✔ Usa **protocolos web** como HTTP para manejar la comunicación cliente-servidor.  
✔ Se definen **endpoints** (URLs específicas) donde los clientes envían solicitudes para acceder o modificar recursos.  
✔ Los clientes envían **solicitudes HTTP** a los endpoints para obtener datos o realizar acciones en el servidor.  
✔ El servidor **procesa la solicitud** y devuelve una respuesta en **JSON** o **XML**.  

---

# 🌐 **REST (Representational State Transfer - Transferencia de estado representacional)**  
✔ **La API más popular en el mercado**  
✔ Exponen datos como **recursos** y usan HTTP para realizar **operaciones CRUD**  
✔ Usa **JSON**  
✔ Permite que cualquier cliente (web, móvil, etc.) consuma la API sin importar la tecnología del backend  
✔ **Altamente escalable**  

**REST trabaja con entidades y recursos** (usuarios, productos, pedidos).  

### 📌 **Ejemplo de API REST**  
📤 **Obtener información de un usuario**  
```http
GET /usuarios/123 HTTP/1.1
Host: api.ejemplo.com
Accept: application/json
```

📥 **Respuesta del servidor**  
```json
{
  "id": 123,
  "nombre": "Juan Pérez",
  "email": "juan@example.com",
  "edad": 25
}
```

### 🔄 **Métodos HTTP en REST**  
| Método  | Descripción                     |
|---------|---------------------------------|
| **GET**    | Obtener un recurso           |
| **POST**   | Crear y guardar un nuevo recurso |
| **PUT**    | Modificar un recurso         |
| **DELETE** | Eliminar un recurso          |

### 📊 **Códigos de Estado HTTP**  
| Código  | Significado                   |
|---------|--------------------------------|
| **2XX** | ✅ Éxito                         |
| **3XX** | 🔄 Recurso movido                 |
| **4XX** | ⚠️ Error del lado del cliente     |
| **5XX** | ❌ Error del lado del servidor    |

---

# ⚙️ **RPC (Remote Procedure Call - Llamada de Procedimiento Remoto)**  
✔ **API más simple**  
✔ Un cliente ejecuta un **bloque de código en otro servidor**  
✔ Mientras que REST se enfoca en **recursos**, RPC se enfoca en **acciones**  
✔ **Eficiente** y permite **llamadas directas a funciones**  
✔ **NO depende de HTTP**, puede usar:  

| 🛠 Tecnología               | 📜 Descripción                                      |
|--------------------------|--------------------------------------------------|
| **Apache Thrift**        | Soporte para múltiples lenguajes de programación. |
| **gRPC** (Google Remote Procedure Call) | Ideal para microservicios debido a su alto rendimiento. |
| **Message Queue (MQ) + RPC** | Utilizado para sistemas de colas y comunicación asíncrona. |

📌 **RPC trata con acciones y procedimientos** (*crearUsuario, eliminarUsuario*).  

### 📌 **Reglas básicas en RPC**  
✔ Los **endpoints contienen el nombre de la operación** que se va a ejecutar.  
✔ Las llamadas a la API se realizan con el **verbo HTTP más apropiado**:

### 🔄 **Métodos HTTP en RPC**  
| Método  | Descripción                     |
|---------|---------------------------------|
| **GET**    | Para solicitudes de solo lectura |
| **POST**   | Para las demás operaciones |

### 📌 **Ejemplo de API RPC**  
📤 **Llamada a un procedimiento remoto para crear un usuario**  
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

📥 **Respuesta del servidor**  
```json
{
  "id": 123,
  "mensaje": "Usuario creado exitosamente"
}
```

---

# 🔷 **GraphQL**  
✔ **Desarrollado por Facebook en 2012**  
✔ **Trabaja con una sola petición** (a diferencia de REST, que puede requerir múltiples llamadas)  
✔ El **cliente tiene control sobre la estructura y el contenido de la respuesta**  
✔ **Autodocumentado** desde el desarrollo  

**En GraphQL, el cliente puede especificar exactamente qué información necesita en su consulta.**  

### 📌 **Ejemplo de API GraphQL**  
📤 **Consulta de usuario en GraphQL**  
```graphql
query ($id: String!) {  
  user(login: $id) {  
    name  
    company  
    createdAt  
  }  
}
```

📥 **Respuesta del servidor**  
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

# 📊 **Comparación de Paradigmas API: Solicitud - Respuesta**  
## 📌 **REST vs RPC vs GraphQL: Pros y Contras**

| Característica      | ✅ REST                                       | ⚙️ RPC                                        | 🔷 GraphQL                                   |
|--------------------|-------------------------------------------|-------------------------------------------|-------------------------------------------|
| **Pros**           | Estandarización y fácil mantenimiento. | Simple y de bajo consumo de ancho de banda. | Reduce múltiples viajes de ida y vuelta. |
| **Contras**        | Cargas útiles grandes. | Puede generar una explosión de funciones. | Requiere optimización adicional. |
| **¿Cuándo usarlo?** | Para APIs CRUD. | Para APIs con múltiples acciones. | Para APIs con flexibilidad en consultas. |
| **Uso de verbos HTTP** | GET, POST, PUT, PATCH, DELETE    | GET, POST                               | GET, POST    
---

# 📡 Paradigma Basado en Eventos

Un paradigma basado en eventos es un modelo de programación donde el flujo de ejecución se determina por eventos, como interacciones del usuario, mensajes o cambios de estado.  

## ⚠️ Problema con las APIs de Solicitud-Respuesta  
Con las APIs de solicitud-respuesta, para servicios con datos que cambian constantemente, la respuesta puede volverse obsoleta rápidamente.  

🔹 En una API de solicitud-respuesta (como REST o RPC), el cliente recibe los datos en el momento de la solicitud.  
🔹 Si los datos en el servidor cambian después de esa respuesta, el cliente **no** se entera automáticamente.  

---  

## 🔄 Polling  
Los desarrolladores usan **polling** para consultar la API periódicamente y detectar cambios en los datos.  

| 🛠️ Tipo de Polling    | 📋 Descripción                          |
|-------------------|----------------------------------|
| ⏳ **Baja frecuencia** | Puede perder eventos importantes. |
| 🚀 **Alta frecuencia** | Genera mucho consumo de recursos. |  

---  

## 🔔 WebHooks  
🔹 **WebHook** es simplemente una **URL** que acepta solicitudes HTTP **POST**, **GET**, **PUT** o **DELETE**.  
🔹 Permite recibir actualizaciones en **tiempo real** sin necesidad de hacer consultas repetitivas.  
🔹 Utilizado en **Slack, Stripe, GitHub, Zapier**, etc.  

### 📌 Polling vs WebHook  

| 🏷️ Característica   | 🔄 **Polling**                       | 🔔 **WebHook**                     |
|-----------------|--------------------------------|--------------------------------|
| 🏃 **Funcionamiento** | El cliente consulta periódicamente. | El servidor envía datos automáticamente. |
| ⚡ **Eficiencia**    | ❌ Ineficiente, muchas solicitudes. | ✅ Solo envía datos cuando es necesario. |
| ⏳ **Frecuencia**   | Definida por el cliente. | En tiempo real. |
| 💻 **Carga en servidor** | Alta, por solicitudes repetitivas. | Baja, solo se envían datos cuando hay cambios. |
| 🔧 **Implementación** | Fácil, requiere solicitudes HTTP. | Más compleja, necesita un endpoint receptor. |  
| 📍 **Ejemplos** | Consultar estados de pedidos. | Notificación de pagos en Stripe. |  

### ⚠️ Consideraciones de WebHooks  
✔ **Fallos:** Es necesario manejar reintentos en caso de fallos de entrega.  
✔ **Firewalls:** Si una aplicación está detrás de un firewall, puede ser difícil recibir WebHooks.  
✔ **Ruido:** Demasiados WebHooks en poco tiempo pueden generar tráfico innecesario.  

### 📌 Casos de Uso de WebHooks  
✅ Una tienda online notificando una venta a un sistema de facturación.  
✅ Un proveedor de pagos (ej. PayPal) notificando sobre un pago recibido.  
✅ Un repositorio en GitHub notificando sobre un nuevo commit.  

---  

## 🔄 WebSockets  
🔹 **WebSockets** establecen un canal de comunicación **bidireccional** mediante una única conexión **TCP**.  
🔹 Permiten una comunicación **full-dúplex**, donde el servidor y el cliente intercambian información simultáneamente.  
🔹 Son ideales para aplicaciones en **tiempo real** como chats y videojuegos en línea.  

### 🎯 Beneficios en APIs Empresariales  
📌 Algunos desarrolladores empresariales que usan **Slack** prefieren **WebSockets** en lugar de WebHooks, ya que pueden recibir eventos de forma segura sin exponer un endpoint HTTP al internet.  

### ✅ Pros y ❌ Contras de WebSockets  

| ✅ Pros                                       | ❌ Contras                           |
|----------------------------------------------|--------------------------------------|
| Comunicación **bidireccional** en tiempo real. | Los clientes deben gestionar las conexiones. |
| Reducción de sobrecarga por solicitudes HTTP. | Puede ser **difícil de escalar** en grandes sistemas. |  

---  

## 📡 HTTP Streaming  
🔹 **HTTP Streaming** permite enviar datos continuamente en una misma conexión sin cerrar la respuesta.  
🔹 Se usa en aplicaciones donde es necesario recibir datos **en tiempo real** sin hacer múltiples solicitudes.  

### 🔧 Métodos para transmitir datos en HTTP Streaming  
1. **📜 Transfer-Encoding: chunked**  
   - Envía datos en fragmentos separados por saltos de línea.  
   - Fácil de procesar y eficiente.  
2. **🌐 SSE (Server-Sent Events)**  
   - Permite que el servidor envíe eventos al cliente a través de una única conexión HTTP.  
   - Compatible con la API estándar **EventSource** en navegadores.  

📌 **Ejemplo:** Twitter usa **HTTP Streaming** para mostrar tweets en tiempo real sin recargar la página.  

---  

## 📊 Comparación: WebHooks vs WebSockets vs HTTP Streaming  

| 🏷️ Característica   | 🔔 **WebHooks**                        | 🔄 **WebSockets**                   | 🌊 **HTTP Streaming**                 |
|-----------------|--------------------------------|------------------------------|--------------------------------|
| 🏃 **¿Qué es?** | Notificación de eventos vía HTTP | Conexión **bidireccional** sobre TCP | Conexión de larga duración sobre HTTP |
| 📦 **Ejemplos** | **Slack, Stripe, GitHub** | **Slack, Trello, Blockchain** | **Twitter, Facebook Live** |
| ✅ **Pros** | Fácil de implementar. Usa HTTP. | Comunicación en tiempo real. Soporte en navegadores. | Soporte HTTP nativo. Se salta firewalls. |
| ❌ **Contras** | No funciona bien en navegadores o firewalls. | Requiere mantener conexiones abiertas. | Difícil manejar eventos bidireccionales. |
| 🎯 **¿Cuándo usarlo?** | Para notificaciones de eventos del servidor. | Para chat en vivo y streaming de datos en tiempo real. | Para actualizaciones unidireccionales en tiempo real. |  

--- 
