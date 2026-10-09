# Escenarios de atributos de calidad del Marketplace

Estos escenarios convierten los atributos identificados en respuestas que se pueden comprobar. Los umbrales numéricos son objetivos iniciales propuestos para el primer sprint; deben validarse con el equipo y medirse en un entorno de prueba acordado antes de considerarlos compromisos de producción.

## EQ-01. Rendimiento: consulta del catálogo

| Elemento | Descripción |
|---|---|
| Atributo | Rendimiento (AC01) |
| Fuente del estímulo | Clientes que navegan el catálogo durante una campaña |
| Estímulo | Búsqueda, filtrado o consulta del detalle de un producto |
| Artefacto | Módulo Catálogo y su acceso al repositorio de productos |
| Entorno | Operación normal, datos representativos y 200 usuarios concurrentes |
| Respuesta | El sistema devuelve los resultados disponibles y conserva la navegación |
| Medida de respuesta | El 95 % de las consultas responde en ≤ 2 s y menos del 1 % termina en error técnico |
| Verificación | Ejecutar una prueba de carga y registrar latencia percentil 95 y errores |
| Estado | Umbral propuesto; pendiente validar carga, datos e infraestructura |

## EQ-02. Disponibilidad: operaciones de compra

| Elemento | Descripción |
|---|---|
| Atributo | Disponibilidad (AC02) |
| Fuente del estímulo | Cliente que intenta comprar durante una campaña |
| Estímulo | Consulta o confirmación de una compra mientras un servicio externo no responde |
| Artefacto | API del Marketplace, módulo Pedidos y sus integraciones |
| Entorno | Sistema publicado con monitoreo y una instancia o integración degradada |
| Respuesta | Se mantienen disponibles las operaciones independientes; una operación dependiente falla de forma controlada y comunica su estado |
| Medida de respuesta | Disponibilidad mensual ≥ 99,5 % para operaciones críticas; 100 % de fallas observadas se registra y comunica sin confirmar una compra incompleta |
| Verificación | Calcular disponibilidad desde monitoreo y revisar pruebas de caída de dependencias |
| Estado | Meta propuesta; falta acordar operaciones críticas, mantenimiento y ventana de medición |

## EQ-03. Escalabilidad: aumento de usuarios

| Elemento | Descripción |
|---|---|
| Atributo | Escalabilidad (AC03) |
| Fuente del estímulo | Incremento de solicitudes de clientes |
| Estímulo | Aumenta progresivamente la concurrencia de navegación y compra |
| Artefacto | Aplicación web, API, Catálogo y almacenamiento |
| Entorno | Prueba controlada con datos, configuración y patrón de solicitudes documentados |
| Respuesta | El sistema absorbe la carga prevista sin exceder los límites de latencia y error |
| Medida de respuesta | Con 200 usuarios concurrentes, percentil 95 ≤ 3 s y errores técnicos < 1 % |
| Verificación | Aumentar la carga por etapas y registrar latencia, errores y uso de recursos |
| Estado | Umbral propuesto; pendiente confirmar crecimiento esperado e infraestructura |

## EQ-04. Seguridad: acceso a operaciones protegidas

| Elemento | Descripción |
|---|---|
| Atributo | Seguridad (AC04) |
| Fuente del estímulo | Usuario sin sesión, con credenciales inválidas o sin permisos |
| Estímulo | Intenta consultar o cambiar información protegida de otro usuario o seller |
| Artefacto | Autenticación, autorización y endpoints de Usuarios, Sellers, Pedidos y Administración |
| Entorno | Pruebas con perfiles cliente, seller y administrador, con sesión válida e inválida |
| Respuesta | La operación se rechaza, no modifica datos y no expone información sensible |
| Medida de respuesta | Se rechaza el 100 % de los intentos no autorizados del conjunto de pruebas y no se exponen datos sensibles en las respuestas revisadas |
| Verificación | Ejecutar casos positivos y negativos por rol, comprobar persistencia y revisar respuestas |
| Estado | Criterio propuesto; falta acordar permisos por rol y catálogo de operaciones protegidas |

