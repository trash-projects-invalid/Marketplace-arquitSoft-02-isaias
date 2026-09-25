# Arquitectura inicial del sistema

## 1. Arquitectura en tres capas

A partir del análisis del sistema (actores, requisitos, atributos de calidad, restricciones y drivers arquitectónicos), se propone organizar la solución en una **arquitectura en tres capas**, la cual separa responsabilidades y facilita la mantenibilidad.

```
┌────────────────────────────────────┐
│           PRESENTACIÓN             │
│       Web / API / Interfaz         │
└─────────────────┬──────────────────┘
                  ↓
┌────────────────────────────────────┐
│         LÓGICA DE NEGOCIO          │
│                                    │
│ Catálogo                           │
│ Carrito                            │
│ Pedidos                            │
│ Sellers                            │
│ Usuarios                           │
└─────────────────┬──────────────────┘
                  ↓
┌────────────────────────────────────┐
│               DATOS                │
│           Base de datos            │
└────────────────────────────────────┘
```

| Capa | Pregunta que responde |
|------|------------------------|
| Presentación | ¿Cómo interactúa el usuario? |
| Lógica de negocio | ¿Qué hace el sistema? |
| Datos | ¿Dónde se almacena la información? |

### Responsabilidades por capa

- **Presentación:** expone la interfaz web y la API REST que será consumida desde el frontend. Encargada de la interacción con clientes, sellers y administradores.
- **Lógica de negocio:** contiene los módulos principales del marketplace: Usuarios, Sellers, Catálogo, Carrito y Pedidos. Aplica las reglas del negocio y orquesta las integraciones externas.
- **Datos:** persiste la información de usuarios, sellers, productos, carrito, pedidos y demás entidades del sistema en una base de datos.

## 2. Diagrama de arquitectura

```mermaid
flowchart TD

    %% =========================
    %% ACTORES
    %% =========================
    subgraph ACTORES["ACTORES"]
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    %% =========================
    %% PRESENTACIÓN
    %% =========================
    subgraph PRESENTACION["PRESENTACIÓN"]
        Web["Aplicación Web → API REST"]
    end

    %% =========================
    %% LÓGICA DE NEGOCIO
    %% =========================
    subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
    end

    %% =========================
    %% DATOS
    %% =========================
    subgraph DATOS["DATOS"]
        BD["Base de datos"]
    end

    %% =========================
    %% SISTEMAS EXTERNOS
    %% =========================
    subgraph EXTERNOS["SISTEMAS EXTERNOS"]
        Pago["Pasarela de pago"]
        ERP["ERP"]
        Envio["Servicio de envío"]
        Facturacion["Servicio de Facturación"]
    end

    %% =========================
    %% FLUJO PRINCIPAL
    %% =========================
    ACTORES --> PRESENTACION
    PRESENTACION --> NEGOCIO
    NEGOCIO --> DATOS

    %% Integraciones
    Pedidos -->|"procesa pago"| Pago
    Pedidos -->|"gestiona entrega"| Envio
    Pedidos -->|"emite comprobante"| Facturacion
    Catalogo -->|"consulta stock"| ERP

    %% =========================
    %% DISTRIBUCIÓN HORIZONTAL
    %% =========================
    Cliente ~~~ Seller
    Seller ~~~ Admin

    Usuarios ~~~ Sellers
    Sellers ~~~ Catalogo
    Catalogo ~~~ Carrito
    Carrito ~~~ Pedidos

    Pago ~~~ ERP
    ERP ~~~ Envio
    Envio ~~~ Facturacion

    %% =========================
    %% ESTILOS
    %% =========================
    style ACTORES fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style PRESENTACION fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style NEGOCIO fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style DATOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style EXTERNOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff

    style Cliente fill:#222,stroke:#fff,color:#fff
    style Seller fill:#222,stroke:#fff,color:#fff
    style Admin fill:#222,stroke:#fff,color:#fff

    style Web fill:#222,stroke:#fff,color:#fff

    style Usuarios fill:#222,stroke:#fff,color:#fff
    style Sellers fill:#222,stroke:#fff,color:#fff
    style Catalogo fill:#222,stroke:#fff,color:#fff
    style Carrito fill:#222,stroke:#fff,color:#fff
    style Pedidos fill:#222,stroke:#fff,color:#fff

    style BD fill:#222,stroke:#fff,color:#fff

    style Pago fill:#222,stroke:#fff,color:#fff
    style ERP fill:#222,stroke:#fff,color:#fff
    style Envio fill:#222,stroke:#fff,color:#fff
    style Facturacion fill:#222,stroke:#fff,color:#fff
```

## 3. Descripción

La arquitectura inicial se organiza en tres capas principales:

- **Presentación:** permite la interacción de los usuarios con el sistema mediante la aplicación web y la API REST.
- **Lógica de negocio:** contiene los principales módulos responsables de las funcionalidades del sistema: usuarios, sellers, catálogo, carrito y pedidos.
- **Datos:** permite almacenar y consultar la información mediante una base de datos.

Además, el módulo de **Pedidos** se integra con sistemas externos como la **pasarela de pago**, el **servicio de envío** y el **servicio de facturación**, mientras que el módulo de **Catálogo** consulta el stock desde el **ERP** corporativo.
