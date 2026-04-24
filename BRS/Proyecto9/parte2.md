<h1 align="center">Proyecto 9 - Certificados digitales</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/BRS/images/bannerPortada.png)

***Fecha:*** 24 de abril de 2026<br>
***Autor:*** Sergio González  

---
## Índice

1. [Introducción](#1-introducción)  
2. [Despliegue del servidor web](#2-despliegue-del-servidor-web)  
3. [Configuración del dominio](#3-configuración-del-dominio)  
4. [Instalación del certificado SSL](#4-instalación-del-certificado-ssl)  
5. [Acceso mediante HTTPS](#5-acceso-mediante-https)  
6. [Análisis de certificado de sitio real](#6-análisis-de-certificado-de-sitio-real)  
7. [Comparativa](#7-comparativa)  
8. [Problemas y solución](#8-problemas-y-solución)  
9. [Conclusión](#9-conclusión)

---
## 1. ***Introducción***

En este proyecto se ha trabajado con la configuración de un servidor web seguro en un entorno realista utilizando una instancia en AWS.

El objetivo principal ha sido aprender a generar y utilizar certificados digitales para habilitar conexiones HTTPS seguras, así como comprobar cómo funcionan estos certificados en un entorno real.

Además, se ha realizado una comparación entre un certificado propio emitido por Let's Encrypt y certificados utilizados en sitios web reales, con el fin de entender mejor cómo funciona la seguridad en la web.

---
## 2. ***Despliegue del servidor web***

Para este proyecto se ha utilizado una instancia en AWS EC2 con sistema Linux.

En esta máquina virtual se ha instalado el servidor web Apache, que es el encargado de servir la página web desde la instancia.

Una vez instalado, se ha comprobado que el servicio funciona correctamente accediendo desde el navegador mediante la dirección IP pública del servidor.

También se ha configurado el firewall de AWS (Security Group) para permitir el tráfico HTTP y HTTPS, lo cual es necesario para poder acceder al servidor desde Internet.

---
### ***Evidencias***
---

- ***Instancia EC2 en AWS en estado activo con su IPv4 pública***

![EC2](https://github.com/user-attachments/assets/0236efd3-73f0-4e42-9e88-606d6b55bbc7)

- ***Página web funcionando con HTTPS mostrando el mensaje "OK HTTPS AWS"***

![HTTPS](https://github.com/user-attachments/assets/4fba8fe9-84ba-4706-9662-0d19a6a72f69)

- ***Configuración del Security Group con puertos 80 y 443 abiertos***

![SG](https://github.com/user-attachments/assets/a8d4908a-2df4-4097-8b42-c1531eb66455)

---
## 3. ***Configuración del dominio***

Para poder acceder al servidor de forma más cómoda, en lugar de utilizar la dirección IP pública de la instancia de AWS, se ha configurado un dominio dinámico mediante DuckDNS.

El dominio utilizado es:

- sgonnor.duckdns.org

Este dominio se ha vinculado a la dirección IP pública de la instancia EC2, de forma que cualquier petición al dominio se redirige automáticamente al servidor en AWS.

Esto permite acceder al servidor web de forma más sencilla y es especialmente útil cuando la IP puede cambiar.

Además, este dominio ha sido el utilizado posteriormente para la generación del certificado SSL con Let's Encrypt.

---
### ***Evidencia***
---

- ***Captura del dominio configurado en DuckDNS***

![DuckDNS](https://github.com/user-attachments/assets/aa196ab7-82da-4001-a753-4855bc8b4d8d)

---
## 4. ***Instalación del certificado SSL***

Para habilitar el acceso seguro mediante HTTPS, se ha utilizado Certbot junto con el servicio de Let's Encrypt.

Con esta herramienta se ha generado un certificado digital válido para el dominio configurado (sgonnor.duckdns.org), que permite cifrar la comunicación entre el servidor y el cliente.

Durante el proceso, Certbot ha verificado el dominio y ha emitido el certificado de forma automática.

Después de esto, el certificado se ha configurado en Apache, lo que ha permitido que el servidor funcione correctamente con HTTPS.

Una vez finalizado, se ha comprobado desde el navegador que el certificado es válido y que la conexión aparece como segura.

---
### ***Evidencias***
---

- ***Captura del certificado digital visto desde el navegador***

![Certificado navegador](https://github.com/user-attachments/assets/8d101e8e-c574-4e4d-8824-daa0f0e5de41)

- ***Captura del resultado de Certbot mostrando el certificado instalado***

![Certbot](https://github.com/user-attachments/assets/ccb9dcf9-9b44-4bd6-a627-58175eadea8f)

---
## 5. ***Acceso mediante HTTPS***

Una vez configurado el servidor web y el certificado SSL, se ha comprobado el acceso al sitio web mediante HTTPS.

Para ello, se ha accedido desde el navegador al dominio configurado (sgonnor.duckdns.org), verificando que la conexión es segura y que el certificado es válido.

El navegador muestra el candado de seguridad, lo que indica que la comunicación entre el cliente y el servidor está cifrada correctamente mediante TLS.

Además, se ha comprobado que el contenido de la página web se carga correctamente sin errores.

---
### Evidencia
---

- ***Captura del navegador accediendo al sitio web mediante HTTPS con el candado de seguridad visible.***

![HTTPS Candado](https://github.com/user-attachments/assets/1dc837e5-4fb5-413e-836f-c9ed3ba6ae62)

---
## 6. ***Análisis de certificado de sitio real***

En este apartado se ha analizado el certificado de un sitio web real para ver cómo funciona en comparación con el del proyecto.

El sitio web elegido ha sido Google:

- https://www.google.com

---
### ***Certificado de Google***
---

El certificado de Google está emitido para el dominio `google.com`.

Está emitido por Google Trust Services, que es una autoridad de certificación utilizada en servicios grandes y conocidos.

Este certificado forma parte de una infraestructura más compleja que la del proyecto, ya que está pensada para millones de usuarios y mayor seguridad.

---
### ***Certificado del proyecto***
---

El certificado que se ha utilizado en este proyecto está emitido para el dominio `sgonnor.duckdns.org`.

Está emitido por Let's Encrypt, que es una autoridad de certificación gratuita bastante usada en servidores web y entornos de aprendizaje.

No incluye información de organización, ya que es un certificado de validación de dominio (DV), que es el más básico.

---
### ***Conclusión***
---

Los dos certificados sirven para lo mismo, que es asegurar la conexión mediante HTTPS.

La diferencia principal es que el de Google está en una infraestructura mucho más grande y compleja, mientras que el del proyecto es más simple pero igualmente válido y seguro para este tipo de prácticas.

---
### ***Evidencia***
---

- ***Captura del certificado digital de Google donde se pueden ver sus datos principales.***

![Certificado Google](https://github.com/user-attachments/assets/41d61d5e-b08e-4b0f-a337-f2e90ca3c40b)

---
## 7. ***Comparativa***

En este apartado se realiza una comparación directa entre el certificado generado en este proyecto y el certificado de un sitio web real (Google), con el objetivo de analizar sus diferencias y similitudes.

---
### Similitudes
---

Ambos certificados cumplen la misma función principal, que es asegurar la comunicación entre el cliente y el servidor mediante HTTPS.

Además:

- Los dos están emitidos por autoridades de certificación confiables.
- Ambos permiten cifrar la información que se transmite.
- Los navegadores los reconocen como certificados válidos.

---
### Diferencias
---

A pesar de cumplir la misma función, existen varias diferencias importantes:

- El certificado del proyecto está emitido por Let's Encrypt, mientras que el de Google está emitido por Google Trust Services.
- El certificado del proyecto es de validación de dominio (DV), que es el nivel más básico, mientras que el de Google forma parte de una infraestructura más avanzada.
- El dominio del certificado de Google es un wildcard (*.google.com), lo que permite cubrir múltiples subdominios, mientras que el del proyecto solo cubre un dominio específico.
- La infraestructura de Google es mucho más compleja y está diseñada para soportar millones de usuarios.

---
### Conclusión
---

Aunque los dos certificados son válidos y cumplen su función correctamente, se pueden ver diferencias en el nivel de infraestructura y complejidad.

El certificado del proyecto es más sencillo y está orientado a entornos de aprendizaje o servidores básicos, mientras que el de Google está pensado para entornos profesionales a gran escala.

Aun así, ambos garantizan una conexión segura mediante HTTPS.

---
## 8. ***Problemas y solución***

Durante la realización del proyecto han surgido algunos problemas que se han tenido que ir solucionando.

Uno de los primeros fue que no se podía acceder al servidor desde el navegador. Esto era porque los puertos no estaban abiertos en el Security Group de AWS. Se solucionó abriendo los puertos 80 (HTTP) y 443 (HTTPS).

Otro problema apareció al usar Certbot, ya que el puerto 80 estaba en uso por Apache. Esto impedía generar el certificado correctamente. Se solucionó utilizando la opción adecuada para integrarlo con el servidor web.

También hubo un momento en el que el navegador indicaba que la conexión no era segura, aunque el certificado estaba creado. Esto se debía a que no estaba bien configurado en Apache, y se solucionó aplicándolo correctamente.

Una vez solucionados estos problemas, el servidor ha quedado funcionando correctamente con HTTPS.

---
## 9. ***Conclusión***

Se ha logrado desplegar un servidor web funcional con HTTPS utilizando certificados digitales válidos en un entorno real con AWS.

A lo largo del proyecto se ha configurado una instancia EC2, un dominio mediante DuckDNS y un certificado SSL con Let's Encrypt, lo que ha permitido asegurar la comunicación entre el cliente y el servidor.

Además, se ha podido analizar y comparar el certificado propio con el de un sitio web real como Google, lo que ayuda a entender mejor cómo funcionan los certificados digitales en distintos entornos.

En general, este proyecto ha servido para ver de forma práctica la importancia del uso de HTTPS y de los certificados digitales en la seguridad de las comunicaciones web.
