# Documento de Investigación sobre Docker

## Introducción

Docker es una plataforma de contenedores que permite crear, ejecutar y administrar aplicaciones y servicios de manera aislada y eficiente. Con Docker, los desarrolladores pueden crear entornos consistentes y reproducibles, independientemente del sistema operativo y las configuraciones de hardware subyacentes. Esta tecnología ha revolucionado la forma en que se construyen y despliegan aplicaciones, facilitando el trabajo en equipos de desarrollo y operaciones (DevOps).

## ¿Qué es Docker?

Docker es una herramienta de contenedorización que permite empaquetar una aplicación y todas sus dependencias (librerías, configuraciones, etc.) en un contenedor. Este contenedor es una unidad ligera, portable y aislada que puede ejecutarse de manera consistente en cualquier sistema operativo o infraestructura que soporte Docker.

El contenedor es una forma de virtualización a nivel de sistema operativo, a diferencia de las máquinas virtuales tradicionales, que virtualizan el hardware completo. Los contenedores comparten el mismo núcleo del sistema operativo anfitrión, lo que los hace más ligeros y rápidos que las máquinas virtuales.

### Beneficios de Docker

1. **Portabilidad**: Un contenedor creado en un entorno puede ejecutarse de manera idéntica en otro entorno, ya sea en la máquina local de un desarrollador, en un servidor o en la nube.
2. **Escalabilidad**: Docker facilita el escalado horizontal de aplicaciones, lo que significa que se pueden crear y gestionar instancias de contenedores de forma eficiente.
3. **Aislamiento**: Los contenedores permiten ejecutar aplicaciones de manera aislada, evitando conflictos entre dependencias y configuraciones.
4. **Eficiencia**: Docker utiliza menos recursos que las máquinas virtuales, lo que mejora el rendimiento y reduce los costos de infraestructura.

## ¿Para qué sirve Docker?

Docker es útil para diversas tareas, especialmente en el desarrollo de software y en la administración de sistemas. Algunas de sus principales aplicaciones son:

- **Desarrollo de aplicaciones**: Los desarrolladores pueden crear entornos de desarrollo consistentes y reproducibles.
- **Despliegue de aplicaciones**: Facilita el despliegue de aplicaciones en diferentes entornos sin preocuparse por las diferencias en la infraestructura.
- **Pruebas automatizadas**: Los equipos de calidad pueden crear entornos de pruebas idénticos a los de producción, lo que mejora la fiabilidad de las pruebas.
- **Microservicios**: Docker es ideal para desplegar arquitecturas basadas en microservicios, ya que permite gestionar y escalar múltiples servicios independientes.

## Instalación de Docker en Ubuntu

### Requisitos previos

Antes de instalar Docker en Ubuntu, asegúrate de que tu sistema esté actualizado. Para ello, ejecuta los siguientes comandos:

```bash
sudo apt update
sudo apt upgrade
```

### Pasos para instalar Docker

1. **Instalar las dependencias necesarias**:
   Docker requiere algunas dependencias para su instalación. Ejecuta el siguiente comando:

   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common
   ```

2. **Añadir la clave GPG de Docker**:
   Docker necesita una clave GPG para verificar los paquetes descargados. Ejecuta:

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

3. **Añadir el repositorio de Docker**:
   Agrega el repositorio de Docker a tu lista de fuentes de paquetes:

   ```bash
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

4. **Actualizar los repositorios**:
   Luego de añadir el repositorio, actualiza los paquetes disponibles:

   ```bash
   sudo apt update
   ```

5. **Instalar Docker**:
   Finalmente, instala Docker:

   ```bash
   sudo apt install docker-ce
   ```

6. **Verificar la instalación**:
   Para comprobar que Docker se ha instalado correctamente, ejecuta:

   ```bash
   sudo docker --version
   ```

   Esto debería devolver la versión de Docker instalada.

### Instalación de Docker Compose

Docker Compose es una herramienta para definir y ejecutar aplicaciones Docker multi-contenedor. Para instalarlo, ejecuta:

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

Para verificar la instalación de Docker Compose:

```bash
docker-compose --version
```

## Comandos de Docker más utilizados

Aquí se presentan algunos de los comandos más utilizados en Docker:

- **docker run**: Ejecuta un contenedor a partir de una imagen.
  ```bash
  docker run [opciones] <imagen>
  ```

