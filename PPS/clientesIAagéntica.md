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

Se van a configurar estos modelos: GPT5, Sonnet4.5, Qwen3-Coder, Gemini3, Kimi-K2 y Minimax-M2.
Los modelos internos que funcionan sin claves es opencode/gpt-5-nano y opencode/claude-sonnet-4-5; los demás se apuntan a Ollama Cloud.

Para ello, configuramos el archivo ***opencode.json*** donde se definirán los modelos que vamos a utilizar en Opencode.

<img width="714" height="828" alt="image" src="https://github.com/user-attachments/assets/705fce70-e4e3-4623-b6e3-32c68d0766fe" />

Ahora, podemos acceder a los diferentes modelos desde Opencode. Si queremos acceder directamente con el modelo a Opencode, ejecutaremos el siguiente comando (ejemplo kimi-k2):

```bash
opencode --model kimi-k2:1t-cloud
```

<img width="898" height="95" alt="image" src="https://github.com/user-attachments/assets/fccf9bef-5c72-4e30-9c0d-06a52498eaae" />
<img width="1140" height="578" alt="image" src="https://github.com/user-attachments/assets/0459ec87-1b52-470d-87af-e19e47da4c1f" />

---
## 6. ***Configuración y habilitación de MCP***

Se han activado varios ***MCP locales*** para que los agentes de OpenCode puedan hacer cosas fuera del modelo de forma segura y sin complicaciones. Todo se configura en el ***opencode.json*** y se activan al abrir OpenCode. Los MCP que se han configurado han sido los siguientes:

- ***Browser (navegador web):*** Sirve para abrir webs y sacar información de ellas.
- ***Files (archivos):*** Permite crear, leer y modificar archivos locales.
- ***Notes (notas):*** Permite crear y gestionar notas rápidas.

<img width="766" height="945" alt="image" src="https://github.com/user-attachments/assets/bfb6aff1-94a6-4c23-b39c-ee9207a3bd6b" />

---
## 7. ***Prueba funcional del agente***

Aquí se comprueba que los modelos y los MCP locales funcionan correctamente dentro de OpenCode. La idea es probar cada modelo y MCP con prompts simples y ver que devuelven resultados correctos.

### 7.1. ***Prueba de modelos***

Se han realizado pruebas con los modelos disponibles, ejecutando prompts simples para cada uno. Algunos modelos no pudieron probarse debido a que requieren acceso premium.

- ***Modelo GPT-5 Nano***

```bash
Dame un resumen de prueba
```

<img width="1200" height="636" alt="image" src="https://github.com/user-attachments/assets/a9b415e9-17b9-4d6e-8d79-9e1beafdb679" />

- ***Modelo kimi-k2***

```bash
Crea una lista de 3 tareas simples
```

<img width="1317" height="576" alt="image" src="https://github.com/user-attachments/assets/2bc0013a-baff-44d3-83b1-47248c60a818" />

- ***Modelo Minimax-M2***

```bash
Genera un breve texto explicativo sobre IA
```

<img width="1316" height="577" alt="image" src="https://github.com/user-attachments/assets/b943738c-35ad-4282-aa54-76e085272f37" />

- ***Modelo Qwen3-Coder***

```bash
Escribe un ejemplo de código Python que sume dos números
```

<img width="1321" height="575" alt="image" src="https://github.com/user-attachments/assets/a1677f55-4a43-4575-8657-f005bd7ae5f9" />

---
### 7.2. ***Prueba MCP Locales***

Se prueban los MCP configurados en ***opencode.json*** con prompts sencillos:

- ***MCP Browser***

```bash
Usa MCP Browser para abrir este enlace https://es.wikipedia.org/wiki/Microsoft y dime cuando fue la fundación
```

<img width="1322" height="574" alt="image" src="https://github.com/user-attachments/assets/7a504657-75d0-4f81-b5b2-a1cf2f8d1155" />

- ***MCP Files***

```bash
Usa MCP Files para crear resumen.txt con el contenido Prueba de MCP Files
```

<img width="1316" height="571" alt="image" src="https://github.com/user-attachments/assets/bae386f5-c8b7-4635-bf0e-fc60ca884f7d" />
<img width="467" height="182" alt="image" src="https://github.com/user-attachments/assets/140e5ae2-db45-4ce2-b652-f274fbad43aa" />


- ***MCP Notes***

```bash
Usa MCP Notes para crear una nota con título Prueba MCP Notes y contenido Esto es una nota de prueba
```

<img width="1319" height="576" alt="image" src="https://github.com/user-attachments/assets/fd6d379f-2536-4195-a24d-687b4e22098f" />
<img width="697" height="212" alt="image" src="https://github.com/user-attachments/assets/ce80e70c-9fc1-4799-9a90-d697766da0fe" />

---
## 8. ***Conclusiones***

Se ha configurado un entorno completo con ***OpenCode***, conectando modelos internos y de ***Ollama Cloud*** para usar ***GPT-5 Nano, Sonnet4.5, Gemini3, Kimi-K2, Minimax-M2 y Qwen3-Coder***.

Se activaron ***MCP locales*** (Browser, Files y Notes) que permiten a los agentes interactuar con el entorno de forma segura.

Las pruebas muestran que los modelos y MCP funcionan correctamente, permitiendo generar texto, código y manejar tareas externas desde OpenCode.

En definitiva, se consiguió un entorno ágil y funcional para trabajar con agentes de IA y capacidades externas de manera integrada.

