# Patrones de diseño

Los patrones documentados corresponden a soluciones visibles en el prototipo y a su aplicación prevista en el monolito modular.

| Patrón | Aplicación en el Marketplace | Evidencia en el prototipo | Beneficio |
|---|---|---|---|
| Repository | Oculta cómo se consultan y guardan productos y pedidos | Interfaces `RepositorioProductos` y `RepositorioPedidos`; adaptadores en memoria y HTTP | Cambiar almacenamiento sin modificar casos de uso |
| Adapter | Traduce contratos internos a APIs de pago y notificación | `ProcesadorPagosNiubiz`, `ProcesadorPagosSimulado`, `NotificadorWhatsApp` | Aislar protocolos y proveedores |
| Strategy | Permite elegir una implementación compatible de pago, persistencia o notificación | Implementaciones de los contratos seleccionadas en `app.config.ts` | Sustituir comportamientos mediante configuración |
| Dependency Injection | Entrega contratos a los casos de uso desde la raíz de composición | Tokens y proveedores de Angular en `app.config.ts` | Reducir acoplamiento y facilitar pruebas |
| Factory Method | Centraliza la creación válida de pedidos | `Pedido.crear(...)` valida cliente, líneas y total | Evitar instancias de Pedido inválidas |

## Colaboración de patrones en la compra

`RegistrarCompraCasoUso` solicita operaciones a contratos de repositorio, pago y notificación. La raíz de composición conecta esos contratos con adaptadores concretos; el adaptador traduce la llamada hacia el proveedor. Así, el caso de uso conserva el vocabulario del negocio y no importa SDKs externos.

## Criterios de uso

- Agregar un patrón cuando resuelva una variación o responsabilidad real del sistema.
- Mantener los contratos pequeños y expresados en términos del negocio.
- Evitar que las capas de dominio y aplicación importen Angular, HTTP o SDKs de proveedores.
- Revisar los límites de seguridad y manejo de fallos al conectar servicios reales.
