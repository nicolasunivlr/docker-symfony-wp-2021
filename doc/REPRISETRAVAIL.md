# Reprise d'un travail déposé sur Git sur une nouvelle machine

> Préambule, avoir un dépôt git du projet Symfony !!!

1. chargez votre clé privée ssh depuis un support amovible

    ```sh
    $ sudo cat /chemin_vers_votre_dossier_ssh/id_rsa | ssh-add -
    ```

**OU**

générez une nouvelle clé en l'ajoutant aux paramètres de votre compte gitlab.

    ```sh
    $ ssh-keygen
    ```

2. Recréez la stack technique basée sur docker avec le Makefile
   
3. Créez un nouveau projet symfony
   
4. Placez vous dans le dossier du projet
   
5. Faites les commandes git suivantes dans le dossier de votre projet Symfony :

    ```sh
    # c'est un petit hack car on ne peut pas faire un pull sur un dossier existant
    git init
    git remote add origin git@gitlab.univ-lr.fr:votre_login/votre_projet.git
    git fetch
    git checkout -t origin/master -f
    ```

6. Ajoutez la bonne configuration à votre fichier .env.local

  ```yml
    DATABASE_URL=mysql://root:root@db:3306/nom_base_a_changer_au_nom_du_projet?serverVersion=mariadb-10.4.14
  ```


7. Dans le dossier de devLP
   
   ```sh
   make bash
   cd votre_projet
   composer install
   ```

8. Votre base de données
- Lancez vos migrations puis vos fixtures

7. Votre application doit fonctionner.

8. Continuez votre travail avec phpstorm.
