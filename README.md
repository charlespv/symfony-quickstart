# Quickstart Symfony 3.4

> EN MODE LE SCOUARNEC

## Prérequis

### Software
 - Git installé PHP 7.1 accessible dans le terminal 
 - MySQL 5.7 accessible
   dans le terminal 
  - Composer installé en global sur la machine
  - PHPStorm conseillé

### Plugin
- Symfony plugin
- .ignore
- PHP annotations
- PHP composer.json support
- PHP Toolbox


## Création du projet
Création du squelette d'application symfony 3.4
Dans le terminal, rentrez : 
```
composer create-project symfony/skeleton votre-projet 3.4
```
*Skeleton inclus désormais Symfony Flex*

## Lancement du projet

Installation de la recipe server HTTP
```
composer req server 
bin/console server:start
```
Vérifier dans votre navigateur.

### Quelques recipes

Installation de la recipe **annotation** qui permet à Symfony de lire la
configuration stockée dans les annotations de classes, attributs et méthodes.

```
composer req annotations
```

Installation de la recipe maker de Symfony. Cette recipe rajoute les commandes de génération en CLI.

```
composer req maker
```
Installation de la recipe de **templating** de Symfony. Cette recipe installe tout ce que **Twig** nécessite pour fonctionner.

```
composer req template
```
### Controller
Création d'un controller MonsterController. Le controller est une classe spécifique qui gère les fonctionnalités codées dans Symfony.
```
php bin/console make:controller
```

Installation de la recipe doctrine, l'ORM utilisé par Symfony. C'est une couche d'abstraction permettant de manipuler et stocker les données.
```
composer req doctrine
```

### Configuration BDD 
Modification du fichier .env qui contient les informations de connexion à la base de données et plus généralement les paramètres de l'application.
```
pico .env
```
Repérez la ligne liée à la BDD et modifier ainsi le fichier :
```
DATABASE_URL=mysql://VOTRE_LOGIN:VOTRE_MDP@127.0.0.1:3306/NOM_DATABASE
```
Vérifier que votre serveur MySQL est lancé et se situe sur port que vous avez indiqué sur la ligne précédente (ici ``` 3306```)
Si votre mdp est vide, écrire : ```VOTRE_LOGIN:@xx.x.x.x:xxxx```
exemple : 
```
DATABASE_URL=mysql://root:@127.0.0.1:3306/monster
```

Création de la base de données spécifiée dans le fichier .env.
```
php bin/console doctrine:database:create
```

### Entity
Création de l'entity Monster grâce à un assistant. L'entity est une classe qui liste les attributs qui définissent l'entity et les setters et getters de ces attributs.
```
php bin/console make:entity
```

Edition de l'entity Monster pour ajouter des des attributs. 
Sur PHPStorm, utiliser la fonction Code -> Generate -> ...
```
pico Entity/Monster.php
```

### Table
Création de la table qui reflète l'entity dans la base de données.
```
php bin/console doctrine:schema:update --force
```

### Admin
Installation de la recipe EasyAdmin qui permet d'administrer les données sans développer quoi que ce soit.
```
composer require admin
```
Edition du fichier de configuration de EasyAdmin pour ajouter l'entity Monster aux entities gérées par EasyAdmin.

Ouvrez le fichier :
```
pico config/packages/easy_admin.yaml
```
Ensuite modifier le fichier ainsi:
```
easy_admin:
    entities:
#        # List the entity class name you want to manage
        - App\Entity\Monster
```


