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

Para el triaje se encendió la máquina y solo se usaron comandos nativos y de lectura, como tasklist, netstat, ipconfig o systeminfo. Toda la información se guardó en un medio externo para no escribir nada en el disco comprometido. Esto permitió ver de forma rápida qué procesos, conexiones y configuraciones tenía el sistema.



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

