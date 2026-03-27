## Instalación de MySQL con Docker

En lugar de instalar MySQL directamente en el servidor, levantamos en un contenedor de Docker.

### Comando utilizado

```bash
docker run --name mysql-container -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password -d mysql
```

### ¿Qué hace este comando?

| Comando | Significado |
|---|---|
| `--name mysql-container` | Le da el nombre `mysql-container` al contenedor |
| `-p 3306:3306` | Expone el puerto 3306 para que sea accesible desde fuera |
| `-e MYSQL_ROOT_PASSWORD=...` | Define la contraseña del usuario `root` de MySQL |
| `-d mysql` | Descarga y corre la imagen oficial de MySQL en segundo plano |


### Conexión desde Rider

Una vez que el contenedor estaba corriendo, se conecta a la base de datos desde **Rider** siguiendo estos pasos:

1. Abrir Rider y buscar la opción **"Connect to Database"**.
2. Seleccionar **"Add manually"** para ingresar los datos de conexión.
3. Llenar los datos así:

| Campo | Valor            |
|---|------------------|
| Host | `Direccion IPv4` |
| Puerto | `3306`           |
| Usuario | `root`           |
| Contraseña | `La contraseña que pusiste al crear el contenedor`       |

4. Hacer clic en **"Test Connection"** para verificar que la conexión funciona y luego en **"OK"**.