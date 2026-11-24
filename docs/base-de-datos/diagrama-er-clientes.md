
# Diagrama Entidad-Relación - Módulo Clientes

**Proyecto:** Insurance Core  
**Documento:** BD-002  
**Versión:** 1.0  
**Estado:** Propuesta inicial

## 1. Diagrama

```mermaid
erDiagram
    PARTY ||--o| NATURAL_PERSON : "tiene"
    PARTY ||--o| LEGAL_ENTITY : "tiene"
    PARTY ||--o{ PARTY_IDENTIFICATION : "posee"
    PARTY ||--o| CUSTOMER : "puede_ser"

    PARTY {
        uuid id PK
        varchar party_type
        varchar email
        varchar phone
        varchar status
        timestamp created_at
        timestamp updated_at
    }

    NATURAL_PERSON {
        uuid party_id PK, FK
        varchar first_name
        varchar last_name
        date birth_date
    }

    LEGAL_ENTITY {
        uuid party_id PK, FK
        varchar legal_name
        varchar trade_name
    }

    PARTY_IDENTIFICATION {
        uuid id PK
        uuid party_id FK
        varchar identification_type
        varchar identification_number
        varchar issuing_country
    }

    CUSTOMER {
        uuid id PK
        uuid party_id FK
        varchar customer_status
        timestamp created_at
    }
```

## 2. Descripción de las relaciones

- PARTY y NATURAL_PERSON: una persona puede tener información específica de persona física.
- PARTY y LEGAL_ENTITY: una persona puede tener información específica de persona jurídica.
- PARTY y PARTY_IDENTIFICATION: una persona puede tener varias identificaciones.
- PARTY y CUSTOMER: una persona puede tener una relación comercial como cliente.

## 3. Consideraciones

- Los identificadores principales serán UUID.
- Las relaciones se implementarán mediante claves foráneas.
- Una persona física no deberá tener simultáneamente un registro de persona jurídica.
- La obligatoriedad de las entidades específicas se garantizará mediante validaciones y restricciones.
- La unicidad de identificaciones deberá contemplar su tipo y ámbito de emisión.

## 4. Observación

El diagrama representa el diseño inicial. Las restricciones definitivas se especificarán durante el diseño físico de PostgreSQL.
