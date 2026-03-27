# Configuración del Docker en el servidor


## Instalación de Docker

Docker se instaló directamente en el servidor siguiendo los pasos oficiales de Ubuntu.

### Pasos realizados

**1. Actualizar los paquetes del sistema:**

Antes de instalar cualquier cosa, se actualiza la lista de paquetes disponibles y se aplican las actualizaciones pendientes para evitar conflictos.

```bash
sudo apt update && sudo apt upgrade -y
```

**2. Instalar dependencias necesarias:**

Se instalan herramientas que Docker necesita para descargar e instalar sus componentes de forma segura.

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

**3. Agregar la clave GPG oficial de Docker:**

Esto le dice al sistema que confíe en los paquetes que vienen de Docker, se usa como medida de seguridad para verificar que lo que se descarga es legítimo.

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

**4. Agregar el repositorio de Docker:**

Se indica de dónde debe descargar Ubuntu los paquetes de Docker, para que el sistema sepa dónde encontrarlos.

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**5. Instalar Docker Engine:**

Con el repositorio ya configurado, aquí se instala Docker con sus componentes principales.

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**6. Verificar que Docker funcione:**

Se corre un contenedor de prueba para confirmar que Docker quedó bien instalado, si todo está bien, imprime un mensaje de bienvenida.

```bash
sudo docker run hello-world
```

