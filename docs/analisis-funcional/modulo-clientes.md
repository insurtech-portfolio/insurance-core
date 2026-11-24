
# Especificación Funcional - Módulo Clientes

**Proyecto:** Insurance Core  
**Documento:** EF-001  
**Versión:** 1.0  
**Estado:** Borrador  
**Módulo:** Clientes

---

## 1. Objetivo

Definir las funcionalidades necesarias para administrar los clientes de una compañía aseguradora.

El módulo permitirá registrar, consultar y actualizar información de personas físicas y jurídicas que mantienen una relación comercial con la aseguradora.

## 2. Alcance

La primera versión contempla:

- Registro de personas físicas.
- Registro de personas jurídicas.
- Consulta de clientes.
- Modificación de información.
- Identificación mediante tipo y número de documento.
- Administración del estado del cliente.

## 3. Actores

| Actor | Responsabilidad |
|---|---|
| Operador administrativo | Registrar y actualizar clientes |
| Ejecutivo comercial | Consultar clientes |
| Administrador | Supervisar la información |

## 4. Requerimientos funcionales

### RF-001 - Alta de clientes

El sistema deberá permitir registrar nuevos clientes.

### RF-002 - Tipos de personas

El sistema deberá permitir registrar personas físicas y jurídicas.

### RF-003 - Consulta de clientes

El sistema deberá permitir consultar clientes mediante identificadores y criterios de búsqueda.

### RF-004 - Modificación de clientes

El sistema deberá permitir actualizar los datos de un cliente existente.

### RF-005 - Identificación única

El sistema deberá impedir registros duplicados según las reglas de identificación definidas para cada tipo de persona.

### RF-006 - Estado del cliente

El sistema deberá permitir administrar el estado del cliente.

## 5. Datos principales

### Persona física

- Tipo de documento.
- Número de documento.
- Nombre.
- Apellido.
- Fecha de nacimiento.
- Correo electrónico.
- Teléfono.
- Domicilio.

### Persona jurídica

- Tipo de identificación fiscal.
- Número de identificación fiscal.
- Razón social.
- Nombre comercial (opcional).
- Correo electrónico.
- Teléfono.
- Domicilio.

## 6. Reglas de negocio

### RN-001 - Identificación

Cada cliente deberá contar con un identificador interno único.

### RN-002 - Documentación

El tipo y número de documento deberán validarse según el tipo de persona.

### RN-003 - Duplicidad

No se permitirá registrar dos clientes con la misma identificación dentro del mismo tipo de identificación.

### RN-004 - Integridad

No se permitirá registrar un cliente sin los datos obligatorios correspondientes a su tipo de persona.

### RN-005 - Estado

La baja lógica de un cliente no deberá eliminar su historial ni sus relaciones con pólizas existentes.

## 7. Criterios de aceptación

- Se puede registrar una persona física.
- Se puede registrar una persona jurídica.
- No se permiten identificaciones duplicadas.
- Se pueden consultar clientes.
- Se pueden modificar sus datos.
- Se conserva la información histórica.
- Se validan los campos obligatorios.

## 8. Fuera del alcance

- Gestión de productores y brokers.
- Administración de usuarios y permisos.
- Gestión de grupos económicos.
- Verificación externa de identidad.
- Prevención de fraude.

## 9. Consideraciones futuras

Se deberá evaluar la separación entre cliente, tomador, asegurado y beneficiario.

Estos conceptos pueden representar roles diferentes dentro de una operación aseguradora y no deben confundirse en el modelo de datos.

---

**Documento sujeto a revisión funcional.**
