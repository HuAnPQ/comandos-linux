### 📥 **Opción 1: Descargar el `.tar` desde Docker Hub y transferirlo**

 

1. **Desde una PC con Docker y acceso a internet** (puede ser tu laptop personal o una máquina en casa):

   ```bash

   docker pull redis/redis-stack:latest

   docker save -o redis-stack.tar redis/redis-stack:latest

   ```

 

2. **Copia el archivo `redis-stack.tar` a tu teléfono**:

   - Conecta el teléfono por USB y transfiere el archivo.

   - O súbelo a una nube (Google Drive, OneDrive, etc.) desde la PC y luego descárgalo en el teléfono.

 

3. **Transfiérelo al servidor sin internet**:

   - Usa un cable USB  si el servidor tiene puerto USB o usar bluetooth.
 

---

### 🌐 **Opción 2: Descargar directamente el `.tar` desde un sitio confiable**

 

Si no puedes usar Docker en otra máquina, puedes **descargar el `.tar` ya generado** desde un sitio como GitHub o Docker Hub (aunque no siempre está disponible como `.tar` directamente):

 

- [Página oficial de Redis Stack en Docker Hub](https://hub.docker.com/r/redis/redis-stack)

- [Repositorio de Redis Stack en GitHub](https://github.com/redis-stack/redis-stack/releases)

 
---

 

### 🧰 Luego

 

Una vez que tengas el archivo en el servidor:

 

```bash

docker load -i redis-stack.tar

docker run -d --name redis-json -p 6379:6379 redis/redis-stack:latest

```

 
