---
title: TP4 &ndash; Programmation web &ndash; Côté serveur &ndash; PHP
subtitle:
layout: tutorial
---

## Introduction

Dans le [TP3](tp3.html), nous avons vu comment créer des forumalire sur un site avec HTML.
Or, la finalité de ce type de formulaire est d'envoyer des données vers **un serveur web** afin de les traiter et de renvoyer une nouvelle page à l'utilisateur.

On a donc la nécéssité d'avoir **un programme** permettant de réaliser des actions et construire une page web selon les données transmisses et connues du serveur.
Cela permet de passer d'un site web **statique** à un site web **dynamique**, qui réagit, de manière automatisée, aux actions de l'utilisateur.
A partir de là, il est possible d'implanter de nombreuses fonctionnalités, par exemple :
- Une fonctionnalité d'inscription.
- Une fonctionnalité de connexion.
- Recherche de contenu.
- Publication d'un message, message dans un chat, article, tweet...
	
Par ailleurs, les possibilités offertent par la programmation côté serveur permettent de réaliser des fonctionnalités sans lien avec les formulaires, par exemple :
- Afficher le contenu d'une base de données (exemple : vidéos sur youtube, articles d'un blog)
- Afficher la date du jour.
- Afficher la liste des utilisateurs d'un site.
- Espace membres.
- Afficher le nombre de connexion...

Lors de ce TP, vous allez donc découvrir le langage de programmation **PHP** qui vous permettra d'améliorer le site de Chuck Norris en lui ajoutant de nouvelles fonctionnalités **dynamiques**.
Assurez vous d'avoir bien compris les concepts liés à [la programmation web côté serveur](cours_prog_web.html).

## Installation et éxécution de Uwamp

