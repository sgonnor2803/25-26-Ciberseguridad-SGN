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

```bash
$user = SQLite3::escapeString($user);
$password = SQLite3::escapeString($password);

$query = 'SELECT userId, password FROM users WHERE username = "' . $user . '"';
```

De esta forma, los datos introducidos por el usuario no pueden modificar la consulta SQL y se reduce el riesgo de SQL Injection.

---
### ***d) Publicación de comentarios en nombre de otros usuarios***
---

En este apartado se analiza una vulnerabilidad encontrada al revisar el archivo de copia `add_comment.php~.php`. Al mirar el código se ve que algunos parámetros se usan directamente en la consulta SQL, lo que permite modificarlos y publicar comentarios como si fueran de otros usuarios.

La aplicación usa la siguiente consulta SQL para guardar los comentarios:

```bash
INSERT INTO comments (playerId, userId, body) VALUES ('".$_GET['id']."', '".$_COOKIE['userId']."', '$body');
```

El problema es que el parámetro `id` no se valida ni se filtra antes de usarse en la consulta.

#### ***Ejemplo de explotación***

Se modifica el parámetro `id` en la URL introduciendo el siguiente payload:

```bash
3', '1', 'Gran Jugadora') -- -
```

<img width="1111" height="233" alt="image" src="https://github.com/user-attachments/assets/2501b015-a450-4d20-bf40-58ef24ebd179" /><br>

Con este payload se cierra la consulta original y se fuerza el `userId`, haciendo que el comentario se guarde como si lo hubiera escrito otro usuario.

<br><img width="1111" height="789" alt="image" src="https://github.com/user-attachments/assets/a8ed92b7-fe10-4dca-9fd3-9f42338b588a" />

#### ***Proceso de explotación***

- Se localiza el archivo de copia `add_comment.php~.php`.
- Se analiza la consulta SQL y se detecta que el parámetro `id` se usa directamente.
- Se modifica el valor de `id` para inyectar SQL.
- El comentario se guarda en la base de datos con otro usuario distinto.

| Campo                                                | Respuesta                                                                                           |
| ---------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Vulnerabilidad detectada**                         | SQL Injection en el parámetro `id` enviado por GET.                                                 |
| **Descripción del ataque**                           | Manipulando `id` se puede cambiar el `userId` del comentario y publicar mensajes como otro usuario. |
| **¿Cómo podemos hacer que sea segura esta entrada?** | Validar que `id` sea numérico y usar consultas preparadas.                                          |

---
### ***Parte 2 – Cross Site Scripting (XSS)***
---

### ***a) Comprobación de XSS en comentarios***
---

Para comprobar si la aplicación es vulnerable a ***Cross Site Scripting (XSS)***, se introduce código JavaScript dentro de un comentario asociado a un jugador.

El siguiente mensaje se introduce como comentario:

```bash
<script>alert('XSS');</script>
```

<img width="1109" height="787" alt="image" src="https://github.com/user-attachments/assets/65bfbdda-0a66-497d-8205-c8b09828c46e" />

Al acceder posteriormente a la página `show_comments.php`, el navegador muestra una ventana emergente con el mensaje **"XSS"**, lo que confirma que el código JavaScript se ejecuta correctamente.

<img width="1112" height="786" alt="image" src="https://github.com/user-attachments/assets/2c24d9f4-3229-4d55-a8c6-aa03a913305e" /><br>

| Introduzco el mensaje ...         | `<script>alert('XSS');</script>` |
| --------------------------------- | -------------------------------- |
| En el formulario de la página ... | `add_comment.php`                |

La aplicación muestra los comentarios sin filtrar ni escapar su contenido, permitiendo la ejecución de código JavaScript almacenado en la base de datos. Por tanto, la aplicación es vulnerable a ***XSS persistente***.

---
### ***b) Uso de & en enlaces HTML***
---

En el código HTML de la página aparece un enlace de donación como este:

```bash
<a href="http://www.donate.co?amount=100&amp;destination=ACMEScouting/">donate</a>
```

<img width="1112" height="618" alt="image" src="https://github.com/user-attachments/assets/c76b26bb-2908-4613-a335-dcffebe969d9" />

Aunque en el HTML se vea `&amp;`, el navegador lo interpreta como un `&` normal al enviar la petición al servidor:

```bash
http://www.donate.co?amount=100&destination=ACMEScouting/
```

Por qué aparece `&amp;`:

- En HTML, el carácter `&` se utiliza para iniciar entidades HTML (como `&lt;` para `<` o `&quot;` para `"`).
- Si se pusiera un `&` directamente en el atributo `href`, el parser HTML podría ***confundirlo con el inicio de una entidad***, rompiendo la URL o el código HTML.

Por eso, los editores y navegadores codifican `&` como `&amp;`, de manera que la URL se interpreta correctamente y el HTML sigue siendo válido.

| Explicación ... | El `&` se codifica como `&amp;` para que el HTML no lo confunda con el inicio de una entidad. El navegador lo decodifica automáticamente, enviando la URL correcta al servidor. |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------|

---
### ***c) Análisis de la vulnerabilidad en show_comments.php***
---

En el código de `show_comments.php` podemos ver que los comentarios se muestran directamente en HTML con esta línea:

```bash
<p>commented: " . $row['body'] . "</p>
```

<img width="814" height="355" alt="image" src="https://github.com/user-attachments/assets/292824a1-e779-42c0-a74e-efc13a15e83a" />

Esto permite que cualquier contenido HTML o JavaScript que un usuario introduzca en los comentarios se ejecute en el navegador de otros usuarios (***XSS persistente***).

<img width="975" height="627" alt="image" src="https://github.com/user-attachments/assets/0aac6750-cb39-462e-8ec2-3c214b36b70f" /><br>

| ¿Cuál es el problema?                    | Los comentarios se imprimen directamente sin escapar su contenido, permitiendo la ejecución de código JavaScript inyectado (XSS persistente). |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Sustituyo el código de la/las líneas ... | `<p>commented: " . $row['body'] . "</p>`                                                                                                      |
| ... por el siguiente código ...          | `<p>commented: " . htmlspecialchars($row['body'], ENT_QUOTES, 'UTF-8') . "</p>`                                                               |

<img width="813" height="559" alt="image" src="https://github.com/user-attachments/assets/c3a5f472-3017-4e88-aef1-3433a36b785f" />

La función `htmlspecialchars()` convierte los caracteres especiales (`<`, `>`, `"`, `'`) en entidades HTML (`&lt;`, `&gt;`, `&quot;`, `&#039;`), evitando que el navegador interprete código malicioso. Así, los comentarios se muestran como texto plano, solucionando la vulnerabilidad XSS persistente.

<img width="979" height="623" alt="image" src="https://github.com/user-attachments/assets/84b9c962-32ef-4c16-afeb-0506c20aa77a" />

Con este cambio, `show_comments.php` ya no permite la ejecución de scripts inyectados en los comentarios, mejorando la seguridad de la aplicación frente a ataques XSS.

---
### ***d) Otras páginas afectadas por XSS***
---

Además de la página `show_comments.php`, se ha detectado otra vulnerabilidad XSS relacionada con la página de login y con todas las páginas que requieren autenticación.

| Otras páginas afectadas ... | Página de login y páginas que usan `auth.php`                                                                                                                                                                       |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ¿Cómo lo he descubierto?    | Provocando un error en el login con una comilla (`"`) y añadiendo código JavaScript en el campo usuario. Al mostrarse el error SQL, la aplicación imprime el valor introducido sin filtrar, ejecutándose el script. |

Al introducir en el campo usuario del formulario de login el siguiente contenido:

```bash
" <script>alert('XSS');</script>
```

<img width="974" height="756" alt="image" src="https://github.com/user-attachments/assets/14a69867-9c99-4d8c-94b7-1450f090f281" /><br>

La comilla hace que la consulta SQL falle y se muestre un mensaje de error. En dicho mensaje aparece el valor introducido por el usuario sin ningún tipo de escape, por lo que el navegador interpreta el `<script>` y ejecuta el `alert`.

<img width="980" height="559" alt="image" src="https://github.com/user-attachments/assets/dbf7493b-e2dd-4a59-a83b-5fce23a606d2" />

<img width="979" height="162" alt="image" src="https://github.com/user-attachments/assets/235b115f-8df9-4d4f-ab5b-0ede899acc7a" />

Esto demuestra que la aplicación es vulnerable a ***XSS reflejado***, ya que muestra directamente datos introducidos por el usuario en mensajes de error, y que esta vulnerabilidad afecta a varias páginas de la aplicación.

---
## 5. ***Autenticación, control de acceso y sesiones***

En este apartado vamos a observar cómo **Talent ScoutTech** maneja el registro, el login y las sesiones. La idea es ver qué falla, qué riesgos hay para los usuarios y cómo podemos arreglarlo para que no se pueda suplantar a nadie ni robar datos. Vamos a revisar registro, login, control de acceso y seguridad de sesiones, y proponer mejoras simples pero efectivas.

