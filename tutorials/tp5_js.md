---
title: TP5 &ndash; Programmation web &ndash; Côté client &ndash; Javascript
subtitle:
layout: tutorial
---

## Introduction

Dans le [TP4](tp_php.html), nous avons amélioré le site de Chuck Norris en ajoutant des fonctionnalités **dynamiques** permettant d'interagir avec le serveur web.

Ce TP s'intéresse au côté **client**, c'est-à-dire votre navigateur.
Vous allez concenvoir des fonctionnalités permettant d'interagir directement avec la page, sans avoir besoin d'une quelconque connexion avec un serveur.
Ces fonctionnalités permettent de rajouter du **dynamisme** directement dans la page, en manipulant le contenu HTML via un programme codé avec le langage **Javascript**.

Tout comme le code **HTML** ou **CSS**, le **Javascript** (JS) est relié directement à la page. Il est donc visible et accessible par l'utilisateur (contrairement au code **PHP**).
On l'utilise quand on a besoin d'avoir une réponse programmée lors de l'interaction avec la page (clic sur un bouton, survol d'un élément, etc...).
Le JavaScript n'a donc pas besoin d'un serveur web pour fonctionner, le programme est directeemnt éxécuté sur le navigateur.

Là où le **PHP** s'intéresse principalement au traitement de données envoyées depuis le client, via des requêtes, le JavaScript va pouvoir gérer les actions de l'utilisateur sans avoir besoin de quitter ou recharger la page. 
Il va agir directement sur le code de la page courante.
Le but du **JavaScript** est donc très différent de celui de **PHP**, même si dans certains cas (que nous ne verrons pas cette année) il peut interagir avec le serveur, sa fonction principale est de manipuler la page, en réponse à des **événements**.

## Javascript

Lorsque l'utilisateur navigue sur une page web, différents **événements** peuvent survenir.

Ces **événements** sont liés aux actions de l'utilisateur sur la page web : Clic sur un élément, survol d'un élément, sélection d'une option une liste déroulante, et bien plus encore...

Lorsque l'un de ces événements survient, il peut être capté et traité par **JavaScript**.

Pour cela, il suffit de définir un **attribut** sur la balise HTML sur laquelle on souhaite rajouter la gestion d'un événement.
On spécifie ensuite la **fonction** Javascript que l'on souhaite appeller lorsque l'événement survient, au niveau de l'élément représenté par cette balise, dans la page web.

Voici une liste **non exhaustive** de ces attributs :

- `onClick` : L'utilisateur a cliqué sur l'élément.
- `onMouseover` : L'utilisateur survole l'élément.
- `onMouseout` : L'utilisateur arrête de survoler un élément.
- `onKeydown` : L'utilisateur appuis sur une touche, en étant à l'intérieur de l'élément.
- `onChange` : L'élément s'est mis à jour (par exemple, quand on sélectionne une option dans un liste déroulante).