Pour réaliser ce TP, vous aurez besoin du logiciel **Uwamp** permettant d'éxécuter simplement un **serveur web**.
Suivez les étapes suivantes :
1. Téléchargez [l'archive contenant Uwamp](https://www.uwamp.com/file/UwAmp.zip).
2. Déplacez l'archive **.zip** dans le dossier **Documents** de votre ordinateur.
3. Extrayez l'archive : Effectuez un clic droit &#8594; 7zip &#8594; Extraire ici. Un dossier **Uwamp** devrait apparaitre.
4. Ouvrez le dossier **Uwamp**, puis **éxécutez** le fichier **Uwamp.exe**.
5. Une fenêtre s'affiche, assurez vous que **Apache** soit bien sur l'état "démarré" (en haut à droite).
6. Ne fermez pas la fenêtre de **Uwamp**.
7. Cliquez sur le bouton **"Dossier www"**. Gardez celui-ci ouvert, ce sera votre dossier de travail pour ce TP.
8. Pour vérifier que tout fonctionne, cliquez sur **"Navigateur www"**. Une page web intitulée Uwamp devrait s'ouvrir.

*Si jamais la fenêtre Uwamp disparait, vous pouvez la ré-ouvrir dans la barre des tâches de Windows, en bas à droite.*
## Le langage PHP

Vous allez devoir, au cours de ce TP, manipuler le langage **PHP**.
Nous allons donc voir son fonctionnement général, et ses spécificités.

### PHP comme langage de génération de pages Web

**PHP sert à créer des documents HTML :**

* Il prend donc en entrée un fichier `.php` <!-- qui contient de l'HTML et du PHP -->
* Il ressort un document HTML
* Pour cela, il exécute les instructions PHP qui lui indique comment générer le
document en sortie.

**Remarque :** PHP peut en générer tout type de document, pas nécessairement du
  HTML.

<!-- Rq 04/09/2019 : Confus de dire contient de l'HTML et du PHP ?
                     Sortie standard
-->

<section>

### Votre premier fichier PHP

Document PHP en entrée :

```php
<?php
  echo "Hello World!";
?>
```

PHP s'exécute sur ce document et produit

```text
Hello World
```

**Explications :**

* Les balises ouvrantes `<?php` et fermantes `?>` doivent entourer le code PHP

* L'instruction `echo` a pour effet d'insérer du texte dans le document en sortie

</section>
<section>

### Imbrication de PHP dans le HTML

Le document `PHP` suivant

```php
<!DOCTYPE html>
<html>
    <head>
        <title> Mon premier php </title>
    </head>
    <body>
      <?php echo "Bonjour"; ?>
    </body>
</html>
```

Produira :

```html
<!DOCTYPE html>
<html>
    <head>
        <title> Mon premier php </title>
    </head>
    <body>
      Bonjour
    </body>
</html>
```

<br>
En fait, les deux fichiers suivants sont équivalents.  

```php
<!DOCTYPE html>
<html>
    <head>
        <title> Mon premier php </title>
    </head>
    <body>
      <?php echo "Bonjour"; ?>
    </body>
</html>
```

```php
<?php
  echo "<!DOCTYPE html>";
  echo "<html>
      <head>
          <title> Mon premier php </title>
      </head>
      <body>";
  echo "Bonjour";
  echo "</body></html>"; ?>
```

En effet, ce qui est en dehors des balises PHP est écrit tel quel dans la page
Web générée (comme si on avait fait `echo`).
</section>

<section>
### Test de la page sur votre serveur HTTP

* Enregistrons ce fichier PHP sur le votre serveur HTTP qui s'écécute grâce à Uwamp. 

* Les fichiers PHP se mettent dans le dossier `www` du dossier `Uwamp`, vous pouvez alors y accéder à partir de l'URL
[http://localhost/](http://localhost/).

<div class="exercise">
1. Ecrivez le fichier `bonjour.php` (ci-dessous) et enregsitrez le dans votre dossier `www` :
2. Ouvrez [http://localhost/bonjour.php](http://localhost/bonjour.php) pour voir la page générée.
3. Regardez les sources pour voir la page complète (Rappel : `CTRL+U`).

```php
<!DOCTYPE html>
<html>
	<head>
		<title> Mon premier php </title>
    </head>
    <body>
		<?php echo "Bonjour"; ?>
    </body>
</html>
  ```
</div>


</section>

## De Python à PHP

Vous allez maintenant apprendre à coder en PHP.

Tout au long de l'année, vous avez appris à programmer avec **Python**.

Chaque langage a ses spécificités et sa syntaxe, mais les concepts restent les mêmes!
Vous allez vous apperçevoir que l'apprentissage des bases d'un nouveau langage est assez rapide : 
Il suffit de comparer le code de concepts élémentaires de programmation avec un langage que vous connaissez déjà.

Dans cette section, nous allons donc comparer le code **Python** de ces concepts clés à leur équivalent en **PHP**.

### Code et instructions

- En PHP, les sections **contenant du code** se trouvent entre des balises `<?php ... ?>`
- Toutes les instructions (code) **terminent par un point-virgule ``;``**
- On utilise `//` Pour commenter une ligne, et `/* ... */` pour commenter plusieurs lignes.

**Python**
```python
print("Hello world!")
#Commentaire d'une ligne
"""
	Commentaire de plusieurs lignes	
"""
```

**PHP**
```php
<?php
echo "Hello world!";
//Commentaire d'une ligne
/*
	Commentaire de plusieurs lignes
*/
?>
```

### Les variables

- En PHP, le nom des variables est **toujours précédé d'un dollar ``$``**
- La manipulation, l'affectation et la lecture de la variable est semblable à Python.
- Les [opérateurs arithmétiques](https://www.php.net/manual/fr/language.operators.arithmetic.php) et [opérateurs d'affectation](https://www.php.net/manual/fr/language.operators.assignment.php) sont les mêmes que pour Python (sauf le double diviser `//` qui n'existe pas).
- Les **chaînes de caractères** se concatènent **avec un ``.`` et non avec ``+``**.

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

**PHP**
```php
<?php
$a = 5;
$b = $a + 2;
$b += 1;
echo $b; //Affiche 8
$texte = "Bonjour";
$texteBis = " le monde!";
$texteFinal = $texte.$texteBis;
echo $texteFinal; //Affiche "Bonjour le monde!"
?>
```

### Structures conditionnelles

- Le contenu d'une condition `if` est obligatoirement entre parenthèses.
- Le bloc conditionnel n'est pas délimité par deux points `:` et l'identation de python, mais par un bloc d'accolades `{ ... }`.
- Le `elif` n'existe pas, il faut écrire `elseif`.
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

**PHP**
```php
<?php
//On suposse qu'on a défini une variable $age plus tôt.
if ($age > 18) {
    echo "Majeur";
}
else if (($age >= 12) && ($age < 18)) {
    echo "Ado";
}
else if (($age >= 6) && ($age < 12)) {
    echo "Enfant";
}
else if (($age < 0) || ($age > 120)) {
    echo "Age très improbable";
}
else {
    echo "Pitchounou";
}

if (!(($age % 2) == 0)) {
    echo "Age impair!";
}
?>
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

**PHP**
```php
<?php
//Affiche les nombres de 0 à 9.
$i = 0;
while($i < 10) {
	echo $i;
	$i += 1;
}

//Détermine au bout de combien d'années le capital dépassera 100000€ avec un taux de croissance de 20% par an.
$capital = 1000;
$annee = 0;
while ($capital < 100000) {
	$capital = $capital * 1.20;
	$annee += 1;
}
echo $annee;
?>
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

**PHP**
```php
<?php
//Affiche les nombres de 0 à 9.
for($i = 0; $i < 10; $i += 1) {
	echo $i;
}

//Affiche les nombres de 15 à 1.
for($i = 15; $i > 0; $i -= 1) {
	echo $i;
}
?>
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

**PHP**
```php
<?php
function puissance($x, $y) {
	$resultat = 1;
	for($i = 0; $i < $y; $i+=1) {
		$resultat *= $x;
	}
	return $resultat;
}
	
//Exemples de tests
echo puissance(2, 2); //Affiche 4
echo puissance(3, 2); //Affiche 9
?>
```

### Les tableaux / dictionnaires

Il n'y a pas de tableaux à proprement parler (comme vous les avez vu) en PHP, mais plutôt une structure hybride entre le tableau et le dictionnaire qui se nomme **tableau associatif**.

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
	
#Affiche tous les éléments du tableau
for element in tab:
	print(element)

#Dictionnaires
d = {} #Initialise un dictionnaire vide.
d["bonjour"] = 5 #Associe la clé "bonjour" à la valeur 5 dans le dictionnaire d
d["a"] = "c" #Associe la clé "a" à la valeur "c" dans le dictionnaire d

#Affiche tous les éléments du dictionnaire
for key in d.keys():
	print(d[key])
```

**PHP**
```php
<?php
//Tableaux
$tab = []; //Initialise un tableau vide.
array_push($tab, 5); //Ajoute 5 à la fin du tableau.
array_push($tab, 7); //Ajoute 7 à la fin du tableau.
$tab[1]; //Lecture du deuxième élément du tableau.
$tab[0] = 10; //Modification du premier élément du tableau.
$a = array_pop($tab); //Retire le dernier élément du tableau.
count($tab); //Taille du tableau (nombre d'éléments contenu).

//Affiche tous les éléments du tableau
for($i = 0; $i < count($tab); $i+=1) {
	echo $tab[$i];
}
	
//Affiche tous les éléments du tableau
foreach($tab as $element) {
	echo $element;
}

//Dictionnaires
$d = []; //Initialise un dictionnaire vide.
$d["bonjour"] = 5; //Associe la clé "bonjour" à la valeur 5 dans le dictionnaire d
$d["a"] = "c"; //Associe la clé "a" à la valeur "c" dans le dictionnaire d

//Affiche tous les éléments du dictionnaire
foreach($d as $element) {
	echo $element;
}

//Affiche tous les éléments du dictionnaire
foreach($d as $key => $element) {
	echo $key." -> ".$element;
}
?>
```

## Compléments - Avec HTML

- Il est possible, dans un même fichier PHP, d'avoir plusieurs blocs de code `<?php ... ?>` à plusieurs endroits.
- Comme nous l'avons vu plus tôt, il est possible de mélanger du code PHP avec du HTML.
- Pour écrire du code HTML (brut) après du code PHP, il faut fermer le bloc PHP (`?>`) écrire le code HTML et, si un bloc d'instruction ouvert (avec accolades) `{` doit être fermé (par exemple, dans le cas d'un `if`, `for`, `while`, etc...), il faut ré-ouvrir un bloc PHP après le code HTML puis fermer le bloc d'instruction `}`.
- On peut aussi directement coder le HTML dans le code PHP la forme d'une chaîne de caractères représentant le code, affichée avec `echo`. Cela à l'avantage de réduire le nombre de blocs PHP.
- Le code PHP **influe** sur la présence du code HTML dans le document : 
	- Un `if` permet d'afficher ou non un bout de code HTML.
	- Une boucle (`for`, `while`) permet de répéter du code HTML, etc...
	
**Exemple 1 - Afficher une page différente selon l'âge**
```php
<?php
//On suposse qu'on a défini une variable $age plus tôt.
if($age > 18) {
//Fermeture pour afficher du HTML
?> 
	<h3>Majeur!</h3>
	<p>Vous êtes majeur</p>
<?php
} //Fermeture du bloc if
else {
//Fermeture pour afficher du HTML
?>
	<h3>Mineur!</h3>
	<p>Vous êtes mineur</p>
<?php
} //Fermeture du bloc else
?>
```

**Exemple 1 - Équivalent**
```php
<?php
//On suposse qu'on a défini une variable $age plus tôt.
if($age > 18) {
	echo "<h3>Majeur!</h3>";
	echo "<p>Vous êtes majeur</p>";
}
else {
	echo "<h3>Mineur!</h3>";
	echo "<p>Vous êtes mineur</p>";
}
?>
```

**Exemple 2 -  Afficher une liste des nombres de 0 à 10**
```php
<ul>
<?php
	for($i=0;$i<=10;$i = $i + 1) {
?>
	<li><?php echo $i; ?></li>
<?php
	} //Fermeture du for
?>
</ul>
```

**Exemple 2 - Équivalent**
```php
<ul>
<?php
	for($i=0;$i<=10;$i = $i + 1) {
		echo "<li>".$i."</li>";
	}
?>
</ul>
```
Vous avez tout compris ? Parfait! Vous avez appris un nouveau langage! Plutôt rapide, non ?

## Premiers pas

Avant de modifier le site de Chuck Norris, vous allez réaliser qulques petits exercices de programmation en PHP pour vous assurer de bien maîtriser ce langage!

Si vous êtes perdus, référez vous à la section précédente pour adapter les exemples donnés aux exercices.

Commencez par créer un dossier `exercices` à l'intérieur du dossier `www` de Uwamp. C'est ici que vous stockerez les fichiers des exercices de cette section.

<div class="exercise">
1. Créez un fichier `tableau.php` à enregistrer dans le dossier `exercices`.
2. Créez un tableau contenant les valeurs 7, 3, 24 et 2
3. Ouvrez des balises `<ul> ... </ul>`.
4. Utilisez une boucle `for` pour afficher chaque valeur du tableau entre des balises `<li> ... </li>` à l'intérieur des balises `<ul> ... </ul>`.
5. Ouvrez [http://localhost/exercices/tableau.php](http://localhost/exercices/tableau.php) pour voir le résultat.
</div>

<div class="exercise">
1. Créez un fichier `nombre_chiffres.php` à enregistrer dans le dossier `exercices`.
2. Dans le fichier, traduisez le programme Python ci-dessous en un programme PHP.
3. Ouvrez [http://localhost/exercices/nombre_chiffres.php](http://localhost/exercices/nombre_chiffres.php) pour voir le résultat.

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
1. Créez un fichier `somme.php` à enregistrer dans le dossier `exercices`.
2. Créez une fonction `somme` renvoyant la somme des éléments d'un tableau.
3. Ecrivez un (ou plusieurs) appel(s) de test pour votre fonction.
4. Ouvrez [http://localhost/exercices/somme.php](http://localhost/exercices/somme.php) pour voir le résultat.
</div>

## Amélioration du site de Chuck Norris

Maintenant que vous maîtrisez PHP, il est temps d'ajouter de nouvelles fonctionnalités au site de Chuck Norris!

### Import et conversion du site

Pour commencez, nous allons importer le site de Chuck Norris sur notre serveur web, et convertir la page d'index et d'inscription avec l'extension `.php`.
<div class="exercise">
1. Copiez collez votre dossier contenant le site de Chuck Norris dans le dossier `www`. Vous pouveez éventuellement reprendre [la correction du TP3]({{site.baseurl}}/corrections/correction_tp3_web_formulaires.zip) pour avoir un site complet.
2. Renommez le dossier contenant le site en `chuck-norris`.
3. Ouvrez les fichiers `index.html` et `inscription.html` avec `Notepad++` puis, sélectionnez **Fichier** &#8594; **Enregistrer sous**. Sélectionnez **"Tout les types"** (all type) et rajoutez l'extension .php à la fin du fichier (pour obtenir `index.php` et `inscription.php`).
4. Vérifiez que les 2 fichiers `.php` apparaissent bien dans le dossier, et supprimez les anciens fichiers `.html`.
5. Dans les deux fichiers php, modifiez les éléments contenus dans le menu `<nav> ... </nav>` afin de remplacer les extensions en `.html` par `.php` au niveau des liens.
6. Sauvegardez les deux fichiers, puis vérifiez que le site fonctionne bien en vous rendant sur [http://localhost/chuck-norris/index.php](http://localhost/chuck-norris/index.php).
</div>

### Date du jour

La première fonctionnalité va être la suivante : Afficher la date du jour (jour de la semaine, numéro du jour, mois, année) sur la page d'accueil!

Tout d'abord, voici le code permettant d'obtenir la date du jour (en français), sous la forme d'une chaîne de caractères, en PHP :

```php
<?php
date_default_timezone_set('Europe/Paris');
setlocale(LC_TIME, "fr_FR");
$today = ucfirst(strftime("%A %d %b %Y", strtotime(date('Y-m-d')))); 
//$today Contient une chaîne de caractères avec la date du jour (en français).
?>
```
<div class="exercise">
1. Dans votre fichier `index.php`, ajoutez une balise `<p> ... </p>` après la balise `blockquote` (plus de détails ci-dessous).
2. Cette balise doit contenir le message **"Bienvenue sur le site de Chuck Norris ! - "** suivi de la date du jour courant **générée grâce à PHP**.
3. Vérifiez que la date du jour s'affiche bien en vous rendant sur [http://localhost/chuck-norris/index.php](http://localhost/chuck-norris/index.php).
</div>

**Placement**

```html
<body>
	<header>
		<nav> ... </nav>
	</header>
	<main>
		<blockquote> ... </blockquote>
		<p><strong>Bienvenue sur le site de Chuck Norris ! - ...</strong></p>
		...
	</main>
</body>
```

**Exemple de résultat**

Si la page est affichée le jeudi 4 mars 2021 :

![Resultat Date PHP]({{site.baseurl}}/assets/result-date-php.PNG)

### Nombre de visiteurs

Maintenant, on aimerait pouvoir stocker, mettre à jour et afficher le nombre de personnes ayant visité notre site.

Cela nécessite de manipuler des fichiers, éventuellement une base de données, mais ces aspects ne sont pas l'objectif de ce cours.

Pour simplifier tout cela, vous avez à votre disposition une **librairie** qui vous fournira les fonctions nécessaires pour effectuer ces actions.

Téléchargez [l'archive contenant les librairies]({{site.baseurl}}/assets/lib.zip) et extrayez la dans votre dossier `chuck-norris`. Un dossier `lib` devrait apparaître.

Importez la librairie `usercount` dans le fichier `index.php` en ajoutant ce bloc au début du fichier  :

```php
<?php
require './lib/usercount.php';
?>
```

Une fois cette librairie importée, vous avez accès à deux nouvelles fonctions que vous pouvez utiliser dans votre code :
- `incrementer_nombre_visiteurs()` : Incrémente le nombre de personnes ayant visités le site, dans le fichier stockant cette information.
- `nombre_visiteurs()` : Renvoie le nombre de personnes ayant visité le site, en allant lire dans le fichier stockant cette information.

<div class="exercise">
1. Dans votre fichier `index.php`, ajoutez une balise `<p> ... </p>` après la ligne contenant la date du jour (plus de détails ci-dessous).
2. Cette balise doit contenir le message **"Nombre de visiteurs :"** suivi du nombre de personnes ayant visité le site.
3. Quelque part dans votre code, vous devez également incrémenter le nombre de visiteurs (pour mettre à jour cette information).
4. Vérifiez que le nombre de visiteurs s'affiche bien en vous rendant sur [http://localhost/chuck-norris/index.php](http://localhost/chuck-norris/index.php) et en rechargeant la page plusieurs fois.
</div>

**Placement**

```html
<body>
	<header>
		<nav> ... </nav>
	</header>
	<main>
		<blockquote> ... </blockquote>
		<p><strong>Bienvenue sur le site de Chuck Norris ! - ...</strong></p>
		<p><strong>Nombre de visiteurs : ...</strong></p>
		...
	</main>
</body>
```

**Exemple de résultat**

![Resultat Visiteurs PHP]({{site.baseurl}}/assets/result-visiteurs-php.PNG)

### Inscription

Il est temps de faire fonctionner le formulaire d'inscription que vous aviez construit lors du [TP3](tp3.html)!

Jusqu'ici, lorsque vous validiez le formulaire, vous obteniez une erreur `404` signfifiant que la ressource de destination est introuvable.

En fait, votre navigateur tente d'envoyer une **requête HTTP** vers un programme PHP du serveur, afin de récupérer et traiter les données transmises par le formulaire. C'est ce fichier que vous allez créer dans cette section.

Lorsque le formulaire est validé, les données sont récupérées par le serveur et le programme du fichier PHP spécifié dans l'attribut `action` de la balise `form` est éxécuté.

Toutes les données du formulaire sont **automatiquement** placées dans un **tableau associatif** (dictionnaire) dont le nom est différent selon la méthode utilisée avec le formulaire `get` ou `post`) :
- `$_GET` pour la méthode `GET` (transmission des données via l'URL).
- `$_POST` pour la méthode `POST` (transmission des données via le corps de la requête).

Ce dictionnaire est directement accessible dans votre code. Les **clés** du dictionnaire correpondent aux valeurs des attributs `name` que vous avez donné aux différents champs de votre formulaire (sous forme de chaînes de caractères). 

**Exemple : Formulaire**

```html
<form action="exemple.php" method="post">
	<div>
		<label for="atr1">Nom : </label>
		<input id="atr1" type="text" name="nom">
	</div>
	<div>
		<label for="atr2">Age : </label>
		<input id="atr2" type="number" name="age">
	</div>
	<div>
		<label for="atr3">Email : </label>
		<input id="atr3" type="email" name="adr_email">
	</div>
</form>
```

**Exemple : Fichier exemple.php**
```php
<?php
//Fichier éxécuté lors de la validation du formulaire.
$nom = $_POST["nom"]; //Contient le nom saisi dans le formulaire (chaîne de caractères)
$age = $_POST["age"]; //Contient l'âge saisi dans le formulaire (nombre)
$adresse_email = $_POST["adr_email"]; //Contient l'adresse email saisi dans le formulaire (chaîne de caractères)
?>
```

Comme pour la fonctionnalité du nombre de visiteurs, nous allons utiliser **une librairie** particulière pour pouvoir gérer les inscriptions. Celle ci permettra de gérer une petite base de données sous la forme d'un fichier **CSV** stockant l'information.

Le bloc de code suivant permet d'importer cette librairie :

```php
<?php
require './lib/csv_lib.php';
?>
```
Une fois cette librairie importée, vous avez accès à deux nouvelles fonctions que vous pouvez utiliser dans votre code :
- `ouvrir_base()` : Charge la base et renvoie **un tableau** contenant un ensemble de **dictionnaires** qui représentent les données des membres.
- `sauvegarder_base($base)` : Sauvegarde et enregistre (dans un fichier CSV) la base de donnée représenté par le **tableau** passé en paramètre.

**Exemple**
```php
<?php
$base = ouvrir_base();
$base[0]; //Informations du premier membre.
$base[0]["nom"]; //Nom de famille du premier membre....
$new_membre = [] //Création d'un nouveau membre.
$new_membre["nom"] = "Smith";
$new_membre["prenom"] = "John";
array_push($base, $new_membre); //On ajoute le nouveau membre dans la base.
sauvegarder_base($base); //On sauvegarde la base.
?>
```

<div class="exercise">
1. Dans votre fichier `inscription.php`, rendez **obligatoires** (`required`) les champs du **nom**, **prénom**, **sexe**, **date de naissance**, **adresse email**, **mot de passe** et **niveau de karaté**.
2. Toujours dans le même fichier, modifiez la valeur du champ `action` par `"validationInscription.php"` et assurez vous que la valeur de l'attribut `method` est `"post"`.
3. Téléchargez le fichier [validationInscription.php]({{site.baseurl}}/assets/validationInscription.php) et placez le dans votre dossier `chuck-norris`.
4. Ce fichier contient la page HTML qui sera affichée après validation de l'inscription. C'est ce fichier qui sera éxécuté lors de la validation du formulaire. Le code HTML n'a pas besoin de modification, mais vous alelz devoir ajouter du code PHP.
5. Ajoutez le code PHP nécessaire dans `validationInscription.php` pour récupérer les données du membre (pas tout, seulement le **nom**, **prénom**, **sexe**, **date de naissance**, **adresse email**, **mot de passe** et **niveau de karaté**) et les enregistrer dans la base (à l'aide des fonctions de la librairie fournie).
6. Retourner sur [la page d'inscription](http://localhost/chuck-norris/inscription.php), complétez le formulaire et vérifiez que tout se passe bien lors de la validation (pas d'erreurs).
7. A partir du dossier `www` du **Uwamp**, rendez vous dans le dossier `database` et ouvrez le fichier `users.csv`. Le membre que vous venez d'enregistrer devrait être présent.

</div>

### Liste des membres

Maintenant que nous pouvons enregistrer des membres via le formulaire, on aimerait bien consulter la liste des membres du fan-club de Chuck Norris, avec leurs informations.

Dans cette section, nous allons ajouter un nouveau fichier PHP qui permettra, à partir des informations de la base, de construire une page HTML contenant un tableau (graphique) avec les informations des membres.

<div class="exercise">
1. Téléchargez le fichier [listeMembres.php]({{site.baseurl}}/assets/listeMembres.php) et placez le dans votre dossier `chuck-norris`.
2. Regardez comment sont construits [les tableaux (graphiques) en HTML](https://developer.mozilla.org/fr/docs/Web/HTML/Element/table).
3. Ajoutez du code PHP (toujours en utilisant les fonctions de la librairie `csv_lib`) entre les balises `<tbody> ... </tbody>` pour construire, pour chaque membre contenu dans la base, une ligne de données (avec les balises `<tr> ... </tr> et <td> ... </td>`) pour remplir le tableau (graphique) de la page.
4. Enregsitrez plusieurs membres via [la page d'inscription](http://localhost/chuck-norris/inscription.php).
5. Rendez vous sur la page [http://localhost/chuck-norris/listeMembres.php](http://localhost/chuck-norris/listeMembres.php) pour vérifier que le tableau s'affiche bien.
6. Rajoutez dans le menu de navigation (`nav`) des fichiers `index.php`, `inscription.html`, `validationInscription.php` et `listeMembres.php` un lien vers la page `listeMembres.php` (nommé "**Liste des membres**").
7. Faites en sorte que les dates de naissance des membres (sur le tableau graphique) s'affichent suivant le même format que la date du jour de la page `index.php`.
</div>