<h1 align="center">Herramientas MCP para análisis de vulnerabilidades</h1>

![imagen portada infraestructura](https://github.com/IES-Rafael-Alberti/25-26-Ciberseguridad-Grupo-5/blob/main/PPS/images/portadainfraestructura.png)

***Fecha:*** 25 de noviembre de 2025
<br>***Autor***: Sergio González

---
## Índice

1. ***[Introducción]()***
2. ***[Preparación del entorno]()***
3. ***[Configuración de MCP para Hexstrike]()***
4. ***[Pruebas de funcionamiento]()***
5. ***[Conclusión]()***

---
## 1. ***Introducción***

En esta parte del proyecto se integra ***Hexstrike*** como herramienta de análisis de vulnerabilidades dentro de OpenCode mediante un servidor ***MCP***. El objetivo es que los agentes puedan lanzar escaneos y obtener resultados directamente desde la IA, usando el servidor de Hexstrike disponible en la red del aula o ejecutado desde WSL. Con esto se amplía la capacidad del agente para tareas de ciberseguridad de forma automática y controlada.

---
## 2. ***Preparación del entorno***

En este apartado se explica cómo preparar el entorno para poder conectar OpenCode con Hexstrike mediante un servidor MCP. Para ello se usará WSL (Kali Linux), donde desplegaremos el MCP y lo dejaremos accesible desde OpenCode a través de localhost.

- Abrimos en la terminal la máquina kali linux de WSL. Para ello, ejecutamos el siguiente comando:

```bash
wsl -d kali-linux
```

<img width="677" height="161" alt="image" src="https://github.com/user-attachments/assets/1094e0b9-76d4-4b50-bca4-ca6911915dd0" />

- Accedemos hacia la carpeta donde vamos a clonar el repositorio del MCP Hexstrike. Para ello, ejecutamos el siguiente comando:

```bash
cd Desktop/Ciberseguridad/PuestaEnProduccionSegura/
```

<img width="1247" height="232" alt="image" src="https://github.com/user-attachments/assets/ebffc22e-8efc-4f6d-acf9-fb1221bcd1df" />

- Clonamos el repositorio Hexstrike en el directorio que elejimos antes y accedemos a él. Para ello, ejecutamos los siguientes comandos:

```bash
git clone https://github.com/0x4m4/hexstrike-ai
cd hexstrike-ai/
```

<img width="1276" height="395" alt="image" src="https://github.com/user-attachments/assets/456e4785-7c40-4a02-896c-493c0d0bede0" />
<img width="1379" height="212" alt="image" src="https://github.com/user-attachments/assets/e941e3aa-2112-4b9b-b180-67fef804ee94" />

- Teniendo el repositorio clonado, vamos a instalar todas las dependencias que necesita el MCP de Hexstrike. Para ello, ejecutamos el siguiente comandos:

```bash
pip3 install -r requirements.txt --break-system-packages
```

<img width="1627" height="758" alt="image" src="https://github.com/user-attachments/assets/9483cb92-47f3-44b1-b338-e08d388d141d" />

- Desplegamos el MCP Hexstrike mediante el siguiente comando:

```bash
python3 hexstrike_server.py
```

<img width="1625" height="759" alt="image" src="https://github.com/user-attachments/assets/9583ca37-4b72-4015-9e2e-a4fd81945088" />

- Comprobamos si el MCP de Hexstrike se está ejecutando correctamente. Para ello. accedemos desde nuestro anfitrion a la siguiente url:

```bash
http://localhost:8888/health
```

<img width="957" height="962" alt="image" src="https://github.com/user-attachments/assets/0cc045ed-eae4-4641-9545-9c70bc2df0b3" />

---
## 3. ***Configuración de MCP para Hexstrike***

En este apartado se configura el servidor MCP que permitirá a los agentes de OpenCode comunicarse con Hexstrike, la herramienta de análisis de vulnerabilidades desplegada en WSL.

- Primero, vamos a configurar el MCP en el archivo de configuración de OpenCode. Añadimos al bloque mcp la siguiente configuración:

```bash
"hexstrike": {
      "type": "local",
      "command": ["python3", "/mnt/c/Users/dryke/Desktop/Ciberseguridad/PuestaEnProduccionSegura/hexstrike-ai/hexstrike_server.py"],
      "enabled": true,
      "timeout": 300
    }
```

<img width="1618" height="770" alt="image" src="https://github.com/user-attachments/assets/141d5e2b-091e-4154-a422-3242f755b148" />

- 

---
## 4. ***Pruebas de funcionamiento***



---
## 5. ***Conclusión***