Vous pouvez retrouver [la liste complète des évenements en ligne](https://www.w3schools.com/jsref/dom_obj_event.asp).
Il suffit de rajouter `on` devant le nom de l'événement.

Voici deux exemples d'utilisation de ces événements, dans le code HTML :

```html
<!-- Appelle la fonction "maFonctionUn" quand on clique sur le bouton-->
<button onClick="maFonctionUn()">Clique sur moi!</button>

<!-- Appelle la fonction "maFonctionDeux" quand on survole l'image-->
<img src="./img/monimage.png" onMouseover="maFonctionDeux()" alt="test">
```

Généralement, le code **Javascript** s'écrit dans un fichier à part (comme pour le **CSS**) qu'on relie à la page. Il faut ajouter une balise `<script>` dans la balise `<head>` de la page. 

Voici un exemple, si on imagine que le fichier **Javascript** se trouve dans : `./js/script.js` :

```html
<!DOCTYPE html>
<html>
	<head>
		<script src="./js/script.js"></script>
	</head>
	<body>
		...
	</body>
</html>
```

**Javascript** permet de manipuler un élément (variable) appellé **document**. Cet élément représente la page HTML courante, et propose différentes fonctions permettant de **sélectionner des sous éléments (balises) de la page** :

- `document.body` : Donne le **body** de la page.
- `document.getElementById("id")` : Récupère une balise de la page, en spécifiant son `id` en paramètres (attribut du même nom lié à la balise).
- `document.getElementsByClassName("classe")` : Récupère **une liste** de balises qui possèdent la classe (**CSS**) spécifiée en paramètre.
- `document.getElementsByTagName("tagname")` : Récupère **une liste** de balises qui possèdent du type spécifié en paramètre (img, p, ul, li, etc...).

```html
<div id="mainDiv" class="bleu">
	<h1 class="bleu">Bienvenue!</h1>
	<p id="par1">Bonjour!</p>
</div>
```

```javascript
var par1 = document.getElementById("par1");
var maDiv = document.getElementById("mainDiv");
var elementsBleus = document.getElementsByClassName("bleu");
```

Quand on récupère **une balise** du document, on peut alors la stocker dans une **variable** et manipuler ses **atributs**, son **contenu**. Ces modifications seront directement reportées sur la page.

Voici quelques attributs / fonctions que l'on peut modifier / appeller sur une balise de la page :

- `innerHTML` : Contenu de la balise (entre la balise ouvrante et fermante).
- `id` : Id de la balise.
- `classList` : Liste des classes de la balise.
- `classList.add("classe")` : Ajoute une classe à la balise.
- `classList.remove("classe")` : Enlève une classe à la balise.
- `value` : Valeur d'un champ input, select, texterea, etc...

```javascript
var par1 = document.getElementById("par1");
par1.classList.add("bleu"); //Ajout de la classe "bleu" sur cette balise
var maDiv = document.getElementById("mainDiv");
maDiv.classList.remove("bleu"); //Suppression de la classe "bleu" sur cette balise
par1.innerHTML = "Nouveau texte"; //Remplace le texte original "Bonjour!" par "Nouveau texte"
```

Il existe beaucoup de fonctions permettant de manipuler la balise. 
De manière générale, il suffit d'écrire `.nomAttribut` pour accèder et manipuler un des attributs de la balise.

Un attribut très intéressant est `style`. Celui-ci permet de modifier directement le **style CSS** appliqué à la balise.
Par exemple :

- `style.color` : Change la couleur du texte contenu dans la balise.
- `style.backgroundColor` : Change la couleur de fond.
- `style.fontSize` : Change la taille de la police du texte contenu dans la balise.

Si on change le **style** de `body`, cela affectera toute la page, car toutes les autres balises sont contenues dans le body.

```javascript
document.body.style.backgroundColor = "black"; //On change la couleur de fond de la page en noir.
var par1 = document.getElementById("par1");
par1.style.color = "white"; /*On change la couleur du texte de ce paragrpahe en blanc.*/
```

Enfin, il est possible de **créer de nouvelles balises et les ajouter à la page** directement depuis le code :

La fonction `document.createElement("nomBalise")` permet de créer la balise, en spécifiant le type de balise en paramètre.

La fonction `appendChild(balise)` permet d'ajouter la balise comme **enfant** (contenu) d'une autre balise. (Le body par exemple, ou une autre balise sélectionnée dans **document**).
```javascript
//Ajout image dans la page
var nouvelleImage = document.createElement("img");
nouvelleImage.src = "./img/test.png";
document.body.appendChild(nouvelleImage);
```

## De Python à Javascript

Comme nous l'avons fait avec **PHP**, nous allons comparer du code **Python** à du code **Javascript** afin que vous maîtrisiez ce langage, avant de vous lancer dans la programmation des ajouts sur le site de Chuck Norris.

Vous allez voir que `Javascript` est très proche de `PHP`, au niveau de la syntaxe.
### Code et instructions

- En **Javascript**, Toutes les instructions (code) **terminent par un point-virgule ``;``**
- On utilise `//` Pour commenter une ligne, et `/* ... */` pour commenter plusieurs lignes.

**Python**
```python
print("Hello world!")
#Commentaire d'une ligne
"""
	Commentaire de plusieurs lignes	
"""
```

**Javascript**
```javascript
console.log("Hello world!");
// Commentaire d'une ligne
/*
Commentaire de plusieurs lignes
*/
```

### Les variables

- En Javascript, quand on utilise une variable **pour la première fois**, on doit faire précéder son nom par le mot clé `var`. Cela s'appelle **une déclaration de variable**.
- La manipulation, l'affectation et la lecture de la variable est semblable à Python.
- Les opérateurs arithmétiques et opérateurs d'affectation sont les mêmes que pour Python (sauf le double diviser `//` qui n'existe pas).