---
### ***a) Seguridad en el registro de usuarios (register.php)***
---

Al revisar la página `register.php` se observa que el registro de usuarios presenta varios problemas de seguridad. La aplicación permite crear usuarios sin apenas controles y utiliza consultas SQL poco seguras, lo que puede provocar ataques como SQL Injection o registros incorrectos.

#### ***Problemas detectados en el registro***

Durante el análisis se han encontrado los siguientes problemas:

- El usuario y la contraseña se usan directamente en la consulta SQL, lo que permite ataques de ***SQL Injection***.
- No se comprueba si los campos están vacíos.
- Los errores no se gestionan de forma segura.
- Las contraseñas se guardan en texto plano.
- El formulario de registro no tiene protección frente a CSRF.

#### ***Medidas aplicadas***

De todas estas vulnerabilidades, se han aplicado las medidas que son más fáciles de implementar sin cambiar el funcionamiento general de la aplicación:

- Se valida que el usuario y la contraseña no estén vacíos.
- Se utilizan ***consultas preparadas*** para evitar SQL Injection.
- Se controla el error de la consulta sin mostrar información sensible.

El código del registro se ha modificado quedando de la siguiente forma:

```bash
<?php
require_once dirname(__FILE__) . '/private/conf.php';

# Require logged users
# require dirname(__FILE__) . '/private/auth.php';

if (isset($_POST['username']) && isset($_POST['password'])) {
        # Just in from POST => save to database
        $username = trim($_POST['username']);
        $password = trim($_POST['password']);

        if ($username === '' || $password === '') {
                die("Por favor, completa todos los campos");
        }

        $username = SQLite3::escapeString($username);
        $password = SQLite3::escapeString($password);

        // Consulta preparada
        $stmt = $db->prepare('INSERT INTO users (username, password) VALUES (:username, :password)');
        $stmt->bindValue(':username', $username, SQLITE3_TEXT);
        $stmt->bindValue(':password', $password, SQLITE3_TEXT);
        $result = $stmt->execute();

        if (!$result) {
                die("Invalid query");
        }

    header("Location: list_players.php");
}
```

#### ***Otras mejoras propuestas***

Existen otras medidas de seguridad que no se han implementado en este apartado porque requieren modificar otras partes de la aplicación:

- Guardar las contraseñas cifradas usando `password_hash()`.
- Añadir protección CSRF a los formularios.

Con estas mejoras, el registro ya no es vulnerable a SQLi y valida que los campos no estén vacíos. Aun se podrían añadir más medidas, pero lo aplicado cubre los riesgos principales para el proyecto.

---
### ***b) Seguridad en el login de usuarios (auth.php)***
---

Al revisar la página `auth.php` se observa que el sistema de login presenta varios problemas de seguridad. La aplicación valida usuarios y contraseñas de forma insegura, lo que permite ataques como ***SQL Injection*** o la ejecución de código malicioso a través de mensajes de error.

#### ***Problemas detectados en el login***

Durante el análisis se han encontrado los siguientes problemas:

- La consulta SQL usaba directamente los valores introducidos por el usuario, lo que permitía ataques de ***SQL Injection***.
- Los mensajes de error no se mostraban escapados, pudiendo provocar ***XSS*** si se incluían datos maliciosos.
- Las contraseñas se comparaban en texto plano.
- Las cookies usadas para la sesión (`user` y `password`) no estaban marcadas como `HttpOnly` ni `Secure`.
- No hay protección frente a ***CSRF*** en los formularios de login y logout.

#### ***Medidas aplicadas***

De todas estas vulnerabilidades, se han aplicado las medidas que son factibles sin cambiar la arquitectura general de la aplicación:

- Se utilizan ***consultas preparadas*** para evitar SQL Injection.
- Se comprueba que la fila devuelta exista antes de comparar la contraseña.
- Los mensajes de error se muestran usando `htmlspecialchars($error)` para evitar XSS.

El código del login se ha modificado quedando de la siguiente forma:

