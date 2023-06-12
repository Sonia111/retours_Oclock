
C'est bien de partir sur une architecture MVC et avoir une structure bien organisée de code , mais ils y a quelques corrections
et améliorations qu'on doit ajouter :


Les points qu’on doit ajouter :

1 -  Avec Apache, il est possible de réécrire les liens pour rendre transparente l'opération.
on doit l’ajouter sous le dossier public un fichier .htaccess avec ce code :

```bash
RewriteEngine On (dynamically setup base URI)
RewriteCond %{REQUEST_URI}::$1 ^(/.+)/(.*)::\2$
RewriteRule ^(.*) - [E=BASE_URI:%1] 
# redirect every request to index.php  and give the relative URL in "_url" GET param)
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f  
# rediriger TOUTES les requêtes qui mène au dossier dans lequel se trouve le .htaccess vers index.php)
RewriteRule ^(.*)$ index.php [QSA,L]
```

Nous pouvons donc maintenant écrire :
```bash
home.html (index.php?page=home)
```

En faite , Le fichier .htaccess est un fichier de configuration Apache . Le fichier est extrêmement puissant
et peut être utilisé pour aider à contrôler plusieurs facettes de pages Web qui sont servies par Apache.
Cela inclut des éléments tels que la gestion des redirections, la protection des liens dynamiques, etc

Que ce soit d’un point de vue SEO ou expérience utilisateur, ce fichier est un élément clé d’une application web.

Pour plus d’informations :
https://httpd.apache.org/docs/2.4/fr/howto/htaccess.html


2 - Il n' y a pas le modéle AppUser qui est déja présent dans la conception dans structure.sql.

3 - Dans le controlleur on doit gérer la connexion des utilisateurs , on peut ajouter un controlleur qui s'appelle AppUserController 
et on gére ici la connexion.
 
4-  on doit ajouter la liste des routes et on définit  la liste des permissions pour ces routes qui
nécessitant une connexion utilisateur dans CoreControlleur.

5- Il n'y a pas de répertoire assets qui va contenir le dossier css. On l’ajoute sous le dossier public de cette façon :

```bash
public
   assets
     css
     images
     js
```



Les améliorations :

1- Dans le fichier index.php on peut  faire extraire les routes dans un fichier qu’on peut appeler “routes.php”
et on le place sous la racine de projet , et après dans ce fichier index.php on fait l’inclure
comme ca:  

```bash
require __DIR__ . '/../app/routes.php';
```

2- Dans Views il manque les templates connexion des utilisateurs et des erreurs et de navigation.

3 - Dans  le dossier Views/Students y a pas les templates  de mise a jour , on peut ajouter l'implémentation dans l'ajout de student.
4- Dans  le dossier Views/Teachers pas de templates de mise ç jour , on peut ajouter l'implémentation dans l'ajout de teacher. 


==> La conception est l'étape la plus importante dans le projet ,
il faut toujours respecter le modéle de conception et la structure de base des données,
vérifier les bonnes entités , leurs relations .


Merci de me tenir au courant s’il y a des points qui ne sont pas clairs. 
