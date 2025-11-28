<h1 align="center">Herramientas MCP para análisis de vulnerabilidades</h1>

![imagen portada infraestructura](https://github.com/IES-Rafael-Alberti/25-26-Ciberseguridad-Grupo-5/blob/main/PPS/images/portadainfraestructura.png)

***Fecha:*** 25 de noviembre de 2025
<br>***Autor***: Sergio González

---
## Índice

1. ***[Introducción](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/HerramientasAnalisisVulnerabilidades.md#1-introducci%C3%B3n)***
2. ***[Preparación del entorno](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/HerramientasAnalisisVulnerabilidades.md#2-preparaci%C3%B3n-del-entorno)***
3. ***[Configuración de MCP para Hexstrike](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/HerramientasAnalisisVulnerabilidades.md#3-configuraci%C3%B3n-de-mcp-para-hexstrike)***
4. ***[Pruebas de funcionamiento](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/HerramientasAnalisisVulnerabilidades.md#4-pruebas-de-funcionamiento)***
5. ***[Conclusión](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/HerramientasAnalisisVulnerabilidades.md#5-conclusi%C3%B3n)***

---
## 1. ***Introducción***

Este proyecto consiste en integrar ***Gemini CLI*** con un servidor MCP ***Hexstrike***. El objetivo es que Gemini pueda comunicarse con el MCP para realizar acciones de análisis de vulnerabilidades de forma automática dentro del entorno de trabajo.

---
## 2. ***Preparación del entorno***

Para integrar Hexstrike como MCP dentro de Gemini CLI, primero se prepara el entorno local donde se ejecutará el servidor MCP:

- Primero, comprobamos que Gemini CLI se puede ejecutar correctamente:

```bash
gemini
```

<img width="952" height="531" alt="image" src="https://github.com/user-attachments/assets/798c4269-be28-4282-8917-73c0ac3e5973" />

- Ahora, vamos a clonar el repositorio del MCP Hexstrike y accedemos a él. Para ello, ejecutamos los siguientes comandos:

```bash
git clone https://github.com/0x4m4/hexstrike-ai/
cd hexstrike-ai
```

<img width="954" height="354" alt="image" src="https://github.com/user-attachments/assets/32428693-15d2-434c-8c49-c54a4e5fe518" />

- Instalamos las dependencias necesarias para ejecutar el MCP Hexstrike. Para ello, ejecutamos el siguiente comando:

```bash
pip3 install -r requirements.txt --break-system-packages
```

<img width="953" height="529" alt="image" src="https://github.com/user-attachments/assets/4a04708a-0ceb-4250-bc70-abae1ac81810" />

- Por último, desplegamos el servidor Hexstrike para conectar más adelante el MCP al Gemini CLI. Para ello, ejecutamos el siguiente comando:

```bash
python3 hexstrike_server.py
```

<img width="954" height="841" alt="image" src="https://github.com/user-attachments/assets/ad09e3fa-6890-4cd7-9ea7-3e47a215b662" />

- Comprobamos que el servidor está desplegado correctamente. Para ello, accedemos a la siguiente url:

```bash
http://127.0.0.1:8888/health
```

<img width="945" height="751" alt="image" src="https://github.com/user-attachments/assets/bfca3e65-75b5-4b96-972a-f0285be65f95" />

---
## 3. ***Configuración de MCP para Hexstrike***



---
## 4. ***Pruebas de funcionamiento***



---
## 5. ***Conclusión***

