# Drivers arquitectónicos

Los drivers arquitectónicos son los requisitos, atributos de calidad y restricciones que influyen significativamente en las decisiones de arquitectura del sistema.

## Listado de drivers arquitectónicos

| ID   | Driver arquitectónico                                                                       | Origen                     | ¿Por qué influye en la arquitectura?                                                             |
| ---- | ------------------------------------------------------------------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------ |
| DA01 | El sistema debe soportar un incremento importante de usuarios durante campañas comerciales. | AC03 – Escalabilidad       | Puede influir en la estrategia de escalamiento y despliegue.                                     |
| DA02 | El sistema debe mantener tiempos de respuesta adecuados durante una alta concurrencia.      | AC01 – Rendimiento         | Puede influir en la comunicación entre componentes, procesamiento y almacenamiento.              |
| DA03 | El sistema debe proteger los datos de usuarios y operaciones de compra.                     | AC04 – Seguridad           | Puede influir en autenticación, autorización y protección de datos.                              |
| DA04 | El sistema debe integrarse con una pasarela de pago externa mediante una API.               | RC04 – Pasarela de pago    | Condiciona la forma de comunicación e integración con servicios externos.                        |
| DA05 | El sistema debe utilizar una API REST para la comunicación entre frontend y backend.        | RC03 – API REST            | Limita las alternativas de comunicación entre las partes del sistema.                            |
| DA06 | El sistema debe permanecer disponible durante la campaña comercial.                         | AC02 – Disponibilidad      | Puede influir en la redundancia de componentes, tolerancia a fallos y estrategias de despliegue. |
| DA07 | El sistema debe integrarse con un servicio externo de envío y otro de facturación.          | RC05 / RC06                | Condiciona el diseño de los puntos de integración y el manejo de estados del pedido.             |
| DA08 | El sistema debe consumir información de productos y stock desde un ERP corporativo.         | RC07 – Integración con ERP | Define un punto de integración crítico con un sistema externo y la frecuencia de sincronización. |