```bash
<?php
require_once dirname(__FILE__) . '/conf.php';

$userId = FALSE;

# Check whether a pair of user and password are valid; returns true if valid.
function areUserAndPasswordValid($user, $password) {
        global $db, $userId;

        // Consulta preparada para evitar SQLi
        $stmt = $db->prepare('SELECT userId, password FROM users WHERE username = :user');
        $stmt->bindValue(':user', $user, SQLITE3_TEXT);
        $result = $stmt->execute();
        $row = $result->fetchArray();

        if ($row && $password == $row['password'])
        {
                $userId = $row['userId'];
                $_COOKIE['userId'] = $userId;
                return TRUE;
        }
        else
                return FALSE;
}

# On login
if (isset($_POST['username']) && isset($_POST['password'])) {
        $_COOKIE['user'] = $_POST['username'];
        $_COOKIE['password'] = $_POST['password'];
}

# On logout
if (isset($_POST['Logout'])) {
        # Delete cookies
        setcookie('user', FALSE);
        setcookie('password', FALSE);
        setcookie('userId', FALSE);

        unset($_COOKIE['user']);
        unset($_COOKIE['password']);
        unset($_COOKIE['userId']);

        header("Location: index.php");
}


# Check user and password
if (isset($_COOKIE['user']) && isset($_COOKIE['password'])) {
        if (areUserAndPasswordValid($_COOKIE['user'], $_COOKIE['password'])) {
                $login_ok = TRUE;
                $error = "";
        } else {
                $login_ok = FALSE;
                $error = "Invalid user or password.";
        }
} else {
        $login_ok = FALSE;
        $error = "This page requires you to be logged in.";
}

if ($login_ok == FALSE) {

?>
    <!doctype html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <link rel="stylesheet" href="css/style.css">
        <title>Práctica RA3 - Authentication page</title>
    </head>
    <body>
    <header class="auth">
        <h1>Authentication page</h1>
    </header>
    <section class="auth">
        <div class="message">
            <?= htmlspecialchars($error) ?><br>
        </div>
        <section>
            <div>
                <h2>Login</h2>
                <form action="#" method="post">
                    <label>User</label>
                    <input type="text" name="username"><br>
                    <label>Password</label>
                    <input type="password" name="password"><br>
                    <input type="submit" value="Login">
                </form>
            </div>

            <div>
                <h2>Logout</h2>
                <form action="#" method="post">
                    <input type="submit" name="Logout" value="Logout">
            </div>
        </section>
    </section>
    <footer>
        <h4>Puesta en producción segura</h4>
        < Please <a href="http://www.donate.co?amount=100&amp;destination=ACMEScouting/"> donate</a> >
    </footer>
    <?php
    exit (0);
}

setcookie('user', $_COOKIE['user']);
setcookie('password', $_COOKIE['password']);


?>
```

#### ***Otras mejoras propuestas***

Existen otras medidas de seguridad que no se han implementado porque requieren modificar otras partes de la aplicación:

- Guardar las contraseñas cifradas usando `password_hash()` y `password_verify()`.
- Usar cookies de sesión seguras (`HttpOnly` y `Secure`).
- Añadir ***protección CSRF*** en los formularios de login y logout.

Con estas mejoras aplicadas, el login ya no es vulnerable a SQLi y los errores no ejecutan código malicioso.

---
### ***c) Gestión del acceso a la página de registro (register.php)***
---

Al revisar la página `register.php`, se observa que actualmente cualquier usuario, registrado o no, puede acceder al registro de usuarios. Esto puede ser problemático si no queremos que se creen nuevos usuarios libremente.

#### ***Problema detectado***

- La página de registro está abierta a todos los usuarios.
- Esto puede permitir registros no autorizados y aumentar riesgos de seguridad.

#### ***Medida aplicada***

Para limitar el acceso sin cambiar toda la aplicación:

- Se comprueba si el usuario ya está autenticado mediante cookies.
- Si el usuario ya tiene sesión activa, se le redirige automáticamente a la página de lista de jugadores (`list_players.php`), evitando que pueda acceder al registro.

El código que implementa esta medida es:

```bash
<?php
require_once dirname(__FILE__) . '/private/conf.php';

# Require logged users
require_once dirname(__FILE__) . '/private/auth.php';

if (isset($_COOKIE['user']) && isset($_COOKIE['password'])) {
        header("Location: list_players.php");
}
```

#### ***Otras mejoras posibles***

Existen otras medidas que podrían aplicarse en un proyecto más avanzado:

- Restringir el registro solo a administradores mediante roles.
- Implementar un sistema de invitaciones para permitir solo usuarios autorizados.
- Deshabilitar completamente el registro en producción.

Con esta medida implementada, la página de registro ya no está accesible para usuarios autenticados, evitando accesos innecesarios o potencialmente peligrosos.

---
## 6. ***Seguridad del servidor web***



---
## 7. ***Informe de pentesting y mitigaciones***



---
## 8. ***Conclusiones***


