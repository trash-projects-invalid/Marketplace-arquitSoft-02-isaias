# Decisiones arquitectónicas (ADR)

Una vez identificados los drivers arquitectónicos, corresponde definir las **decisiones arquitectónicas (ADR — Architecture Decision Record)** que responden a dichos drivers, junto con su justificación.

Un ADR documenta una decisión importante de diseño, el **condición** que la motiva, las **alternativas consideradas** y el **resultado** esperado.

## Listado de decisiones arquitectónicas

| ID      | Decisión arquitectónica                                  | Driver relacionado                            | Resultado                                                                                                                                      |
| ------- | -------------------------------------------------------- | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| ADR-001 | Adoptar un estilo monolito modular                       | DA01 – Escalabilidad<br>DA06 – Mantenibilidad | Módulos independientes de Catálogo, Carrito, Pedidos, Pagos y Usuarios dentro de una misma aplicación desplegable.                             |
| ADR-002 | Aplicar Clean Architecture como enfoque interno          | DA06 – Mantenibilidad                         | Separación del sistema en Dominio, Aplicación, Infraestructura y Presentación, con dependencias dirigidas hacia el dominio.                    |
| ADR-003 | Estrategia de caché para datos de consulta frecuente     | DA02 – Rendimiento                            | Capa de caché (Redis) para productos y resultados de búsqueda, reduciendo la carga sobre la fuente de datos.                                   |
| ADR-004 | Integración de pagos mediante interfaces y adaptadores   | DA04 – Pago externo                           | Contrato `PasarelaDePagoPort` y adaptador concreto para la pasarela externa, desacoplando los casos de uso del proveedor de pagos.             |
| ADR-005 | Autenticación y autorización centralizadas               | DA03 – Seguridad                              | Módulo de seguridad con autenticación de clientes/sellers y autorización por roles (RBAC) sobre los endpoints de la API REST.                  |
| ADR-006 | Comunicación frontend-backend mediante API REST          | DA05 – API REST                               | API REST como único punto de entrada al backend, consumida desde la aplicación web.                                                            |
| ADR-007 | Alta disponibilidad mediante redundancia y despliegue    | DA07 – Disponibilidad                         | Despliegue con redundancia de instancias y balanceo, junto con planes de respaldo para la base de datos.                                       |
| ADR-008 | Integración con envío y facturación mediante adaptadores | DA08 – Integración externa                    | Contratos `ServicioEnvioPort` y `ServicioFacturacionPort` con sus adaptadores, aislando al dominio de los proveedores externos.                |
| ADR-009 | Sincronización con el ERP corporativo                    | DA09 – Integración con ERP                    | Servicio de sincronización que consulta el ERP de forma periódica para mantener actualizados productos y stock en el catálogo del marketplace. |

## Detalle de las decisiones

### ADR-001 — Monolito modular

- **Decisión:** desplegar el marketplace como un único artefacto, pero organizado internamente en módulos de negocio bien delimitados (Catálogo, Carrito, Pedidos, Pagos, Usuarios).
- **Justificación:** responde a la necesidad de escalar durante campañas y, al mismo tiempo, poder modificar un módulo sin afectar al resto.
- **Resultado:** módulos débilmente acoplados dentro de una misma aplicación desplegable.

### ADR-002 — Clean Architecture como enfoque interno

- **Decisión:** estructurar el código aplicando Clean Architecture, separando las reglas del negocio de los detalles tecnológicos.
- **Justificación:** el driver de mantenibilidad exige poder cambiar la interfaz, la base de datos o las integraciones externas sin modificar las reglas del dominio.
- **Resultado:** capas de Dominio, Aplicación, Infraestructura y Presentación, con dependencias dirigidas siempre hacia el dominio.

### ADR-003 — Estrategia de caché

- **Decisión:** introducir una capa de caché (por ejemplo, Redis) para datos de consulta frecuente como productos, categorías y resultados de búsqueda.
- **Justificación:** ante una alta concurrencia en campañas, se requiere reducir el número de consultas repetitivas hacia la fuente de datos.
- **Resultado:** mejora de los tiempos de respuesta y disminución de la carga sobre la base de datos.

### ADR-004 — Integración de pagos mediante puertos y adaptadores

- **Decisión:** definir un contrato `PasarelaDePagoPort` en la capa de aplicación y un adaptador concreto en infraestructura que se comunique con la pasarela externa.
- **Justificación:** desacoplar los casos de uso de pago del proveedor real, facilitando pruebas y posibles cambios de proveedor.
- **Resultado:** el dominio y los casos de uso desconocen los detalles de la pasarela de pago.

### ADR-005 — Autenticación y autorización

- **Decisión:** implementar un módulo de seguridad con autenticación para clientes y sellers, y autorización basada en roles para los endpoints de la API REST.
- **Justificación:** se manejan datos sensibles (cuentas, pedidos, pagos) que deben protegerse frente a accesos no autorizados.
- **Resultado:** endpoints protegidos según el rol del usuario (cliente, seller, administrador).

### ADR-006 — API REST como contrato frontend-backend

- **Decisión:** toda la comunicación entre la aplicación web y el backend se realiza exclusivamente mediante una API REST.
- **Justificación:** es una restricción explícita del proyecto y permite mantener frontend y backend desacoplados.
- **Resultado:** la interfaz web consume únicamente servicios REST del backend.

### ADR-007 — Alta disponibilidad

- **Decisión:** desplegar la aplicación con redundancia de instancias detrás de un balanceador y aplicar estrategias de respaldo a la base de datos.
- **Justificación:** el marketplace debe permanecer disponible durante las campañas comerciales.
- **Resultado:** tolerancia a fallos de instancia y recuperación ante incidentes de datos.

### ADR-008 — Integración con envío y facturación

- **Decisión:** definir los puertos `ServicioEnvioPort` y `ServicioFacturacionPort` en aplicación, con sus adaptadores concretos en infraestructura.
- **Justificación:** mantener aislado el dominio de los proveedores reales y simplificar la sustitución o pruebas de estos servicios.
- **Resultado:** el flujo del pedido delega en adaptadores la entrega y la emisión del comprobante.

### ADR-009 — Sincronización con el ERP

- **Decisión:** incorporar un servicio de sincronización que consulte periódicamente el ERP para mantener actualizados los datos de productos y stock en el marketplace.
- **Justificación:** el catálogo debe reflejar el inventario real del ERP corporativo.
- **Resultado:** la información de productos y stock expuesta al cliente es coherente con el ERP.
