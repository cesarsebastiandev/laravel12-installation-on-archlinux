## Personalización de la terminal de ArchLinux

Este es el repositorio con instrucciones del video de YouTube: [🔧 Personaliza tu Terminal en Arch Linux como un PRO | Neofetch + Zsh + Oh My Zsh + Kitty 🎨](PENDIENTE) 

## Apóyanos

[Suscríbete](https://www.youtube.com/@CesarSebastianDev?sub_confirmation=1) a nuestro canal de YouTube

Donaciones por Paypal: [https://www.paypal.com/donate/?hosted_button_id=UNLT89FVZF6TE](https://www.paypal.com/donate/?hosted_button_id=UNLT89FVZF6TE)

## Instrucciones paso a paso:

## Actualizar el repositorio oficial de ArchLinux

```
sudo pacman -Sy
```
---

## Actualizar los paquetes ya instalados en ArchLinux

```
sudo pacman -Syu
```
---

## Instalar PHP en la version 8.4 y reiniciar la terminal para que se refresquen y noten estos cambios
```
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
```
---

## Checar la version de php
```
php -v
```
---

## Instalar este paquete para descomprimir archivos
```
sudo pacman -S unzip
```
---

## Instalar composer para gestionar las dependencias de Laravel
```
composer global require laravel/installer
```
---

## Verificar la version del instalador de Laravel
```
laravel --version
```
---

## Instalar Flatpak como gestor de software amigable
```
sudo pacman -S flatpak
```
---

## Visitar la tienda de software flatpak e instalar lo siguiente:
`visual studio code`
`db gate`
`postman`
---
## Continuamos con la instalacion de docker y docker-compose
---

## Instalar docker
```
sudo pacman -S docker
```
---

## Instalar docker-compose
```
sudo pacman -S docker-compose
```
---

## Verificar el estatus actual de docker
```
systemctl status docker
```
---

## Habilitar el servicio de docker
```
sudo systemctl enable docker.service
```
---

## Levantar el servicio de docker
```
sudo systemctl start docker.service
```
---

## Volvemos a verificar el estatus actual de docker, esta vez ya debe estar corriendo
```
systemctl status docker
```
---

## Agregamos un usuario al grupo de docker para evitar usar sudo en todas sus ejecuciones
```
sudo usermod -aG docker $USER
```
---

## Hacemos que los cambios se apliquen  de inmediato sin tener que iniciar sesion o reiniciar la terminal
```
newgrp docker
```
---

## Revisar la lista de contenedores que estan corriendo
```
docker ps
```
---

## Revisar la lista de contenedores activos o inactivos
```
docker ps -a 
```
---




## PENDIENTE AGREGAR LA INSTALACION DE CHAOTIC AUR




---
## Continuamos con la instalacion de nodejs usando nvm para manejar diferentes versiones
---

## Instalar nvm usando curl
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```
---

## Cerrar la terminal y volver abrirla
---
## Abrir el archivo de configuracion zshrc escribiendo en la terminal:
---
```
code .
```
### Enseguida se abren todos los archivos en visual studio code y ahi buscamos el archivo .zshrc
### Debe tener una estructura igual a esta, en caso de que no la tengas, se agrega hasta el final
```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```
---
## Abres otra terminal y guardas cambios con:
---
```
source ~/.zshrc
```
## Verificar la version de nvm con
---
```
nvm --version
```

## Instalar nodejs en su version mas reciente
---
```
nvm install --lts
```

## Usar nodejs en su version mas reciente
---
```
nvm use --lts
```
## Cierra la terminal, vuelve abrirla y ahora checa la version de nodejs
---
```
node -v
```

---
## Creamos nuestro primer proyecto de laravel12
---
## El comando es:
---
```
laravel new nombre_del_proyecto
```
## Elegimos los siguientes paquetes:
`el kit de Livewire`
`Laravel built-in authentication`
`Laravel Volt`
`Pest`
`Mysql como motor de base de datos`
## Pregunta que si quiero correr npm install y npm run build
`yes`
---
## Abro el proyecto de Laravel con visual studio code
---
```
cd nombre_del_proyecto
```
---
```
code .
```
---
## Creo un archivo docker-compose en la raiz del proyecto
---
```
docker-compose.yaml
```
## y le agrego esto:
---
```
version: '3.8'

volumes:
  volMysql:
services:
  dbMysql:
    image: mysql:8.4
    container_name: laravel-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: mypassword
      MYSQL_DATABASE: laravel_db
    ports:
      - 3306:3306
    volumes:
      - volMysql:/var/lib/mysql
```
---
## En base a las configuraciones del archivo docker-compose, configuro el archivo .env
---

## Levanto el contenedor de docker que hemos configurado
---
```
docker-compose up -d
```

## Levanto las migraciones del proyecto con:
---
```
php artisan migrate
```

## Levanto el proyecto de Laravel12
---
```
composer run dev
```
## En el navegador va correr en:
---
```
http://127.0.0.1:8000/
```
### O
```
http://localhost:8000/
```
---
## Hago pruebas y registros en la app
---
## Donde rayos se guardan los datos y registros?
---
## Puedes conectarte a un cliente de base de datos, pueden ser:
`Datagrip`
`DB Gate`
`Extension en visual studio code llamada MySQL`
### Solo pones las credenciales de tu base de datos que fueron configuradas en el archivo de docker-compose
---
## Acceder al servidor de MySQL via terminal
---
## En la misma terminal donde tienes corriendo el contenedor de docker, hacer lo siguiente:
---
```
docker exec -it laravel-db bash
```
```
mysql -u root -p
```
## Ya estas dentro del server de MySQL, aqui solo te mueves con comandos SQL crack:
### Mostrar las bases de datos disponibles
```
SHOW databases;
```
### Acceder a una base de datos
```
USE nombre_base_de_datos;
```
### Muestra las tablas de esa BD
```
SHOW tables;
```
### Describe una tabla
```
DESCRIBE nombre_tabla;
```
### Hacer una consulta a la tabla
```
SELECT * FROM users;
```
### Para salirse de ahi
```
exit;
```
---
## Comandos basicos de docker que deberias saber:
---
## Revisar la lista de contenedores que estan corriendo
```
docker ps
```
---

## Revisar la lista de contenedores activos o inactivos
```
docker ps -a 
```
---

## Revisar la lista de imagenes que tengo
```
docker images
```
---
## Revisar la lista de imagenes que tengo
```
docker images
```
---
## Borrar una imagen de docker
```
docker rmi nombre_imagen
```
---
## Borrar todas las imagenes
```
docker image prune
```
---
## Levantar un contenedor
```
docker-compose up -d
```
---
## Borrar el contenedor y tambien el volumen
```
docker-compose down -v
```
---

## Detener el contenedor
```
docker stop nombre_contenedor
```
---
## Borrar el contenedor
```
docker rm nombre_contenedor
```
---
## FIN

