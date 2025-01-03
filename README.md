# API de Información de Cliente y Productos Financieros

Este proyecto implementa una serie de microservicios para gestionar información de clientes y productos financieros. Los microservicios están desarrollados utilizando Java 11, Spring WebFlux, y otros componentes modernos. La API está diseñada para ser consumida desde herramientas como Postman y está protegida por autenticación OAuth.

## Funcionalidades

### Microservicios Implementados

1. **Microservicio de Información de Cliente**  
   Este microservicio maneja la información básica de los clientes, como nombres, apellidos, tipo de documento, y número de documento.

2. **Microservicio de Productos Financieros**  
   Este microservicio gestiona los productos financieros de los clientes, como cuentas de ahorro, tarjetas de crédito, entre otros. Los productos incluyen el tipo, nombre y saldo.

3. **Microservicio Backend For Frontend (BFF)**  
   Este microservicio integra los microservicios de información de cliente y productos financieros. Actúa como una capa de integración para las solicitudes del frontend.

### Endpoints de la API

La API expone un único endpoint para obtener la información del cliente y sus productos financieros:

- **GET /api/v1/cliente/{codigoUnico}**  
  Devuelve la información de un cliente, incluyendo sus productos financieros.

#### Parámetros:

- **codigoUnico**: (Requerido) Un valor encriptado que representa al cliente.

#### Respuesta:

```json
{
  "nombres": "Juan",
  "apellidos": "Pérez",
  "tipoDocumento": "DNI",
  "numeroDocumento": "12345678",
  "productosFinancieros": [
    {
      "tipo": "Cuenta de Ahorro",
      "nombre": "Cuenta Principal",
      "saldo": 1500.50
    },
    {
      "tipo": "Tarjeta de Crédito",
      "nombre": "Visa Clásica",
      "saldo": 1200.00
    }
  ]
}
