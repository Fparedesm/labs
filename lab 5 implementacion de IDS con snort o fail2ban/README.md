Lab 2. implementación de IDS con Snort o Fail2Ban (Habilidad: Aplicar IDS)

Entorno: Ubuntu Server (Víctima) y Kali (Atacante).
Actividad: Configurar un sistema de detección y respuesta automática.
Tarea:
Instalar Fail2Ban para proteger el servicio SSH.
Lanzar un ataque de fuerza bruta desde Kali con hydra.
Verificar en los logs cómo el IDS detecta el ataque y bloquea la IP del atacante automáticamente en el firewall (iptables).

Objetivo: Implementar sistemas que detecten y detengan ataques en tiempo real.
Entorno: Ubuntu Server con SSH expuesto y Kali Linux.
Dinámica:
Instalación y Configuración: Instalar Fail2Ban en Ubuntu.
sudo apt install fail2ban
Configurar un archivo jail.local para monitorear el log de /var/log/auth.log.

El Ataque: Desde Kali, lanzar una ráfaga de intentos fallidos.
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://[IP_Víctima]

Observación: En el Ubuntu, el alumno debe monitorear el archivo de log: tail -f /var/log/fail2ban.log.

Verificación de Defensa: Ver cómo la IP de Kali es baneada automáticamente en el firewall.
sudo iptables -L -n
Habilidad ganada: Dominio de sistemas de detección de intrusos y respuesta automática ante incidentes.

¿QUE SE HARA?

Se implementara un ids como fail2ban para poder monitorear y detectar actividades sospechosas como intentos de acceso no autorizados al servicio ssh. fail2ban sera configurado para bloquear direcciones IP que realicen multiples intentos fallidos de autenticacion.

LO QUE SE VERA 

Ataque de fuerza bruta desde kali con hydra, instalacion y configuracion de fail2ban, monitoreo con fail2ban y bloqueo de ip a la maquina atacante.

FINALIDAD

Implementar y configurar un IDS como fail2ban de manera exitosa para que este cumpla con el objetivo de añadir una capa de seguridad al entorno.

HERRAMIENTAS

-ubuntu server

-kali linux

-hydra

-ssh

-fail2ban

Comenzamos con el laboratorio instalando el e inicializando el servicio ssh en la maquina ubuntu server.

