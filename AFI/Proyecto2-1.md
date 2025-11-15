<h1 align="center">Proyecto 2.1 - Incident Investigation</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/bannerPortada.png)

***Fecha:*** 11 de noviembre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Introducción](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-1.md#1-introducci%C3%B3n)***
2. ***[Metodología Forense Aplicada](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-1.md#2-metodolog%C3%ADa-forense-aplicada)***
3. ***[Recolección de Evidencias](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-1.md#3-recolecci%C3%B3n-de-evidencias)***
4. ***[Descripción de las Evidencias](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-1.md#4-descripci%C3%B3n-de-las-evidencias)***
5. ***[Cadena de Custodia](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-1.md#5-cadena-de-custodia)***
6. ***[Almacenamiento de las Evidencias](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-1.md#6-almacenamiento-de-las-evidencias)***
7. ***[Conclusiones](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-1.md#7-conclusiones)***

---
## 1. ***Introducción***

En este informe se explica cómo se han obtenido las evidencias necesarias de la máquina comprometida proporcionada para el ejercicio, siguiendo una metodología básica de análisis forense y evitando modificar el sistema. Para la investigación se han obtenido tres elementos principales: la memoria RAM utilizando la función dumpvmcore de VirtualBox, un triaje con información esencial del estado de la máquina y una copia del disco para su análisis posterior. En las siguientes secciones se detalla cómo se han recogido, descrito y almacenado estas evidencias manteniendo la cadena de custodia.

---
## 2. ***Metodología Forense Aplicada***

Para este proyecto se ha seguido la misma metodología que en el trabajo anterior, basada en las fases de las normas ISO 27037, 27041, 27042 y 27043. El objetivo ha sido obtener todas las evidencias sin modificar la máquina comprometida y mantener la cadena de custodia durante todo el proceso.

Primero se definió el alcance y se preparó el entorno de trabajo. Para la memoria RAM se utilizó la función dumpvmcore de VirtualBox, que permite extraer un volcado completo desde el host sin ejecutar herramientas dentro del sistema. También se generó una copia del disco convirtiendo el archivo VMDK a un formato seguro para su análisis. Para el triaje se arrancó la máquina y únicamente se ejecutaron comandos nativos en modo lectura (tasklist, netstat, ipconfig…), guardando toda la salida en un soporte externo para evitar cualquier modificación del disco original. Todas las evidencias se trabajaron siempre sobre copias para asegurar que los archivos originales no se alterasen.

Una vez recogidas, las evidencias se almacenaron por separado registrando fechas, responsables y los hashes correspondientes. El análisis se realiza únicamente sobre las copias de trabajo, y todo el proceso se ha documentado para mantener una metodología coherente con la que ya utilizamos en el proyecto anterior.

---
## 3. ***Recolección de Evidencias***

Para recoger las evidencias de la máquina comprometida se siguió un proceso simple y ordenado, intentando no modificar nada del sistema original. La recolección se basó en tres partes: la memoria RAM, el triaje y el disco.

---
### 3.1. ***Memoria RAM***
---

La memoria se obtuvo utilizando la función dumpvmcore de VirtualBox, que permite extraer un volcado completo de la RAM de la máquina mientras está encendida. Este método genera un archivo .raw con el contenido íntegro de la memoria sin necesidad de ejecutar herramientas dentro del sistema, evitando así modificar la evidencia. El volcado se realizó desde el host y se guardó en un soporte externo para mantener la integridad del equipo analizado.

- Primero iniciamos la máquina para poder crear el volcado de la RAM.

<img width="1221" height="744" alt="Captura de pantalla 2025-11-15 103102" src="https://github.com/user-attachments/assets/9824d312-d8d1-43a2-8f86-188605547aa5" />

- Ahora, generamos el volcado de memoria ejecutando el siguiente comando, con la máquina virtual encendida (estando en la carpeta de evidencias):

```bash
"C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" debugvm "FORENSIC_10" dumpvmcore --filename memoria.raw
```

<img width="1466" height="206" alt="image" src="https://github.com/user-attachments/assets/5ddea789-4a3c-41e4-9f1f-be26debb293c" />

<img width="1045" height="274" alt="image" src="https://github.com/user-attachments/assets/b51c8717-3632-408a-a5f5-0110464012ea" /><br>
> Esto generó un archivo llamado memoria.raw con todo el contenido de la RAM.

- Por último, calculamos los hashes del archivo para asegurarnos de su integridad y guardamos la evidencia en su carpeta correspondiente dentro de la cadena de custodia, junto con la fecha, quién la recogió, etc...

```bash
Get-FileHash memoria.raw -Algorithm MD5 | Out-File hashes_memoria.txt -Append
Get-FileHash memoria.raw -Algorithm SHA256 | Out-File hashes_memoria.txt -Append
Get-FileHash memoria.raw -Algorithm SHA1 | Out-File hashes_memoria.txt -Append
```

<img width="1473" height="516" alt="image" src="https://github.com/user-attachments/assets/8fa65bea-4a04-4df2-a2bb-7ec02c3f24b6" />

Los hashes obtenidos se guardaron en un archivo ***hashes_memoria.txt*** para tener un registro claro dentro de la cadena de custodia y poder comprobar la integridad de la evidencia en cualquier momento.

---
### 3.2. ***Triaje***
---

Para el triaje se arrancó la máquina comprometida, pero solo para obtener información básica del sistema sin modificar nada. No se instaló ninguna herramienta ni se ejecutaron programas externos; solo se usaron comandos nativos de Windows que funcionan en modo lectura.

Los comandos que se utilizaron fueron:

- ***tasklist -->*** para ver procesos activos
- ***netstat -nao -->*** conexiones de red y puertos
- ***ipconfig /all -->*** información de red
- ***systeminfo -->*** información general del sistema
- ***dir /s en rutas clave -->*** estructura de archivos
- ***wmic useraccount get name,sid -->*** usuarios del sistema

Cada comando se ejecutó redirigiendo la salida a una memoria USB o carpeta externa.

- Primero, montamos la carpeta compartida en la máquina virtual. Para ello, ejecutamos el siguiente comando:

```bash
net use Z: \\DESKTOP-F44P71J\Evidencias_FORENSIC_10
```

<img width="798" height="707" alt="image" src="https://github.com/user-attachments/assets/05e2338f-08ce-4f5f-9d2d-5db5bd3cd6fe" /><br>
> En esta imagen, nos muestra como se ha montado correctamente el dispositivo en local, mediante las credenciales del host remoto.

<img width="800" height="704" alt="image" src="https://github.com/user-attachments/assets/c82850bc-d1d4-4644-8c7b-4387c2403266" />

- Ahora, ya podemos empezar a recopilar toda la información de la máquina. Vamos a empezar por la captura de los procesos activos:

```bash
tasklist > Z:\tasklist.txt
```

<img width="801" height="253" alt="image" src="https://github.com/user-attachments/assets/9b24e57f-1d7f-4d42-9f93-b4bc1ce7122c" />
<img width="1001" height="589" alt="image" src="https://github.com/user-attachments/assets/4383df1a-9965-4185-afcc-2c09f9266c4a" />

Y calculamos los hashes para la integridad de este archivos:

```bash
Get-FileHash tasklist.txt -Algorithm MD5 | Out-File hashes_tasklist.txt -Append
Get-FileHash tasklist.txt -Algorithm SHA256 | Out-File hashes_tasklist.txt -Append
Get-FileHash tasklist.txt -Algorithm SHA1 | Out-File hashes_tasklist.txt -Append
```

<img width="1279" height="516" alt="image" src="https://github.com/user-attachments/assets/8f4de245-715a-49a1-926a-9a025eecb9ba" />

- Capturamos la información de las conexiones de red y puertos:

```bash
netstat -nao > Z:\netstat.txt
```

<img width="800" height="284" alt="image" src="https://github.com/user-attachments/assets/c54febfc-286e-4a77-93df-cfd8ee0528f2" />
<img width="1001" height="587" alt="image" src="https://github.com/user-attachments/assets/d43be08b-2402-43a8-a519-240919361f37" />

Y calculamos los hashes para la integridad de este archivos:

```bash
Get-FileHash netstat.txt -Algorithm MD5 | Out-File hashes_netstat.txt -Append
Get-FileHash netstat.txt -Algorithm SHA256 | Out-File hashes_netstat.txt -Append
Get-FileHash netstat.txt -Algorithm SHA1 | Out-File hashes_netstat.txt -Append
```

<img width="1274" height="509" alt="image" src="https://github.com/user-attachments/assets/7965340a-86c1-4b0d-b275-84ecccf6ec3b" />

- Capturamos la información de la red:

```bash
ipconfig /all > Z:\ipconfig.txt
```

<img width="798" height="287" alt="image" src="https://github.com/user-attachments/assets/1166e457-5339-485d-b50c-db883fd22f30" />
<img width="998" height="590" alt="image" src="https://github.com/user-attachments/assets/0045ede2-4112-4e89-9011-d715ffce3022" />

Y calculamos los hashes para la integridad de este archivos:

```bash
Get-FileHash ipconfig.txt -Algorithm MD5 | Out-File hashes_ipconfig.txt -Append
Get-FileHash ipconfig.txt -Algorithm SHA256 | Out-File hashes_ipconfig.txt -Append
Get-FileHash ipconfig.txt -Algorithm SHA1 | Out-File hashes_ipconfig.txt -Append
```

<img width="1278" height="516" alt="image" src="https://github.com/user-attachments/assets/00cb41e7-a896-4712-81c7-e01dea0f8eb0" />

- Capturamos la información general del sistema:

```bash
systeminfo > Z:\systeminfo.txt
```

<img width="799" height="273" alt="image" src="https://github.com/user-attachments/assets/98aaa333-e353-496f-90c3-3206aa370411" />
<img width="1000" height="587" alt="image" src="https://github.com/user-attachments/assets/4dc1688d-48fb-42cd-badc-977fa291f622" />

Y calculamos los hashes para la integridad de este archivos:

```bash
Get-FileHash systeminfo.txt -Algorithm MD5 | Out-File hashes_systeminfo.txt -Append
Get-FileHash systeminfo.txt -Algorithm SHA256 | Out-File hashes_systeminfo.txt -Append
Get-FileHash systeminfo.txt -Algorithm SHA1 | Out-File hashes_systeminfo.txt -Append
```

<img width="1277" height="519" alt="image" src="https://github.com/user-attachments/assets/7411a496-ee9d-46d7-88b1-90e1752c054d" />

- Capturamos la información de las estructuras claves como las siguientes carpetas:
  - Carpeta del usuario comprometido:

```bash
dir "C:\Users\Administrador" /s > Z:\dir_users.txt
```

<img width="801" height="274" alt="image" src="https://github.com/user-attachments/assets/8ac89b77-2230-4316-b93d-701bc48398c2" />
<img width="1001" height="588" alt="image" src="https://github.com/user-attachments/assets/a3641e48-bd9b-4996-b07b-b53312d783e7" />

Y calculamos los hashes para la integridad de este archivos:

```bash
Get-FileHash dir_users.txt -Algorithm MD5 | Out-File hashes_dir_users.txt -Append
Get-FileHash dir_users.txt -Algorithm SHA256 | Out-File hashes_dir_users.txt -Append
Get-FileHash dir_users.txt -Algorithm SHA1 | Out-File hashes_dir_users.txt -Append
```

<img width="1273" height="521" alt="image" src="https://github.com/user-attachments/assets/705f54e7-663d-4a94-bfa6-f58cb021de05" />

  - Carpetas Program Files y Program Files (x86):

```bash
dir "C:\Program Files" /s > Z:\dir_programfiles.txt
dir "C:\Program Files (x86)" /s >> Z:\dir_programfiles.txt
```

<img width="801" height="299" alt="image" src="https://github.com/user-attachments/assets/8b9bffb7-a863-4601-a995-bbe11a235ab4" />
<img width="1000" height="587" alt="image" src="https://github.com/user-attachments/assets/4474dee0-95c9-4fe5-9fb1-1f4f9d68a74b" />

Y calculamos los hashes para la integridad de este archivos:

```bash
Get-FileHash dir_programfiles.txt -Algorithm MD5 | Out-File hashes_dir_programfiles.txt -Append
Get-FileHash dir_programfiles.txt -Algorithm SHA256 | Out-File hashes_dir_programfiles.txt -Append
Get-FileHash dir_programfiles.txt -Algorithm SHA1 | Out-File hashes_dir_programfiles.txt -Append
```

<img width="1409" height="531" alt="image" src="https://github.com/user-attachments/assets/65400616-bf63-4cfa-98ca-b00ee1ee43ff" />

  - Carpeta Inicio automático

```bash
dir "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup" /s > Z:\dir_startup.txt
```

<img width="800" height="272" alt="image" src="https://github.com/user-attachments/assets/ca01eaeb-c062-456a-b536-82d505a5820d" />
<img width="997" height="589" alt="image" src="https://github.com/user-attachments/assets/d3f40a5c-d6f7-4960-bb59-86db995962ce" />

Y calculamos los hashes para la integridad de este archivos:

```bash
Get-FileHash dir_startup.txt -Algorithm MD5 | Out-File hashes_dir_startup.txt -Append
Get-FileHash dir_startup.txt -Algorithm SHA256 | Out-File hashes_dir_startup.txt -Append
Get-FileHash dir_startup.txt -Algorithm SHA1 | Out-File hashes_dir_startup.txt -Append
```

<img width="1329" height="516" alt="image" src="https://github.com/user-attachments/assets/389d02c2-970a-4587-9f42-087af0c0e0d8" />

---
### 3.2. ***Disco de la máquina***
---

El disco se obtuvo usando el archivo VMDK incluido en la exportación de la máquina. Ese archivo se convirtió a un formato forense que se puede abrir con herramientas como FTK Imager. Todo se hizo desde el equipo host para evitar modificar el disco real de la máquina virtual.



---
## 4. ***Descripción de las Evidencias***



---
## 5. ***Cadena de Custodia***



---
## 6. ***Almacenamiento de las Evidencias***



---
## 7. ***Conclusiones***