**Python**
```python
a = 5
b = a + 2
b += 1
print(b) #Affiche 8
texte = "Bonjour"
texteBis = " le monde!"
texteFinal = texte + texteBis
print(texteFinal) #Affiche "Bonjour le monde!"
```

**Javascript**
```javascript
var a = 5;
var b = a + 2;
b += 1;
console.log(b); //Affiche 8
var texte = "Bonjour";
var texteBis = " le monde!";
var texteFinal = texte + texteBis;
console.log(texteFinal); //Affiche "Bonjour le monde!"
```

### Structures conditionnelles

- Le contenu d'une condition `if` est obligatoirement entre parenthèses.
- Le bloc conditionnel n'est pas délimité par deux points `:` et l'identation de python, mais par un bloc d'accolades `{ ... }`.
- Le `elif` n'existe pas, il faut écrire `else if`.
- Le `and` devient `&&` et le `or` devient `||`.
- Le `not` n'existe pas, il est remplacé par `!`.
- Les comparateurs (`=, !=, >=, >, <, <=, !=`) sont les mêmes que pour python.

**Python**
```python
#On suposse qu'on a défini une variable age plus tôt.
if age > 18:
    print("Majeur")
elif (age >= 12) and (age < 18):
    print("Ado")
elif (age >= 6) and (age < 12):
    print("Enfant")
elif (age < 0) or (age > 120):
	print("Age très improbable")
else:
    print("Pitchounou")
	
if(not(age % 2 == 0)):
    print("Age impair!")
```

**Javascript**
```javascript
//On suposse qu'on a défini une variable age plus tôt.
if (age > 18) {
    console.log("Majeur");
}
else if ((age >= 12) && (age < 18)) {
    console.log("Ado");
}
else if ((age >= 6) && (age < 12)) {
    console.log("Enfant");
}
else if ((age < 0) || (age > 120)) {
	console.log("Age très improbable");
}
else {
    console.log("Pitchounou");
}	
if(!(age % 2 == 0)) {
    console.log("Age impair!");
}
```

### Les boucles

#### Boucle while

- Même principe que pour une boucle en python, avec les mêmes spécificités de syntaxe que pour les structures conditionnelles (accolades, etc...).

**Python**
```python
#Affiche les nombres de 0 à 9.
i = 0
while(i < 10):
	print(i)
	i += 1
	
#Détermine au bout de combien d'années le capital dépassera 100000€ avec un taux de croissance de 20% par an.
capital = 1000
annee = 0
while (capital < 100000):
	capital = capital * 1.20
	annee += 1
print(annee)
```

**Javascript**
```javascript
//Affiche les nombres de 0 à 9.
var i = 0;
while(i < 10) {
	console.log(i);
	i += 1;
}

/*Détermine au bout de combien d'années le capital dépassera 100000€ avec un taux de croissance de 20% par an.*/
var capital = 1000
var annee = 0
while (capital < 100000) {
	capital = capital * 1.20;
	annee += 1;
}
console.log(annee);
```

#### Boucle for

