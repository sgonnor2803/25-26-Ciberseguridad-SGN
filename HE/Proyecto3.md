<h1 align="center">Proyecto 3 - Talent ScoutTech</h1>

![Imagen Presentación](https://github.com/sgonnor2803/25-26-Ciberseguridad-SGN/blob/master/HE/images/bannerPortada.png)

***Fecha:*** 10 de diciembre de 2025
<br>***Autor***: Sergio González

---

## Índice

1. ***[Introducción](#1-introducción)***
2. ***[Despliegue del entorno](#2-despliegue-del-entorno)***
3. ***[Auditoría de seguridad de la aplicación](#3-auditoría-de-seguridad-de-la-aplicación)***
4. ***[Explotación de vulnerabilidades web](#4-explotación-de-vulnerabilidades-web)***
5. ***[Autenticación, control de acceso y sesiones](#5-autenticación-control-de-acceso-y-sesiones)***
6. ***[Seguridad del servidor web](#6-seguridad-del-servidor-web)***
7. ***[Informe de pentesting y mitigaciones](#7-informe-de-pentesting-y-mitigaciones)***
8. ***[Conclusiones](#8-conclusiones)***

---
## 1. ***Introducción***

En este proyecto vamos a auditar la aplicación ***Talent ScoutTech***, que sirve para registrar y evaluar jugadores deportivos. La idea es revisar la seguridad de la aplicación y del servidor, buscando vulnerabilidades como ***SQLi, XSS, fallos de control de acceso o CSRF***, y proponer mejoras.

El objetivo no es solo encontrar los fallos, sino entender cómo se producen, explotarlos de forma controlada y aprender a corregirlos siguiendo buenas prácticas de seguridad y las guías de OWASP. Esto nos permite ver cómo se protege la información de los usuarios y cómo mejorar la seguridad de aplicaciones web en general.

---
## 2. ***Despliegue del entorno***

Para realizar la auditoría de seguridad se ha desplegado la aplicación Talent ScoutTech a partir del archivo `Web_Talent-ScoutTech.zip` proporcionado en el enunciado. El despliegue se ha realizado en un entorno local sobre ***Kali Linux***, utilizando un servidor web Apache, PHP y SQLite3, tal y como se indica en las instrucciones del ejercicio.

### Despliegue en Kali Linux

#### 1. Se instalan los paquetes necesarios para el funcionamiento de la aplicación:

```bash
sudo apt install apache2 php sqlite3 php-sqlite3 -y
```

<img width="601" height="277" alt="image" src="https://github.com/user-attachments/assets/14b88f94-02b5-40d0-b749-d7b205d0e158" />

#### 2. Se arranca el servidor web Apache:

```bash
sudo systemctl start apache2
```

<img width="970" height="555" alt="image" src="https://github.com/user-attachments/assets/9a450d85-ba20-441d-b15c-91240a3bc370" />

#### 3. Se descomprime el archivo `Web_Talent-ScoutTech.zip` en el directorio del servidor web:

```bash
sudo unzip Web_Talent-ScoutTech.zip -d /var/www/html/
```

<img width="972" height="617" alt="image" src="https://github.com/user-attachments/assets/1f79da75-ba6e-4c2d-8366-13430c03f306" />

#### 4. Se ajustan los permisos para que el servidor web pueda acceder correctamente a los archivos y a la base de datos SQLite:

```bash
sudo chown -R www-data:www-data /var/www/html/web
sudo chmod -R 755 /var/www/html/web
```

<img width="574" height="326" alt="image" src="https://github.com/user-attachments/assets/36335dde-5042-4a9f-a4d5-69e6b489d962" />

#### 5. Por último, se accede a la aplicación desde el navegador:

```bash
http://localhost/web
```

<img width="993" height="752" alt="image" src="https://github.com/user-attachments/assets/e59ac1a6-a78e-4a31-8642-b58e8acc295b" />

---
## 3. ***Auditoría de seguridad de la aplicación***

En este apartado se explica cómo se ha analizado la seguridad de la aplicación ***Talent ScoutTech***. Las pruebas se han hecho de forma práctica, interactuando con la aplicación como lo haría un usuario o un atacante.

Durante el análisis se han buscado fallos habituales en aplicaciones web, como inyecciones ***SQL, XSS, problemas de autenticación o ataques CSRF***, siguiendo las ideas básicas de OWASP. Las vulnerabilidades encontradas y su explotación se explican en los siguientes apartados.

---
## 4. ***Explotación de vulnerabilidades web***

En este apartado se analizan y explotan distintas vulnerabilidades web presentes en la aplicación ***Talent ScoutTech***. A lo largo de este bloque se trabajará con los siguientes tipos de ataques:

- ***SQL Injection (SQLi)***
- ***Cross Site Scripting (XSS)***
- ***Cross Site Request Forgery (CSRF)***

---
### ***Parte 1 – SQL Injection (SQLi)***
---

### ***a) Comprobación de SQL Injection en el formulario de login***
---

Para comprobar si el formulario de login es vulnerable a SQL Injection, se prueban valores especiales en los campos de entrada. Al introducir una comilla doble (`"`) en el campo de usuario, la aplicación devuelve un error SQL, lo que indica que el valor introducido se está usando directamente en la consulta.

Error mostrado por la aplicación:

```bash
Invalid query: SELECT userId, password FROM users WHERE username = """. 
Field user introduced is: "
```

<img width="995" height="173" alt="image" src="https://github.com/user-attachments/assets/10f3d844-bd4b-4bec-a4ab-63c24abf2313" />

A partir de este error se puede deducir la consulta que se ejecuta:

```bash
SELECT userId, password FROM users WHERE username = "<usuario>"
```

| Campo                                                      | Valor      |
| ---------------------------------------------------------- | ---------- |
| Escribo los valores                                        | `"`        |
| En el campo                                                | Usuario    |
| Del formulario de la página                                | Login      |
| Campos del formulario web utilizados en la consulta SQL    | Usuario    |
| Campos del formulario web no utilizados en la consulta SQL | Contraseña |

Esto confirma que el formulario es vulnerable a ***SQL Injection*** en el campo de usuario y que el campo contraseña no se utiliza correctamente en la consulta.

---
### ***b) Impersonación de usuarios con diccionario y Hydra***
---

Como no se conoce ni el número de usuarios ni sus nombres, se crea un diccionario de usuarios falsos utilizando SQL Injection. Para ello, se generan múltiples payloads que fuerzan la consulta SQL a validar usuarios distintos usando `LIMIT` y `OFFSET`.

Para generar el diccionario de usuarios se utiliza el siguiente comando:

```bash
for n in {1..50}; do echo "\" OR 1=1 LIMIT 1 OFFSET $n -- -" >> users.txt; done
```

<img width="975" height="618" alt="image" src="https://github.com/user-attachments/assets/18bd744d-15dd-4fc8-8ade-46089181c832" />

Después, se utiliza el diccionario de contraseñas proporcionado en el enunciado, guardado en el archivo `passwords.txt`, y se automatiza el ataque con Hydra usando el formulario de login. Para ello, ejecutamos el siguiente comando:

```bash
hydra -L users.txt -P passwords.txt localhost http-post-form "/web/insert_player.php:username=^USER^&password=^PASS^:F=Invalid user or password."
```

<img width="971" height="365" alt="image" src="https://github.com/user-attachments/assets/3c471a74-cee2-4452-9a99-e369e075e5cb" />

Hydra prueba todas las combinaciones de usuarios generados y las contraseñas del diccionario. Cuando una combinación es válida, el acceso es permitido.

**Resultado obtenido:**
- ***Usuario (payload SQLi): " OR 1=1 LIMIT 1 OFFSET 1 -- -***
- ***Contraseña: 1234***

Esto permite acceder a la aplicación como un usuario real sin conocer previamente su nombre, logrando así la impersonación de usuarios.

| Concepto                                   | Descripción                                                      |
|-------------------------------------------|------------------------------------------------------------------|
| Explicación del ataque                    | El ataque consiste en repetir peticiones de login utilizando SQL Injection en el campo usuario y probando contraseñas comunes mediante un diccionario con Hydra |
| Usuario con el que se accede              | " OR 1=1 LIMIT 1 OFFSET 1 -- -                                   |
| Contraseña con la que se accede           | 1234                                                             |

---
### ***c) Error en el uso de SQLite3::escapeString()***
---

#### ***Explicación del error***
---

El problema principal es que se está usando `SQLite3::escapeString()` sobre toda la consulta SQL, cuando debería usarse solo sobre los datos que introduce el usuario.

En esta línea se escapa la consulta completa:

```bash
$query = SQLite3::escapeString('SELECT userId, password FROM users WHERE username = "' . $user . '"');
```

Esto hace que el campo `username` siga siendo vulnerable a SQL Injection.
Además, el campo `password` no se escapa ni se usa en la consulta SQL, ya que se compara después en PHP.

---
#### ***Solución***
---

Para corregirlo, hay que ***escapar correctamente tanto el usuario como la contraseña*** antes de utilizarlos.

Código corregido:

```bash
$user = SQLite3::escapeString($user);
$password = SQLite3::escapeString($password);

$query = 'SELECT userId, password FROM users WHERE username = "' . $user . '"';
```

De esta forma, los datos introducidos por el usuario no pueden modificar la consulta SQL y se reduce el riesgo de SQL Injection.

---
### ***d) Publicación de comentarios en nombre de otros usuarios***
---



---
## 5. ***Autenticación, control de acceso y sesiones***



---
## 6. ***Seguridad del servidor web***



---
## 7. ***Informe de pentesting y mitigaciones***



---
## 8. ***Conclusiones***





