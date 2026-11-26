
# PostgreSQL con Docker

**Proyecto:** Insurance Core
**VersiÃ³n de PostgreSQL:** 17
**Infraestructura:** Docker Desktop + Docker Compose
**Estado:** ConfiguraciÃ³n inicial implementada

## 1. Objetivo

Ejecutar PostgreSQL en un contenedor Docker para el desarrollo local de Insurance Core.

La base de datos se administra mediante Docker Compose, utilizando un volumen persistente para conservar la informaciÃ³n entre reinicios del contenedor.

## 2. Estructura de archivos

```text
insurance-core/
â”‚
â”œâ”€â”€ .env
â”œâ”€â”€ .gitignore
â”‚
â”œâ”€â”€ docs/
â”‚   â””â”€â”€ infraestructura/
â”‚       â””â”€â”€ docker-postgresql.md
â”‚
â””â”€â”€ infrastructure/
    â””â”€â”€ docker/
        â””â”€â”€ docker-compose.yml
```

El archivo `.env` contiene las variables de configuraciÃ³n y credenciales locales. EstÃ¡ excluido del control de versiones mediante `.gitignore`.

## 3. ConfiguraciÃ³n de PostgreSQL

| ParÃ¡metro | Valor |
|---|---|
| Imagen Docker | postgres:17 |
| Motor | PostgreSQL |
| VersiÃ³n verificada | 17.12 |
| Proyecto Compose | insurance-core |
| Servicio | postgres |
| Contenedor | insurance-core-postgres-1 |
| Base de datos | insurance_core |
| Usuario | insurance_admin |
| Puerto | 5432 |
| Volumen | insurance-core_insurance_core_postgres_data |

## 4. Variables de entorno

El archivo `.env` debe existir en la raÃ­z del repositorio.

Variables requeridas:

```dotenv
POSTGRES_DB=insurance_core
POSTGRES_USER=insurance_admin
POSTGRES_PASSWORD=REEMPLAZAR_POR_UNA_CONTRASEÃ‘A_LOCAL
POSTGRES_PORT=5432
```

No publicar el archivo `.env` ni incluir credenciales reales en GitHub.

## 5. Iniciar PostgreSQL

Desde la raÃ­z del repositorio:

```powershell
docker compose -f infrastructure/docker/docker-compose.yml up -d
```

Este comando crea e inicia el servicio PostgreSQL.

## 6. Verificar el estado

```powershell
docker compose -f infrastructure/docker/docker-compose.yml ps
```

Para consultar los contenedores activos:

```powershell
docker ps
```

El contenedor debe mostrar el estado `healthy`.

## 7. Consultar los registros

```powershell
docker compose -f infrastructure/docker/docker-compose.yml logs postgres
```

Para seguir los registros en tiempo real:

```powershell
docker compose -f infrastructure/docker/docker-compose.yml logs -f postgres
```

## 8. Conectarse a PostgreSQL

Desde PowerShell:

```powershell
docker exec -it insurance-core-postgres-1 psql -U insurance_admin -d insurance_core
```

Dentro de PostgreSQL:

```sql
SELECT version();
```

Consultar la conexiÃ³n:

```sql
\conninfo
```

Listar las bases de datos:

```sql
\l
```

Listar las tablas:

```sql
\dt
```

Salir:

```sql
\q
```

## 9. Detener PostgreSQL

```powershell
docker compose -f infrastructure/docker/docker-compose.yml stop
```

Este comando detiene el servicio sin eliminar el contenedor ni el volumen.

Para volver a iniciarlo:

```powershell
docker compose -f infrastructure/docker/docker-compose.yml start
```

## 10. Eliminar el contenedor

```powershell
docker compose -f infrastructure/docker/docker-compose.yml down
```

Elimina el contenedor y la red del proyecto, pero conserva el volumen persistente.

Para volver a crear el contenedor:

```powershell
docker compose -f infrastructure/docker/docker-compose.yml up -d
```

## 11. Persistencia de datos

Los datos se almacenan en un volumen Docker:

`insurance-core_insurance_core_postgres_data`

El volumen permite conservar los datos aunque el contenedor sea eliminado y creado nuevamente.

**Advertencia:** no utilizar `docker compose down -v` salvo que se quiera eliminar deliberadamente el volumen y todos los datos almacenados en PostgreSQL.

## 12. ConvenciÃ³n de nombres

Se utiliza el nombre del proyecto `insurance-core` para agrupar los recursos administrados por Docker Compose.

El servicio se denomina `postgres` y Docker Compose genera automÃ¡ticamente el nombre del contenedor.

Esta convenciÃ³n permite mantener separados los entornos de distintos proyectos, como Insurance Core, Odoo y Contact Center Insurance.

## 13. Estado de implementaciÃ³n

- [x] Docker Desktop operativo.
- [x] Docker Compose operativo.
- [x] PostgreSQL 17 desplegado.
- [x] Base de datos insurance_core creada.
- [x] Volumen persistente configurado.
- [x] Healthcheck operativo.
- [x] ConexiÃ³n PostgreSQL verificada.
- [x] DocumentaciÃ³n inicial preparada.

## 14. PrÃ³ximos pasos

- Implementar el esquema fÃ­sico del mÃ³dulo Clientes.
- Crear las tablas y restricciones de integridad.
- Versionar los scripts SQL.
- Verificar las relaciones y restricciones mediante consultas.
