%% Diagrama de secuencia con validación de errores
sequenceDiagram
    title API de Información del Cliente y Productos Financieros con Validación

    participant User as Usuario/Cliente
    participant BFF as Backend For Frontend (BFF)
    participant Auth as Servidor de Autorización OAuth2
    participant ClienteAPI as Microservicio Cliente
    participant ProductosAPI as Microservicio Productos
    participant ClienteDB as Base de Datos Cliente
    participant ProductosDB as Base de Datos Productos

    %% Solicitudes y respuestas con validación de errores
    User ->> BFF: Solicitud con "codigoUnico" encriptado
    BFF ->> Auth: Validar Token de acceso
    alt Token Inválido
        Auth -->> BFF: Error: Token inválido
        BFF -->> User: Respuesta con error de autenticación
    else Token Válido
        Auth -->> BFF: Token Válido
        BFF ->> ClienteAPI: Obtener datos del cliente (código único desencriptado)
        alt Cliente no encontrado
            ClienteAPI -->> BFF: Error: Cliente no encontrado
            BFF -->> User: Respuesta con error: Cliente no encontrado
        else Cliente encontrado
            ClienteAPI ->> ClienteDB: Consultar información del cliente por "codigoUnico"
            ClienteDB -->> ClienteAPI: Datos del cliente (nombres, apellidos, tipoDocumento, numeroDocumento)
            BFF ->> ProductosAPI: Obtener productos financieros del cliente (ID Cliente)
            alt Productos no encontrados
                ProductosAPI -->> BFF: Error: Sin productos financieros
                BFF -->> User: Respuesta con advertencia: Sin productos financieros
            else Productos encontrados
                ProductosAPI ->> ProductosDB: Consultar productos financieros (tipo, nombre, saldo)
                ProductosDB -->> ProductosAPI: Datos de productos financieros
                BFF -->> User: Respuesta con datos del cliente y productos financieros
            end
        end
    end