- **docker ps**: Muestra los contenedores en ejecución.
  ```bash
  docker ps
  ```

- **docker ps -a**: Muestra todos los contenedores, incluyendo los detenidos.
  ```bash
  docker ps -a
  ```

- **docker build**: Crea una imagen a partir de un Dockerfile.
  ```bash
  docker build -t <nombre_imagen> .
  ```

- **docker stop**: Detiene un contenedor en ejecución.
  ```bash
  docker stop <nombre_contenedor>
  ```

- **docker start**: Inicia un contenedor detenido.
  ```bash
  docker start <nombre_contenedor>
  ```

- **docker exec**: Ejecuta un comando en un contenedor en ejecución.
  ```bash
  docker exec -it <nombre_contenedor> <comando>
  ```

- **docker rm**: Elimina un contenedor.
  ```bash
  docker rm <nombre_contenedor>
  ```

- **docker rmi**: Elimina una imagen.
  ```bash
  docker rmi <nombre_imagen>
  ```

- **docker logs**: Muestra los registros de un contenedor.
  ```bash
  docker logs <nombre_contenedor>
  ```

## Anexo: Instalación y ejecución de un contenedor interesante

En esta sección, se describe el proceso de instalación y ejecución de un contenedor de **nginx**, que es un servidor web popular.

### Pasos:

1. **Ejecutar el contenedor de nginx**:
   Utilizamos el siguiente comando para ejecutar un contenedor de nginx:

   ```bash
   docker run -d -p 8080:80 --name nginx-container nginx
   ```

   Este comando descargará la imagen de nginx (si no la tienes) y la ejecutará en segundo plano. El contenedor estará accesible en el puerto 8080 de tu máquina local.

2. **Verificar que el contenedor está en ejecución**:
   Ejecuta:

   ```bash
   docker ps
   ```

3. **Acceder a nginx desde el navegador**:
   Abre tu navegador y ve a `http://localhost:8080`. Deberías ver la página de bienvenida de nginx.

4. **Detener y eliminar el contenedor**:
   Para detener y eliminar el contenedor, ejecuta:

   ```bash
   docker stop nginx-container
   docker rm nginx-container
   ```

## Crear un contenedor desde cero

Para crear un contenedor desde cero, lo primero que necesitamos es un **Dockerfile**. Un Dockerfile es un archivo de texto que contiene las instrucciones necesarias para construir una imagen Docker.

### Ejemplo de Dockerfile:

```dockerfile
# Usar una imagen base de Ubuntu
FROM ubuntu:20.04

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar archivos al contenedor
COPY . /app

# Instalar dependencias
RUN apt-get update && apt-get install -y python3 python3-pip

# Instalar paquetes de Python
RUN pip3 install -r requirements.txt

# Exponer el puerto 5000
EXPOSE 5000

# Comando para ejecutar la aplicación
CMD ["python3", "app.py"]
```

### Pasos para construir y ejecutar el contenedor:

1. **Construir la imagen**:
   En el mismo directorio donde se encuentra el Dockerfile, ejecuta:

   ```bash
   docker build -t myapp .
   ```

2. **Ejecutar el contenedor**:
   Para ejecutar el contenedor con la imagen creada:

   ```bash
   docker run -d -p 5000:5000 --name myapp-container myapp
   ```

3. **Verificar que la aplicación está corriendo**:
   Accede a `http://localhost:5000` para verificar que la aplicación está en ejecución.

## Presentación a la clase

### ¿Qué es Docker?

Docker es una plataforma que permite ejecutar aplicaciones dentro de contenedores, que son entornos aislados y ligeros. Esto facilita la portabilidad, el aislamiento y la escalabilidad de las aplicaciones.

### ¿Para qué sirve Docker?

Docker se utiliza para crear, gestionar y ejecutar contenedores de aplicaciones. Es muy útil para desarrollar aplicaciones consistentes, facilitar el despliegue en diferentes entornos y optimizar la infraestructura.

### ¿Cómo instalar Docker?

Para instalar Docker en Ubuntu, basta con seguir los pasos de instalación previamente descritos, que incluyen actualizar el sistema, agregar el repositorio de Docker, e instalarlo usando el gestor de paquetes apt.

---

Este documento ha cubierto los aspectos esenciales de Docker, su instalación en Ubuntu, los comandos más comunes, y cómo trabajar con contenedores.
