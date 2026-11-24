
# Diccionario de Datos - Módulo Clientes

**Proyecto:** Insurance Core  
**Documento:** BD-003  
**Versión:** 1.1  
**Estado:** Diseño lógico revisado  
**Motor:** PostgreSQL

---

## 1. Tabla: party

Representa la identidad principal de una persona física o jurídica.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| id | UUID | Sí | Identificador único |
| party_type | VARCHAR(20) | Sí | NATURAL_PERSON / LEGAL_ENTITY |
| email | VARCHAR(150) | No | Correo electrónico |
| phone | VARCHAR(30) | No | Teléfono |
| street | VARCHAR(150) | No | Calle |
| street_number | VARCHAR(20) | No | Número de domicilio |
| floor | VARCHAR(10) | No | Piso |
| apartment | VARCHAR(10) | No | Departamento |
| postal_code | VARCHAR(15) | No | Código postal |
| locality | VARCHAR(100) | No | Localidad |
| province | VARCHAR(100) | No | Provincia |
| country_code | VARCHAR(2) | No | Código de país |
| status | VARCHAR(20) | Sí | Estado de la persona |
| created_at | TIMESTAMPTZ | Sí | Fecha de creación |
| updated_at | TIMESTAMPTZ | Sí | Fecha de actualización |

**Clave primaria:** id.

**Valores permitidos para party_type:**
- NATURAL_PERSON
- LEGAL_ENTITY

**Valores permitidos para status:**
- ACTIVE
- INACTIVE

El domicilio principal será opcional en esta primera versión.

---

## 2. Tabla: natural_person

Contiene los datos específicos de personas físicas.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| party_id | UUID | Sí | Identificador de Party |
| first_name | VARCHAR(100) | Sí | Nombre |
| last_name | VARCHAR(100) | Sí | Apellido |
| birth_date | DATE | No | Fecha de nacimiento |

**Clave primaria:** party_id.

**Clave foránea:** party_id → party.id.

---

## 3. Tabla: legal_entity

Contiene los datos específicos de personas jurídicas.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| party_id | UUID | Sí | Identificador de Party |
| legal_name | VARCHAR(200) | Sí | Razón social |
| trade_name | VARCHAR(200) | No | Nombre comercial |

**Clave primaria:** party_id.

**Clave foránea:** party_id → party.id.

---

## 4. Tabla: party_identification

Almacena los documentos e identificaciones de las personas.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| id | UUID | Sí | Identificador único |
| party_id | UUID | Sí | Persona relacionada |
| identification_type | VARCHAR(30) | Sí | Tipo de identificación |
| identification_number | VARCHAR(50) | Sí | Número de identificación |
| issuing_country | VARCHAR(2) | Sí | Código de país emisor |

**Clave primaria:** id.

**Clave foránea:** party_id → party.id.

**Restricción de unicidad:**

(identification_type, identification_number, issuing_country).

La identificación no se utilizará como clave primaria.

---

## 5. Tabla: customer

Representa la relación comercial entre una persona y la aseguradora.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| id | UUID | Sí | Identificador único |
| party_id | UUID | Sí | Persona relacionada |
| customer_status | VARCHAR(20) | Sí | Estado del cliente |
| created_at | TIMESTAMPTZ | Sí | Fecha de alta |

**Clave primaria:** id.

**Clave foránea:** party_id → party.id.

**Restricción de unicidad:** party_id.

**Valores permitidos para customer_status:**
- ACTIVE
- INACTIVE

Una persona podrá tener una única relación de cliente con la aseguradora.

---

## 6. Reglas de integridad

### RI-001 - Identificación única

Cada Party deberá contar con un identificador interno único.

### RI-002 - Tipo de persona

Cada Party deberá tener un único tipo de persona:

- NATURAL_PERSON.
- LEGAL_ENTITY.

### RI-003 - Especialización

Una Party de tipo NATURAL_PERSON deberá tener un registro asociado en natural_person.

Una Party de tipo LEGAL_ENTITY deberá tener un registro asociado en legal_entity.

Una misma Party no podrá tener simultáneamente ambas especializaciones.

### RI-004 - Identificaciones

Una identificación no podrá duplicarse considerando conjuntamente:

- Tipo de identificación.
- Número de identificación.
- País emisor.

### RI-005 - Relación comercial

Una Party podrá tener como máximo un registro Customer.

### RI-006 - Integridad referencial

No se permitirá eliminar una Party cuando existan relaciones comerciales o identificaciones asociadas que deban conservarse.

### RI-007 - Estados

Los estados deberán utilizar valores controlados y no admitir textos libres.

### RI-008 - Conservación histórica

La baja de una persona o cliente será lógica. No se eliminarán físicamente registros que deban conservarse por razones operativas o históricas.

---

## 7. Consideraciones de diseño

- Los identificadores internos utilizarán UUID.
- Las fechas y horas utilizarán TIMESTAMPTZ.
- Se utilizarán claves foráneas para garantizar integridad referencial.
- Se aplicarán restricciones UNIQUE donde corresponda.
- Se utilizarán restricciones CHECK para los valores controlados.
- Los campos de domicilio serán opcionales.
- Se contemplará la protección de datos personales.
- Los identificadores fiscales y documentos no serán claves primarias.
- Se evitará duplicar personas por su participación en diferentes roles aseguradores.

---

## 8. Consideraciones de implementación

La implementación deberá contemplar:

- Validaciones de integridad entre Party y sus especializaciones.
- Control de duplicidad de identificaciones.
- Validación de datos obligatorios según el tipo de persona.
- Control de estados.
- Baja lógica.
- Auditoría de modificaciones.
- Pruebas de integridad referencial.

Las reglas que involucren varias tablas deberán validarse en la lógica de negocio de Django y, cuando corresponda, mediante restricciones adicionales en PostgreSQL.

---

## 9. Fuera del alcance inicial

- Múltiples domicilios.
- Múltiples contactos.
- Representantes legales.
- Grupos económicos.
- Verificación externa de identidad.
- Gestión de productores y brokers.
- Gestión de beneficiarios.
- Gestión de tomadores y asegurados.

Estos conceptos podrán incorporarse en futuras versiones.

---

## 10. Decisiones pendientes para futuras versiones

- Definir catálogo completo de tipos de identificación.
- Evaluar domicilios múltiples.
- Evaluar contactos múltiples.
- Definir reglas de validación específicas para DNI, CUIT y CUIL.
- Incorporar auditoría detallada de cambios.
- Definir tratamiento de datos personales y políticas de conservación.

---

## 11. Estado del documento

Diseño lógico revisado del módulo Clientes.

**Versión:** 1.1

**Próximo paso:** diseño físico e implementación en PostgreSQL.

