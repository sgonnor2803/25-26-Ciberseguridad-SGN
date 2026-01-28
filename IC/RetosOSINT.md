<h1 align="center">Retos OSINT</h1>

<p align="center">
  <img src="https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/IC/images/bannerPortada.png" alt="Portada OSINT">
</p>

**Fecha:** 28 de enero de 2026  
**Autor:** Sergio González  

---

## Índice

1. [Introducción](#introducción)
2. [Caso 1 – Jirafa en peligro de extinción]()
3. [Caso 2 – Verificación de un tuit sobre ataque en Pakistán]()
4. [Caso 3 – XXXXX](#caso-3--xxxxx)
5. [Caso 4 – XXXXX](#caso-4--xxxxx)
6. [Conclusiones finales](#conclusiones-finales)

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
## 3. ***Caso 2 – Verificación de un tuit sobre ataque en Pakistán***

En este caso tenemos un tuit de un periodista con casi 140.000 seguidores que muestra un vehículo destruido entre humo y fuego. El tuit dice que hubo un ataque suicida del TTP en un puesto policial en Khyber, Pakistán, el 19 de enero de 2023, en el que murieron tres policías. Nuestro objetivo es comprobar si la foto realmente corresponde a ese hecho.

### Planificación
Para resolverlo decidí:  
- Buscar la imagen en fuentes abiertas y ver de dónde venía realmente.  
- Revisar páginas web y artículos que pudieran dar contexto a la foto.  
- Comparar lo que encontrara con la fecha y el lugar que dice el tuit.  
- Determinar si la foto es del ataque o si se estaba usando fuera de contexto.

### Ejecución
- Primero miré la página de ***[Wikipedia sobre Al‑Qaeda in Iraq](https://en.wikipedia.org/wiki/Al-Qaeda_in_Iraq)*** para ver si había alguna relación con la foto o el evento. Allí solo se habla de Irak entre 2004 y 2006, así que no encontré nada sobre Pakistán ni sobre el supuesto ataque de 2023.

- Después revisé el artículo de ***[qafqazinfo.az](https://qafqazinfo.az/news/detail/iraqda-silahli-hucum-12-nefer-olduruldu-161018)***. Allí sí aparece un vehículo destruido, pero corresponde a un **ataque en Tikrit, Irak, en 2016**, nada que ver con Pakistán en 2023.

- Comparando todo, queda claro que la foto **fue usada fuera de contexto**, y que el tuit no mostraba realmente el ataque que decía.

### Análisis y comentarios
El caso se resolvió buscando la fuente de la imagen y comparando con la información disponible en las páginas que revisé. La evidencia indica que la foto **no corresponde al ataque en Khyber, Pakistán, en 2023**, sino a un evento anterior en Irak (2016). Esto sirve como ejemplo de cómo se pueden reutilizar imágenes para engañar en redes sociales.

### Tabla resumen

| Pregunta | Respuesta |
|--------|----------|
| Verificación del tuit | La foto **no corresponde al ataque descrito en Pakistán**; proviene de un ataque en Irak en 2016 y fue usada fuera de contexto |
