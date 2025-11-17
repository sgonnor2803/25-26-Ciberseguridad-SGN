<h1 align="center">Proyecto 2.3 - Incident Investigation</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/bannerPortada.png)

***Fecha:*** 11 de noviembre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Introducción](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-3.md#1-introducci%C3%B3n)***
2. ***[Metodología del análisis forense](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-3.md#2-metodolog%C3%ADa-del-an%C3%A1lisis-forense)***
3. ***[Evidencias obtenidas](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-3.md#3-evidencias-obtenidas)***
4. ***[Hallazgos principales del incidente](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-3.md#4-hallazgos-principales-del-incidente)***
5. ***[Conclusión](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/Proyecto2-3.md#5-conclusi%C3%B3n)***

---
## 1. ***Introducción***

En este informe se recoge todo el proceso de análisis forense realizado sobre la máquina comprometida del proyecto. El objetivo es entender qué ocurrió, qué vulnerabilidad se explotó, qué dejó el atacante dentro del sistema y qué evidencias soportan cada una de las conclusiones.

Durante la investigación se han revisado los distintos tipos de evidencias: memoria RAM, triaje del sistema y la imagen completa del disco. Con todo ello, se ha podido reconstruir el ataque, identificar la vulnerabilidad utilizada y detectar los artefactos maliciosos que quedaron activos tras la intrusión.

El documento incluye tanto la parte técnica del análisis como una visión más general del incidente, y al final se añaden los hallazgos bien organizados en un anexo para poder consultarlos de forma rápida.

---
## 2. ***Metodología del análisis forense***

En este proyecto se sigue la misma línea de trabajo que en el ejercicio anterior, tomando como referencia las fases definidas por las normas ISO 27037, 27041, 27042 y 27043. El objetivo es obtener todas las evidencias sin modificar la máquina comprometida y conservar la cadena de custodia en todo momento.

Primero se prepara el entorno y se define qué evidencias deben extraerse: la memoria RAM, el triaje inicial y la imagen del disco. Para evitar cambios en el sistema, la extracción se realiza desde el host y no desde la propia máquina analizada.

Una vez recopiladas, las evidencias se separan y se registran con sus fechas y hashes para asegurar su integridad. Todo el análisis posterior se realiza únicamente sobre copias de trabajo, manteniendo una documentación ordenada y coherente con la metodología usada en el proyecto previo.

---
## 3. ***Evidencias obtenidas***

Durante el análisis reuní tres bloques principales de evidencias: la memoria RAM, el triaje del sistema y la imagen completa del disco. Cada una se obtuvo siguiendo el procedimiento forense para no modificar la máquina original y siempre trabajando sobre copias.

### 3.1. ***Memoria RAM***

Se extrajo usando la herramienta dumpvmcore de VirtualBox, que permite sacar el volcado directamente desde el host. Con esto conseguí un fichero .raw con el contenido completo de la RAM en el momento de la captura.
Esta evidencia es importante porque normalmente es donde aparece el malware en ejecución, procesos sospechosos o restos del exploit.

### 3.2. ***Triaje del sistema***

Para el triaje se encendió la máquina pero únicamente se usaron comandos de solo lectura (tasklist, netstat, ipconfig, systeminfo, etc.). Toda la información se guardó en una carpeta compartida para evitar escribir en el disco original.
En este grupo de evidencias fue donde apareció el proceso raro (KzcmVNSNkYkueQf.exe) y donde también recogí información sobre la red y el sistema.

### 3.3. ***Imagen del disco***

La copia del disco se obtuvo convirtiendo el archivo .vmdk original a .raw usando qemu-img. Esta imagen sirve para revisar archivos eliminados, configuraciones antiguas, restos de herramientas y cualquier rastro permanente dejado en el sistema.
Dentro de esta evidencia fue donde encontré el script crea_user.py, que prácticamente confirma la explotación del servidor Easy File Sharing.

Todas las evidencias se guardaron con sus hashes, fechas y responsable, de forma organizada, y siempre manteniendo la estructura necesaria para consultarlas de manera independiente en el análisis posterior.

---
## 4. ***Hallazgos principales del incidente***

A continuación se recogen los hallazgos más relevantes encontrados durante el análisis:

### 4.1. ***Script malicioso (crea_user.py)***

#### Ruta encontrada:
#### C:\Users\Usuario\Desktop\crea_user.py

Este script es el exploit clave del ataque. Es un código público conocido que explota un Buffer Overflow en Easy File Sharing Web Server 7.2 mediante una petición malformada al endpoint /sendemail.ghp.
Dentro del script aparece un payload generado con msfvenom, lo que indica uso directo de Metasploit para crear un usuario nuevo en el sistema. Es la prueba más clara de que la máquina fue explotada con este CVE.

<img width="1563" height="874" alt="image" src="https://github.com/user-attachments/assets/eadb4266-ee98-4ec4-8187-047c5fb69b84" />

### 4.2. ***Proceso sospechoso ejecutándose***

Dentro del listado de procesos aparece un ejecutable con nombre aleatorio:

- ***KzcmVNSNkYkueQf.exe***
- ***PID 2640***

Este archivo no pertenece a Windows ni a ninguna aplicación legítima. Los nombres aleatorios así suelen indicar actividad maliciosa o un payload dejado tras la explotación. Su presencia confirma que, después de usar el exploit, se ejecutó código propio del atacante.

<img width="998" height="590" alt="image" src="https://github.com/user-attachments/assets/9f8d489a-fb65-4eb7-8f1d-06b2d030d9d7" />

### 4.3. ***Eventos de autenticación anómalos***

Se detectan numerosos eventos 4624 (logon exitoso) seguidos de 4672 (asignación de privilegios especiales). Este patrón suele aparecer cuando se explota un servicio y se obtiene ejecución con permisos elevados. Los eventos repetidos en muy poco tiempo sugieren actividad automática, no un comportamiento normal del usuario.

<img width="735" height="356" alt="image" src="https://github.com/user-attachments/assets/e1aef76e-d4ed-4010-902d-a8e56c012c77" />

### 4.4. ***Log del activador KMS (KMSpico)***

Dentro del sistema apareció un log generado por KMSpico/KMS Tools. En él se ve cómo el activador abre el puerto 1688, modifica reglas del firewall, cambia valores del registro y activa Windows mediante un KMS Emulator local.

Este archivo demuestra que la máquina ya tenía software pirata que modifica servicios del sistema, lo cual aumenta la superficie de ataque y puede haber facilitado que el atacante encontrase la máquina en mal estado de seguridad.

<img width="1563" height="797" alt="image" src="https://github.com/user-attachments/assets/273433da-48a2-464b-a1b1-e4a567d48803" />

### 4.5. ***Usuario creado por el atacante***

- Usuario: ***ihacklabs***
- Contraseña: ***Ihack12/***

El propio shellcode del exploit crea un usuario nuevo en el sistema con privilegios administrativos. Esto confirma que, después de explotar la vulnerabilidad, el atacante buscó persistencia inmediata dentro del sistema.

---
## 5. ***Conclusión***

El análisis forense permitió reconstruir el incidente de forma bastante clara. La máquina fue comprometida explotando una vulnerabilidad conocida en Easy File Sharing Web Server 7.2, y el script crea_user.py encontrado en el disco lo confirma directamente. Tras aprovechar ese fallo, el atacante dejó un ejecutable con nombre aleatorio en ejecución y creó un usuario nuevo para mantener acceso al sistema.

Además del ataque en sí, aparecieron rastros de un activador KMS instalado previamente. Aunque no está relacionado directamente con la intrusión, sí demuestra que el sistema ya tenía cambios no oficiales y menos medidas de seguridad de lo habitual, lo que siempre facilita que un atacante pueda trabajar con más libertad.

En conjunto, las evidencias obtenidas muestran que el ataque tuvo éxito debido a la vulnerabilidad del servicio expuesto y a la falta de medidas de protección en la máquina.
