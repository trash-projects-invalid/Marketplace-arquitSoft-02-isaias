# Diseño interno de módulos

## Alcance

Este diseño detalla las colaboraciones internas del flujo de compra para el monolito modular propuesto. Los contratos de dominio y los casos de uso del prototipo Clean Architecture en `tecnologia/clean-architecture/src/app/` sirven como ejemplo ejecutable, no como implementación completa de la API objetivo.

## Módulos y contratos

| Módulo | Elementos internos | Contrato que expone |
|---|---|---|
| Catálogo | Producto, filtro de catálogo, consulta de productos | `RepositorioProductos` |
| Carrito | Carrito, línea de carrito, reglas de stock y total | Comandos de agregar/quitar y consulta de total |
| Pedidos | Pedido, estado de pedido, caso de uso de compra | `RepositorioPedidos` |
| Pagos | Resultado de cobro y adaptador de proveedor | `ProcesadorPagos` |
| Notificaciones | Mensaje de confirmación y adaptador de canal | `NotificadorCliente` |

## Secuencia interna: confirmar compra

```mermaid
sequenceDiagram
  actor Cliente
  participant UI as Presentación
  participant CU as RegistrarCompraCasoUso
  participant Cart as Carrito / Producto
  participant Pay as ProcesadorPagos
  participant RepoP as RepositorioPedidos
  participant RepoCat as RepositorioProductos
  participant Notify as NotificadorCliente

  Cliente->>UI: Confirmar compra
  UI->>CU: ejecutar(cliente, carrito, medioPago)
  CU->>Cart: validar carrito y stock
  Cart-->>CU: total calculado
  CU->>Pay: cobrar(total, medioPago)
  Pay-->>CU: aprobado / rechazado
  alt pago aprobado
    CU->>Cart: descontar stock
    CU->>RepoCat: guardar productos actualizados
    CU->>CU: crear Pedido
    CU->>RepoP: guardar pedido
    CU->>Notify: confirmar pedido
    CU-->>UI: pedido confirmado
  else pago rechazado
    CU-->>UI: error de pago
  end
```

## Clases principales del prototipo

```mermaid
classDiagram
  class Producto {
    +id: string
    +precioBase: number
    +stockDisponible: number
    +hayStockPara(cantidad)
    +descontar(cantidad)
  }
  class Carrito {
    +agregar(producto, cantidad)
    +quitar(productoId)
    +calcularSubtotal()
    +calcularTotal()
  }
  class Pedido {
    +id: string
    +estadoActual
    +crear(clienteId, lineas, total, autorizacion)
    +cancelar()
  }
  class RegistrarCompraCasoUso {
    +ejecutar(comando)
  }
  class RepositorioProductos {
    <<interface>>
    +buscarPorId(id)
    +guardar(producto)
  }
  class RepositorioPedidos {
    <<interface>>
    +guardar(pedido)
  }
  class ProcesadorPagos {
    <<interface>>
    +cobrar(monto, medioPago)
  }
  class NotificadorCliente {
    <<interface>>
    +confirmarPedido(clienteId, pedidoId, total)
  }
  RegistrarCompraCasoUso --> Carrito
  RegistrarCompraCasoUso --> Pedido
  RegistrarCompraCasoUso --> RepositorioProductos
  RegistrarCompraCasoUso --> RepositorioPedidos
  RegistrarCompraCasoUso --> ProcesadorPagos
  RegistrarCompraCasoUso --> NotificadorCliente
  Carrito o-- Producto
  Pedido o-- Producto
```

## Reglas y límites

- Las entidades `Producto`, `Carrito` y `Pedido` validan invariantes del negocio sin depender de Angular o de una base de datos.
- `RegistrarCompraCasoUso` coordina el flujo y depende de interfaces; infraestructura provee adaptadores concretos.
- La composición de adaptadores queda en `app.config.ts` del prototipo.
- El prototipo descuenta stock después de recibir aprobación de pago. La consistencia entre pago externo y persistencia requiere idempotencia y compensación en el backend objetivo.
- Los datos de tarjeta no deben persistirse ni incluirse en logs; el prototipo usa un medio de pago simulado y no procesa datos productivos.
