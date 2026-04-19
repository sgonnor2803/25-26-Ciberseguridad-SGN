<h1 align="center">Hardening de router ASUS RT-AX95Q</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/BRS/images/bannerPortada.png)

***Fecha:*** 19 de abril de 2026  
***Autor:*** Sergio González

---
## Índice

1. [Introducción](#1-introducción)  
2. [Seguridad de acceso al sistema](#2-seguridad-de-acceso-al-sistema)  
3. [Seguridad de red WiFi](#3-seguridad-de-red-wifi)  
4. [Segmentación de red y red de invitados](#4-segmentación-de-red-y-red-de-invitados)  
5. [Servicios y protocolos inseguros](#5-servicios-y-protocolos-inseguros)  
6. [Firewall y protección del sistema](#6-firewall-y-protección-del-sistema)  
7. [Actualización y mantenimiento del firmware](#7-actualización-y-mantenimiento-del-firmware)  
8. [Conclusiones](#8-conclusiones)
9. [Anexo I. Hardening básico de un router ASUS (panel de administración)](#9-anexo-i-hardening-básico-de-un-router-asus-panel-de-administración)

---
## 1. ***Introducción***

En este trabajo se va a analizar la seguridad de un router doméstico ASUS RT-AX95Q, aplicando técnicas básicas de hardening. La idea es ver cómo está configurado el dispositivo de forma inicial y qué cambios se pueden hacer para mejorar su seguridad.

Un router es una parte muy importante dentro de una red, ya que es el punto por donde pasa todo el tráfico de Internet. Por eso, si no está bien configurado, puede convertirse en un punto débil y afectar a todos los dispositivos conectados.

A lo largo del trabajo se revisan diferentes aspectos como el acceso al sistema, la red WiFi, la segmentación de red, los servicios activos, el firewall y las actualizaciones del firmware. En cada caso se explica el estado inicial, los posibles riesgos y algunas mejoras que se pueden aplicar.

El objetivo es entender qué configuraciones son más importantes para mejorar la seguridad de una red doméstica y cómo pequeños cambios pueden marcar la diferencia.

---
## 2. ***Seguridad de acceso al sistema***

En este apartado se analiza la seguridad del acceso al sistema del router, es decir, todo lo relacionado con la administración del dispositivo.

Se revisa cómo está configurado el acceso inicial al panel de control, qué posibles riesgos existen si no está correctamente protegido y qué mejoras se pueden aplicar para reforzar esta parte, que es una de las más importantes dentro del hardening del router.

---
### 2.1. ***Estado inicial del sistema***
---

Al acceder al panel de administración del router ASUS RT-AX95Q, se puede observar que la configuración inicial del sistema no está suficientemente reforzada en términos de seguridad.

En el estado en el que se encuentra el dispositivo, el acceso al panel de administración no presenta una configuración especialmente endurecida desde el punto de vista de la seguridad. Además, el firmware del router se encuentra desactualizado desde 2020, lo que implica la posible ausencia de parches de seguridad importantes publicados posteriormente por el fabricante.

<p align="center"><img width="799" height="348" alt="Screenshot_1" src="https://github.com/user-attachments/assets/a1269b8c-de50-4160-b57a-45ef56c414c1" /></p>

<p align="center"><img width="800" height="549" alt="Screenshot_2" src="https://github.com/user-attachments/assets/f8bf1550-9495-4430-b27e-115440c20450" /></p>

---
### 2.2. ***Riesgos asociados***
---

Este tipo de configuración puede generar varios problemas de seguridad importantes. En primer lugar, un firmware desactualizado puede dejar expuesto el dispositivo a vulnerabilidades ya conocidas y publicadas, lo que facilita posibles ataques si el equipo está accesible desde una red comprometida.

Por otro lado, si no se refuerza correctamente el acceso al sistema, un atacante que consiga entrar al panel de administración podría tomar el control completo del router. Esto incluye la posibilidad de modificar la configuración de red, redirigir el tráfico o incluso desactivar medidas de seguridad existentes.

---
### 2.3. ***Medidas de mejora aplicadas***
---

Para mejorar la seguridad en este apartado, lo primero que se debería hacer es establecer una contraseña de administrador fuerte y única, evitando cualquier tipo de credencial por defecto o fácil de adivinar.

También es muy importante mantener el firmware del dispositivo actualizado, ya que el fabricante suele publicar parches de seguridad que corrigen vulnerabilidades detectadas con el tiempo. Mantener el sistema actualizado reduce considerablemente la superficie de ataque.

<p align="center"><img width="801" height="348" alt="Screenshot_3" src="https://github.com/user-attachments/assets/27aff5c8-c182-4860-8dd2-8418baddeb9b" /></p>

<p align="center"><img width="799" height="582" alt="Screenshot_4" src="https://github.com/user-attachments/assets/e0c95731-d73c-4b38-926d-d4172c188bd3" /></p>

Como medida adicional más avanzada, también se podría reforzar el acceso al router mediante el uso de una VPN para la administración remota.

De esta forma, en lugar de exponer directamente el panel de administración a la red, el acceso se realizaría a través de un túnel cifrado, lo que añade una capa extra de seguridad. Esto es especialmente útil en entornos más profesionales o cuando se necesita acceso remoto seguro al dispositivo.

Sin embargo, en un entorno doméstico o de pequeña red, esta medida no siempre es necesaria, por lo que se considera una mejora opcional dentro del hardening.

---
### 2.4. ***Conclusión***
---

En resumen, el acceso al sistema es la base de la seguridad del router, ya que controla toda su configuración interna.

Una mala protección en este punto puede comprometer completamente el dispositivo, independientemente del resto de medidas aplicadas, por lo que es esencial reforzarlo desde el inicio del proceso de hardening.

---
## 3. ***Seguridad de red WiFi***

En este apartado se analiza la seguridad de la red WiFi del router, que es una de las partes más importantes dentro de cualquier infraestructura de red.

Se estudian los parámetros de configuración inalámbrica, como el tipo de cifrado, la contraseña de acceso y el uso de WPS, con el objetivo de identificar posibles debilidades y proponer mejoras para reforzar la seguridad general de la red.

---
### 3.1. ***Estado inicial de la red inalámbrica***
---

En la configuración inicial del router se observa que la red WiFi no está completamente endurecida desde el punto de vista de la seguridad.

En la primera captura se puede ver la configuración general de la red inalámbrica, donde se aprecia que el cifrado utilizado es WPA2-Personal. Aunque este estándar sigue siendo funcional, actualmente no es el más seguro, ya que existen alternativas más modernas como WPA3. En esta misma pantalla también se observa que el SSID está visible y que no se encuentra oculto, además de que la contraseña configurada es “12345678”, lo que supone una debilidad importante debido a su baja complejidad.

<p align="center"><img width="797" height="647" alt="Screenshot_5" src="https://github.com/user-attachments/assets/5fa57e72-b030-4ac9-b15f-fbe737459f97" /></p>

En la segunda captura se muestra la configuración del sistema WPS, el cual aparece activado. Este mecanismo permite una conexión más rápida a la red, pero también introduce riesgos de seguridad, ya que puede ser vulnerable a ataques de fuerza bruta mediante el PIN de acceso.

<p align="center"><img width="801" height="417" alt="Screenshot_6" src="https://github.com/user-attachments/assets/28546605-e0e0-4772-9ca4-25d2de3be27c" /></p>

Por último, en esta configuración no se aprecia ningún tipo de segmentación de red adicional, lo que indica que todos los dispositivos conectados comparten el mismo entorno de red sin separación entre usuarios o dispositivos.

---

### 3.2. ***Riesgos asociados***
---

Esta configuración presenta varios riesgos importantes.

El uso de una contraseña débil facilita enormemente ataques de acceso a la red WiFi, ya que puede ser adivinada o vulnerada en muy poco tiempo mediante ataques automatizados. El uso de WPA2 en lugar de WPA3 también implica una menor resistencia frente a ataques modernos.

El hecho de tener WPS activado aumenta aún más el riesgo, ya que este sistema puede ser vulnerable a ataques de fuerza bruta sobre el PIN de conexión.

Además, al no existir segmentación de red, cualquier dispositivo conectado a la WiFi forma parte del mismo entorno, lo que aumenta el impacto en caso de que un dispositivo sea comprometido.

---
### 3.3. ***Medidas de mejora aplicadas***
---

Para mejorar la seguridad de la red WiFi, se recomienda en primer lugar actualizar el cifrado a WPA3-Personal, o en su defecto WPA2/WPA3 mixto si hay dispositivos incompatibles.

<p align="center"><img width="796" height="176" alt="Screenshot_8" src="https://github.com/user-attachments/assets/c73296a9-5561-4ce0-b429-e1130bec06ab" /></p>

También es fundamental cambiar la contraseña actual por una clave robusta, larga y aleatoria, evitando combinaciones simples o predecibles.

<p align="center"><img width="796" height="172" alt="Screenshot_9" src="https://github.com/user-attachments/assets/f191fd3e-e303-4f8a-b0df-3671e2a10f4f" /></p>

El sistema WPS debería ser desactivado completamente, ya que no aporta beneficios reales de seguridad en entornos modernos.

<p align="center"><img width="795" height="415" alt="Screenshot_10" src="https://github.com/user-attachments/assets/015c1c11-08f7-456a-922c-b94a318f9d85" /></p>

Por otra parte, aunque ocultar el SSID no es una medida de seguridad fuerte por sí sola, puede aplicarse como capa adicional de protección básica.

<p align="center"><img width="799" height="138" alt="Screenshot_11" src="https://github.com/user-attachments/assets/98b5d719-8854-42d1-9b44-1093e5909863" /></p>

Finalmente, como mejora adicional, se puede considerar la creación de una red de invitados separada, con acceso limitado a la red interna, para aislar dispositivos externos del entorno principal.

---
### 3.4. ***Conclusión***
---

La red WiFi es uno de los puntos más críticos en cualquier infraestructura, ya que suele ser la principal vía de acceso a la red interna.

Una mala configuración en este apartado puede comprometer fácilmente todo el sistema, por lo que es fundamental aplicar medidas de seguridad adecuadas como cifrado moderno y contraseñas seguras.

---
## 4. ***Segmentación de red y red de invitados***

En este apartado se analiza la segmentación de la red dentro del router, centrándonos especialmente en la red de invitados y en la separación entre dispositivos dentro del entorno de red.

La segmentación es una medida de seguridad importante, ya que permite aislar distintos tipos de dispositivos y reducir el impacto en caso de que alguno de ellos sea comprometido.

---
### 4.1. ***Estado inicial de la red***
---

En la configuración inicial del router se observa que no existe una segmentación real de la red, ya que la red de invitados no está habilitada.

Esto implica que todos los dispositivos que se conectan al router forman parte de la misma red interna, sin separación entre usuarios habituales y posibles dispositivos externos.

<p align="center"><img width="667" height="810" alt="Screenshot_13" src="https://github.com/user-attachments/assets/1341f7d2-3f3f-44a5-b095-2903786a6f20" /></p>

---
### 4.2. ***Riesgos asociados***
---

La ausencia de segmentación de red supone varios riesgos importantes.

En primer lugar, cualquier dispositivo que se conecte a la red principal puede tener acceso potencial al resto de dispositivos conectados, lo que aumenta el impacto de una posible infección o acceso no autorizado.

Además, si un dispositivo externo comprometido accede a la red WiFi, podría comunicarse con otros equipos internos, facilitando movimientos laterales dentro de la red.

Esto significa que un único dispositivo vulnerable podría comprometer la seguridad del resto de la infraestructura.

---
### 4.3. ***Medidas de mejora aplicadas***
---

Para mejorar esta situación, se propone habilitar una red de invitados independiente del resto de la red interna.

Esta red debe configurarse de forma que:

- No tenga acceso a la red local.
- Solo permita acceso a Internet.
- Mantenga aislamiento entre clientes conectados.

<p align="center"><img width="798" height="508" alt="Screenshot_12" src="https://github.com/user-attachments/assets/752f4e25-ded6-465d-b019-34d2655fa0c2" /></p>

De esta forma, los dispositivos externos o no confiables pueden conectarse a Internet sin comprometer la seguridad de la red principal.

En entornos más avanzados, esta segmentación se puede complementar con VLANs, separando diferentes tipos de dispositivos según su función o nivel de confianza.

---
### 4.4. ***Conclusión***
---

La segmentación de red es una medida fundamental dentro de la seguridad de redes, ya que permite limitar el alcance de posibles ataques.

Sin una correcta separación entre dispositivos, cualquier compromiso dentro de la red puede extenderse fácilmente al resto de equipos conectados.

---
## 5. ***Servicios y protocolos inseguros***

En este apartado se analizan los distintos servicios y protocolos que pueden estar activos en el router y que, en caso de no estar correctamente configurados, pueden suponer un riesgo de seguridad.

Muchos routers incluyen funcionalidades activadas por defecto que facilitan la conectividad, pero que no siempre son necesarias en un entorno seguro.

---
### 5.1. ***Estado inicial de los servicios***
---

En la configuración inicial del router se observa que algunos servicios están habilitados por defecto sin una necesidad clara de uso.

Uno de los elementos más relevantes es UPnP (Universal Plug and Play), que permite a los dispositivos de la red abrir puertos de forma automática en el router. Aunque esto facilita el uso de ciertas aplicaciones, también puede ser un problema de seguridad si un dispositivo malicioso solicita la apertura de puertos sin control del usuario.

<p align="center"><img width="1003" height="498" alt="Screenshot_14" src="https://github.com/user-attachments/assets/bd099992-e838-4128-af55-5eea9dcad9f5" /></p>

También se observa la presencia de opciones relacionadas con la WAN y servicios externos, lo que puede implicar exposición de ciertos servicios si no se restringen adecuadamente.

---
### 5.2. ***Riesgos asociados***
---

El principal riesgo de estos servicios es la apertura automática o innecesaria de puertos en el router, lo que puede aumentar la superficie de ataque del sistema.

En el caso de UPnP, un dispositivo infectado dentro de la red podría solicitar la apertura de puertos hacia el exterior sin que el usuario lo detecte, facilitando posibles accesos no autorizados.

Además, si existen servicios expuestos en la WAN sin control adecuado, el router puede quedar accesible desde Internet, lo que incrementa el riesgo de ataques externos.

---
### 5.3. ***Medidas de mejora aplicadas***
---

Para mejorar la seguridad en este apartado, se recomienda desactivar UPnP en caso de no ser estrictamente necesario.

<p align="center"><img width="1001" height="498" alt="Screenshot_15" src="https://github.com/user-attachments/assets/236b5a10-c579-454b-a4fc-3307e66ebe2d" /></p>

En su lugar, es preferible realizar la apertura de puertos de forma manual, controlando exactamente qué servicios se exponen al exterior.

También es recomendable revisar los servicios accesibles desde la WAN y limitar al máximo aquellos que no sean necesarios.

De forma adicional, se puede reforzar la seguridad configurando correctamente los servidores DNS y evitando el uso de configuraciones automáticas no controladas.

---
### 5.4. ***Conclusión***
---

Los servicios y protocolos activos en un router pueden suponer un riesgo importante si no se gestionan correctamente.

Reducir los servicios innecesarios y controlar manualmente las conexiones externas ayuda a disminuir la superficie de ataque y mejora significativamente la seguridad general de la red.

---
## 6. ***Firewall y protección del sistema***

En este apartado se analiza la configuración del firewall del router y las medidas de protección que ofrece el sistema frente a accesos no autorizados y tráfico potencialmente malicioso.

El firewall es una de las capas principales de seguridad en un router, ya que se encarga de filtrar el tráfico de red y controlar qué conexiones se permiten o se bloquean.

---
### 6.1. ***Estado inicial del firewall***
---

En la configuración inicial del router se observa que el firewall no tiene reglas personalizadas definidas y que la protección adicional del sistema no está completamente activada.

En particular, no se han configurado reglas específicas de filtrado de tráfico, lo que significa que el comportamiento del firewall se basa en configuraciones generales del sistema.

<p align="center"><img width="799" height="746" alt="Screenshot_16" src="https://github.com/user-attachments/assets/a08ecb4b-3be8-4f3d-afca-618adb22b5ab" /></p>

También se detecta que la protección contra ataques DoS (Denial of Service) no está activada, lo que reduce la capacidad del router para mitigar ciertos tipos de ataques de saturación.

<p align="center"><img width="999" height="484" alt="Screenshot_17" src="https://github.com/user-attachments/assets/4e297cc5-08ef-4217-bb0b-5b14b0442978" /></p>

---
### 6.2. ***Riesgos asociados***
---

La ausencia de reglas de firewall personalizadas puede permitir tráfico no deseado hacia o desde la red sin un control específico.

Esto puede ser especialmente problemático si existen servicios expuestos o configuraciones inseguras en otros apartados del router.

Por otro lado, si la protección contra ataques DoS no está activada, el dispositivo puede ser más vulnerable a intentos de saturación de tráfico, lo que podría afectar al rendimiento de la red o incluso provocar caídas del servicio.

---
### 6.3. ***Medidas de mejora aplicadas***
---

Para mejorar la seguridad en este apartado, se recomienda activar la protección DoS del sistema, lo que permite mitigar parte de los ataques de saturación más comunes.

<p align="center"><img width="996" height="485" alt="Screenshot_18" src="https://github.com/user-attachments/assets/4387a892-5db4-41db-a20a-d3d4b9c96e4a" /></p>

También es recomendable definir reglas básicas de firewall que permitan controlar el tráfico entrante y saliente de la red, limitando únicamente los servicios necesarios.

En entornos más avanzados, estas reglas pueden adaptarse en función del tipo de dispositivos conectados y del nivel de confianza de cada segmento de red.

---
### 6.4. ***Conclusión***
---

El firewall es una de las piezas clave en la seguridad de cualquier red, ya que actúa como barrera entre la red interna y posibles amenazas externas.

Una configuración básica o incompleta puede dejar expuesto el sistema a múltiples riesgos, por lo que es importante ajustarlo correctamente y activar todas las medidas de protección disponibles.

---
## 7. ***Actualización y mantenimiento del firmware***

En este apartado se analiza el estado de actualización del firmware del router y la importancia del mantenimiento del sistema como parte de la seguridad general del dispositivo.

El firmware es el software interno del router, y su correcta actualización es fundamental para corregir vulnerabilidades y mejorar la seguridad del sistema.

---
### 7.1. ***Estado inicial del firmware***
---

En la configuración inicial del router se observa que el firmware no se encuentra actualizado desde el año 2020.

<p align="center"><img width="1003" height="676" alt="Screenshot_19" src="https://github.com/user-attachments/assets/6ba4d80b-2049-4af4-a348-4fd51c7415fb" /></p>

Esto implica que el dispositivo no dispone de las actualizaciones de seguridad publicadas posteriormente por el fabricante, lo que puede dejarlo expuesto a vulnerabilidades conocidas que ya han sido corregidas en versiones más recientes.

---
### 7.2. ***Riesgos asociados***
---

El uso de un firmware desactualizado supone uno de los riesgos más importantes dentro de la seguridad de un router.

En primer lugar, pueden existir vulnerabilidades conocidas que han sido publicadas y documentadas, lo que facilita que un atacante pueda explotarlas si el dispositivo está accesible.

Además, la falta de actualizaciones puede implicar también la ausencia de mejoras en los sistemas de protección, lo que reduce la eficacia de otras medidas de seguridad configuradas en el router.

---
### 7.3. ***Medidas de mejora aplicadas***
---

Para mejorar la seguridad en este apartado, se recomienda actualizar el firmware del router a la última versión disponible proporcionada por el fabricante.

<p align="center"><img width="998" height="719" alt="Screenshot_20" src="https://github.com/user-attachments/assets/46d2541f-60aa-4693-a7f2-4a7a97b320cd" /></p>

Es importante realizar estas actualizaciones de forma periódica, ya que no solo corrigen fallos de seguridad, sino que también pueden mejorar el rendimiento y la estabilidad del sistema.

En entornos más críticos, se puede establecer un mantenimiento programado para revisar regularmente la existencia de nuevas versiones de firmware.

---
### 7.4. ***Conclusión***
---

El mantenimiento del firmware es un aspecto clave dentro de la seguridad de cualquier dispositivo de red.

Mantener el sistema actualizado reduce significativamente el riesgo de explotación de vulnerabilidades y es una de las medidas más efectivas dentro del hardening de routers.

---
## 8. ***Conclusiones***

En este trabajo se ha realizado un análisis completo de la seguridad de un router doméstico, evaluando diferentes aspectos relacionados con su configuración y posibles vulnerabilidades.

A lo largo del proyecto se han identificado varias debilidades importantes, como el uso de credenciales débiles, la falta de actualización del firmware, la activación de servicios innecesarios como UPnP o WPS, y la ausencia de segmentación de red adecuada.

También se ha podido comprobar cómo pequeñas configuraciones mal establecidas pueden afectar directamente a la seguridad global de la red, permitiendo posibles accesos no autorizados o aumentando la superficie de ataque del sistema.

Como resultado, se han propuesto diferentes medidas de mejora orientadas a reforzar la seguridad del router, como el uso de contraseñas robustas, la actualización del firmware, la desactivación de servicios no necesarios, la implementación de redes de invitados y la correcta configuración del firewall.

En conclusión, el hardening de un router es un proceso fundamental dentro de la seguridad de redes, ya que permite reducir riesgos y proteger tanto el dispositivo como la red a la que da acceso. Una configuración adecuada puede marcar una gran diferencia en la protección frente a amenazas externas.

---
## 9. ***Anexo I. Hardening básico de un router ASUS (panel de administración)***

Este anexo recoge un análisis de distintas recomendaciones de seguridad aplicables a routers domésticos ASUS, basadas en buenas prácticas generales de configuración y seguridad.

La idea es revisar algunas medidas habituales y valorar su utilidad real dentro de un entorno doméstico, teniendo en cuenta tanto la seguridad como la facilidad de uso.

---
### 1. ***Acceso remoto desde WAN***
---

Una de las opciones que suelen incluir los routers es la posibilidad de acceder al panel de administración desde Internet.

Aunque puede ser útil en algunos casos, normalmente en entornos domésticos no es necesario, y puede suponer un riesgo de seguridad si queda expuesto a ataques desde el exterior.

Por este motivo, lo más recomendable es mantener esta opción desactivada si no se va a utilizar.

---
### 2. ***Servicios de administración adicionales***
---

Algunos routers incluyen servicios como Telnet o SSH, o herramientas de diagnóstico que no siempre son visibles en la configuración principal.

Estos servicios pueden ser útiles en ciertos casos, pero si no se utilizan, lo más seguro es desactivarlos, ya que pueden aumentar la superficie de ataque del dispositivo.

---
### 3. ***Configuración de DNS***
---

El uso de servidores DNS seguros es una recomendación habitual para mejorar la seguridad de la navegación.

Configurar manualmente DNS de confianza puede ayudar a evitar ciertos ataques relacionados con la resolución de nombres o redirecciones no deseadas.

Sin embargo, en muchos casos los routers utilizan automáticamente los DNS del proveedor de Internet, lo que puede limitar el control del usuario sobre este aspecto.

---
### 4. ***Registro de eventos (logging)***
---

Los registros del sistema del router permiten ver lo que ocurre en la red, como intentos de conexión o cambios en la configuración.

Aunque no siempre se revisan, pueden ser útiles para detectar comportamientos extraños o posibles problemas de seguridad.

Por eso es recomendable tenerlos activados si el dispositivo lo permite.

---
### 5. ***Cifrado del panel de administración***
---

En algunos routers, el acceso al panel de administración puede hacerse mediante HTTP en lugar de HTTPS.

Esto puede suponer un problema, ya que la información viaja sin cifrar dentro de la red y podría ser interceptada.

Por ello, es recomendable utilizar siempre HTTPS cuando esté disponible.

---
### 6. ***Servicios en la nube y aplicaciones móviles***
---

Algunos routers incluyen funciones en la nube o aplicaciones móviles para facilitar la gestión del dispositivo.

Aunque son cómodas, también implican depender de servicios externos, lo que puede no ser ideal desde el punto de vista de la seguridad.

En caso de no ser necesarias, es mejor desactivarlas.

---
### 7. ***Conclusión***
---

En general, el hardening de un router no consiste solo en cambiar contraseñas o actualizar el firmware, sino en revisar todas las opciones disponibles y desactivar aquellas que no sean necesarias.

Muchas veces los riesgos vienen de funciones que están activadas por defecto y que el usuario no utiliza, por lo que es importante hacer una revisión completa de la configuración.
