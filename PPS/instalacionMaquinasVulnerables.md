<h1 align="center">Instalación de Máquinas Vulnerables: dockerlabs.es</h1>

![imagen portada infraestructura](https://github.com/IES-Rafael-Alberti/25-26-Ciberseguridad-Grupo-5/blob/main/PPS/images/portadainfraestructura.png)

***Fecha:*** 27 de noviembre de 2025
<br>***Autor***: Sergio González

---
## Índice

1. ***[Introducción](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#1-introducci%C3%B3n)***
2. ***[Preparación del Entorno](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#2-preparaci%C3%B3n-del-entorno)***
3. ***[Despliegue de la Máquina Vulnerable](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#3-despliegue-de-la-m%C3%A1quina-vulnerable)***
4. ***[Reconocimiento y Análisis de Vulnerabilidades](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#4-reconocimiento-y-an%C3%A1lisis-de-vulnerabilidades)***
5. ***[Explotación de Vulnerabilidades](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#5-explotaci%C3%B3n-de-vulnerabilidades)***
6. ***[Medidas de Mitigación y Buenas Prácticas](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#6-medidas-de-mitigaci%C3%B3n-y-buenas-pr%C3%A1cticas)***
7. ***[Conclusiones](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#7-conclusiones)***

---
## 1. ***Introducción***

En este proyecto vamos a usar ***WSL*** junto con ***Kali Linux*** para crear un entorno desde el que poder lanzar herramientas de análisis y trabajar con contenedores cómodamente desde Windows.

Una vez preparado el entorno, desplegaremos una ***máquina vulnerable de DockerLabs***. Sobre ella haremos un proceso básico de reconocimiento, análisis y explotación de vulnerabilidades para entender cómo se detectan los fallos y, después, cómo se podrían mitigar aplicando buenas prácticas.

---
## 2. ***Preparación del Entorno***

En este apartado se configura WSL para poder acceder correctamente a los servicios que se ejecuten dentro de los contenedores, y después se accede a Kali Linux para trabajar desde allí.

---
### 2.1. ***Configuración de red en WSL***

Para que los puertos de los contenedores sean accesibles desde Windows como si fueran localhost, es necesario ajustar la red de WSL.

- Primero, accedemos a ***WSL Settings*** desde Windows:

<img width="1332" height="697" alt="image" src="https://github.com/user-attachments/assets/fc78865d-324c-4026-89e4-97d13588d259" />

- Luego, nos ubicamos en el apartado ***Funciones de red***, y en la primera opción cambiamos el modo de red a ***Mirrored*** y en la segunda opción ***deshabilitamos el firewall de WSL***:

<img width="1335" height="696" alt="image" src="https://github.com/user-attachments/assets/3ba9ddaf-0db3-44d0-a459-238080733b60" />

Con esto, cualquier servicio levantado en Kali bajo WSL será accesible desde el navegador o terminal de Windows usando localhost.

---
### 2.2. ***Acceder a Kali Linux en WSL***

Después de ajustar la configuración de red, el siguiente paso es entrar en la distribución de Kali Linux dentro de WSL, que será el entorno desde el que se desplegarán las máquinas de Dockerlabs.

- Primero vamos a instalar kali linux en WSL. Para ello, ejecutamos el siguiente comando:

```bash
wsl --install kali-linux
```

<img width="1483" height="180" alt="image" src="https://github.com/user-attachments/assets/3f11d74f-5fba-457a-bae6-cf50b98bc30c" /><br>
> Este mensaje se nos muestra ya que he instalado anteriormente la distribución kali-linux.

- Ahora, accedemos a la máquina kali-linux de WSL. Para ello, ejecutamos el siguiente comando:

```bash
wsl -d kali-linux
```

<img width="798" height="192" alt="image" src="https://github.com/user-attachments/assets/3ca6c738-72a5-443e-bd97-13c6305a4245" />

Con esto, Kali linux queda listo para comenzar con el despliegue de la máquina vulnerable.

---
## 3. ***Despliegue de la Máquina Vulnerable***

En este apartado se muestra cómo descargar y poner en marcha una máquina vulnerable desde DockerLabs utilizando Docker dentro de Kali Linux en WSL. Este será el sistema sobre el que realizaremos el reconocimiento y análisis de vulnerabilidades.

### 3.1. ***Descargar la máquina vulnerable desde DockerLabs***

- Descargamos el comprimido de la ***máquina Vacaciones*** de la página Dockerlab. Este es el ***[enlace](https://mega.nz/file/YCEGAISD#y6iWUG_auH4vUApClb9ix7H6JmOCKm4vAYS2TjQn59g)*** para descargarlo.

<img width="961" height="709" alt="image" src="https://github.com/user-attachments/assets/93c47159-d24b-4718-89fa-7af4b983bc16" />
<img width="1409" height="652" alt="image" src="https://github.com/user-attachments/assets/96ffa87e-a2f3-439b-9f85-ffdc59f0b273" />

- Nos ubicamos en el directorio Downloads desde la máquina kali-linux de WSL. Luego, descomprimimos el .zip que nos acabamos de descargar para poder desplegar la máquina. Para ello, ejecutamos los siguientes comandos:

```bash
cd Downloads/
unzip vacaciones.zip
```

<img width="901" height="330" alt="image" src="https://github.com/user-attachments/assets/ec03ef03-fa3f-4bf6-b46a-bd994c784c80" />
<img width="868" height="400" alt="image" src="https://github.com/user-attachments/assets/37bc3648-5e27-4317-81c6-03e9b13d6b5a" />

### 3.2. ***Modificación del archivo auto_deploy.sh***

- Una vez tenemos los archivos, vamos a modificar el script ***auto_deploy.sh*** para que los puertos y servicios de la máquina docker se puedan acceder desde la máquina kali linux de WSL. Para ello, vamos ejecutar este comando y modificaremos la siguiente línea:

```bash
nano auto_deploy.sh

# Línea ha modificar
docker run -d --network host --name $CONTAINER_NAME $IMAGE_NAME > /dev/null
```

<img width="821" height="146" alt="image" src="https://github.com/user-attachments/assets/8624ba8d-9107-4a86-b000-6acf61707aa4" />
<img width="1479" height="757" alt="image" src="https://github.com/user-attachments/assets/1fae0cb2-419f-42ce-9fed-67a2b5ad99d7" />

### 3.3. ***Ejecutar el script para levantar la máquina***

Ejecutamos el siguiente comando para desplegar la máquina Vacaciones de Dockerlabs:

```bash
sudo ./auto_deploy.sh vacaciones.tar
```

<img width="850" height="312" alt="image" src="https://github.com/user-attachments/assets/cd071061-7968-45da-bcf4-d46f335d7efb" /><br>
> No nos muestra la ip ya que podemos acceder desde la máquina anfitriona.

- Comprobamos que se ha desplegado el contenedor correctamente. Para ello, ejecutamos el siguiente comando:

```bash
docker ps
```

<img width="1479" height="257" alt="image" src="https://github.com/user-attachments/assets/63f8fa8c-d954-4f8c-af49-9ee25777cd4a" />

---
## 4. ***Reconocimiento y Análisis de Vulnerabilidades***



---
## 5. ***Explotación de Vulnerabilidades***



---
## 6. ***Medidas de Mitigación y Buenas Prácticas***



---
## 7. ***Conclusiones***

