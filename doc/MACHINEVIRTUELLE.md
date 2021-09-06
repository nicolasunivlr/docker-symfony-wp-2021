## Prérequis
- Vous avez déjà tous les logiciels installés.

## Spécificités

1. Vous stockerez vos fichiers dans /home/$USER
1. Il faut refaire certaines manipulations à chaque début de TP :
    - git config...
    - ajout des clés ssh
    - construction des images docker
    - récupération de vos fichiers symfony/wordpress
    - récupération de votre base de données

## Installation

1. Dupliquer le projet :
    ```bash
    git clone https://gitlab.univ-lr.fr/ntrugeon/docker-symfony-wp-2020.git devPhpLP
    # on se place dans le bon dossier
    cd devPhpLP
    ```

2. Modifier le ficher .env pour changer la commande docker et activer le proxy
   - PROXY=http://wwwcache.univ-lr.fr:3128 (à décommenter)

3. Construire et exécuter les conteneurs (Cela peut prendre un peu de temps)

    ```bash
    $ make build
    $ make up
    ```

4. Installer Symfony
    1. On installe symfony en version minimale grâce au Makefile.
        
        ```bash
        $ make newSF nom_de_mon_projet
        ```
        - cela va créer le projet via composer, un virtualhost ainsi qu'une base de données dédiée

    2. On installe les composants nécessaires à nos applications également avec Composer

        ```bash
        $ make bash
        $ cd nom_de_mon_projet
        $ composer require --dev profiler maker
        $ composer require annotations twig orm form validator
        ```
    
    3. Ouvrir le dossier symfony du projet dans phpStorm

5. Installer Wordpress
   1.  On installe wordpress grâce au Makefile.
        
        ```bash
        $ make newWP nom_de_mon_projet
        ```
        - cela va créer le projet via composer, un virtualhost ainsi qu'une base de données dédiée
    
   2. Ouvrir le dossier wordpress du projet dans phpStorm, et modifier **.env** 
      1. en commentant les 3 premières lignes du .env
      2. en ajoutant la ligne DATABASE_URL comme ceci :

        ```yml
        DATABASE_URL='mysql://root:root@db:3306/nom_base_a_changer_au_nom_du_projet'
        ```
      3. en renseignant les informations associées au projet et spécifique à wordpress : WP_HOME, WP_SITEURL, ...

6. C'est parti :-)

## Je commence à travailler sur un projet

Vous avez juste à exécuter `make up`, puis:

* Ouvrez votre projet avec phpStorm
* Ouvrez votre navigateur [nom_de_mon_projet.localhost:8000](http://nom_de_mon_projet.localhost:8000)
* Logs du serveur web : logs/apache2

## Je finis de travailler sur le projet
Vous avez juste à exécuter `make down`.

Pensez à envoyer sur votre git les données.

** OU **

Comme vous avez connecté votre lecteur personnel à la machine virtuelle, vous pouvez sauvegarder les dossiers projets **ET** virtualhosts hormis les dossiers **vendor** et **var** du répertoire symfony.
Créez un zip de projets et virtualhosts et copiez dans votre lecteur personnel ou un média amovible

## Reprise du travail sur une autre séance

Suivez la [doc associée](REPRISETRAVAIL.md)

## Comment cela fonctionne ?

Vous pouvez aller regarder le fichier `docker-compose.yml`, avec les images `docker-compose` correspondantes:

* `db`: le container mariadb 10.4,
* `php`: php-fpm en version 7.4,
* `apache`: le serveur web apache2 sur le port 8000,

## Commandes utiles

```bash
# On rentre dans un conteneur en bash
$ make bash

# Commandes symfony
$ make bash
$ cd nom_de_mon_projet
$ sf make:controller
$ sf make:entity
$ composer req composant_utile
...

# Supprimer tous les conteneurs (en cas de gros plantage, à utiliser en dernier recours)
$ make cleanAll
```

## FAQ
* Je ne comprends rien, que faire ?
Allez voir votre prof !

* Xdebug?
Xdebug est déjà configuré
Il faut ajouter le module Xdebug helper pour Firefox ou pour Chrome
Il faut également configurer Phpstorm en se connectant au port  `9001` avec l'id `PHPSTORM`. Vous pouvez suivre ce [lien](https://blog.eleven-labs.com/fr/debug-run-phpunit-tests-using-docker-remote-interpreters-with-phpstorm/). Le dépôt que vous utilisez est déjà paramétré. Utilisez docker-compose à la place de docker dans le "Remote" de l'interpréteur PHP.