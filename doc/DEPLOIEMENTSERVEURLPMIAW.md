- [Avant de commencer](#avant-de-commencer)
  - [Attention](#attention)
  - [Prérequis](#prérequis)
- [Mise en production d'un site Symfony sur le serveur Lpmiaw](#mise-en-production-dun-site-symfony-sur-le-serveur-lpmiaw)
  - [Récupération des fichiers](#récupération-des-fichiers)
  - [Installation des dépendances](#installation-des-dépendances)
  - [Paramétrages](#paramétrages)
  - [Enjoy !](#enjoy-)
- [Mise en production d'un site Wordpress sur le serveur Lpmiaw](#mise-en-production-dun-site-wordpress-sur-le-serveur-lpmiaw)
  - [Récupération des fichiers](#récupération-des-fichiers-1)
  - [Installation des dépendances](#installation-des-dépendances-1)
  - [Restauration de la base de données en modifiant l'url](#restauration-de-la-base-de-données-en-modifiant-lurl)
  - [Paramétrages](#paramétrages-1)
  - [Enjoy !](#enjoy--1)

# Avant de commencer

## Attention

Une fois le site en place, vous ne devez pas modifier vos fichiers sources directement sur le serveur. On considère que ce serveur est un serveur de production.

Il ne doit utiliser que la branche master git de votre projet et se synchroniser avec elle.

## Prérequis

1. Avoir généré une clé ssh pour son compte sur le serveur : ssh-keygen
1. Avoir ajouté cette clé dans son profil gitlab.
1. Avoir une branche master propre et fonctionnelle sur sa machine

# Mise en production d'un site Symfony sur le serveur Lpmiaw

## Récupération des fichiers

- votre dépôt git ne doit contenir que vos fichiers symfony et non l'environnement technique basé sur docker

```sh
git clone url_mon_projet_symfony
```

## Installation des dépendances

```sh
cd mon_projet_symfony
composer install
```

## Paramétrages

- Créez un fichier .env.local en spécifiant l'accès à la base de données et éventuellement les autres paramètres de votre application.
- Vérifier que les fichiers de migration sont propres (pas deux fichiers qui font la même chose...)
- Lancer les migrations
- Lancez les fixtures pour peupler votre base de données.

## Enjoy !

# Mise en production d'un site Wordpress sur le serveur Lpmiaw

## Récupération des fichiers

```sh
git clone url_mon_projet_wordpress
```

## Installation des dépendances

```sh
cd mon_projet_wordpress
composer install
```

## Restauration de la base de données en modifiant l'url


## Paramétrages

- Créez un fichier .env sur le modèle .env.example en spécifiant le DATABASE_URL et WP_HOME, WP_SITEURL, ...

## Enjoy !