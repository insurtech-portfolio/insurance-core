
# Modelo Conceptual - Módulo Clientes

**Proyecto:** Insurance Core  
**Documento:** BD-001  
**Versión:** 1.0  
**Estado:** Propuesta inicial

## 1. Objetivo

Definir las entidades principales del módulo Clientes y sus relaciones conceptuales.

## 2. Entidades

### Party
Representa la identidad de una persona física o jurídica.

### NaturalPerson
Contiene los datos específicos de una persona física.

### LegalEntity
Contiene los datos específicos de una persona jurídica.

### PartyIdentification
Almacena los documentos e identificaciones asociados a una persona.

### Customer
Representa la relación comercial de una persona con la aseguradora.

## 3. Relaciones

- Una Party corresponde a una persona física o jurídica.
- Una Party puede tener una NaturalPerson o una LegalEntity, según su tipo.
- Una Party puede tener una o varias identificaciones.
- Una Party puede tener una relación Customer.
- Una persona podrá participar en múltiples pólizas con diferentes roles.

## 4. Reglas de integridad

- Cada Party tendrá un identificador único.
- Una Party deberá tener un único tipo de persona.
- Una Party física tendrá datos de NaturalPerson.
- Una Party jurídica tendrá datos de LegalEntity.
- No se permitirán identificaciones duplicadas dentro del mismo ámbito de identificación.
- Una persona no deberá duplicarse por participar en diferentes roles aseguradores.

## 5. Decisiones de diseño

- Separar identidad de relación comercial.
- Diferenciar personas físicas y jurídicas.
- Permitir múltiples identificaciones.
- Mantener preparado el modelo para los roles aseguradores.
- Utilizar identificadores internos independientes de DNI o CUIT.

## 6. Fuera del alcance

- Gestión de grupos económicos.
- Representantes legales.
- Múltiples domicilios.
- Múltiples contactos.
- Validación externa de identidad.
- Gestión de productores y brokers.

## 7. Tecnología

Base de datos: PostgreSQL.
