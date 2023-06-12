J’ai bien apprécié ton travail , la conception et la structure de projet est bien organisé ,
mais il y a quelques points qu’on doit ajouter ensemble et d’autres points  qui nécessitent des améliorations :

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


2- Il n'y a pas de répertoire assets qui va contenir le dossier css. On l’ajoute sous le dossier public de cette façon :
```bash
public
    assets
     css
     images
      js
```

3- Ajouter ce template add-update.tpl.php sous user dans Views.


Les améliorations :

1- Dans le fichier index.php on peut  faire extraire les routes dans un fichier qu’on peut appeler “routes.php” 
et on le place sous la racine de projet , et après dans ce fichier index.php on fait l’inclure 
comme ca: 
```bash
 require __DIR__ . '/../app/routes.php';
 ```

2 - Dans le fichier index.php et dans l’implémentation des routes il y a la fonction 
map qui peut prendre en paramètre les 2 méthodes GET et POST , donc on peut éviter les redondances et
l’améliorer comme ça : ( exemple ici pour l’ajout de student)

```bash
$router->map(
'GET | POST',
'/students/add',
[
'method' => 'studentAddGet',
'controller' => StudentController::class
],
'student_add_get'
);
```
3- Dans le controlleur  CoreControlleur  : il y a une répétition :

```bash
'student_update_get' => ['admin', 'user'],
'student_update_get' => ['admin', 'user'],
```


4- Dans le controlleur  CoreControlleur Mettre les accès et les autorisations aux
routes dans un fichier à part sous la racine de projet , par exemple on le nomme 
un fichier acl.php  ,puis on fait l’inclure comme ca: 

```bash
require __DIR__ . '/../acl.php';
```

5 - Renommer user sous Views avec appuser;
6 - Sous  les templates Student et Teacher on peut rassembler l'ajout et la mise à jour dans une seule template.


==> C'est bien d'avoir une bonne conception et une bonne  structure d'un projet , mais il faut éviter les redondances et
respecter les PSR ( par exemple un fichier php si on peut le segmenter c'est mieux , pour ne pas avoir un fichier lent , et chaque
fichier  doit avoir un retour bien déterminé , cà va infulencer sur la performance de l'application )

Merci de me tenir au courant s’il y a des points qui ne sont pas clairs. 






