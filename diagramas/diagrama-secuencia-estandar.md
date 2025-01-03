%% Diagrama de secuencia sin validación de errores
sequenceDiagram
    title API de Información del Cliente y Productos Financieros

    participant User as Usuario/Cliente
    participant BFF as Backend For Frontend (BFF)
    participant Auth as Servidor de Autorización OAuth2
    participant ClienteAPI as Microservicio Cliente
    participant ProductosAPI as Microservicio Productos
    participant ClienteDB as Base de Datos Cliente
    participant ProductosDB as Base de Datos Productos

    %% Solicitudes y respuestas
    User ->> BFF: Solicitud con "codigoUnico" encriptado
    BFF ->> Auth: Validar Token de acceso
    Auth -->> BFF: Token Válido
    BFF ->> ClienteAPI: Obtener datos del cliente (código único desencriptado)
    ClienteAPI ->> ClienteDB: Consultar información del cliente por "codigoUnico"
    ClienteDB -->> ClienteAPI: Datos del cliente (nombres, apellidos, tipoDocumento, numeroDocumento)
    BFF ->> ProductosAPI: Obtener productos financieros del cliente (ID Cliente)
    ProductosAPI ->> ProductosDB: Consultar productos financieros (tipo, nombre, saldo)
    ProductosDB -->> ProductosAPI: Datos de productos financieros
    BFF -->> User: Respuesta con datos del cliente y productos financieros
