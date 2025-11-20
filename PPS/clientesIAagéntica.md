<h1 align="center">Usar clientes IA agéntica</h1>

![imagen portada infraestructura](https://github.com/IES-Rafael-Alberti/25-26-Ciberseguridad-Grupo-5/blob/main/PPS/images/portadainfraestructura.png)

***Fecha:*** 20 de noviembre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Introducción](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#1-introducci%C3%B3n)***
2. ***[Selección de la herramienta de IA agéntica](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#2-selecci%C3%B3n-de-la-herramienta-de-ia-ag%C3%A9ntica)***
3. ***[Instalación del entorno](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#3-instalaci%C3%B3n-del-entorno)***
4. ***[Instalación de la herramienta elegida](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#4-instalaci%C3%B3n-de-la-herramienta-elegida)***
5. ***[Configuración de los modelos recomendados](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#5-configuraci%C3%B3n-de-los-modelos-recomendados)***
6. ***[Configuración y habilitación de MCP](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#6-configuraci%C3%B3n-y-habilitaci%C3%B3n-de-mcp)***
7. ***[Prueba funcional del agente](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#7-prueba-funcional-del-agente)***
8. ***[Conclusiones](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/PPS/clientesIAag%C3%A9ntica.md#8-conclusiones)***

---
## 1. ***Introducción***

El proyecto consiste en montar un entorno para trabajar con ***OpenCode*** como herramienta de IA agéntica. Se prepara Node con nvm, se conecta OpenCode a ***Ollama Cloud*** y se activa ***MCP*** para poder usar acciones externas. También se dejan configurados todos los modelos recomendados en 2025 (***Sonnet4.5, GPT5.1, Gemini3, Kimi-K2, Minimax-M2 y Qwen3-Coder***) para poder usarlos desde la misma herramienta sin complicaciones.

---
## 2. ***Selección de la herramienta de IA agéntica***

La herramienta elegida para este proyecto es ***OpenCode***, por su compatibilidad con ***Ollama Cloud***, soporte de MCP y facilidad para trabajar con múltiples modelos de código abiertos. OpenCode permite que los agentes ejecuten acciones externas de forma segura y está bien documentada, lo que facilita su instalación y configuración en el entorno de pruebas.

---
## 3. ***Instalación del entorno***

- Primero, vamos a descargar nvm desde el siguiente ***[enlace](https://github.com/coreybutler/nvm-windows/releases)***.

<img width="1919" height="713" alt="image" src="https://github.com/user-attachments/assets/12c6be20-ba20-4e94-a461-2153c61b7084" />
<img width="1919" height="228" alt="image" src="https://github.com/user-attachments/assets/bc70fd4e-f05b-4a04-b65b-0685e4e52675" />

- Ejecutamos el ***.exe*** y seguimos los pasos para la instalación de nvm.

<img width="581" height="477" alt="image" src="https://github.com/user-attachments/assets/42931bd7-7713-4c95-9c00-a23a6bd3f407" />

- Teniendo nvm, vamos a instalar Node. Para ello, ejecutamos los siguientes comandos en este orden:

```bash
nvm install 24.11.1
nvm use 24.11.1
```

<img width="493" height="246" alt="image" src="https://github.com/user-attachments/assets/80e55055-a5fd-4c42-b99b-745f0d11e302" />
<img width="384" height="122" alt="image" src="https://github.com/user-attachments/assets/68b350c1-6dda-48c5-983e-b42090c839ca" />

- Comprobamos que se ha instalado node y npm correctamente. Para ello, ejecutamos los siguientes comandos:

```bash
node -v
npm -v
```

<img width="348" height="167" alt="image" src="https://github.com/user-attachments/assets/73d2741c-3174-4244-88f5-e47eb75bb290" /><br>
> Como podemos ver, se ha instalado node y npm dandonos la versión correctamente.

---
## 4. ***Instalación de la herramienta elegida***

OpenCode se instala desde npm mediante el paquete ***opencode-ai***, por lo que una vez configurado Node y npm en el sistema se puede instalar directamente.

- Para instalar Opencode ejecutamos el siguiente comando:

```bash
npm i -g opencode-ai
```

<img width="425" height="147" alt="image" src="https://github.com/user-attachments/assets/732eb5a2-5fc8-478b-afe5-87b9fdd2c9c1" />

- Comprobamos que se ha instalado correctamente Opencode. Para ello, ejecutamos el siguiente comando:

```bash
opencode --version
```

<img width="410" height="132" alt="image" src="https://github.com/user-attachments/assets/8311a6df-3e25-4ebf-ae43-4a02911a2d69" />

Y para abrir Opencode, ejecutamos el siguiente comando:

```bash
opencode
```

<img width="335" height="84" alt="image" src="https://github.com/user-attachments/assets/cbc13f3c-a515-49a0-941a-a5d9cf2f02c4" />
<img width="1099" height="634" alt="image" src="https://github.com/user-attachments/assets/15425f3c-7a3d-46e5-9bbf-0626e5ae055d" />

---
## 5. ***Configuración de los modelos recomendados***



---
## 6. ***Configuración y habilitación de MCP***



---
## 7. ***Prueba funcional del agente***



---
## 8. ***Conclusiones***




