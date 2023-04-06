# Installation de Docker sur un projet concret

 ## Table des matières 

 - [Première installation](#id-premiereInstallation) 
 - [Mise en place du docker sur la SAE : Explore](#id-section2)

<br>

## Première installation


Veuillez retrouver la première installation sur ce dépôt : https://github.com/odilonv/TP-Docker .

<br>

# Mise en application des différents concepts

Au niveau des différentes configurations, nous allons installer les conteneurs suivants : Apache, Nginx, Serveur de base de données PostgreSQL ainsi qu’un Pgadmin. 

<br>

## 1. Débutons par le résultat

![Ca1pture](https://user-images.githubusercontent.com/120033089/230320887-c22c8580-41d1-4f3b-88c3-3c3bac030e79.PNG)
<br>
![2Capture](https://user-images.githubusercontent.com/120033089/230321038-b46fd8f3-8ffe-4554-8a55-cbd4591b410c.PNG)

## 2. Différents fichiers utilisés

### <code>docker-compose.yml</code>

```
version: "3.8"

services:
  web89 :
    image: php:8.2-apache
    container_name: web89
    volumes:
      - ./web89/SAE-WEBSITE/web:/var/www/html/SAE-WEBSITE/web
      - ./web89/SAE-WEBSITE/:/var/www/html/SAE-WEBSITE
      - ./web89/apache/sites_enabled:/etc/apache2/sites_enabled
      - ./web89/php/custom-php.ini:/use/local/etc/conf.d/custom-php.ini
    

    ports:
      - 89:80


  mysql:
    image: mysql:5.7
    container_name: mysql1
    environment:
      MYSQL_DATABASE: sae
      MYSQL_USER: sae
      MYSQL_PASSWORD: totoLolo
      MYSQL_ROOT_PASSWORD: totoLolo
      UPLOAD_LIMIT: 20M

    ports:
      - 3306:3306
    volumes:
      - ./mysql1/mysql:/var/lib/mysql
      - ./mysql1/db/custom.cnf:/etc/mysql/conf.d/custom.cnf

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: pma1
    depends_on:
      - mysql
    ports:
      - 83:80
    environment:
      - PMA_HOST=mysql

  # web90:
  #   build: web90 # dossier contenant le fichier Dockerfile
  #   container_name: web90
  #   volumes:
  #     - ./web90/html:/var/www/html
  #     - ./web90/apache/sites_enabled:/etc/apache2/sites_enabled
  #     - ./web90/php/custom-php.ini:/use/local/etc/php/conf.d/custom-php.ini
  #   ports:
  #     - 90:80

```

### <code>Dockerfile</code>

```
FROM php:8.2-apache

# Installe Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Active le module de réécriture Apache2 et redémarre Apache2
RUN a2enmod rewrite && service apache2 restart

# Installe l'extension pdo_mysql pour PHP
RUN docker-php-ext-install pdo_mysql

# Définit le répertoire de travail par défaut
WORKDIR /var/www/html

RUN apt-get update && apt-get install -y nano 
RUN apt-get install -y git 
# renseignez votre mail 
RUN git config --global user.email "odilon.vidal@icloud.com" 

# renseignez votre nom de user 
RUN git config --global user.name "odilonv"
RUN apt-get install -y wget 
RUN docker-php-ext-install pdo_mysql 
RUN apt-get install -y zip
```
