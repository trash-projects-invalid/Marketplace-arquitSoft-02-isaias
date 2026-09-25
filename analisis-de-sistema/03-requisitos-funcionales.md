# Requisitos funcionales

Los requisitos funcionales describen las funciones que el sistema debe realizar. Se obtienen a partir de las historias de usuario identificadas.

> **Diferencia importante**
> - **Historia de usuario:** expresa la necesidad desde el punto de vista del usuario.
> - **Requisito funcional:** expresa lo que el sistema debe hacer para satisfacer esa necesidad.

## Listado de requisitos funcionales

| ID | Requisito funcional |
|----|---------------------|
| RF01 | El sistema debe permitir buscar productos mediante criterios de búsqueda. |
| RF02 | El sistema debe permitir consultar la información y disponibilidad de los productos. |
| RF03 | El sistema debe permitir registrar y actualizar productos en la plataforma. |
| RF04 | El sistema debe permitir agregar, modificar y eliminar productos del carrito de compra. |
| RF05 | El sistema debe permitir generar un pedido a partir de los productos del carrito. |
| RF06 | El sistema debe permitir consultar los pedidos realizados y su estado. |
| RF07 | El sistema debe permitir registrar, actualizar y desactivar sellers de la plataforma. |
| RF08 | El sistema debe permitir consultar el detalle de un pedido realizado. |
| RF09 | El sistema debe permitir el registro e inicio de sesión de usuarios (clientes y sellers). |
| RF10 | El sistema debe permitir procesar el pago de un pedido mediante la pasarela de pago. |
| RF11 | El sistema debe permitir al seller consultar los pedidos que incluyen sus productos. |
| RF12 | El sistema debe permitir al administrador consultar y gestionar los pedidos de la plataforma. |
| RF13 | El sistema debe permitir emitir y consultar comprobantes de pago de los pedidos. |
| RF14 | El sistema debe permitir gestionar la información de envío de un pedido. |

## Relación entre historias de usuario y requisitos funcionales

| Historia de usuario | Requisitos funcionales relacionados |
|---------------------|--------------------------------------|
| HU01 Buscar y consultar productos | RF01, RF02 |
| HU02 Gestionar productos | RF03 |
| HU03 Gestionar carrito | RF04 |
| HU04 Realizar pedido | RF05, RF08, RF10 |
| HU05 Gestionar sellers | RF07 |
| HU06 Consultar pedidos | RF06, RF08 |
| HU07 Registro e inicio de sesión | RF09 |
| HU08 Seller consulta pedidos con sus productos | RF11 |
| HU09 Administrador consulta y gestiona pedidos | RF12 |
| HU10 Consultar comprobantes de pago | RF13 |
