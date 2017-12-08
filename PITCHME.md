# Apprendre AnguarJS Part 1

## HITEMA - Par Ariel Dorol

---

# Qu'est-ce que Angular.js ?

- Angular.js est un framework JavaScript crée chez Google
- Basé sur le(s) pattern(s) (MVC, MVVM, MV* Whatever)
- Permet de créer des applications web côté front-end
- Permet d'accélrer la création d'une SPA

---

# SP quoi ? SPA !

Tout d'abord, éclaircisson un point.

### Qu'est-ce qu'une SPA

Une SPA (single page application) est une application web accessible via une page web unique.

Autrement dit, on peut naviguer sans recharger la page entièrement.

---

#  Site web classique VS SPA

- Première page chargée rapidement
- Pages suivantes plus lentes
- Serveur renvoie du HTML pour chaque requête
- La logique est faite SURTOUT côté serveur

---

![image](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/dev4634/single-page-application-and-angular-js-background/Images/1pagelifecycle.jpg)

---

#  Site web classique VS SPA

- Première page chargée un peu lentement
- Pages suivantes beaucoup plus rapides
- Serveur renvoie du JSON / XML pour chaque requête (sauf la 1ère)
- La logique est faite AUTANT côté client que serveur

---

![image](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/rahul4_saxena/single-page-application-spa-using-angularjs-web-api-and-m/Images/SAP%20Lifecycle.jpg)

--- 

# Pourquoi Angular ? Pourquoi les frameworks ?

- 2006, jQuery arrive et le JS prends de l'ampleur
- Mais... jQuery est une librairie sans structure
- 2010, il y a de plus en plus d'applications web complexes
- Les apps deviennent dur à maintenir
- La logique métier est très présente côté front
- Le front-end web commence à séparer les données du visuel / rendu

Ainsi, les frameworks comme Backbone.js et Angular.js sont apparus pour résoudre ce problème.

---

# Installation

Il y a 3 moyens d'installer Angular.js :

- Une balise script vers le fichier local ou un CDN
```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.6/angular.min.js"></script>
```
- npm `npm install angularjs` OU yarn `yarn add angularjs`
- bower `bower install angularjs`

---

# Les directives et le template

Angular.js fonctionne sur un principe propre à lui : les directives.

Les directives :
- Indique au template HTML comment réagir aux données et à Angular
- Sont commes des attributs magiques
- Nous évite de manipuler le DOM manuellement
- Commencent souvent par **ng-**

La première directive c'est `ng-app`.

Elle indique à Angular sur quelle balise il peut commencer à agir.

---

# Les directives et le template : ng-app

```
<!doctype html>
<html ng-app>
  <head>
    <script src="://ajax.googleapis.com/ajax/libs/angularjs/1.6.6/angular.min.js"></script>
  </head>
  <body> ... </body>
</html>
```

Ici, on plug Angular sur TOUTE notre page

---

# Les directives et le template : ng-init

Une directive importante aussi c'est `ng-init`.

- Elle sert à initialiser des variables
- Les directives peuvent prendre en valeur des expressions JS
- Les expressions peuvent aussi être entre accolades {{ }}

```
<div ng-init="firstname = 'Sam'">
    Bonjour <strong>{{ firstname }}</strong>
</div>
```

---

# Les directives et le template : expressions

- Les expressions doivent être courtes
- Les expressions n'ont pas accès aux variables globales de window (scope Angular)
- Les expressions n'ont pas besoin de **var** devant les variables
- Les expressions peuvent être dans des attributs "normaux"

```
<div ng-init="std = { firstname: 'Orelsan', birthyear: 1990 }; age = 2017 - std.birthyear">
    Bonjour <strong>{{ std.firstname }}</strong> tu es {{ age > 18 ? 'majeur' : 'mineur'  }}
    <p title="{{ std.birthyear }}">survol moi pour voir mon année de naissance</p>
</div>
```

---

# Les directives et le template : events

- On peut écouter des événements grâce à des directives
- Une directive d'événement a accès à une variable spécial : **$event**
- **$event** représente l'objet event en JS

```
<div ng-init="firstname = 'Bruce'">
    <p>Je suis {{ firstname }}</p>
    <p>
        <a href="//google.com" ng-click="$event.preventDefault(); firstname = 'Eren jaeger'">
            Change de nom
        </a>
    </p>
</div>
```

---

# Les directives et le template : TP

## Le compteur

Créez un compteur avec un bouton **plus** et un bouton **moins** qui vont incrémenter ou décrémenter un nombre affiché à l'écran.

---

```
<div ng-init="count = 0">
    <div>{{ count }}</div>
    <button ng-click="count = count + 1">plus</button>
    <button ng-click="count = count - 1">moins</button>
</div>
```

