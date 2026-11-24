
# Insurance Core

MVP de un sistema de gestión aseguradora (Core Insurance), orientado a administrar los principales procesos relacionados con clientes, productos, cotizaciones y pólizas.

## 1. Objetivo

Desarrollar una aplicación web que permita representar el funcionamiento básico de una compañía de seguros, aplicando conceptos del negocio asegurador y buenas prácticas de análisis funcional y desarrollo de software.

## 2. Alcance funcional

La primera versión contempla cuatro módulos:

### Clientes
- Alta de clientes.
- Consulta de información.
- Modificación de datos.
- Identificación de personas físicas y jurídicas.

### Productos de seguros
- Administración de productos.
- Configuración básica de coberturas.
- Definición de características comerciales.

### Cotizaciones
- Registro de solicitudes de cotización.
- Selección de productos.
- Cálculo de prima.
- Consulta del resultado de cotización.

### Pólizas
- Emisión de pólizas.
- Consulta de pólizas.
- Modificaciones básicas.
- Control de vigencia.
- Cancelación de pólizas.

## 3. Fuera del alcance inicial

Los siguientes procesos no forman parte de la primera versión:

- Gestión integral de siniestros.
- Cobranzas y medios de pago.
- Liquidación de comisiones.
- Contabilidad.
- Reaseguros.
- Integraciones externas con aseguradoras.

## 4. Tecnologías

### Backend
- Python
- Django
- Django REST Framework

### Frontend
- Next.js
- React
- TypeScript

### Base de datos
- PostgreSQL

### Herramientas
- Git
- GitHub
- Docker
- GitHub Actions

## 5. Arquitectura prevista

La solución tendrá una arquitectura separada en tres componentes:

- Frontend: aplicación web desarrollada con Next.js.
- Backend: API REST desarrollada con Django REST Framework.
- Base de datos: PostgreSQL.

La comunicación entre frontend y backend se realizará mediante APIs REST.

## 6. Metodología de trabajo

El desarrollo se realizará mediante entregas pequeñas e incrementales:

1. Relevamiento funcional.
2. Documentación de requerimientos.
3. Diseño de base de datos.
4. Desarrollo del backend.
5. Desarrollo del frontend.
6. Pruebas funcionales y técnicas.
7. Documentación final.

## 7. Estado del proyecto

**Estado:** Planificación inicial.

**Versión objetivo:** MVP 1.0.

## 8. Finalidad

Proyecto educativo y demostrativo destinado a construir un portfolio profesional orientado a la industria Insurtech.