- La boucle `for` diffère largement de celle de Python, en effet, on n'indique pas de `range` pour faire varier la variable, mais on utilise une sorte de while transformé où la variable du parcours est initialisée et incrémentée automatiquement.
- Le for est divisé en trois parties, séparées par un point-virgule `;`:
	- On initialise la variable du parcours (qu'on nomme comme on veut).
	- On donne la condition d'arrêt (comme pour un while). généralement, on place la borne à ne pas dépasser.
	- On indique comment la variable est incrémenté à la fin d'un tour de boucle.

**Python**
```python
#Affiche les nombres de 0 à 9.
for i in range(0, 10):
	print(i)

#Affiche les nombres de 15 à 1.
for i in range(15, 0, -1):
	print(i)
	
```

**Javascript**
```javascript
//Affiche les nombres de 0 à 9.
for(var i=0;i < 10; i+=1) {
	console.log(i);
}
/*Affiche les nombres de 15 à 1.*/
for(var i=15;i > 0; i-=1) {
	console.log(i);
}
```

### Les fonctions

- Le mot `def` est remplacé par `function`.
- De même que pour les structures condtionnelles, on utilise des accolades `{ ... }` pour délimiter le code de la fonction.
- Le `return` s'utilise de la même façon qu'avec Python.
- L'appel d'une fonction est aussi similaire.

**Python**
```python
def puissance(x, y):
	resultat = 1
	for i in range(0, y):
		resultat *= x
	return resultat
	
#Exemples de tests
print(puissance(2, 2)) #Affiche 4
print(puissance(3, 2)) #Affiche 9
```

**Javascript**
```javascript
function puissance(x, y) {
	var resultat = 1;
	for(var i = 0; i < y; i+=1) {
		resultat *= x;
	}
	return resultat;
}
	
//Exemples de tests
console.log(puissance(2, 2)); //Affiche 4
console.log(puissance(3, 2)); //Affiche 9
```

### Les tableaux
Comme pour **PHP**, il n'y a pas de tableaux à proprement parler (comme vous les avez vu) en Javascript, mais des **tableaux associatifs**.

Le principe est exactement le même que pour un **dictionnaire** : On associe des clés à des valeurs, dans la structure.

Si on veut manipuler cette structure comme un **tableau**, on utilise des clés numériques.

On utilisera donc cette même structure pour gérer un **tableau** ou **un dictionnaire**.

Différentes fonctions permettent de manipuler et d'ajouter des éléments à ce "tableau associatif".

**Python**
```python

#Tableaux
tab = [] #Initialise un tableau vide.
tab.append(5) #Ajoute 5 à la fin du tableau.
tab.append(7) #Ajoute 7 à la fin du tableau.
tab[1] #Lecture du deuxième élément du tableau.
tab[0] = 10 #Modification du premier élément du tableau.
a = tab.pop() #Retire le dernier élément du tableau.
len(tab) #Taille du tableau (nombre d'éléments contenu).

#Affiche tous les éléments du tableau
for i in range(0, len(tab)):
	print(tab[i])

#Dictionnaires
d = {} #Initialise un dictionnaire vide.
d["bonjour"] = 5 #Associe la clé "bonjour" à la valeur 5 dans le dictionnaire d
d["a"] = "c" #Associe la clé "a" à la valeur "c" dans le dictionnaire d

#Affiche tous les éléments du dictionnaire
for key in d.keys():
	print(d[key])
```

**Javascript**
```javascript
//Tableaux
var tab = []; /*Initialise un tableau vide.*/
tab.push(5); /*Ajoute 5 à la fin du tableau.*/
tab.push(7); /*Ajoute 7 à la fin du tableau.*/
tab[1]; /*Lecture du deuxième élément du tableau.*/
tab[0] = 10; /*Modification du premier élément du tableau.*/
a = tab.pop(); /*Retire le dernier élément du tableau.*/
tab.length; /*Taille du tableau (nombre d'éléments contenu).*/

/*Affiche tous les éléments du tableau*/
for(var i=0; i < tab.length; i+=1) {
	console.log(tab[i]);
}

/*Dictionnaires*/
var d = []; //Initialise un dictionnaire vide.
d["bonjour"] = 5; //Associe la clé "bonjour" à la valeur 5 dans le dictionnaire d
d["a"] = "c"; //Associe la clé "a" à la valeur "c" dans le dictionnaire d

/*Affiche tous les éléments du dictionnaire*/
for(var key in d) {
    console.log(d[key]);
}
```

## Premiers pas avec Javascript

Le code **Javascript** s'éxécute dans le navigateur. On peut directement l'éxécuter dans la console (`F12` puis `Console` sur votre navigateur).

Néanmoins, il existe des outils pour tester son code javascript plus confortablement.

Rendez vous donc sur [Jsfiddle](https://jsfiddle.net/). Vous coderez dans la section **JavaScript**, en bas à gauche.

Pour visualiser votre résultat, appuyez sur le bouton **Run** (tout en haut à gauche).

Le résultat devrait alors aparaître, il faut cliquer sur le bouton **Console** en bas de la section **Result**, en bas à droite.

Nous allons reprendre deux exercices du TP précédent. L'objectif est de passer rapidement sur les modifications du site de Chuck Norris.

<div class="exercise">
Sur [Jsfiddle](https://jsfiddle.net/), traduisez le programme Python ci-dessous en un programme Javascript.
```python
def nombre_chiffres(n):
    """
    Entrees :
        n : Nombre entier (int)
    Retourne le nombre de chiffres composant le nombre n.
    """
    nombre = n
    compteur = 1
    while(nombre >= 10):
        nombre = nombre // 10
        compteur += 1
    return compteur
    
#Exemples de test
print(nombre_chiffres(13250)) #Affiche 5
```
</div>

<div class="exercise">
Sur [Jsfiddle](https://jsfiddle.net/), traduisez le programme Python ci-dessous en un programme Javascript.

```python
def somme(tab):
    """
    Entrees :
        tab : Un tableau de nombres.
    Retourne la somme des nombres contenus dans le tableau tab.
    """
    s = 0
	for i in range(len(tab)):
		s += tab[i]
	return s
    
#Exemples de test
print(somme([1,2,5,4,8])) #Affiche 20
```
</div>

## Amélioration du site de Chuck Norris

Maintenant que vous maîtrisez la syntaxe de **JavaScript**, vous allez pouvoir ajouter quelques petites fonctionnalités dynamiques au site de Chuck Norris!

Il faudra **allumer Uwamp** car nous utilisons toujours une version du site codée, en partie, en PHP.

Avant toute chose, si vous n'aviez pas terminé le **TP4**, [téléchargez la correction]({{site.baseurl}}/corrections/correction_tp4_php.zip) et **remplacez votre dossier ``chuck-norris``** par celui de la correction. (Dans le dossier `www` de Uwamp).

Le premier exercice va consister à créer et relier à la page `index.php` le fichier **Javascript** qui contiendra votre code.
<div class="exercise">
- Dans le dossier `chuck-norris`, créez un dossier `js`.
- Ouvrez `Notepad++`, appuyez sur **Fichier** puis **Nouveau**.
- Entrez le code suivant : `console.log("Hello world!");`
- Sauvegardez votre fichier sous le nom de `script.js` (en sélectionnant le type **All types**) dans le dossier `js` crée précedemment.
- Ouvrez, avec `Notepad++` la pge `index.php`.
- Dans la section `<head> ... </head>` ajoutez le code pour inclure votre fichier, comme affiché plus bas.
- Rendez vous sur [http://localhost/chuck-norris/](http://localhost/chuck-norris/) et ouvrez la console (`F12` puis `Console`). Vous devriez visualiser le message "Hello world!".

```html
<head>
	...
	<script src="./js/script.js"></script>
</head>
```
</div>

Pour les exercices suivants, pensez à reagrder la section [Javascript](#javascript) de ce TP pour vous aider.

### Différents thèmes

Certains sites proposent différents **thèmes**. Il s'agit de changer la couleur de l'arrière plan et du texte selon la configuration choisie par l'utilisateur.

On souhaite proposer trois thèmes :

- Le thème par défaut : Fond gris et texte en noir (ce que nous utilisons acutellement).
- Le thème nuit : Fond noir et texte en blanc.
- Le thème clair : Fond blanc et texte en noir.

Pour implémenter cette fonctionnalités, nous allons ajouter trois boutons à la page `index.php` permettant de passer d'un thème à l'autre.

Le code HTML de cet ensemble de bouton sera :

```html
<div>
	<button onClick="changerCouleurFondDefaut()">Thème par défaut</button>
	<button onClick="changerCouleurFondNoir()">Thème nuit</button>
	<button onClick="changerCouleurFondBlanc()">Thème clair</button>
</div>
``` 

Comme vous l'aurez remarquer, on fait appel à l'événement `onClick`. Lorsque l'utilisateur cliquera sur le bouton, la fronction spécifiée sera appellée dans le code javascript.

Le code des trois fonctions est très similaire, il faut :

1. Récupérez le `body` de la page.
2. Changer la valeur de `backgroundColor` de l'attribut `style` du `body` selon le thème (**"black"** pour le thème nuit, **"white"** pour le thème clair, et **"#838892"** pour le thème par défaut).
3. Changer la valeur de `color` (couleur du texte) de l'attribut `style` du body selon le thème (**"white"** pour le thème nuit, **"black"** pour le thème clair et celui par défaut).

<div class="exercise">
- Placez le code de l'ensemble de bouton dans `index.php`, juste après le nombre de visiteurs, et juste avant la biographie.
- Implémentez le code des trois fonctions `changerCouleurFondDefaut`, `changerCouleurFondNoir` et `changerCouleurFondBlanc` dans le fichier `script.js` en suivant la méthode décrite ci-dessus.
- Rendez vous sur [http://localhost/chuck-norris/](http://localhost/chuck-norris/), cliquez sur les différents boutons et vérifiez que tout fonctionne bien comme attendu.
</div>
### Multilangue pour la citation

On aimerait maintenant avoir une option pour choisir la langue de la citation, tout au début de la page d'accueil.

Pour cela, on va placer une liste déroulante qui nous permettra de choisir entre anglais et français.

Pour implémenter le fonctionnement désiré, nous allons inclure, en avance, la citation traduite en anglais. mais celle-ci sera cachée, grâce à du **CSS**.

La fonction que vous devrez implémenter consistera a "révéler" la citation correspondate à la langue choisie, en masquant l'autre.

Le nouveau code de la balise `<blockquote>` aura donc cette allure :
```html
<blockquote>
	<select id="choixLangueCitation" onChange="changerLangueCitation()">
		<option value="fr">Français</option>
		<option value="en">Anglais</option>
	</select>
	<div id="citation-fr">
		<p>"Little John: Braddock ! Je vous préviens, attention où vous mettez les pieds !<br>
			Braddock : Je mets les pieds où je veux, Little John… et c'est souvent dans la gueule."</p>
		<cite>Chuck Norris, Portés disparus 3 (1988), écrit par Arthur Silver, Larry Levinson, James Bruner, Chuck Norris, Steve Bing</cite>
	</div>
	<div id="citation-en" class="invisible">
		<p>"Little John: Braddock! I'm warning you. Don't step on any toes !<br>
			Braddock : I don't step on toes, Littlejohn. I step on necks."</p>
		<cite>Chuck Norris, Missing in Action 3 (1988), written by Arthur Silver, Larry Levinson, James Bruner, Chuck Norris, Steve Bing</cite>
	</div>
</blockquote>
```

Il faudra alors ajouter une nouvelle classe CSS (dans le fichier `styles.css`) "invisible", permettant de rendre invisible un élément de la page HTML.

```css
.invisible {
	display:none;
}
```

L'algorithme de la fonction `changerLangueCitation` suivra la logique suivante :

1. On récupère, dans des variables, les balises correspondates aux IDs **"choixLangueCitation"**, **"citation-fr"** et **"citation-en"**.
2. On récupère la **valeur** sélectionnée dans la balise **"choixLangueCitation"**. Cela est accessible via l'attribut `value`.
3. Si cette valeur est "fr", on ajoute la classe "invisible" à la balise correspondante à **"citation-en"** et on enlève la classe **"invisible"** à la balise correspondante à **"citation-fr"**.
4. Si cette valeur est "en", on fait l'inverse.

<div class="exercise">
- Dans `index.php`, remplacez le code de la balise `<blockquote> ... </blockquote>` par le nouveau code proposé ci-dessus.
- Dans `styles.css` (dans le dossier `css`), ajoutez le code de la classe `.invisible`, disponnible ci-dessus.
- Implémentez le code de la fonction `changerLangueCitation` dans le fichier `script.js` en suivant la méthode décrite ci-dessus.
- Rendez vous sur [http://localhost/chuck-norris/](http://localhost/chuck-norris/), sélectionnez une langue, puis l'autre, et vérifiez que le texte de la citation est bien mis à jour.
</div>
### Rickroll

On veux faire croire aux utilisateurs qu'ils ont une chance de vaincre Chuck Norris (bien sûr, c'est impossible).

Nous allons "troller" l'utilisateur avec un meme bien connu : **Le rickroll**. Cela consiste à renvoyer l'utilisateur sur le clip **Never Gonna Give You Up** de **Rick Astley**.

Avant tout, nous allons inclure la section "piégée" à la fin de la page :

```html
<h2 class="impair">Vaincre Chuck Norris ?</h2>
	<p>Il est impossible de vaincre Chuck Norris. Il serait même inconveable de seulement y penser.
		Néamoins, vous pouvez toujours tenter votre chance en appuyant sur ce bouton : </p>
	<div id="rickroll" class="centre">
		<button id="buttonRick" onClick="rickroll()">Vaincre Chuck Norris</button>
	</div>
```

Pour centrer le bouton, il faut créer une nouvelle classe **CSS** dans le fichier **styles.css** :

```css
.centre {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

L'algorithme de la fonction `rickroll` suivra la logique suivante :

1. On récupère, dans des variables, les balises correspondates aux IDs **"buttonRick"** et **"rickroll"**.
2. On ajoute à la balise correspondante à **"buttonRick"** la classe **"invisible"**.
3. On **crée** une variable contenant une **nouvelle balise** **"iframe""**.
4. On configure les attributs de cette variable :
	1. `src` : **"https://www.youtube.com/embed/dQw4w9WgXcQ?autoplay=1"**
	2. `width` : **600**
	3. `height` : **400**
5. On ajoute cette variable comme **enfant** de la variable contenant la balise **"rickroll"**.

<div class="exercise">
- Dans `index.php`, ajoutez le code HTML contenant le bouton rickroll, proposé ci-dessus. Vous le placerez tout en bas de la page, avant le lien "Retour au début".
- Dans `styles.css` (dans le dossier `css`), ajoutez le code de la classe `.centre`, disponnible ci-dessus.
- Implémentez le code de la fonction `rickroll` dans le fichier `script.js` en suivant la méthode décrite ci-dessus.
- Rendez vous sur [http://localhost/chuck-norris/](http://localhost/chuck-norris/), appuyez sur le bouton "Vaincre Chuck Norris" et vérifiez que le **rickroll** se produit bien.
</div>
### Konami code

Le **Konami code** est un code permettant, dans certains jeux, de débloquer des secrets ou de tricher.

Il s'éxécute ainsi : **Haut, Haut, Bas, Bas, Gauche, Droite, Gauche, Droite, B, A**.

Ce code a été repris et caché dans certains sites web, pour déclencher une fonctionnalité cachée.

Nous allons implémenter le Konami Code sur le site de Chuck Norris. Pour cela on va ajouter la détection de l'événement `onKeydown` sur la balise `<html>` de notre page.
Cela permettra de détecter quand l'utilisateur appuis sur des touches de son clavier.

 ```html
<html onKeydown="checkKonami(event)">
...
</html>
```

Voici une partie du code **JavaScript** qui permettra de réaliser cette fonctionnalité :

```javascript
var konami_keys = [38, 38, 40, 40, 37, 39, 37, 39, 66, 65];
n_konami = 0;

function checkKonami(event) {
	key = event.keyCode;
	if(key == konami_keys[n_konami]) {
		n_konami = ???;
		if(n_konami == ???) {
			declencherKonami();
			n_konami = ???;
		}
	}
	else {
		n_konami = ???;
	}
}

function declencherKonami() {
	var iframe = document.createElement("iframe");
	iframe.src = "https://www.youtube.com/embed/YZ3XjVVNagU?autoplay=1";
	iframe.style.display = "None";
	document.body.appendChild(iframe);
	all_images = document.getElementsByTagName("img");
	for(var i =0; i < all_images.length; i++) {
		img = all_images[i];
		img.src = "https://media.tenor.com/images/0a49a9f1ea824ca712bd5e2f7c5a95fd/tenor.gif"
	}
}
```

La logique du code de la fonction `checkKonami` est la suivante :

1. On a un tableau `konami_keys` contenant, dans l'ordre, le code numérique des touches sur lequelles l'utilisateur doit appuyer pour délncher le code.
2. La variable `n_konami` compte le nombre de touches **validées**, c'est-à-dire, sur combien de touches du code a déjà appuyé l'utilisateur.
3. Lorsque l'utilisateur appuis sur une mauvaise touche, on remet `n_konami` à 0.
4. Lorsque l'utilisateur appuis sur une bonne touche, on incrémente `n_konami` de 1.
5. Lorsque l'utilisateur a appuyé sur toutes les bonnes touches (`n_konami` est donc égal au nombres d'éléments dans `konami_keys`), on déclenche la fonctionnalité cachée et on remet `n_konami` à 0.

<div class="exercise">
- Dans `index.php`, ajoutez la gestion de l'événement `onKeydown` sur la balise `<html>` comme présenté dans le code HTML ci-dessus.".
- Copiez le code **Javascript** ci-dessus dans le fichier `script.js` et complétez le code de la fonction `checkKonami` (en remplaçant les `???`) en suivant la méthode décrite ci-dessus.
- Rendez vous sur [http://localhost/chuck-norris/](http://localhost/chuck-norris/), et tapez le konami code sur votre clavier, en restant sur la page. Vérifiez que quelque chose se passe bien.
</div>