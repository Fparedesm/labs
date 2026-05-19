<h1>Lab 3: Protocolos de Comunicación Seguros (Habilidad: Tráfico e Intercepción)</h1>
Entorno: Kali (Wireshark) y un servidor Apache/Nginx

Actividad: Análisis de tráfico inseguro vs. cifrado.
Herramientas: Wireshark, Certbot (Let's Encrypt), OpenVPN/WireGuard.
Tarea: Capturar una sesión HTTP y ver la contraseña en texto plano. Luego, configurar un certificado SSL (HTTPS) y verificar que el tráfico ahora es ilegible. Configurar un túnel SSH con llaves deshabilitando el acceso por contraseña.

Dinámica:
Sniffing de HTTP: El alumno llena un formulario en una web HTTP mientras corre Wireshark. Verá su usuario y contraseña en texto plano (filtro http.request.method == "POST").

Hardening con SSH Tunneling: Aprender a crear un túnel local para proteger tráfico inseguro.
ssh -L 8080:localhost:80 usuario@servidor

---

<h1>¿QUE SE HARA?</h1>

En este laboratorio se levantara una pagina con ubuntu server con apache esta pagina será modificada con un formulario simple el cual usara del método http post. Luego de la configuración de la pagina desde la maquina atacante se entrara, se ingresaran las credenciales y se enviara el formulario. Desde la misma maquina atacante se iniciara wireshark para poder visualizar el trafico y ver si es posible capturar las credenciales en texto plano.

Para evitar esto se creara un túnel ssh el cual deberá ser solo ingresado mediante la clave de una llave la cual será creada en este laboratorio, también, se incorporara y configurara un certificado ssl para obtener https y de esta manera evitar que las credenciales del usuario se vean a través de wireshark en texto plano.

---

<h1>¿QUE SE VERA?</h1>

Se podrá ver lo insegura que es una pagina sin certificado ssl debido a la facilidad que hay en el que sea interceptada con herramientas como wireshark.

También vera la configuración y creación de un túnel ssh y el certificado ssl junto con la utilización de la herramienta wireshark.

---

<h1>FINALIDAD</h1>

Implementar herramientas y protocolos de protección para lograr una comunicación segura mediante cifrado.

---

<h1>HERRAMIENTAS</h1>

-Wireshark

-Apache

-ssl

-ssh

-Kali Linux

-Ubuntu Server

---

<h1>DESARROLLO</h1>

Primero instalamos apache en la maquina victima para poder así levantar la pagina
<img src="images/1apache-instalacion.png" alt="instalacion apache">

Luego de esto se inicializa apache
<img src="images/2inicializacion.png" alt="inicializacion">

Una vez inicializado se verifica que el servicio este corriendo correctamente en la maquina
<img src="images/3verificacion.png" alt="servicio corriendo">

Cuando ya nos hayamos asegurado de que apache este corriendo entramos al archivo index.html para modificarlo
<img src="images/4creacion.png" alt="creacion pagina">

Rellenamos el index html
<img src="images/5creacion-pag.png" alt="Creación pagina">

Luego de esto en la maquina atacante iniciamos wireshark y cargamos la pagina
<img src="images/6wireshark.png" alt="wireshark">

Elegimos la interfaz eth0 ya que es la interfaz que están usando las maquinas en este momento
<img src="images/7interfaz.png" alt="interfaz">

Luego de elegir la interfaz se establece el filtro el cual es http con el método post
<img src="images/8filtro.png" alt="filtro">

Para comenzar con la intercepción del trafico se ingresan las credenciales y se apreta el botón para que el navegador utilice el método post
<img src="images/9credenciales.png" alt="Credenciales">

Una vez ingresadas las credenciales y enviado el formulario se ingresa nuevamente a wireshark para revisar si se han interceptado los datos

<img src="images/10captura.png" alt="captura de datos">

Como se puede ver en la imagen los datos fueron interceptados y las credenciales ingresadas se pueden visualizar en texto plano mediante wireshark

Una forma de evitar de que los datos viajen en texto plano es implementar un túnel ssh

<img src="images/11tunel.png" alt="tunel">

Como se puede ver en el comando se abre un puerto local haciendo que el trafico pase al puerto 80 del servidor.

Luego de esto entramos nuevamente a la pagina utilizando el puerto local 8080 y colocamos nuevamente las credenciales.
<img src="images/12se-entra-con-cifrado.png" alt="cifrado">

Cuando entramos nuevamente a wireshark, no se detecta nada mediante el método http post 
<img src="images/13no-captura.png" alt="no captura">

pero si cambiamos el filtro a ssh se puede visualizar desde wireshark las transmisiones que han sido realzadas están ahora de forma encriptada.
<img src="images/14datos-protegidos.png" alt="datos protegidos">

Ahora se pasara a la creación de llaves mediante el siguiente comando
<img src="images/15creacion-llave.png" alt="creacion llave">

<img src="images/16.png" alt="creacion llavve">

la llave es añadida al servidor
<img src="images/17.png" alt="llave añadida">

Luego de que la llave sea añadida se configura el archivo ssh para desactivar la autenticación mediante contraseña
<img src="images/18configura-ssh.png" alt="desactivar autenticacion">

<img src="images/19desactiva-password.png" alt="desactivar autenticacion">

Una vez desactivada la opción al realizar una conexión ssh ya no se nos pedirá la contraseña solo la clave de la llave que creamos anteriormente.

<img src="images/20pide-llave-no-password.png" alt="verificacion">

Finalmente pasaremos a la etapa de implementación del ssl.

Para comenzar con la creación del certificado ssl se ingresa el siguiente comando

<img src="images/21creacion-certificado.png" alt="creacion certificado">

Luego de para activar ssl en apache se ingresan los siguientes comandos 
<img src="images/22habilita-ssl-apache.png" alt="activacion">

<img src="images/23habilitar-https-por-defecto.png" alt="activacion">

Luego de esto se deben realizar las siguientes configuraciones en el archivo ssl 
<img src="images/24.png" alt="configuracion">

<img src="images/25configuracion-ssl.png" alt="configuracion">

Con estas configuraciones ya realizadas se puede ingresar al sitio mediante https de la siguiente manera
<img src="images/26se-ingresa-con-https.png" alt="ingreso">

<img src="images/27.png" alt="ingreso">

Como se puede ver ahora es imposible interceptar datos sensibles.

Con este sitio que ya contiene una protección tls ingresamos las credenciales y abrimos wireshark para interceptarlas
<img src="images/22wireshark.png" alt="wireshark">
