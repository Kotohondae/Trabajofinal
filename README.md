# Trabajofinal
Trabajo final de telematica 

# Montaje de un contenedor Docker usando AWS

# Paso a paso para desplegar el juego Tetris en HTML

Este proyecto contiene una versión básica del juego clásico Tetris en HTML y JavaScript, que se ejecuta dentro de un contenedor Docker con NGINX, preparado para reiniciarse automáticamente al encender tu instancia EC2.

# 1. Creacion de la instancia y conexion
Instancia EC2 en Ubuntu, con puertos 22 (ssh) y puerto 80 (http).
Se conecta a la instancia desde una terminal, usando el comando --> ssh -i "llave.pem" ubuntu@ip-publica-instancia

# 2. Actualizacion de paquetes e instalacion del Docker

sudo apt update
sudo apt-get install docker.io -y
sudo systemctl enable docker && sudo systemctl start docker --> Para iniciar el docker y dejarlos activo permanentemente.
sudo systemctl status docker --> Para confirmar si todo esta bien instalado.

# 3. Crear carpeta del proyecto

mkdir tetris-html && cd tetris-html

# 4. Creacion del archivo HTML

sudo nano index.html --> Aqui se pegara el html del juego.

# 5. Crear el Dockerfile

nano Dockerfile --> Dentro se pega esto: FROM nginx:alpine COPY index.html /usr/share/nginx/html/index.html
Se guarda el archivo con --> Ctrl + S y sal con Ctrl + X
Este docker usara NGINX, este sirve para crear una imagen de contenedor que despliega una página web HTML estática.

# 6. Construir la imagen Docker

sudo docker build -t tetris-html .

# 7. Ejecutar el contenedor con reinicio automático

sudo docker run -d -p 80:80 --restart unless-stopped --name tetris-game tetris-html
El "--restart unless-stopped" reinicia el contenedor automaticamente, si este se cae o vuelves a encender el AWS solo tendras que encender la intancia y se activara automaticamente.

# 8. Paso final. Acceder al juego desde el navegador
http:// --> Desde un navegador, ya asi podremos jugar nuestro tetris tranquilamente.
