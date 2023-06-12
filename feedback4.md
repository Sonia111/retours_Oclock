
C'est bien de partir sur une architecture MVC et avoir une structure bien organisée de code , mais ils y a quelques corrections
et améliorations qu'on doit ajouter :


Les points qu’on doit ajouter :

1- App doit etre en miniscule : app pas App. (pour plus d'informations on peut voir les PSR en PHP )

2 -  Avec Apache, il est possible de réécrire les liens pour rendre transparente l'opération.
on doit l’ajouter sous le dossier public un fichier .htaccess avec ce code :

```bash
RewriteEngine On (dynamically setup base URI)
RewriteCond %{REQUEST_URI}::$1 ^(/.+)/(.*)::\2$
RewriteRule ^(.*) - [E=BASE_URI:%1] (redirect every request to index.php  and give the relative URL in "_url" GET param)
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f  (rediriger TOUTES les requêtes qui mène au dossier dans lequel se trouve le .htaccess vers index.php)
RewriteRule ^(.*)$ index.php [QSA,L]
```

Nous pouvons donc maintenant écrire :

home.html (index.php?page=home)

En faite , Le fichier .htaccess est un fichier de configuration Apache . Le fichier est extrêmement puissant
et peut être utilisé pour aider à contrôler plusieurs facettes de pages Web qui sont servies par Apache.
Cela inclut des éléments tels que la gestion des redirections, la protection des liens dynamiques, etc

Que ce soit d’un point de vue SEO ou expérience utilisateur, ce fichier est un élément clé d’une application web.

Pour plus d’informations :
https://httpd.apache.org/docs/2.4/fr/howto/htaccess.html

 
3-  on doit ajouter la liste des routes et on définit  la liste des permissions pour ces routes qui
nécessitant une connexion utilisateur dans CoreControlleur.

4- Il n'y a pas de répertoire assets qui va contenir le dossier css. On l’ajoute sous le dossier public de cette façon :

public
   assets
     css
     images
     js


Les améliorations :

1- Dans le fichier index.php on peut  faire extraire les routes dans un fichier qu’on peut appeler “routes.php”
et on le place sous la racine de projet , et après dans ce fichier index.php on fait l’inclure
comme ca:  require __DIR__ . '/../app/routes.php';


2- Pas besoin d'ajouter sous Utills les dossier data.sql et structure.sql.

3 - Dans  le dossier Views/Students ,on peut rassembler l'implémentation de l'ajout et de la mise ç jour de student dans le meme template.
(pareil pour Teachers et appuser) ( C'est mieux de remplacer Students par Student et Teachers par Teacher)


==> C'est bien d'avoir une bonne conception de projet , mais on peut améliorer surtout cotés Views , on peut avoir moins de templates 
donc plus de performance pour l'application.


Merci de me tenir au courant s’il y a des points qui ne sont pas clairs. 
