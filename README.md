# Marketplace de productos para mascotas

Marketplace académico de productos para mascotas, con GoPet como referencia funcional. Proyecto del curso Arquitectura de Software, desarrollado por Isaias Ramos Lopez.

## Organización del repositorio

La documentación del análisis, arquitectura y diseño vive en `docs/`. El ejemplo ejecutable de Clean Architecture vive en `tecnologia/`.

```text
.
├── docs/
│   ├── 01-analisis-de-sistema/
│   ├── 02-arquitectura/
│   ├── 03-diseño-de-software/diseño-interno/
│   ├── 04-modelo-c4/
│   └── imagenes/
├── tecnologia/clean-architecture/  # Angular + TypeScript
├── GUIA-003-ASF.pdf
└── GUIA-004-ASF.pdf
```

## Ejecutar el ejemplo Clean Architecture

El ejemplo Angular se gestiona con [Bun](https://bun.sh) y usa adaptadores en memoria para funcionar sin base de datos ni credenciales.

```bash
cd tecnologia/clean-architecture
bun install
bun dev             # http://localhost:4200
bun run pruebas     # pruebas del dominio, sin Angular
bun run build       # compilación de producción
```

## Documentación

### Análisis del sistema

- [Actores](docs/01-analisis-de-sistema/01-actores.md)
- [Historias de usuario](docs/01-analisis-de-sistema/02-historias-del-usuario.md)
- [Requisitos funcionales](docs/01-analisis-de-sistema/03-requisitos-funcionales.md)
- [Atributos de calidad](docs/01-analisis-de-sistema/04-atributos-de-calidad.md)
- [Restricciones](docs/01-analisis-de-sistema/05-restricciones.md)
- [Drivers arquitectónicos](docs/01-analisis-de-sistema/06-driver-arquitectonicos.md)
- [Decisiones arquitectónicas (ADR)](docs/01-analisis-de-sistema/07-decision-arquitectonica.md)
- [Escenarios medibles de calidad](docs/01-analisis-de-sistema/08-escenarios-atributos-calidad.md)

### Arquitectura y diseño

- [Arquitectura inicial](docs/02-arquitectura/arquitectura-inicial.md)
- [Estilo arquitectónico](docs/02-arquitectura/estilo-arquitectonico.md)
- [Enfoque Clean Architecture](docs/02-arquitectura/enfoque-arquitectonico.md)
- [Componentes arquitectónicos](docs/02-arquitectura/componentes-arquitectonicos.md)
- [Diseño interno de módulos](docs/03-diseño-de-software/diseño-interno/diseño-interno-de-modulos.md)
- [Patrones de diseño](docs/03-diseño-de-software/diseño-interno/patrones-de-diseño.md)
- [Principios SOLID](docs/03-diseño-de-software/diseño-interno/principios-de-diseño.md)
- [Modelo C4](docs/04-modelo-c4/README.md)
- [Recursos gráficos y fuente Mermaid](docs/imagenes/)

## Alcance de la implementación

El código es un ejemplo de capas Dominio, Aplicación, Infraestructura y Presentación para catálogo, carrito y compra. Los diagramas C4 describen la arquitectura objetivo propuesta, que incluye API REST, almacenamiento e integraciones externas aún no implementadas. Los umbrales de calidad están marcados como objetivos pendientes de validación.
