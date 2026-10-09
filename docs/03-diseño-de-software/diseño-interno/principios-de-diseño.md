# Principios de diseño SOLID

| Principio | Aplicación al Marketplace | Ejemplo o criterio |
|---|---|---|
| **S — Responsabilidad única** | Cada módulo y clase tiene una razón principal para cambiar | `Carrito` mantiene reglas de carrito; `RegistrarCompraCasoUso` coordina el proceso; un adaptador se ocupa del protocolo externo |
| **O — Abierto/cerrado** | Extender proveedores sin reescribir reglas del negocio | Implementar `ProcesadorPagos` para otro proveedor sin cambiar el caso de uso |
| **L — Sustitución de Liskov** | Cada implementación respeta el comportamiento esperado por su contrato | Todos los `ProcesadorPagos` retornan un resultado coherente para aprobación, rechazo y error |
| **I — Segregación de interfaces** | Los consumidores dependen de contratos pequeños que reflejan sus necesidades | Mantener separados repositorio de productos, repositorio de pedidos, pagos y notificaciones |
| **D — Inversión de dependencias** | Las políticas de negocio dependen de abstracciones, no de detalles | Casos de uso importan contratos; infraestructura los implementa; composición elige adaptadores |

## Dirección de dependencias

```mermaid
flowchart LR
  Presentacion[Presentación] --> Aplicacion[Aplicación / casos de uso]
  Infraestructura[Infraestructura / adaptadores] -. implementa contratos .-> Dominio[Dominio / entidades y contratos]
  Aplicacion --> Dominio
```

En el diagrama, la infraestructura implementa contratos definidos hacia el núcleo. Los componentes externos no deben ser importados desde Dominio. La raíz de composición conoce tanto los contratos como las implementaciones y conecta ambos lados.

## Revisión de cambios

Para cada cambio se revisa si mantiene una responsabilidad clara, si las implementaciones siguen cumpliendo sus contratos y si las dependencias apuntan hacia el núcleo. Las pruebas del dominio deben poder ejecutarse sin iniciar Angular ni servicios externos.
