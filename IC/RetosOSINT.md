<h1 align="center">Retos OSINT</h1>

<p align="center">
  <img src="https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/IC/images/bannerPortada.png" alt="Portada OSINT">
</p>

**Fecha:** 28 de enero de 2026  
**Autor:** Sergio González  

---

## Índice

1. [Introducción](#1-introducción)
2. [Caso 1 – Jirafa en peligro de extinción](#2-caso-1--jirafa-en-peligro-de-extinción)
3. [Caso 2 – Verificación de un tweet sobre ataque en Pakistán](#3-caso-2--verificación-de-un-tweet-sobre-ataque-en-pakistán)
4. [Caso 3 – Identificación de una estación de tren](#4-caso-3--identificación-de-una-estación-de-tren)
5. [Caso 4 – Geolocalización de un video en Tirana](#5-caso-4--geolocalización-de-un-video-en-tirana)

---
## 1. ***Introducción***

En este documento se presentan varios casos prácticos en los que se analiza información que se puede encontrar públicamente en Internet.

Cada caso tiene un objetivo distinto y se resuelve utilizando herramientas OSINT para buscar, recopilar y analizar información. En los apartados siguientes se muestra el proceso seguido en cada uno de ellos, junto con los resultados obtenidos y las conclusiones más relevantes.

---
## 2. ***Caso 1 – Jirafa en peligro de extinción***

En este caso se nos proporciona una imagen de una jirafa recién nacida. El objetivo es averiguar su lugar y fecha de nacimiento, su residencia actual y obtener evidencia visual de su hábitat.

<p align="center">
  <img width="300" height="505" alt="Jirafa Willow" src="https://github.com/user-attachments/assets/85bb0d95-3a83-4112-8265-8d41bb25486b" />
</p>

### Planificación
Para resolverlo decidí:  
- Realizar una **búsqueda inversa de la imagen** para localizar su origen.  
- Buscar información en noticias, blogs y páginas de zoológicos sobre el nacimiento y traslado del animal.  
- Confirmar su nombre y residencia actual.  
- Localizar imágenes o videos recientes que muestren a la jirafa en su hábitat.

### Ejecución
- La búsqueda inversa en **TinEye** indicó que la foto original estaba en [Zooborns](https://zooborns.com/2009/10/27/baby-giraffe-calf-at-the-virginia-zoo/), confirmando que nació en el **Virginia Zoo, Norfolk, Virginia, EE. UU., el 21 de octubre de 2009**.

<img width="1163" height="1020" alt="image" src="https://github.com/user-attachments/assets/0ea7cdb2-3cf9-415c-a0c1-e71b7e2c4475" />

- Investigando más, encontré que se llama **Willow**. Para ello hice una búsqueda en Google con las palabras `"giraffe 2009 naming poll virginia zoo"` y encontré un artículo que confirma que fue trasladada a **Disney’s Animal Kingdom, Florida**, llegando allí el **12 de octubre de 2010** ([The Pocomoke Public Eye](https://thepocomokepubliceye.blogspot.com/2010/10/virginia-zoo-giraffe-calf-failed-to.html)).

<img width="1267" height="1020" alt="image" src="https://github.com/user-attachments/assets/2337de65-2edb-43a0-952d-092b1bed5736" />

- Para confirmar su ubicación actual, localicé un video en YouTube que la muestra en su hábitat en Disney: [Video de Willow](https://www.youtube.com/shorts/DZ4A3dkiKs8).

<img width="545" height="811" alt="image" src="https://github.com/user-attachments/assets/ebee0f9f-770c-4a75-8385-0702c7331c54" />

### Análisis y comentarios
El caso se resolvió combinando búsqueda inversa de imagen, palabras clave en motores de búsqueda y revisión de fuentes secundarias. La evidencia encontrada permite confirmar tanto el nacimiento como la residencia actual y proporciona soporte visual reciente.

### Tabla resumen

| Pregunta | Respuesta |
|--------|----------|
| Lugar y fecha de nacimiento | Virginia Zoo, Norfolk, Virginia, EE.UU (21 octubre 2009) |
| Residencia actual | Disney’s Animal Kingdom, Florida, EE.UU |
| Fecha de llegada | 12 octubre 2010 |
| Fotografía en su hábitat actual | [Video mostrando a Willow](https://www.youtube.com/shorts/DZ4A3dkiKs8) |

---
## 3. ***Caso 2 – Verificación de un tweet sobre ataque en Pakistán***

En este caso se analiza un tweet publicado el 19 de enero de 2023 por un periodista con casi 140.000 seguidores. En el tweet aparece la imagen de un vehículo destruido entre humo y fuego, acompañada del mensaje:  
“#BREAKING: TTP carried out a suicide attack on a police post in Khyber city of Pakistan that killed three Pakistani police officers”.  
El objetivo es comprobar si la imagen corresponde realmente al hecho descrito.

<p align="center">
  <img width="400" height="523" alt="image" src="https://github.com/user-attachments/assets/fc75bac3-e959-468f-9513-44577aac61ff" />
</p>

### Planificación
Para resolver este caso decidí:  
- Localizar el tweet original utilizando búsquedas avanzadas en Twitter.  
- Analizar la imagen del tweet mediante búsqueda inversa para comprobar su origen.  
- Buscar páginas y artículos que dieran contexto a la imagen encontrada.  
- Comparar la información obtenida con la fecha y el lugar indicados en el tweet.

### Ejecución
- Para localizar el tweet, utilicé la **búsqueda avanzada de Twitter**, introduciendo el texto exacto del mensaje en el campo *“This exact phrase”*:  
  `#BREAKING: TTP carried out a suicide attack on a police post in Khyber city of Pakistan that killed three Pakistani police officers`.
  De esta forma pude encontrar el ***[tweet original](https://x.com/TajudenSoroush/status/1616108524026617856)*** publicado por el periodista.

  <img width="1269" height="1020" alt="image" src="https://github.com/user-attachments/assets/4abc407f-064d-4bb1-9dac-d8cbe0a36e87" />

- Tras localizar el tweet original y descargar la imagen, realicé una **búsqueda inversa con TinEye Reverse Image Search**. Los resultados llevaron a un artículo de ***[qafqazinfo.az](https://qafqazinfo.az/news/detail/iraqda-silahli-hucum-12-nefer-olduruldu-161018)*** donde aparece un vehículo destruido muy similar al de la imagen del tweet. En este caso, el artículo hace referencia a un **ataque ocurrido en Tikrit, Irak, en 2016**, lo que demuestra que la fotografía no corresponde al supuesto ataque en Khyber, Pakistán, en 2023 y fue utilizada fuera de contexto.

<img width="1264" height="1020" alt="image" src="https://github.com/user-attachments/assets/f6763b30-1205-4461-9d38-a7a3382a6e33" />

### Análisis y comentarios
El caso se resolvió localizando primero el tweet mediante búsqueda avanzada en Twitter y, posteriormente, verificando la imagen con búsqueda inversa y fuentes abiertas. La evidencia encontrada demuestra que la foto **fue usada fuera de contexto** y no corresponde al ataque ocurrido en Khyber, Pakistán, en enero de 2023.

### Tabla resumen

| Pregunta | Respuesta |
|--------|----------|
| Verificación del tweet | La foto **no corresponde al ataque descrito en Pakistán**; pertenece a un ataque ocurrido en Irak en 2016 y fue usada fuera de contexto |

---
## 4. ***Caso 3 – Identificación de una estación de tren***

En este caso se nos proporciona una imagen compartida en redes sociales donde se puede ver claramente una estación de tren. El objetivo es identificar el nombre de la estación y averiguar cuál es la estructura más alta que aparece en la imagen, indicando también su altura.

<p align="center">
  <img width="600" height="444" alt="image" src="https://github.com/user-attachments/assets/432cc43a-d54c-4803-911b-41c4d0d54969" />
</p>

### Planificación
Para resolver este caso decidí:
- Fijarme bien en la imagen para ver si aparecía algún nombre o cartel.
- Utilizar **Google Maps** y **Street View** para localizar la estación.
- Comparar los edificios que se ven en la foto con el entorno real.
- Identificar cuál de esas estructuras es la más alta y buscar su altura en Internet.

### Ejecución
- Al observar la imagen, se distingue claramente el cartel de **“Flinders Street”**, lo que permitió identificar la estación como **Flinders Street Station**, situada en **Melbourne, Australia**.

<img width="1269" height="1020" alt="image" src="https://github.com/user-attachments/assets/fcc9d286-f07d-4200-9fb3-5532cadaf026" />

- Para asegurarme, busqué la estación en **Google Maps** y utilicé **Street View**, comprobando que tanto la fachada como el entorno coinciden con la imagen proporcionada.

<img width="1269" height="1020" alt="image" src="https://github.com/user-attachments/assets/cff6075a-ae3b-4df9-a016-e8f00775521a" />

- Una vez localizada la estación, analicé los edificios que se ven detrás utilizando Google Maps y Google Earth. Comparando la imagen con el skyline de Melbourne, se identificó como estructura más alta visible el edificio **Focus Apartments (también conocido como Focus Melbourne)**. Buscando información pública sobre este edificio, se comprobó que tiene una altura aproximada de **167 metros**.

<img width="1266" height="757" alt="image" src="https://github.com/user-attachments/assets/0ab85d19-eae3-4b93-9c3e-7ce6a503f6a6" />

### Análisis y comentarios
Este caso se resolvió principalmente mediante observación y el uso de Google Maps. El cartel visible en la estación facilitó mucho la identificación y la comparación del skyline permitió determinar la estructura más alta sin necesidad de herramientas más avanzadas.

### Tabla resumen

| Pregunta | Respuesta |
|--------|----------|
| Nombre de la estación | Flinders Street Station (Melbourne, Australia) |
| Estructura más alta visible | Focus Apartments (Focus Melbourne) |
| Altura de la estructura | 167 metros |

---
## 5. ***Caso 4 – Geolocalización de un video en Tirana***

En este caso se nos proporciona un video publicado por la cuenta de Twitter **@VisitTirana** el 16 de febrero de 2023. En él se ve a una persona caminando por una calle de Tirana. Nuestro objetivo es:  
a) Estimar a qué hora se grabó el video.  
b) Determinar las coordenadas exactas de dónde caminaba la persona en ese momento.

<p align="center">
  <img width="400" alt="Captura del video" src="https://gralhix.com/wp-content/uploads/2023/08/osintexercise009.png" />
</p>

### Planificación
Para resolver este caso decidí:  
- Analizar la captura del video para identificar edificios, farolas, señales u otros puntos reconocibles.  
- Revisar la hora de publicación del tweet y comparar con la **iluminación y sombras** del video para estimar la hora de grabación.  
- Usar **Google Maps** y **Street View** para localizar la calle exacta y confirmar la ubicación.  
- Consultar la **hora de la puesta de sol en Tirana** para corroborar la estimación.  
- Tomar las coordenadas exactas una vez identificado el lugar.

### Ejecución
- Primero, localicé el ***[tweet original](https://x.com/VisitTirana/status/1626342426318077963)***. La publicación indica **11:07 PM**, pero esto solo refleja la hora de subida, no la grabación.  

<img width="1269" height="1020" alt="tweet original" src="https://github.com/user-attachments/assets/7ff0cb9f-568a-4730-8164-74f926c9a491" />

- Observando la captura del video, identifiqué varios elementos clave: edificios con fachadas distintivas, farolas y señales. Con **Google Maps / Street View** comparé estos detalles y logré ubicar la calle exacta: **Rruga e Kavajës con Rruga 28 Nëntori, Tirana, Albania**. Registré las coordenadas: **41.3268985° N, 19.8069296° E**.  

<img width="1272" height="1020" alt="geolocalización en street view" src="https://github.com/user-attachments/assets/e13d43b3-25b3-4a1e-b990-e718327a4d6c" />

- Para estimar la hora real de grabación, comparé la **iluminación y sombras visibles en el video** con la posición del sol en Tirana el 16 de febrero. Según los datos de [Time and Date](https://www.timeanddate.com/sun/albania/tirana?month=2&year=2023), la puesta de sol ocurre a las **18:47**. Observando la luz en el video (sombras largas, dirección de la luz y color), concluí que la grabación se realizó unas **2 horas antes de la puesta de sol**, aproximadamente a las **16:47–16:50**, coincidiendo con la luz de la tarde.

<img width="1266" height="1020" alt="image" src="https://github.com/user-attachments/assets/fbe8eb0f-6ced-47cd-ac1c-f5a8b1751493" />

### Análisis y comentarios
Este caso se resolvió combinando **observación visual**, **comparación con Google Maps / Street View** y **verificación de la posición del sol**. La tabla de luz solar permite justificar la estimación de la hora, mostrando que la grabación ocurrió alrededor de **16:47–16:50**, justo antes de que el sol se pusiera. Este análisis demuestra cómo se puede geolocalizar un video incluso sin metadatos completos.

### Tabla resumen

| Pregunta | Respuesta |
|--------|----------|
| Hora aproximada de grabación | 16:47–16:50 (hora local de Tirana, 16 febrero 2023) |
| Coordenadas del lugar | 41.3268985° N, 19.8069296° E |
