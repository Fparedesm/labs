Lab 1. Practica de defensa activa

Gestión de Parches y Hardening (Habilidad: Implementar parches)
Entorno: Ubuntu Server desactualizado.
Actividad: Los alumnos reciben un informe de vulnerabilidades (simulado).
Tarea: 1. Identificar servicios vulnerables usando nmap --script vuln. 2. Aplicar parches específicos usando apt-get install --only-upgrade [paquete]. 3. Configurar Unattended Upgrades para automatizar parches críticos.

Entorno: Una VM Ubuntu Server "congelada" en una versión antigua o con servicios vulnerables (ej. un servicio de impresión o una versión de OpenSSH con vulnerabilidades conocidas).
Dinámica:
Escaneo Inicial: Desde Kali, usar nmap -sV --script vuln [IP_Ubuntu]. Los alumnos deben identificar al menos 3 vulnerabilidades con su código CVE correspondiente.

Investigación: Buscar en la base de datos del NVD (NIST) qué permite hacer ese CVE (ej. RCE o DoS).

Aplicación de Parche:
Simular la política de "parches críticos primero".
Uso de apt-get install --only-upgrade [servicio] para no romper dependencias globales.

Configuración de Seguridad Autónoma: Instalar unattended-upgrades.
sudo apt install unattended-upgrades
Configurar /etc/apt/apt.conf.d/50unattended-upgrades para que solo se instalen parches de "Security".
Habilidad ganada: Capacidad de priorizar la remediación basada en el impacto organizacional.

¿QUE SE VA HACER?

Se utilizara una maquina ubuntu server desactualizada con el objetivo de identificar las vulnerabilidades que esta presenta, para posteriormente realizar una remediación aplicando parches de seguridad.

También se investigaran al menos 3 CVE detectados en la maquina victima con la pagina nvd para poder verificar cuales son los peligros que este representa para el sistema.

LO QUE SE VERA

Se lograran observar múltiples servicios y sus vulnerabilidades, también se podrá observar un escaneo de vulnerabilidades por parte de la maquina atacante la cual es una kali linux, esta hará el escaneo con nmap, configuraciones para el proceso de remediación en el sistema mediante aplicación de parches o actualizaciones.

FINALIDAD

Aprender acerca de la importancia sobre como funciona el proceso de remediación o fortalecimiento de un equipo para evitar posibles ataques inminentes, estas medidas son importantes para disminuir los riesgos de seguridad y mantener el equipo (ubuntu server) actualizado al día.

HERRAMIENTAS

-Ubuntu server (metasploitable3)

-Kali Linux

-nmap

-nvd

DESARROLLO

Primero comenzamos haciendo un escaneo con la maquina atacante kali linux hacia la maquina victima desactualizada (ubuntu server) 
<img src="images/1escaneo.png" alt="escaneo">

Como se puede ver en la imagen el escaneo contiene los parámetros de -sV para detectar los servicios que están corriendo en la maquina y sus versiones correspondientes -O para detectar el sistema operativo y un script vuln para detectar las vulnerabilidades conocidas en los servicios que fueron detectados.

Como se puede apreciar en la foto el escaneo fue un éxito.

y se detectaron las siguientes CVE

<img src="images/5vulnerabilidades.png" alt="vulnerabilidades">

Se detecto el CVE CVE-2013-4124 este afecta a las versiones antiguas de samba el impacto principal que podría tener esta vulnerabilidad es un posible ataque de denegación de servicios. El atacante podría enviar paquetes SMB manipulados para ocasionar el ataque de denegación de servicio sobre exigiendo el uso de memoria en el sistema

<img src="images/4vulnerabilidades.png" alt="vulnerabilidades">

También se encontró el CVE-2007-6750 el cual afecta a versiones antiguas de apache http server. Esta vulnerabilidad puede traer ataques de denegación de servicio conocido como slowloris. Con esta vulnerabilidad el atacante puede ser capaz de enviar múltiples peticiones http y consumir los recursos del servidor apache para que este servicio tarde o directamente no pueda responder.

<img src="images/3vulnerabilidades.png" alt="vulnerabilidades">

El otro CVE encontrado es el CVE-2015-3306 esta vulnerabilidad afecta a versiones ProFTPD. La vulnerabilidad permite a los atacantes remotos abusen de comandos SITE CPFR o SITE  CPTO con el objetivo de leer o escribir archivos dentro del sistema, ocasionando un impacto de acceso no autorizado a información sensible.

A continuacion se aplicaran los parches a cada servicio.

<img src="images/6parches.png" alt="parches">

<img src="images/7parches.png" alt="parches">

<img src="images/8parches.png" alt="parches">

Luego de esto se configuran las actualizaciones automáticas de seguridad con el siguiente comando.

<img src="images/9unattended-upgrades.png" alt="actualizaciones">

Con este comando se automatiza la descarga e instalación de actualizaciones de seguridad en el sistema.

Ahora se configurara el archivo de unattended upgrades el cual define las reglas de que actualizaciones serán llevadas a cabo automáticamente en el sistema.

<img src="images/10configuracion.png" alt="configuracion">

Dentro del archivo se hace la siguiente modificacion con el objetivo de instalar solo actualizaciones de seguridad.

<img src="images/11configuracion.png" alt="configuracion">


