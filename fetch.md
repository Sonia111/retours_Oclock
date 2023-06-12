

Fetch c'est une fonction JavaScript native qui permet de faire des requêtes Ajax.
Les requêtes Ajax ce sont des requêtes HTTP que l'on fait depuis le JavaScript du navigateur vers un serveur.

C'est à dire que le navigateur va chercher des informations sur un serveur pour rafraîchir
la page web qu'il est en train d'afficher et cela sans la recharger.


Avant que fetch existe on utilisait pour faire nos requêtes Ajax une interface qui s'appelle XMLHttpRequest. 

Alors pourquoi utiliser fetch ?  Et bien la raison essentielle c'est que fetch travaille avec des promesses.

Et c'est quoi une promesse?

Avec les promesses vous avez la possibilité de chaîner les opérations asynchrones. 
Ca permet de les écrire les unes en dessous des autres et de les exécuter les unes après les autres.

Vous allez avoir du code qui va ressembler au pseudo code ci-dessous et qui sera très lisible. C'est ça l'avantage.

```bash

requete1.then(
         traiter la réussite de la réquete 1
         puis lancer la requete 2
        )
        .then(
        traiter la réussite de la réquete 2
        puis lancer la requete 3
        )
        .then(
        ...
        )
        .catch(
        Traiter une erreur dans l'une des requetes 
        )
```
Par exemple on va tester dans la console de navigateur une route d'ajout de teacher avec Fetch: 

```bash
fetch("http://localhost:80/teachers/add", {
        method: "POST",
        headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
        },
        body: JSON.stringify({
        firstname: 'Sonia',
        lastname: 'BEN RACHED'
        })
})
.then(response => response.json())
.then(response => alert(response))
.catch(error => alert("Erreur : " + error));
```