---

# Les directives et le template : TP suite

## Limiter le compteur

En sachant que vous pouvez mettre des expressions JS, limitez le compteur à : 

- maximum : 20
- minimum : 0

---

```
<div ng-init="count = 0">
    <div>{{ count }}</div>
    <button ng-click="count = count < 20 ? count + 1 : 20">plus</button>
    <button ng-click="count = count > 0 ? count - 1 : 0">moins</button>
</div>
```

OU

```
<div ng-init="count = 0">
    <div>{{ count }}</div>
    <button ng-click="count < 20 && (count = count + 1)">plus</button>
    <button ng-click="count > 0 && (count = count - 1)">moins</button>
</div>
```

---

# Le data-binding (système MVVM)

Dans un système MVC classique (serveur) on a ceci :

![image](https://docs.angularjs.org/img/One_Way_Data_Binding.png)

---

# Le data-binding (système MVVM)

Me système Angular cela va dans les deux sens.

Donc, on a plutôt ceci (two-way-data-binding) :

![image](https://docs.angularjs.org/img/Two_Way_Data_Binding.png)

---

# Le data-binding (système MVVM)

On obtient ce two-way-data-binding en récupérant les entrées de l'utilisateur.

Pour cela, on a besoin de la directive `ng-model`.

```
<div>
    <p><input type="text" ng-model="firstname"></p>
    <p>Bonjour <strong>{{ firstname }}</strong><p>
    <p><button ng-click="firstname = ''">vider le champ</button></p>
</div>
```

---

# Le data-binding (système MVVM)

Dans l'ordre :
- Le champ input est lié à la varaible `firstname`
- La variable `firstname` est affichée dans le template
- Quand la valeur du champ change, `firstname` prends sa valeur
- La variable `firstname` est updatée dans le template
- Quand on click sur le bouton, `firstname` change encore de valeur
- Le champ et le template sont updaté par rapport à `firstname`

Cela va dans les 2 sens, entrées <=> sorties

---

# Le data-binding (système MVVM) : TP

## Quel âge as-tu ?

Créez deux champs : 
- Un permet de récupérer l'année de naissance
- L'autre permet de récupérer l'année futur (cette année ou plus)

Affichez ensuite l'âge de l'utilisateur en fonction de ce qui est rentré dans chaque champ.

---

# Le data-binding (système MVVM) : TP

## Inverser les caractères du mot

- Créez un champ qui permet de rentrer un mot
- Affichez le mot rentré en caractères inversés
- Affichez le nombre de caractères dans le mot

---

# Le data-binding (système MVVM) : TP

## Bloquer le bouton

- Créez une case à cocher et un bouton content le mot "envoyer"
- Bloquez le bouton si la case à chocher vaut false

TIP : cherchez par rapport à l'attribut HTML disabled

---

# Les directives conditionnelles

Angular permet d'ajouter une logique conditionnelle liée aux balises HTML.
Chacune des directives peut contenir une expression renvoyant **true** ou **false**.

- `ng-if` permet de supprimer (false) / ajouter (true) un élément du DOM
- `ng-show` permet d'afficher un élément du template si c'est **true**
- `ng-hide` permet de cacher un élément du template si c'est **true**

---

# Les directives conditionnelles

## Différence entre `ng-if` et `ng-show` / `ng-hide` : 

- `ng-show` & `ng-hide` ne font que manipuler le style display
- `ng-if` manipule la présence dans le DOM

---

# Les directives conditionnelles : TP

## Modal

- Créez un paragraphe avec la phrase : "Quel est ton nom ?"
- Créez en dessous un bouton "répondre"
- Quand on click sur le bouton, une modal apparait
- La modal contient un champ pour rentrer le nom et un bouton pour valider
- Quand on click sur valider, la modal se ferme
- La paragraphe "Quel est ton nom ?" n'est plus affiché
- Un paragraphe "Ton nom est XXX" est affiché, où **XXX** représente la valeur rentrée

---

# Les attributs spéciaux

Il y a quelque attributs HTML spéciaux qui ne peuvent pas avoir d'interpolation.

Ce sont les attributs : **href** et **src**.

## Pourquoi ?

Car la navigateur charge les sources plus vite qu'angular.

Utilisez  à la place :

- `ng-href="http://monlien.fr/{{page_id}}"`
- `ng-src="http://monlien.fr/{{page_id}}"` 

---

# Les attributs spéciaux

Certains attributs ont besoin de valeurs booléens, pour ceux-là, vous avez des directives aussi.

- `ng-selected="expression"` : qui sert à définir la balise option selectionnée
- `ng-checked="expression"` : qui sert à définir la valeur cochée d'une checkbox
- `ng-disabled="expression"` : qui sert à définir si un élément est disabled
- `ng-selected="expression"` : qui sert à définir la balise option selectionnée

---

# Les Modules & Controllers

On a jusqu'à présent fait de la logique simple. Pour de la logique plus complexe, on peut créer un **controller** qui va détenir plus de logique et nous éviter de faire trop de **ng-init** et surtout permettre de définir des fonctions.

Un controller a besoin d'un module, chaque app angular aura toujours un module qui est là pour rassembler : des controllers, des services, des directives persos...

Le nom du module est à préciser sur la directive `ng-app`.
Le nom du controller est à préciser sur la directive `ng-controller`.

---

# Les Modules & Controllers

Un controller se définit comme ceci :

```javascript
var app = angular.module('monModule', []);

app.controller('MonController', MonControllerFunc);

function MonControllerFunc() {

}
```

---

# Les Modules & Controllers

Dans un controller on peut définir des propriétés et des methods à exposer dans le template.

Pour cela, on les ajoute sur le scope. Chaque controller peut injecter des dépendances dynamiquement grâce aux paramètres.

Le nom des paramètres à son importance car c'est comme cela qu'Angular sait quelle dépendance importer.

Dans un controller on a accès à tout le JS normal, donc les variables globales aussi.

---

# Les Modules & Controllers

```javascript
var app = angular.module('monModule', []);

app.controller('MonController', MonControllerFunc);

function MonControllerFunc($scope) {
    $scope.firstname = 'Sasuke';
    $scope.lastname = 'Uchiha';

    $scope.getName = function() {
         window.alert($scope.firstname + ' ' + $scope.lastname);
    }
}
```

---

# Les Modules & Controllers

```
<!DOCTYPE html>
<html ng-app="monModule">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div ng-controller="MonController">
        pour connaître mon nom <button ng-click="getName()">click ici</button>
    </div>
</body>
</html>
```

---

# Les Modules & Controllers

Attention, les dépendances sont injectées dynamiquement grâce à leur nom, donc, en cas de minification de votre code, ça ne marche plus.

## Pourquoi ?

Car **$scope** par exemple deviendra peut être **a** et angular ne saura pas de quelle dépendance il s'agit. Pour pallier à ce soucis on écrira le controller comme ceci :

---

# Les Modules & Controllers


```javascript
var app = angular.module('monModule', []);

app.controller('MonController', MonControllerFunc);

function MonControllerFunc($scope, $timeout) {}
MyController.$inject = ['$scope', '$timeout'];
```

OU sinon une autre manière encore :

---

# Les Modules & Controllers

```javascript
var app = angular.module('monModule', []);

app.controller('MonController', ['$scope', '$timeout', MonControllerFunc]);

function MonControllerFunc($scope, $timeout) {}
```

Pour en savoir plus : https://docs.angularjs.org/guide/di

---

# La validation de formulaire

Angular permet de valider des champs out-of-the-box.

Pour rendre un formulaire "validable", il vous faut ajouter plusieurs choses obligatoires : 

- Une balise **form** avec un attribut **name** et **novalidate**
- Chaque champ du **form** doit avoir un attribut **name** et une directive **ng-model**
- Un formluaire doit forcément être entouré d'une balise avec un controller

---

# La validation de formulaire

Vous pouvez ensuite ajouter plein de types de validation :

https://docs.angularjs.org/api/ng/type/form.FormController

```
<form name="contact" novalidate>
    <input type="email" name="u_mail" ng-model="u_mail" required>
    <!-- les erreurs en général -->
    <p ng-show="contact.$submitted && contact.$invalid">Le formulaire est invalid</p>
    <p ng-show="contact.$submitted && contact.u_mail.$invalid">Le champ est invalid</p>
    <!-- sinon plus précis -->
    <p ng-show="contact.$submitted && contact.u_mail.$error.email">Le champ a un email invalid</p>
    <p ng-show="contact.$submitted && contact.u_mail.$error.maxlength">Le champ est trop long</p>
    <p><input type="submit"></p>
</form>
```

---

# La validation de formulaire

Quand vous ajoutez un **name** sur le formulaire, la valeur de cet attribut se retrouve sur le **$scope** car Angular detecte votre formulaire au sein de **chaque controller** et le bind automatiquement sur le scope.

Dans votre controller vous pouvez donc utiliser plein de fonctions du formulaire, voir : 

https://docs.angularjs.org/api/ng/type/form.FormController

---

# La validation de formulaire

Sur le formulaire vous avez accès au champ grâce à leur name.

Pour un form avec le name "contact" et un champ avec un name "firstname" vous pouvez donc faire `contact.firstname` pour accèder au champ et vérifier ses erreurs comme dans l'exemple du slide précédent.
