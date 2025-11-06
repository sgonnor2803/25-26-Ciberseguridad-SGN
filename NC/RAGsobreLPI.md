<h1 align="center">RAG sobre la LPI. Casos prácticos.</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/NC/images/bannerPortada.jpg)

***Fecha:*** 06 de noviembre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Introducción]()***
2. ***[Casos prácticos detallados]()***
3. ***[Comparativa resultado web Justicio.es]()***

---
## 1. ***Introducción***

Para este proyecto se ha utilizado **NotebookLM** como herramienta de apoyo basada en modelos de recuperación aumentada (*Retrieval-Augmented Generation – RAG*).  
El primer paso fue **subir el texto completo de la Ley de Propiedad Intelectual (LPI)**, concretamente el documento oficial publicado en el BOE:

> **Fuente:** [BOE-A-1996-8930 – Ley de Propiedad Intelectual (versión consolidada)](https://www.boe.es/buscar/act.php?id=BOE-A-1996-8930)

De forma opcional, también se amplió el contexto con la función **“Descubrir fuentes”** de NotebookLM, que permite añadir información relacionada procedente de otros documentos y artículos jurídicos.

A continuación se incluye una **captura de NotebookLM**, donde se muestra la fuente principal (LPI) y el entorno de trabajo configurado para realizar las consultas:

<img width="1919" height="1014" alt="image" src="https://github.com/user-attachments/assets/70c5ceb6-d6b7-44f5-823b-596b8c78033f" />

---
## 2. ***Casos prácticos detallados***

### Caso 1: Derechos de creación artística – "Plagio musical entre Pablo Alborán y Zzoilo"

En 2021 surgió una polémica entre los artistas **Pablo Alborán** y **Zzoilo** por las similitudes entre las canciones *“Tu refugio”* y *“Mon Amour”*. Aunque no llegó a haber una demanda formal, el caso generó debate sobre los límites del **plagio musical** y cómo protege la **Ley de Propiedad Intelectual (LPI)** a los autores.

La LPI, en sus artículos 10 y 17, establece que toda creación original (ya sea una canción, pintura o texto) queda protegida automáticamente desde el momento en que se crea, sin necesidad de registrarla.  
El conflicto surge cuando una nueva obra se parece demasiado a otra anterior, ya que podría considerarse una **vulneración de derechos de autor** si se demuestra que hay copia intencionada o sustancial.

En este caso, se analizaron melodías y estructuras de ambas canciones, concluyendo que las similitudes eran casuales y que no existía plagio. Este ejemplo muestra cómo la LPI protege la **originalidad y la autoría artística**, algo clave en la era digital, donde la difusión de contenidos es masiva y los límites entre inspiración y copia son cada vez más difusos.

---

### Caso 2: Derechos de propiedad industrial – “Apple vs. Samsung por el diseño del iPhone”

Un ejemplo muy conocido en el ámbito de la **propiedad industrial** es el conflicto entre **Apple** y **Samsung**, que empezó en 2011. Apple acusó a Samsung de copiar el diseño y algunas funciones del iPhone, como la forma con bordes redondeados o la disposición de los iconos en pantalla.

Según la **Ley de Propiedad Intelectual** y la **Ley de Patentes**, los diseños industriales y las patentes registradas protegen tanto la **apariencia** como la **innovación técnica** de un producto.  
Apple alegó que Samsung había infringido varias de estas protecciones, utilizando elementos muy similares en sus dispositivos.

Tras varios años de juicios, en 2018 Samsung fue condenada a pagar una indemnización a Apple por violar parte de sus patentes de diseño. Este caso demuestra la importancia de la propiedad industrial para proteger la **innovación tecnológica** y evitar la **competencia desleal**, sobre todo en un sector tan competitivo como el de la electrónica.

---
## 3. ***Comparativa resultado web Justicio.es***

En esta parte del proyecto se ha realizado una comparación entre los resultados obtenidos a través del cuaderno de **NotebookLM**, creado previamente con la **Ley de Propiedad Intelectual (LPI)**, y la información disponible en la web **Justicio.es**.  
El objetivo es comprobar cómo interpreta cada fuente los conceptos de **derechos de autor** y **propiedad industrial**, y analizar las posibles diferencias en la forma de presentar la información.

### Consultas en NotebookLM

A continuación se muestran las respuestas generadas por NotebookLM sobre los casos anteriores.

- ***Caso 1***: Derechos de creación artística

<img width="1331" height="824" alt="image" src="https://github.com/user-attachments/assets/bfb74c7b-5335-4b49-a5f1-2e8a4401b08d" />
<img width="1331" height="816" alt="image" src="https://github.com/user-attachments/assets/a1b048e4-5295-4e9a-b13e-6d3c56b3958a" />
<img width="1329" height="819" alt="image" src="https://github.com/user-attachments/assets/1678a46b-79b4-43b2-a34e-362c462e325d" />
<img width="1330" height="823" alt="image" src="https://github.com/user-attachments/assets/a3817404-1a76-40a5-a1ac-a939471d76e2" />

En resumen, la consulta en NotebookLM sobre el caso de Pablo Alborán y Zzoilo destaca que la Ley de Propiedad Intelectual protege toda obra original y que el plagio se entiende como la copia sustancial de otra creación. También aclara que las similitudes menores o casuales no se consideran infracción si no afectan a la parte esencial de la obra.

- ***Caso 2***: Derechos de propiedad industrial

<img width="1336" height="820" alt="image" src="https://github.com/user-attachments/assets/d3f09b21-4230-4204-b905-f8b35cc275ef" />
<img width="1332" height="819" alt="image" src="https://github.com/user-attachments/assets/9b0d48f7-1cdc-476c-99f1-242b35346f34" />
<img width="1329" height="821" alt="image" src="https://github.com/user-attachments/assets/b697ca00-6cc9-4c28-82d7-9b21fb08ac64" />
<img width="1335" height="822" alt="image" src="https://github.com/user-attachments/assets/2cb256e8-be7c-4381-b1a4-524036dc44e1" />
<img width="1328" height="344" alt="image" src="https://github.com/user-attachments/assets/ea1ec773-1cda-4a4c-81b7-f8205b78c419" />

En resumen, la consulta en **NotebookLM** sobre el caso Apple vs. Samsung destaca que la ley protege tanto la innovación técnica como el diseño original de un producto.
También señala que la infracción de estos derechos puede conllevar indemnizaciones y que ambas protecciones son compatibles y complementarias.

### Consultas en Justicio.es

A continuación se muestran las respuestas generadas por Justicio.es sobre los casos anteriores.

- ***Caso 1***: Derechos de creación artística

<img width="1205" height="825" alt="image" src="https://github.com/user-attachments/assets/f77faccc-b6fd-4dc6-8240-738aa39aa441" />
<img width="1207" height="826" alt="image" src="https://github.com/user-attachments/assets/dd0c724b-71cf-4bd1-95db-ddd4eae73a91" />
<img width="1205" height="829" alt="image" src="https://github.com/user-attachments/assets/7b2d135a-80c0-4baf-94ad-2f863551db04" />
<img width="1204" height="824" alt="image" src="https://github.com/user-attachments/assets/be56fc84-147a-445e-ac2d-d86eace15678" />
<img width="1206" height="750" alt="image" src="https://github.com/user-attachments/assets/c255fc2d-2559-46a1-aae6-92a102723991" />

En resumen, la información obtenida en **Justicio.es** señala que los casos de plagio musical se evalúan según la Ley de Propiedad Intelectual, basándose en la originalidad de la obra y la prueba de una copia sustancial. Solo si se demuestra una similitud significativa y no casual entre las canciones, se consideraría una infracción de derechos de autor.

- ***Caso 2***: Derechos de propiedad industrial

<img width="1206" height="828" alt="image" src="https://github.com/user-attachments/assets/a1a3e444-389c-4f61-8a23-eebb79ba879f" />
<img width="1208" height="770" alt="image" src="https://github.com/user-attachments/assets/8db82965-b233-42d8-9f75-cceda6d6973b" />
<img width="1203" height="833" alt="image" src="https://github.com/user-attachments/assets/cd39f8a9-6b5b-4661-bed4-02ff9f826199" />
<img width="1205" height="757" alt="image" src="https://github.com/user-attachments/assets/fd28d383-b43d-400f-b62a-3d3538010d87" />
<img width="1205" height="748" alt="image" src="https://github.com/user-attachments/assets/b972ad5f-5e88-42b6-9a3e-ae607dbdb113" />
<img width="1115" height="666" alt="image" src="https://github.com/user-attachments/assets/46f8df55-05ad-4a31-aec1-36edf4218750" />
<img width="1186" height="839" alt="image" src="https://github.com/user-attachments/assets/932494e4-4d73-437a-8d8a-01fbddc3f5bf" />

En resumen, según Justicio.es, el caso Apple vs. Samsung se analiza bajo la Ley de Propiedad Industrial e Intelectual, que protege diseños y patentes frente a copias o imitaciones. La legislación española y europea permite a las empresas reclamar daños y defender sus innovaciones, garantizando una competencia justa en el ámbito tecnológico.

## Conclusión comparativa

En resumen, NotebookLM ofrece una visión más clara y explicativa sobre los casos, centrada en interpretar la ley de forma sencilla y comprensible. Por otro lado, Justicio.es aporta un enfoque más técnico y detallado, apoyado directamente en la normativa y jurisprudencia española y europea.

Ambas herramientas coinciden en los puntos clave de la Ley de Propiedad Intelectual e Industrial, aunque difieren en la forma de presentar la información. Mientras NotebookLM facilita la comprensión general, Justicio.es refuerza la precisión legal y el uso de referencias oficiales.
