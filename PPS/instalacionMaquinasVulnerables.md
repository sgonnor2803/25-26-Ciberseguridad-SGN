<h1 align="center">Instalación de máquinas vulnerables: dockerlabs.es</h1>

![imagen portada infraestructura](https://github.com/IES-Rafael-Alberti/25-26-Ciberseguridad-Grupo-5/blob/main/PPS/images/portadainfraestructura.png)

***Fecha:*** 27 de noviembre de 2025
<br>***Autor***: Sergio González

---
## Índice

1. ***[Introducción]()***
2. ***[Preparación del Entorno]()***
3. ***[Despliegue de la Máquina Vulnerable]()***
4. ***[Reconocimiento y Análisis de Vulnerabilidades]()***
5. ***[Explotación de Vulnerabilidades]()***
6. ***[Medidas de Mitigación y Buenas Prácticas]()***
7. ***[Conclusiones]()***

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

- Luego, nos ubicamos en el apartado ***Funciones de red***, y en la primera opción cambiamos el modo de red a ***Mirrored***:

<img width="1335" height="696" alt="image" src="https://github.com/user-attachments/assets/3ba9ddaf-0db3-44d0-a459-238080733b60" />

Con esto, cualquier servicio levantado en Kali bajo WSL será accesible desde el navegador o terminal de Windows usando localhost.

---
## 3. ***Despliegue de la Máquina Vulnerable***



---
## 4. ***Reconocimiento y Análisis de Vulnerabilidades***



---
## 5. ***Explotación de Vulnerabilidades***



---
## 6. ***Medidas de Mitigación y Buenas Prácticas***



---
## 7. ***Conclusiones***