## EQ-05. Mantenibilidad: cambio de proveedor de pagos

| Elemento | Descripción |
|---|---|
| Atributo | Mantenibilidad (AC05) |
| Fuente del estímulo | Equipo de desarrollo |
| Estímulo | Sustituye el proveedor de pagos o modifica una regla del carrito |
| Artefacto | Módulo Pagos, sus adaptadores y los casos de uso de compra |
| Entorno | Código organizado por módulos, con contratos y pruebas del flujo de compra |
| Respuesta | El cambio queda aislado en el adaptador o módulo responsable y el flujo conserva el contrato acordado |
| Medida de respuesta | Todas las pruebas del módulo y de regresión pasan; no se agregan dependencias que violen las reglas de arquitectura |
| Verificación | Revisar el diff, ejecutar pruebas del dominio y comprobar dependencias entre capas |
| Estado | Criterio propuesto; reglas de dependencia y conjunto de regresión por definir |

## EQ-06. Usabilidad: completar una compra

| Elemento | Descripción |
|---|---|
| Atributo | Usabilidad (AC06) |
| Fuente del estímulo | Cliente nuevo que compra desde la aplicación web |
| Estímulo | Busca un producto, lo agrega al carrito y confirma la compra |
| Artefacto | Interfaz de catálogo, carrito y confirmación de pedido |
| Entorno | Primera visita, sin asistencia, en un viewport de escritorio y uno móvil acordados |
| Respuesta | La interfaz guía el flujo, muestra precio y errores con claridad y confirma el resultado |
| Medida de respuesta | Al menos 9 de 10 participantes completan la tarea en ≤ 3 minutos sin ayuda y sin errores críticos |
| Verificación | Prueba moderada con 10 participantes y registro de finalización, tiempo y bloqueos |
| Estado | Objetivo propuesto; pendiente definir participantes y dispositivos de evaluación |

## EQ-07. Interoperabilidad: pasarela de pago

| Elemento | Descripción |
|---|---|
| Atributo | Interoperabilidad (AC07) |
| Fuente del estímulo | Pasarela de pago externa |
| Estímulo | Recibe una solicitud de cobro y devuelve aprobación, rechazo o timeout |
| Artefacto | Adaptador de pagos y caso de uso Registrar compra |
| Entorno | Ambiente de pruebas del proveedor, contrato versionado y credenciales no productivas |
| Respuesta | El adaptador traduce la respuesta externa al contrato interno; no se registra como pagado un cobro rechazado o incierto |
| Medida de respuesta | 100 % de los casos de contrato definidos se traducen correctamente; el timeout se informa dentro de 5 s y no genera pedido pagado |
| Verificación | Pruebas de contrato para aprobación, rechazo, error de red y timeout |
| Estado | Criterio propuesto; pendiente acordar contrato, proveedor y timeout con el equipo |

## Resumen

| Código | Atributo | Criterio principal |
|---|---|---|
| EQ-01 | Rendimiento | p95 de consulta ≤ 2 s con 200 usuarios; errores < 1 % |
| EQ-02 | Disponibilidad | ≥ 99,5 % mensual para operaciones críticas |
| EQ-03 | Escalabilidad | p95 ≤ 3 s con 200 usuarios; errores < 1 % |
| EQ-04 | Seguridad | Rechazo del 100 % de intentos no autorizados probados |
| EQ-05 | Mantenibilidad | Pruebas aprobadas y dependencias acordes a las reglas de arquitectura |
| EQ-06 | Usabilidad | 9/10 usuarios completan compra en ≤ 3 minutos sin ayuda |
| EQ-07 | Interoperabilidad | Casos de contrato completos y timeout controlado en ≤ 5 s |
