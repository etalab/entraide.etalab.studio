# Entraide.etalab.studio
## Objectif

Cette application est une plateforme d'échange et d'entraide pour les agents de la mission Etalab.

## Ressources mobilisées

- [Question2Answer](https://github.com/q2a/question2answer)
- [Thème Etalab q2a](https://github.com/etalab/q2a-theme-etalab) accessible reprenant le [Design Système de l'Etat](https://www.systeme-de-design.gouv.fr/)

## Déploiement

- Créer l'application avec `dokku apps:create <nom_application>`
- Créer la base de données avec `dokku mariadb:create <nom_db>`
- Lier la base de données à l'application `dokku mariadb:link <nom_db> <nom_application>`

**Attention** : La commande ci-dessus va afficher dans la console l'adresse de la base de données SQL sous cette forme : 

`<protocole>://<nom_utilisateur>:<mot_de_passe>@<nom_hote>:<port>/<nom_db>`

- Récupérer le projet avec `git clone https://github.com/etalab/entraide.etalab.studio.git`

- Accéder au dossier avec `cd entraide.etalab.studio`
- Éditer le `.gitignore`, il faut enlever cette section : 

```
  # Ignore Q2A config file and .htaccess in development
  /qa-config.php
  /.htaccess
```

- Renommer le `qa-config-example.php` en `qa-config.php`

- Éditer le fichier `qa-config.php` à la racine du projet, il faut préciser les variables de connexion à la base de données :

```
  define('QA_MYSQL_HOSTNAME', '<nom_hote>');
  define('QA_MYSQL_PORT', '<port>');
  define('QA_MYSQL_USERNAME', '<nom_utilisateur>');
  define('QA_MYSQL_PASSWORD', getenv('DATABASE_PASSWORD'));
  define('QA_MYSQL_DATABASE', '<nom_db>');
```

- Préparer le push de la branche locale contenant les variables de connexion à la base de données :

```
  git remote add dokku dokku@<ip_serveur>:<nom_application>
  git checkout -b deploy
  git add qa-config.php
  git commit -m "Credentials database"
```

- Configurer la variable d'environnement nécessaire avec `dokku config:set <nom_application> DATABASE_PASSWORD=<mot_de_passe>`

- Déployer l'application avec `git push dokku deploy:master`

**Attention** : En cas de problème, on peut forcer le push avec `git push -f dokku deploy:master`

- Créer un compte administrateur lors de la première connexion

- Sélectionner sur le site, une fois connecté.e avec le compte administrateur dans Admin > Général le [thème Etalab](https://github.com/etalab/q2a-theme-etalab) : 
-- Thème du site
-- Thème pour mobile

## Licence et contribution
