<h1 align="center">Proyecto 2.1: Incident Investigation</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/bannerPortada.png)

***Fecha:*** 11 de noviembre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Introducción]()***
2. ***[Metodología Forense Aplicada]()***
3. ***[Recolección de Evidencias]()***
4. ***[Descripción de las Evidencias]()***
5. ***[Cadena de Custodia]()***
6. ***[Almacenamiento de las Evidencias]()***
7. ***[Conclusiones]()***

---
## 1. ***Introducción***

En este informe se explica cómo se han obtenido las evidencias necesarias de la máquina comprometida proporcionada para el ejercicio, siguiendo una metodología básica de análisis forense y evitando modificar el sistema. Para la investigación se han obtenido tres elementos principales: la memoria RAM mediante una snapshot, un triaje con información esencial del estado de la máquina y una copia del disco para su análisis posterior. En las siguientes secciones se detalla cómo se han recogido, descrito y almacenado estas evidencias manteniendo la cadena de custodia.

---
## 2. ***Metodología Forense Aplicada***

Para este proyecto se ha seguido la misma metodología que usamos en el trabajo anterior, basada en las fases de las normas ISO 27037, 27041, 27042 y 27043. El objetivo ha sido obtener todas las evidencias sin modificar la máquina comprometida y manteniendo la cadena de custodia durante todo el proceso.

Primero se definió el alcance y se preparó el entorno de trabajo. Después se creó una snapshot en caliente, ya que esta nos permite capturar el estado de la máquina en ese momento y extraer de ahí la memoria RAM sin ejecutar nada dentro del sistema. También se generó una copia del disco convirtiendo el archivo VMDK a un formato que pudiéramos analizar sin riesgo de modificarlo. Para el triaje se arrancó la máquina y solo se usaron comandos nativos en modo lectura (tasklist, netstat, ipconfig…), guardando toda la salida en un soporte externo para no tocar el disco original. Todas las evidencias se trabajaron siempre sobre copias para asegurar que los archivos originales no se alteraban.

Una vez recogidas, las evidencias se almacenaron por separado registrando fechas, responsables y los hashes correspondientes. El análisis se realiza únicamente sobre las copias de trabajo, y todo el proceso se ha documentado para mantener una metodología coherente con la que ya utilizamos en el proyecto anterior.

---
## 3. ***Recolección de Evidencias***



---
## 4. ***Descripción de las Evidencias***



---
## 5. ***Cadena de Custodia***



---
## 6. ***Almacenamiento de las Evidencias***



---
## 7. ***Conclusiones***

