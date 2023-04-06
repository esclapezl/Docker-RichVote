# Installation de Docker sur un projet concret

 ## Table des matières 

 - [Première installation](#id-premiereInstallation) 
 - [Mise en place du docker sur la SAE : Explore](#id-section2)

<br>

## Première installation

Veuillez retrouver la première installation sur ce dépôt : https://github.com/odilonv/TP-Docker .

<br>

# Configurations & Concepts utilisés

Au niveau des différentes configurations, nous allons installer les conteneurs suivants : Apache, Nginx, Serveur de base de données PostgreSQL ainsi qu’un Pgadmin. 
Cependant pour installer ceux-ci nous allons mettre en application les notions : compose, network, volume et build.

<br>

## 1. Notion de Network :


### I/Bridge

Créer un conteneur nginx en mode “bridge” :
<code>docker run -dp 80:80 -- network bridge nginx</code>
Vous pouvez aussi utiliser : docker run -dp 81:80 nginx car le mode bridge est le mode de réseau par défaut de Docker.
