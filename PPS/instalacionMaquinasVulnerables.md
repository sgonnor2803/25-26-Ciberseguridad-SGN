
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
6. ***[Escalada de Privilegios](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#6-escalada-de-privilegios)***
7. ***[Medidas de Mitigación y Buenas Prácticas](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#7-medidas-de-mitigaci%C3%B3n-y-buenas-pr%C3%A1cticas)***
8. ***[Comparativa del análisis manual vs. análisis con Hexstrike MCP](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#8-comparativa-del-an%C3%A1lisis-manual-vs-an%C3%A1lisis-con-hexstrike-mcp)***
9. ***[Conclusiones](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/instalacionMaquinasVulnerables.md#9-conclusiones)***

---
## 1. ***Introducción***

En este proyecto vamos a usar ***WSL*** junto con ***Kali Linux*** para crear un entorno desde el que poder lanzar herramientas de análisis y trabajar con contenedores cómodamente desde Windows.

Una vez preparado el entorno, desplegaremos una ***máquina vulnerable de DockerLabs***. Sobre ella haremos un proceso básico de reconocimiento, análisis y explotación de vulnerabilidades para entender cómo se detectan los fallos y, después, cómo se podrían mitigar aplicando buenas prácticas.

---
## 2. ***Preparación del Entorno***

En este apartado se configura WSL para poder acceder correctamente a los servicios que se ejecuten dentro de los contenedores, y después se accede a Kali Linux para trabajar desde allí.

---
### 2.1. ***Configuración de red en WSL***
---

Para que los puertos de los contenedores sean accesibles desde Windows como si fueran localhost, es necesario ajustar la red de WSL.

- Primero, accedemos a ***WSL Settings*** desde Windows:

<img width="1332" height="697" alt="image" src="https://github.com/user-attachments/assets/fc78865d-324c-4026-89e4-97d13588d259" />

- Luego, nos ubicamos en el apartado ***Funciones de red***, y en la primera opción cambiamos el modo de red a ***Mirrored*** y en la segunda opción ***deshabilitamos el firewall de WSL***:

<img width="1335" height="696" alt="image" src="https://github.com/user-attachments/assets/3ba9ddaf-0db3-44d0-a459-238080733b60" />

Con esto, cualquier servicio levantado en Kali bajo WSL será accesible desde el navegador o terminal de Windows usando localhost.

---
### 2.2. ***Acceder a Kali Linux en WSL***
---

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

---
### 3.1. ***Descargar la máquina vulnerable desde DockerLabs***
---

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

---
### 3.2. ***Modificación del archivo auto_deploy.sh***
---

- Una vez tenemos los archivos, vamos a modificar el script ***auto_deploy.sh*** para que los puertos y servicios de la máquina docker se puedan acceder desde la máquina kali linux de WSL. Para ello, vamos ejecutar este comando y modificaremos la siguiente línea:

```bash
nano auto_deploy.sh

# Línea ha modificar
docker run -d --network host --name $CONTAINER_NAME $IMAGE_NAME > /dev/null
```

<img width="821" height="146" alt="image" src="https://github.com/user-attachments/assets/8624ba8d-9107-4a86-b000-6acf61707aa4" />
<img width="1479" height="757" alt="image" src="https://github.com/user-attachments/assets/1fae0cb2-419f-42ce-9fed-67a2b5ad99d7" />

---
### 3.3. ***Ejecutar el script para levantar la máquina***
---

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

En este apartado se realiza el reconocimiento inicial de la máquina vulnerable desplegada. El objetivo es identificar los servicios que tiene abiertos, sus versiones y posibles puntos débiles sobre los que profundizar más adelante.

Esta es la ip que nos ha dado al desplegar la máquina:

<img width="555" height="254" alt="image" src="https://github.com/user-attachments/assets/77bb00d2-e841-4b7b-95c4-4ca2f3e0476d" />

---
### 4.1. ***Comprobación de conexión***
---

Desde kali, ejecutamos el siguiente comando con la herramienta ping, que permite comprobar si tenemos tanto acceso como si responde:

```bash
ping -c 2 172.17.0.2
```

<img width="563" height="301" alt="image" src="https://github.com/user-attachments/assets/1fa1a9a9-cfcd-4feb-987e-b9bfce037a46" />

---
### 4.2. ***Escaneo de puertos con Nmap***
---

El primer paso de cualquier análisis es descubrir qué puertos y servicios están activos, descubriendo sus versiones. Para ello, ejecutamos el siguiente comando:

```bash
nmap -p- -sVC --min-rate 5000 -n -Pn 172.17.0.2
```

<img width="794" height="467" alt="image" src="https://github.com/user-attachments/assets/06d8159a-5e7c-4cd4-934a-d830fe32d470" /><br>

***Descripción del comando:***
- ***-p- →*** escanea todos los puertos (1 al 65535)
- ***-sV →*** intenta identificar la versión de los servicios encontrados
- ***-sC →*** ejecuta los scripts básicos de reconocimiento de Nmap
- ***--min-rate 5000 →*** acelera el envío de paquetes para que el escaneo tarde menos
- ***-n →*** sin resolución DNS
- ***-Pn →*** desactiva el ping inicial (trata al host como si estuviera activo)
- ***172.17.0.2 →*** IP de la máquina vulnerable dentro de Docker

***Puertos encontrados:***

- ***22/tcp — SSH***
  - ***Servicio:*** OpenSSH 7.6p1
  - ***Sistema:*** Ubuntu
  - Es un servicio habitual para administración remota.

- ***80/tcp — HTTP***
  - ***Servicio:*** Apache 2.4.29
  - ***Sistema:*** Ubuntu
  - Puede indicar la presencia de un sitio web sencillo o en desarrollo.

---
### 4.3. ***Enumeración del servicio web***
---


### 4.3.1. ***Análisis con WhatWeb***
---

Para analizar el servicio HTTP que se ejecuta en el puerto ***80***, se utilizó la herramienta ***WhatWeb***, que permite identificar tecnologías, versiones y otros metadatos del servidor.

Para ello, ejecutamos el siguiente comando:

```bash
whatweb http://172.17.0.2
```

<img width="956" height="218" alt="image" src="https://github.com/user-attachments/assets/27e9a59b-6a64-4c91-b12c-1a8b79ccd02f" />

***Resultados obtenidos:***
- ***Servidor web:*** Apache 2.4.29
- ***Sistema operativo:*** Ubuntu Linux
- ***Respuesta HTTP:*** 200 OK
- ***Dirección IP interna:*** 172.17.0.2

Estos datos confirman que el servidor está funcionando correctamente y utiliza versiones relativamente antiguas.

---
### 4.3.2. ***Revisión manual del sitio web***
---

Al acceder desde el navegador a http://172.17.0.2, la página muestra únicamente un comentario HTML:

```bash
<!-- De : Juan Para: Camilo , te he dejado un correo es importante... -->
```

<img width="952" height="244" alt="image" src="https://github.com/user-attachments/assets/c91d77c1-5f2e-4b87-84ab-26c392e74fab" />

Aunque a simple vista parece una página vacía, el comentario revela información sensible:
- Se mencionan dos nombres de usuarios: Juan y Camilo.
- Es probable que Camilo sea un usuario real del sistema.
- Esta información puede resultar útil para posteriores fases de acceso o autenticación (por ejemplo, en el servicio SSH del puerto 22).

---
## 5. ***Explotación de Vulnerabilidades***

En esta fase el objetivo es conseguir acceso a la máquina usando la información que ya habíamos encontrado. Mientras revisábamos el servicio web vimos un comentario HTML que mencionaba a un usuario:

```bash
<!-- De : Juan Para: Camilo , te he dejado un correo es importante... -->
```

Esto nos dio una pista evidente: ***Camilo*** podría ser un usuario del sistema.
Además, como el puerto ***22 (SSH)*** estaba abierto, tenía sentido intentar un ataque de fuerza bruta para ver si su contraseña era débil.

---
### 5.1. ***Ataque de fuerza bruta con Hydra***
---

Para probar contraseñas utilicé ***Hydra***, que permite automatizar ataques de diccionario sobre servicios como SSH.

Comando usado:

```bash
hydra -l camilo -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```

***Qué significa:***
- ***-l camilo →*** el usuario que queremos probar
- ***-P rockyou.txt →*** diccionario con miles de contraseñas
- ***ssh://172.17.0.2 →*** objetivo del ataque (el SSH de la máquina)

Hydra finalmente encontró la contraseña correcta:

<img width="1726" height="372" alt="image" src="https://github.com/user-attachments/assets/1bb56f04-41c8-4e4d-a35d-e361545cf465" />

---
### 5.2. ***Ataque de fuerza bruta con Hydra***
---

Con el usuario y la contraseña ya confirmados, solo debemos de conectarnos mediante SSH. Para ello, ejecutamos el siguiente comando:

```bash
ssh camilo@172.17.0.2
```

<img width="810" height="342" alt="image" src="https://github.com/user-attachments/assets/1e0def6f-4a26-4cfd-9752-dda3e68fa48d" /><br>

Y efectivamente, estamos logueados como camilo y ya tenemos acceso inicial al sistema.

---
## 6. ***Escalada de Privilegios***

Una vez dentro del sistema como el usuario camilo, el siguiente paso fue intentar conseguir más privilegios hasta llegar a root. Para ello fui revisando el sistema y encontré una pista clave.

---
### 6.1. ***Descubrimiento de credenciales de otro usuario***
---

Durante la enumeración interna localicé un archivo de correo en:

```bash
/var/mail/camilo/correo.txt
```

<img width="1118" height="220" alt="image" src="https://github.com/user-attachments/assets/f1751004-94ea-4ded-a15b-91d18ef9fed7" />

Dentro del mensaje, Juan le había dejado a Camilo su contraseña, que resultó ser ***2k84dicb***.

Esto nos permite cambiar de usuario, de camilo hacia el usuario juan:

```bash
su juan
```

<img width="406" height="184" alt="image" src="https://github.com/user-attachments/assets/0849a74c-cbe8-41a5-8a43-fa4c54f08dc3" />

---
### 6.2. ***Comprobación de privilegios con sudo***
---

Ya como juan, revisé qué permisos especiales tenía:

```bash
sudo -l
```

<img width="1064" height="203" alt="image" src="https://github.com/user-attachments/assets/8510fe1f-65e9-45e5-93ee-380af4a959a9" />

Esto quiere decir que Juan puede ejecutar ruby como root sin necesidad de contraseña.
Esto es un vector de escalada bastante claro.

Consultando GTFObins (una referencia de técnicas de escalada usando binarios del sistema), encontré que ruby permite abrir una shell con permisos elevados.

El comando recomendado es:

```bash
sudo ruby -e 'exec "/bin/bash"'
```

<img width="1082" height="161" alt="image" src="https://github.com/user-attachments/assets/f86bb368-7bb3-4178-8fd4-62500918ff18" />

En este punto ya tenemos control total sobre la máquina y podemos realizar cualquier acción con permisos máximos.

---
## 7. ***Medidas de Mitigación y Buenas Prácticas***

Después de analizar y explotar la máquina, se pueden sacar varias mejoras importantes para evitar que este tipo de ataques funcionen en un entorno real. Aquí están las principales medidas que deberían aplicarse:

---
### 7.1. ***Proteger el servicio SSH***
---

- ***Deshabilitar el acceso SSH a usuarios sin necesidad real.***
En este caso, camilo tenía acceso cuando no parece ser imprescindible.

- ***Usar contraseñas fuertes o, mejor todavía, claves SSH.***
Hydra consiguió romper la contraseña porque el sistema permitía autenticación por contraseña simple.

- ***Limitar intentos de login.***
Configurar Fail2Ban o ajustes de sshd_config para evitar ataques de fuerza bruta.

---
### 7.2. ***Evitar filtraciones de información en servicios web***
---

- No dejar ***comentarios HTML con información sensible***, como nombres de usuarios o mensajes internos.

- Revisar el contenido expuesto y eliminar todo lo que no sea necesario para el funcionamiento de la página.

---
### 7.3. ***Gestionar correctamente el correo interno***
---

- No enviar contraseñas por correo en texto plano.
En el sistema, la contraseña de Juan estaba en un archivo accesible por otros usuarios.

- Si se usa correo interno, limitar los permisos y limpiar mensajes antiguos.

---
### 7.4. ***Revisar privilegios sudo***
---

- Evitar dar permisos sudo sin contraseña a usuarios normales.
Aquí, Juan podía ejecutar ruby como root sin ningún tipo de control.

- Usar sudo -l de forma periódica para revisar permisos peligrosos.

---
### 7.5. ***Revisar privilegios sudo***
---

Algunos binarios como ruby, python, perl, awk, etc., pueden abrir shells si se ejecutan como root.
Si es necesario permitirlos con sudo, añadir restricciones usando secure_path, noexec, o reglas tipo sudoers más específicas.

---
### 7.6. ***Actualizar servicios***
---

Apache 2.4.29 y OpenSSH 7.6p1 son versiones antiguas.
Mantener los servicios al día reduce vulnerabilidades conocidas.

---
### 7.7. ***Segregar usuarios y permisos***
---

- Un usuario no debería poder leer el correo de otro.
- Revisar permisos de archivos sensibles y carpetas de sistema.

## 8. ***Comparativa del análisis manual vs. análisis con Hexstrike MCP***

Después de hacer el escaneo manual a la máquina 172.17.0.2, se volvió a repetir todo pero usando el MCP Hexstrike desde Gemini. La diferencia es clara: a mano toca ir comando por comando (nmap, nikto, gobuster, hydra…), interpretar la salida y montar conclusiones. Con Hexstrike, la IA lo hace todo seguida y te devuelve un informe ya ordenado.

Hexstrike encontró lo mismo que en el análisis manual: Apache viejo, cabeceras de seguridad que faltan, la fuga de los usuarios juan y camilo en el HTML, y que la mejor forma de entrar sería un ataque de fuerza bruta al SSH. Básicamente, llega a las mismas conclusiones, pero mucho más rápido y sin tener que ir comprobando cada herramienta una por una.

<img width="1919" height="1045" alt="image" src="https://github.com/user-attachments/assets/16d47c22-09df-4b07-99ba-55cdc4e97857" />

En resumen: manual = lento pero controlado. Hexstrike = rápido y te da la película completa sin pelearte con los comandos.

---
## 9. ***Conclusiones***

El uso de WSL junto con Kali Linux ha permitido trabajar con la máquina vulnerable de forma sencilla y práctica, ofreciendo un entorno cómodo para realizar todas las pruebas sin configuraciones complejas.

Durante el análisis se comprobó cómo varios errores básicos, como un usuario expuesto en la web, una contraseña débil en SSH, credenciales guardadas en texto plano y permisos sudo mal configurados, pueden encadenarse y facilitar que un atacante obtenga acceso completo al sistema.

En conclusión, esta práctica demuestra la importancia de revisar la configuración de los servicios y aplicar medidas de seguridad básicas para evitar que fallos simples terminen comprometiendo toda la máquina.
