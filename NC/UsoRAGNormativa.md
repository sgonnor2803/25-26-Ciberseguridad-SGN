<h1 align="center">Uso de RAG para consultas sobre normativa</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/NC/images/bannerPortada.jpg)

***Fecha:*** 30 de octubre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Investigar sanciones caso](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/NC/UsoRAGNormativa.md#1-investigar-sanciones-caso)***
2. ***[Desarrollar un caso práctico](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/NC/UsoRAGNormativa.md#2-desarrollar-un-caso-pr%C3%A1ctico)***

---

## 1. ***Investigar sanciones caso***

Estas son las sanciones más importantes que pueden ser aplicables a la intrusión en servidores que contienen datos personales:

- ***Violación de Principios Fundamentales ([Art. 83.5 RGPD](https://eur-lex.europa.eu/legal-content/ES/TXT/?uri=CELEX%3A32016R0679#d1e2750-1-1))***

Sanción por infracciones relativas a los principios básicos para el tratamiento (Art. 5 RGPD), lo cual incluye la violación de la integridad y confidencialidad de los datos

- ***Violación de Integridad y Confidencialidad ([Art. 72.1.g LOPDGDD](https://www.boe.es/buscar/act.php?id=BOE-A-2018-16673#a7-4))***

El tratamiento de datos personales vulnerando los principios y garantías establecidos en el artículo 5 del RGPD, incluyendo la violación del principio de integridad y confidencialidad.

- ***Fallos en la Seguridad ([Art. 83.4 RGPD](https://eur-lex.europa.eu/legal-content/ES/TXT/?uri=CELEX%3A32016R0679#d1e2689-1-1))***

Sanción por infracciones de las obligaciones del responsable y del encargado relativas a la seguridad del tratamiento (Art. 32 RGPD), es decir, la falta de implementación de medidas técnicas y organizativas apropiadas para garantizar un nivel de seguridad adecuado al riesgo.

- ***Quebrantamiento de Medidas Técnicas ([Art. 73.1.g LOPDGDD](https://www.boe.es/buscar/act.php?id=BOE-A-2018-16673#a7-5))***

El quebrantamiento, como consecuencia de la falta de la debida diligencia, de las medidas técnicas y organizativas que se hubiesen implantado conforme a lo exigido por el artículo 32.1 del RGPD.

- ***Indemnización a los Afectados ([Art. 82.1 RGPD](https://eur-lex.europa.eu/legal-content/ES/TXT/?uri=CELEX%3A32016R0679#d1e2593-1-1))***

Derecho de toda persona a recibir indemnización por los daños y perjuicios materiales o inmateriales sufridos como consecuencia de una infracción del RGPD.

- ***Multa Fija y Prohibición de Operación ([Art. 39.1.a LSSI](https://www.boe.es/buscar/act.php?id=BOE-A-2002-13758#a39))***

Multa administrativa aplicable a prestadores de servicios de la sociedad de la información por infracciones Muy Graves. Incluye la posible prohibición de actuación en España (máximo de dos años) si hay reiteración de infracciones muy graves.

- ***Publicación del Infractor ([Art. 39.4.a LSSI](https://www.boe.es/buscar/act.php?id=BOE-A-2002-13758#a39))***

Las infracciones graves y muy graves podrán llevar aparejada la publicación de la resolución sancionadora en el "Boletín Oficial del Estado" o en la página de inicio del sitio de Internet del prestador, una vez que aquella tenga carácter firme.

## 2. ***Desarrollar un caso práctico***

### Descripción del caso
---

La empresa DataSegur S.L., dedicada al almacenamiento de información en la nube para pequeñas empresas, sufre una intrusión en uno de sus servidores.
Un ex empleado, Carlos M., logra acceder utilizando unas credenciales antiguas que la empresa no había eliminado tras su salida. Durante el acceso, copia una base de datos con información personal de unos 2.000 clientes, que incluye nombres, direcciones, números de DNI y datos bancarios.

Posteriormente, intenta vender esa información a través de foros en la dark web. El equipo de seguridad detecta la intrusión una semana después, al observar accesos sospechosos en los registros del sistema. La empresa notifica el incidente a la Agencia Española de Protección de Datos (AEPD) y a los afectados.


### Posibles consecuencias penales y administrativas
---

#### Consecuencias penales (para el ex empleado)

- El acceso sin autorización a un sistema informático que contiene datos personales constituye un delito de descubrimiento y revelación de secretos, según el ***artículo 197*** del Código Penal.
- Por haber accedido, copiado y tratado de vender información personal, Carlos M. podría enfrentarse a una pena de prisión de 1 a 4 años y a una multa de 12 a 24 meses.
- Además, los afectados podrían reclamar indemnización por los daños y perjuicios ocasionados (***artículo 82 del RGPD***).


#### Consecuencias administrativas (para la empresa)

- La empresa DataSegur S.L. podría ser sancionada por no aplicar las medidas técnicas y organizativas adecuadas para proteger los datos (***artículo 32 del RGPD***).
- Estas infracciones pueden suponer multas de hasta 10 millones de euros o el 2% del volumen de negocio anual, según el ***artículo 83.4 del RGPD***.
- Según la LOPDGDD (***art. 72.1.g***), también se consideraría una infracción muy grave por vulnerar el principio de integridad y confidencialidad.
- Además, la AEPD podría exigir la publicación de la sanción y la notificación pública del incidente, afectando a la reputación de la empresa.

