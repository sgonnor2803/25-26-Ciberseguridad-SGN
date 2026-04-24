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

En esta parte del proyecto se ha hecho un análisis de seguridad del servidor web que se había montado previamente en AWS.

Para ello se ha utilizado una herramienta que permite comprobar certificados SSL/TLS y ver si la conexión HTTPS está bien configurada y es segura.

También se han revisado algunos ejemplos de certificados que no son válidos en otros sitios web, para ver qué tipos de errores pueden aparecer y cómo afectan a la seguridad.

El objetivo de esta parte es entender mejor cómo funcionan los certificados digitales en sitios reales y por qué son importantes para mantener una conexión segura en Internet.

---
## 2. ***Análisis del certificado del servidor***

En este apartado se ha analizado el certificado del servidor web del proyecto utilizando la herramienta SSL Labs.

El dominio analizado ha sido:

- https://sgonnor.duckdns.org

---
### Resultado del análisis
---

La herramienta SSL Labs ha mostrado que el servidor tiene una configuración correcta de SSL/TLS, obteniendo una calificación de:

- **Nota: A**

Esto indica que la configuración del certificado es segura y está bien implementada en el servidor.

---
### Observaciones del análisis
---

A partir del informe generado se pueden destacar los siguientes puntos:

- El certificado está emitido por **Let's Encrypt**, una autoridad de certificación gratuita y ampliamente utilizada.
- El certificado es válido y está correctamente instalado en el servidor.
- La conexión HTTPS está cifrada correctamente mediante TLS.
- El navegador reconoce el certificado como seguro.
- No se detectan vulnerabilidades críticas en la configuración del servidor.
- Se utilizan protocolos modernos y seguros, compatibles con navegadores actuales.

---
### Conclusión del análisis
---

En general, el servidor tiene una configuración SSL correcta y segura, adecuada para un entorno de pruebas o aprendizaje como este proyecto.

Aunque no es una infraestructura profesional, cumple correctamente con los requisitos de seguridad actuales para conexiones HTTPS.

---
### Evidencia
---

![SSL Labs](https://github.com/user-attachments/assets/90333a3c-6e63-4737-ae4b-edd29367a336)

---
## 3. ***Certificados inválidos***

En este apartado se han analizado tres ejemplos de certificados incorrectos o no válidos para entender los errores más comunes en SSL/TLS.

---
### 3.1. ***Certificado caducado***
---

En este caso se ha analizado una página web que tiene un certificado SSL caducado, lo que hace que el navegador lo detecte como no seguro.

El sitio utilizado ha sido:

- https://expired.badssl.com/

Además del acceso desde el navegador, también se ha revisado con SSL Labs para ver su configuración.

---
### ***Problema detectado***
---

El problema es que el certificado ha caducado, es decir, ha pasado su fecha de validez y ya no se considera seguro para establecer una conexión HTTPS.

---
### ***Resultado del análisis (SSL Labs)***
---

SSL Labs muestra que el certificado no es válido porque está caducado, lo que afecta directamente a la seguridad del sitio.

Por este motivo, el navegador muestra avisos de que la conexión no es segura.

---
### ***Consecuencias***
---

- El navegador avisa de que el sitio no es seguro.
- La conexión HTTPS no es fiable.
- El usuario puede ver alertas de seguridad.
- Aunque la página funcione, no es recomendable confiar en ella.

---
### ***Explicación***
---

Este error suele pasar cuando no se renuevan los certificados a tiempo. Es un fallo bastante común y hace que los navegadores bloqueen o avisen al usuario por seguridad.

---
### ***Evidencia***
---

![Certificado caducado](https://github.com/user-attachments/assets/a7fff71c-a9f1-4f2b-8d76-b3589cd0ab52)

---
### 3.2. ***Certificado autofirmado***
---

En este caso se ha analizado una página web que utiliza un certificado autofirmado, lo que hace que el navegador no lo considere seguro.

El sitio utilizado ha sido:

- https://self-signed.badssl.com/

Además, se ha comprobado su configuración mediante la herramienta SSL Labs.

---
### ***Problema detectado***
---

El problema es que el certificado no está emitido por una autoridad de certificación reconocida, sino que está generado por el propio servidor (autofirmado).

---
### ***Resultado del análisis (SSL Labs)***
---

SSL Labs indica que el certificado no es de confianza, ya que no ha sido validado por una entidad certificadora (CA).

Esto hace que los navegadores no puedan verificar su autenticidad.

---
### ***Consecuencias***
---

- El navegador muestra advertencias de seguridad.
- La conexión HTTPS no se considera fiable.
- No se puede garantizar que el servidor sea realmente quien dice ser.
- El usuario recibe avisos antes de acceder al sitio.

---
### ***Explicación***
---

Los certificados autofirmados no pasan por una autoridad de certificación, por lo que no hay ninguna entidad externa que valide su autenticidad.

Aunque pueden servir para pruebas o entornos locales, no son adecuados para sitios web públicos porque no generan confianza en los navegadores.

---
### ***Evidencia***
---

![Certificado autofirmado](https://github.com/user-attachments/assets/58efbb54-d00d-4aac-9a70-c0f6a96b1bf5)

---
### 3.3. ***Error de dominio***
---

En este caso se ha analizado una página web que presenta un error en el certificado relacionado con el dominio.

El sitio utilizado ha sido:

- https://wrong.host.badssl.com/

También se ha revisado su configuración mediante la herramienta SSL Labs.

---
### ***Problema detectado***
---

El problema es que el certificado SSL no coincide con el dominio al que se está accediendo.

Es decir, el certificado está emitido para un dominio diferente, por lo que no es válido para este sitio.

---
### ***Resultado del análisis (SSL Labs)***
---

SSL Labs muestra que el certificado presenta un error de coincidencia de nombre (hostname mismatch), lo que hace que no sea válido para el dominio analizado.

Por este motivo, los navegadores no pueden verificar correctamente la identidad del servidor.

---
### ***Consecuencias***
---

- El navegador muestra advertencias de seguridad.
- La conexión HTTPS no es fiable.
- No se puede asegurar que el servidor sea el correcto.
- El usuario recibe avisos antes de acceder al sitio.

---
### ***Explicación***
---

Este tipo de error ocurre cuando el certificado ha sido emitido para un dominio distinto al que se está utilizando.

Es un fallo de configuración bastante común y puede provocar problemas de seguridad, ya que el usuario no puede estar seguro de que está accediendo al servidor correcto.

---
### ***Evidencia***
---

![Error de dominio](https://github.com/user-attachments/assets/6d33623f-6984-4a64-b007-5400bd6f50c3)

---
## 4. ***Conclusión***

En esta parte del proyecto se ha podido comprobar cómo funciona la seguridad SSL/TLS en un entorno real.

Por un lado, el análisis del servidor propio ha mostrado que el certificado está bien configurado y que la conexión HTTPS es segura, lo cual indica que se ha realizado correctamente el proceso.

Por otro lado, al analizar certificados inválidos se han visto errores bastante comunes como certificados caducados, autofirmados o con problemas de dominio, que hacen que los navegadores no confíen en la conexión.

En general, esta parte ha servido para entender mejor la importancia de los certificados digitales y cómo afectan directamente a la seguridad de los sitios web.
