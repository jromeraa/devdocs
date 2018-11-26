# Entorn de treball LAMP

Vist a http://www.adcisolutions.com/knowledge/docker-drupal-developers-how-create-lamp

## Crear un contenidor MySQL

Si cal crear la base de dades

`docker run --name mysql55 -e MYSQL_ROOT_PASSWORD=root -d -v "$PWD/mysql55":/var/lib/mysql mysql:5.5 --max-allowed-packet=512M `

Si ja existeix la base de dades

`docker run --name mysql55 -d -v "$PWD/mysql55":/var/lib/mysql mysql:5.5 --max-allowed-packet=512M`

`--name` nom que s'assignarà al contenidor

`-d`     executa el contenidor en segon pla

`-e`     permet sobreescriure variebles d'entorn

`-v`     permet muntar directoris de dades externs al contenidor dins d'ell

`--max-allowed-packet=512M` permet importar bases de dades pesades

## Crear una contenidor Apache-PHP

1. Crear un Dockerfile amb el següent contingut

  ```
  # use a module of apache for php 5.5
  FROM php:5.4-apache

  # enable a module of apache for “clean urls”
  RUN a2enmod rewrite

  # install modules of apache that will be required for Drupal 7
  RUN apt-get update && apt-get install -y libpng-dev libjpeg-dev && \
  	rm -rf /var/lib/apt/lists/* && docker-php-ext-configure gd \
	  --with-png-dir=/usr --with-jpeg-dir=/usr && docker-php-ext-install gd
  RUN docker-php-ext-install mysqli
  RUN docker-php-ext-install pdo_mysql
  RUN docker-php-ext-install mbstring
  ```

2. Construir una imatge del servidor Apache-PHP a partir del Dockerfile

  `docker build -t php54-apache .`

  `-t` nom que s'assignarà a la imatge

3. Crear un contenidor que enllaci la imatge del servidor APACHE-PHP amb el contenidor MySQL

  `docker run --name=cristianismeijusticia.local --link mysql55:db -d -v "$PWD/src":/var/www/html -v "$PWD/docker/config/php.ini":/usr/local/etc/php/php.ini -p 80:80 php54-apache`

  `--name` nom que s'assignarà al contenidor

  `--link` enllaça el contenidor amb el contenidor MySQL. In this case in the file /etc/host will add a new row with ip address of the MySQL container. In the future we can use hostname “db” instead of ip address.

  `-p 80:80` indicate the port forwarding from the host machine to our container.

## Conectar via terminal

`docker exec -it CONTENIDOR bash`
