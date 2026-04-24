<h1 align="center">Proyecto 9 - Análisis SSL</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/BRS/images/bannerPortada.png)

***Fecha:*** 24 de abril de 2026<br>
***Autor:*** Sergio González

---
## Índice

1. [Introducción](#1-introducción)
2. [Análisis del certificado del servidor](#2-análisis-del-certificado-del-servidor)
3. [Certificados inválidos](#3-certificados-inválidos)
4. [Conclusión](#4-conclusión)

---
## 1. ***Introducción***

En esta parte del proyecto se ha realizado un análisis de seguridad SSL/TLS del servidor web desplegado en AWS.

El objetivo es comprobar la validez del certificado digital utilizado en el proyecto y entender cómo se comporta frente a herramientas de análisis de seguridad.

Además, se han analizado diferentes sitios web con certificados incorrectos o no válidos, con el fin de identificar errores comunes en la configuración de SSL/TLS.

---
## 2. ***Análisis del certificado del servidor***

En este apartado se ha analizado el certificado del servidor propio del proyecto utilizando la herramienta SSL Labs.

- Dominio analizado: sgonnor.duckdns.org
- Herramienta utilizada: SSL Labs (Qualys)

### Resultado del análisis

- Calificación obtenida: (A / A+ / B según tu caso)

### Observaciones

- El certificado es válido y está emitido por Let's Encrypt.
- La conexión HTTPS está correctamente cifrada.
- El servidor utiliza protocolos seguros como TLS.
- No se detectan vulnerabilidades críticas.

---
### Evidencia
---

![SSL Labs](AQUÍ_TU_CAPTURA)

---
## 3. ***Certificados inválidos***

En este apartado se han analizado tres ejemplos de certificados incorrectos o no válidos para entender los errores más comunes en SSL/TLS.

---
### 3.1. ***Certificado caducado***
---

- Problema: el certificado ha expirado  
- Consecuencia: el navegador muestra advertencia de seguridad  
- Motivo: no se ha renovado a tiempo  

---
### 3.2. ***Certificado autofirmado***
---

- Problema: el certificado no está emitido por una autoridad confiable  
- Consecuencia: el navegador no confía en la conexión  
- Motivo: no existe validación por una CA  

---
### 3.3. ***Error de dominio***
---

- Problema: el certificado no coincide con el dominio visitado  
- Consecuencia: advertencia de “sitio no seguro”  
- Motivo: configuración incorrecta del certificado  

---
## 4. ***Conclusión***

El análisis realizado permite entender la importancia de una correcta configuración SSL/TLS en los servidores web.

El certificado del proyecto es válido y seguro, mientras que los certificados inválidos analizados muestran errores comunes que afectan directamente a la seguridad de las comunicaciones.

Esto demuestra la importancia de utilizar certificados correctamente configurados y mantenidos en entornos reales.
