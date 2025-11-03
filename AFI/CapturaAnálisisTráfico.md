<h1 align="center">Captura y Análisis de Tráfico de Red en Conexiones HTTP</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/bannerPortada.png)

***Fecha:*** 03 de noviembre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Preparación de la Herramienta](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/CapturaAn%C3%A1lisisTr%C3%A1fico.md#1-preparaci%C3%B3n-de-la-herramienta)***
2. ***[Captura de Tráfico](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/CapturaAn%C3%A1lisisTr%C3%A1fico.md#2-captura-de-tr%C3%A1fico)***
3. ***[Conexión a un Sitio Web](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/CapturaAn%C3%A1lisisTr%C3%A1fico.md#3-conexi%C3%B3n-a-un-sitio-web)***
4. ***[Análisis del Tráfico Capturado](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/CapturaAn%C3%A1lisisTr%C3%A1fico.md#4-an%C3%A1lisis-del-tr%C3%A1fico-capturado)***
5. ***[Informe y Conclusiones](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/CapturaAn%C3%A1lisisTr%C3%A1fico.md#5-informe-y-conclusiones)***

---

## 1. ***Preparación de la Herramienta***

En primer lugar, procedemos a preparar el entorno de trabajo utilizando una máquina virtual con Kali Linux, sistema operativo especializado en ciberseguridad. Dentro de este entorno instalamos y configuramos Wireshark, herramienta que emplearemos para la captura y análisis del tráfico de red.

- En primer lugar, como he dicho anteriormente, vamos a descargar e instalar wireshark en nuestro sistema. Para ello, ejecutamos el siguiente comando:

```bash
sudo apt install wireshark
```

![Imágen Captura Tráfico 1](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/capturaAn%C3%A1lisisTr%C3%A1fico1.png)

- Comprobamos que se ha instalado correctamente el paquete, ejecutamos el siguiente comando:

```bash
wireshark --version
```

![Imágen Captura Tráfico 2](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/capturaAn%C3%A1lisisTr%C3%A1fico2.png)
> Como podemos ver, se ha instalado correctamente la versión 4.4.9. de Wireshark.

- Por último, podemos ejecutar Wireshark desde el siguiente comando:

![Imágen Captura Tráfico 3](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/capturaAn%C3%A1lisisTr%C3%A1fico3.png)

![Imágen Captura Tráfico 4](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/capturaAn%C3%A1lisisTr%C3%A1fico4.png)

> El símbolo "**&**" nos permite ejecutar Wireshark y ponerlo en segundo plano, para poder seguir usando la terminal.

---
## 2. ***Captura de Tráfico***

En este apartado, se explicará como capturar tráfico HTTP mediante dicha herramienta. Partimos desde el anterior apartado, con la herramienta ejecutada y lista para usarla.

- Primero, elegiremos la interfaz que queremos utilizar para la captura de paquetes de dicha red. En mi caso elegire la interfaz eth0, que es la red que tiene acceso a internet.

![Imágen Captura Tráfico 5](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/capturaAn%C3%A1lisisTr%C3%A1fico5.png)

![Imágen Captura Tráfico 6](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/capturaAn%C3%A1lisisTr%C3%A1fico6.png)
> En la última imágen, se muestra como la herramienta Wireshark captura todos los paquetes de la red que hemos elegido.

- Por último, vamos a preparar la herramienta para el siguiente apartado. Vamos a filtra los paquetes de la red, mostrando solo los paquetes que sean por el protocolo HTTP. Para ello, utilizaremos lo filtros que nos proporciona Wireshark.

![Imágen Captura Tráfico 7](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/AFI/images/capturaAn%C3%A1lisisTr%C3%A1fico7.png)

---
## 3. ***Conexión a un Sitio Web***



---
## 4. ***Análisis del Tráfico Capturado***



---
## 5. ***Informe y Conclusiones***

