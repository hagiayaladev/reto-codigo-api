graph TD
    subgraph BFF["Backend For Frontend Service"]
        BFFAPI[Backend For Frontend API]
    end

    subgraph ClienteMicroservice["Cliente Microservice"]
        ClienteAPI[Spring WebFlux API Cliente]
        ClienteDB[(Base de Datos Cliente)]
    end

    subgraph ProductosMicroservice["Productos Microservice"]
        ProductosAPI[Spring WebFlux API Productos]
        ProductosDB[(Base de Datos Productos)]
    end

    subgraph AuthServer["Authorization Server"]
        Auth[Servidor de Autorización OAuth2]
    end

    User[Usuario/Cliente] -->|Solicitud con Token| BFFAPI
    BFFAPI -->|Validar Token| Auth
    BFFAPI -->|Obtener datos del Cliente| ClienteAPI
    ClienteAPI -->|Consulta| ClienteDB
    BFFAPI -->|Obtener Productos| ProductosAPI
    ProductosAPI -->|Consulta| ProductosDB

    %% Estilos para los nodos
    style User fill:#f9f,stroke:#000,stroke-width:4px,color:#000
    style BFF fill:#bbf,stroke:#000,stroke-width:2px,color:#000
    style ClienteMicroservice fill:#bfb,stroke:#000,stroke-width:2px,color:#000
    style ProductosMicroservice fill:#ffb,stroke:#000,stroke-width:2px,color:#000
    style AuthServer fill:#bbb,stroke:#000,stroke-width:2px,color:#000

    %% Definición de clases de servicios
    classDef service fill:#ddd,stroke:#000,stroke-width:2px,color:#000
    class BFFAPI,ClienteAPI,ProductosAPI,Auth service
