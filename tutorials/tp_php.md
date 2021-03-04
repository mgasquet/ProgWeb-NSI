---
title: TP4 &ndash; Programmation web &ndash; Côté serveur &ndash; PHP
subtitle:
layout: tutorial
---

## Introduction

Dans le TP3, nous avons vu comment créer des forumalire sur un site avec HTML.
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
Avant de vous lancer, assurez vous d'avoir bien compris les concepts liés à [la programmation web côté serveur](cours_prog_web.html).

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

<div class="exercise" id="exlabel">
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
- Les [opérateurs arithmétiques](https://www.php.net/manual/fr/language.operators.arithmetic.php) et [opérateurs d'affectation](https://www.php.net/manual/fr/language.operators.assignment.php) sont les mêmes que pour Python.
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
- Le for est divisé en trois parties :
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

### Les tableaux / dictionnaires

## Premiers pas

## Amélioration du site de Chuck Norris

