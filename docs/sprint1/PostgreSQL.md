## Instalación de PostgreSQL con Docker

La instalación de PostgreSQL se hace igual a como se hizo con MySQL.

### Comando a usar

```bash
docker run --name postgres-container -p 5432:5432 -e POSTGRES_PASSWORD=PASSWORD -d postgres
```

### ¿Qué hace este comando?

| Comando | Significado |
|---|---|
| `--name postgres-container` | Le da el nombre `postgres-container` al contenedor |
| `-p 5432:5432` | Expone el puerto 5432 |
| `-e POSTGRES_PASSWORD=...` | Define la contraseña del usuario `postgres` de PostgreSQL |
| `-d postgres` | Descarga y corre la imagen oficial de PostgreSQL en segundo plano |

### Conexión desde Rider

El proceso es el mismo que con MySQL:

1. Abrir Rider y buscar la opción **"Connect to Database"**.
2. Seleccionar **"Add manually"** para ingresar los datos de conexión.
3. Llenar los datos así:

| Campo | Valor |
|---|---|
| Host | `Dirección IPv4` |
| Puerto | `5432` |
| Usuario | `postgres` |
| Contraseña | La contraseña que pusiste al crear el contenedor |
| Base de datos | `postgres` |

4. Hacer clic en **"Test Connection"** para verificar que la conexión funciona y luego en **"OK"**.