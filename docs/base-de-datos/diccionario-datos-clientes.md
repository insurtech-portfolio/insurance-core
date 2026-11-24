
# Diccionario de Datos - Módulo Clientes

**Proyecto:** Insurance Core  
**Documento:** BD-003  
**Versión:** 1.0  
**Estado:** Propuesta inicial  
**Motor:** PostgreSQL

## 1. Tabla: party

Representa la identidad principal de una persona física o jurídica.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| id | UUID | Sí | Identificador único |
| party_type | VARCHAR(20) | Sí | NATURAL_PERSON / LEGAL_ENTITY |
| email | VARCHAR(150) | No | Correo electrónico |
| phone | VARCHAR(30) | No | Teléfono |
| status | VARCHAR(20) | Sí | Estado de la persona |
| created_at | TIMESTAMPTZ | Sí | Fecha de creación |
| updated_at | TIMESTAMPTZ | Sí | Fecha de actualización |

Clave primaria: id.

## 2. Tabla: natural_person

Contiene los datos específicos de personas físicas.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| party_id | UUID | Sí | Identificador de Party |
| first_name | VARCHAR(100) | Sí | Nombre |
| last_name | VARCHAR(100) | Sí | Apellido |
| birth_date | DATE | No | Fecha de nacimiento |

Clave primaria: party_id.

Clave foránea: party_id → party.id.

## 3. Tabla: legal_entity

Contiene los datos específicos de personas jurídicas.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| party_id | UUID | Sí | Identificador de Party |
| legal_name | VARCHAR(200) | Sí | Razón social |
| trade_name | VARCHAR(200) | No | Nombre comercial |

Clave primaria: party_id.

Clave foránea: party_id → party.id.

## 4. Tabla: party_identification

Almacena las identificaciones de personas.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| id | UUID | Sí | Identificador único |
| party_id | UUID | Sí | Persona relacionada |
| identification_type | VARCHAR(30) | Sí | Tipo de identificación |
| identification_number | VARCHAR(50) | Sí | Número de identificación |
| issuing_country | VARCHAR(2) | Sí | Código de país emisor |

Clave primaria: id.

Clave foránea: party_id → party.id.

Restricción de unicidad propuesta:
(identification_type, identification_number, issuing_country).

## 5. Tabla: customer

Representa la relación comercial entre una persona y la aseguradora.

| Campo | Tipo PostgreSQL | Obligatorio | Descripción |
|---|---|---|---|
| id | UUID | Sí | Identificador único |
| party_id | UUID | Sí | Persona relacionada |
| customer_status | VARCHAR(20) | Sí | Estado del cliente |
| created_at | TIMESTAMPTZ | Sí | Fecha de alta |

Clave primaria: id.

Clave foránea: party_id → party.id.

Restricción de unicidad: party_id.

## 6. Consideraciones generales

- Los identificadores utilizarán UUID.
- Las fechas y horas utilizarán TIMESTAMPTZ.
- Los estados tendrán valores controlados.
- Se utilizarán claves foráneas para garantizar integridad referencial.
- Las identificaciones no se utilizarán como claves primarias.
- Las restricciones de unicidad deberán contemplar el ámbito de emisión de cada identificación.

## 7. Consideraciones de implementación

La estructura definitiva deberá contemplar:

- Validaciones de integridad entre Party y sus especializaciones.
- Control de duplicidad de identificaciones.
- Protección de información personal.
- Baja lógica cuando corresponda.
- Auditoría de modificaciones.

## 8. Estado

Diccionario de datos inicial sujeto a revisión antes de su implementación.
