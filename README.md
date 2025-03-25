# Paradigmas API

## Definición de API  
**Interfaz de Programación de Aplicaciones (API)**:  
Una API es una interfaz que establece cómo se deben gestionar las solicitudes y respuestas mediante:  
- **Métodos**  
- **Endpoints**  
- **Tipos de datos**  
- **Protocolos**  

## ¿Qué es un Paradigma?  
Un **paradigma** es un modelo o enfoque que define cómo estructurar, diseñar o resolver un problema en un contexto específico.  

## ¿Qué es un Paradigma de API?  
Un **paradigma de API** es un conjunto de principios y enfoques para diseñar correctamente una API.  

- La API **expone** (pone a disposición) ciertos datos o funciones del backend para que otras aplicaciones puedan utilizarlos.  
- Permite que las aplicaciones interactúen con el backend **sin conocer su implementación interna**.  

---

# **Paradigma de Solicitud - Respuesta**  
📌 **Ejemplos**: REST, RPC, SOAP, GraphQL.  

- Usa **protocolos web** como HTTP para manejar la comunicación cliente-servidor.  
- Se definen **endpoints** (URLs específicas) donde los clientes envían solicitudes para acceder o modificar recursos.  
- Los clientes envían **solicitudes HTTP** a los endpoints para obtener datos o realizar acciones en el servidor.  
- El servidor **procesa la solicitud** y devuelve una respuesta en **JSON** o **XML**.  

---

# **REST (Representational State Transfer - Transferencia de estado representacional)**  
✔ **La API más popular en el mercado**  
✔ Exponen datos como **recursos** y usan HTTP para realizar **operaciones CRUD**  
✔ Usa **JSON**  
✔ Permite que cualquier cliente (*web, móvil, etc.*) consuma la API sin importar la tecnología del backend  
✔ **Altamente escalable**  

📌 **REST trabaja con entidades y recursos** (*usuarios, productos, pedidos*).  

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
✔ **No depende de HTTP**, puede usar:  
  - **Apache Thrift** (soporte para múltiples lenguajes)  
  - **gRPC (Google Remote Procedure Call)** (ideal para microservicios)  
  - **Message Queue (MQ) + RPC** (para sistemas de colas)  

📌 **RPC trata con acciones y procedimientos** (*crearUsuario, eliminarUsuario*).  

### **Reglas básicas en RPC**  
1. Los **endpoints contienen el nombre de la operación** que se va a ejecutar.  
2. Las llamadas a la API se realizan con el **verbo HTTP más apropiado**:  
   - **GET** → Para solicitudes de solo lectura.  
   - **POST** → Para las demás operaciones.  

---

# **GraphQL**  
✔ **Desarrollado por Facebook en 2012**  
✔ **Trabaja con una sola petición** (a diferencia de REST, que puede requerir múltiples llamadas)  
✔ El **cliente tiene control sobre la estructura y el contenido de la respuesta**  
✔ **Autodocumentado** desde el desarrollo  

📌 **En GraphQL, el cliente puede especificar exactamente qué información necesita en su consulta.**  
```graphql
query ($id: String!) {  
  user(login: $id) {  
    name  
    company  
    createdAt  
  }  
}
