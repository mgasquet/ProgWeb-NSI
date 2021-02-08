---
title: TP3 &ndash; Les formulaires
subtitle:
layout: tutorial
---

<!--
Rajouter mise-en-page "Solved by flexbox" des formulaires
Il faudrait pour cela avoir vu flex-grow avant
-->


<!--
Input type : date, email, file, hidden, range, color, number, tel, url, search
multiple
input list avec datalist (avec autocomplétion)
input/textarea Spellcheck
https://developer.mozilla.org/fr/docs/Web/HTML/Element/Input
https://openclassrooms.com/courses/apprenez-a-creer-votre-site-web-avec-html5-et-css3/les-formulaires-8

-->

<!-- Corriger absence d'explications sur <option value=""> et selected -->

Pour ce TP, reprenez votre dossier `TP_Web_Site` du [TP précédent](tp2.html) (éventuellement mis à jour avec [la correction]({{site.baseurl}}/corrections/correction_tp2_web_css.zip))

## Introduction

Nous allons ajouter un formulaire d'inscription à notre site de fans de
**Chuck Norris**, en utilisant la balise `<form>`.  Cette balise
`<form>` nous permettra d'avoir des réponses à des questions des plus ouvertes
("Que voulez-vous dire à Chuck ?") aux plus fermées ("Parmi ces trois choix
quel est votre sport favori ?", "Quel est votre sexe ?" ... ).  Il y a
beaucoup de types de questions, correspondant chacune à un type de balises
`<input>` ou `<textarea>` que nous verrons par la suite.

## La balise  `<form>` et les balises `<input>`

Le coeur du formulaire est constitué par deux types de balises : `<form>` et
`<input>`.


La balise `<form>` délimite le contenu du formulaire et renseigne plusieurs
attributs nécessaires au fonctionnement du formulaire :

* `method`: nom de la méthode HTTP utilisée pour envoyer les données. Peut
  prendre pour valeur `post` ou `get` :

   * `get` envoie les données comme composantes de l'URL du serveur et requiert
   par conséquent que :

      1. les données soient encodées pour être compatibles avec les
   spécifications URL,
      1. l'ensemble des données du formulaire plus l'URL du serveur forment une
   chaîne de caractères de moins de 2000 caractères (limite imposée par certains
   navigateurs).

   * `post` envoie les données dans le corps de la requête HTTP et ne
   présente pas la limitation de taille, elle est donc à privilégier.

* `action` : URL du serveur où les données du formulaire doivent être
  envoyées. 

La balise `<input>` permet de définir différents champs dans lesquels
l'utilisateur peut entrer des données. Ces champs offrent plus ou moins de
liberté d'expression selon le type utilisé. La balise `<input>` a pour attributs:

* [`type`](http://www.w3schools.com/tags/att_input_type.asp) : définit l'apparence
  visuelle du champ et la nature des données qui peuvent y être renseignées.
* [`value`](http://www.w3schools.com/tags/att_input_value.asp) : la valeur
envoyée au serveur. Si elle est déjà renseignée lors de la création du formulaire,
 elle fait office de valeur par défaut.
* [`name`](http://www.w3schools.com/tags/att_input_name.asp) : le nom que prendra la donnée envoyée au serveur.  Si l'input a pour `name` "firstname" et pour valeur "Éric", dans le cas d'une method `get` l'URL lors la soumission du formulaire contiendra 'firstname=Éric' et si la méthode est `post` ces valeurs seront transmises via les champs `Form Data` de la requête HTTP.


Afin de pouvoir être envoyé, votre formulaire doit obligatoirement contenir une
balise `<input>` avec l'attribut `type` fixé à `“submit”`. Cette balise définit
le bouton qui déclenchera l'envoi des données au serveur lorsque l'on cliquera
dessus.

<!-- La value de ce bouton permet de changer ce qui est écrit dessus -->

<div class="exercise" id="start">

Nous allons voir comment est envoyée la valeur d'un `<input>` lorsque l'on soumet un formulaire.

 1. Créez une nouvelle page `inscription.html` au site de Chuck Norris (donc, dans le dossier `TP_Web_Site`). Cette page
 va contenir le formulaire d'inscription au fan-club de Chuck que nous allons
 construire dans ce TP.
 
 1. Pour avoir un **template** de base pour la page, reprenez le code de la page `ìndex.html` et copiez le dans votre nouvelle page `inscription.html`. 
	Supprimez tout le contenu (intérieur) du body, et changez le titre de la page par "Inscription au fan-club de Chuck Norris".

1. Ajoutez à la page `inscription.html` le formulaire suivant (dans le body) :

   ```html
   <form action="sendToTpServer.php" method="post">
     <input name="uname" type="text" >
     <input type="submit" value="Envoyer">
   </form>
   ```

  1. **Avec Firefox** : Affichez la page et ouvrez la console (F12) pour aller sur l'onglet
  'Réseau', entrez la valeur `dupont` au champ texte, puis cliquez sur le bouton
  "Envoyer" du formulaire (il est normal d'avoir une erreur).  Vous devez voir une requête contenant
  `sendToTpServer` dans la console. Cherchez
  la valeur `dupont` dans les détails de la transaction, à droite, dans l'onglet 'Requête'.
  
 1. Donnez à l'attribut `method` du formulaire la valeur `get`. Cliquez sur le
    bouton "Envoyer" du formulaire, l'URL doit maintenant finir par
    "sendToTpServer.php?uname=dupont".


</div>

**Note** : il est normal que l'URL `sendToTpServer.php`
n'existe pas (le fameux code de retour HTTP **404** apparaît dans
la console), puisque nous n'avons pas encore fait le TP sur la partie serveur. Nous verrons, dans un futur TP, comment le serveur peut
récupérer les données envoyées par notre formulaire et les traiter.


## La balise `<label>`

Il serait bien de préciser à l'utilisateur à quoi notre champ `<input>` fait référence. La balise [`<label>`](http://www.w3schools.com/tags/tag_label.asp) permet d'associer la question sous-tendue ("Nom?") à l'input. Cette balise comporte un attribut `for` qui doit prendre pour valeur la valeur de l'attribut `id` du champ auquel est associé le `label`  (il faut donc penser à donner un `id` à notre `<input>`).


<div class="exercise" id="exlabel">

1. Remplacez le code de votre champ `<input>` par le code suivant :

   ```html
   <label for="surname">Nom</label>
   <input id="surname" name="uname" type="text">
   ```

 1. Rajoutez au formulaire une entrée qui correspondra au prénom (calqué sur l'exemple précédent).
 1. Validez ce dernier et vérifiez que vos deux champs sont bien présents dans
    l'URL du navigateur (l'URL doit finir par
    `sendToTpServer.php?uname=dupont&firstname=super` et la `method` du
    formulaire doit toujours être `get`).
 1. Pour ne pas "coller" les champs du formulaire à la suite, il faut englober le couple de balises `<label>` et `<input>` entre des balises `<div>...</div>`. Appliquez cette modificaton.
 1. Si vous souhaitez que le champ (`<input>`) se place en dessous du label et non à côté, vous devez englober le champ entre des balises `<p>...</p>` (Modifiez selon votre goût).
</div>

## Les principaux types de balises `<input>` 


Il existe un assez grand nombre de [types d'input](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input) (vous pouvez cliquez dessus pour voir un exemple) :

 * Le type [`radio`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/radio) permet de ne sélectionner qu'une seule des options
possibles.
 * Le type [`checkbox`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/checkbox) (case à cocher) permettent de sélectionner autant d'options que l'utilisateur le souhaite.
 * Le type [`password`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/password) masque automatiquement les caractères entrés.
 * Les types [`email`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/email), [`URL`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/url), 
 [`tel`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/tel), [`date`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/date), [`time`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/time) et [`number`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/number), etc. permettent
 d'adapter le clavier virtuel quand la page est affichée sur un smartphone.
 Suivant le navigateur, une présentation différente peut être associée. Des
 validateurs sont associés à ces champs, par exemple, une valeur de champ email doit contenir un "@".

<div class="exercise" id="exinput">
 
 A l'aide de [cette page](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input) (en regardant les exemples), ajoutez dans le formulaire les `<input>` libellés :

 1. "Sexe" avec les deux valeurs que vous connaissez, il s'agira d'inputs [`radio`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/radio).
 1. "Date de naissance" avec le type d'input [`date`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/date).
 1. "Mot de passe" avec le type d'input [`password`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/password).
 1. "Email" avec le type d'input de type ... [`email`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/email).
 1. "Niveau en karaté" avec le type d'input [`number`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/number) allant de 0 à 5 (cherchez comment appliquer cette contrainte).
 1. "Niveau d'engagement" (encore des inputs [`radio`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/radio)) avec un choix parmi trois valeurs libellées "Basique (5 €) ", "Gold (15 €)" et "Tatane in your face (50 €)".
 1. "J'ai bien lu les clauses que je n'ai pas lues" associé à une case à cocher ([`checkbox`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input/checkbox)). 
 1. Vérifier par envoi du formulaire que tous les champs sont bien renseignés (via la console, avec `F12`). On rappelle que c'est l'attribut `name` de l'input qui est utilisé.
 1. Faite en sorte qu'il y ait un saut de ligne entre chaque `<input>` (comme
    dans la section précédente).
 1. Au besoin, vous pouvez ajouter plus d'espace entre deux champs en ajoutant une balise `<br>` entre les deux `<div>` qui contiennent les champs.
 
</div>


**Notes :** 

 * Certains de ces inputs sont issus de la norme HTML5. De
fait leurs adoptions au sein des navigateurs n'est pas uniforme. Les
développeurs web peuvent être amenés à demander la nature du parc informatique
cible du site web qu'ils doivent implémenter (en clair ils demandent : "quelle
est la version d'Internet Explorer encore en cours sur votre parc ?"). Le site
[caniuse.com](http://caniuse.com/) permet ensuite de savoir si nous pouvons utiliser
tel ou tel aspect pour la réalisation d'un site. Les types `date` et `time` par
exemple sont [plus ou moins bien supportés](http://caniuse.com/#search=date) par
les navigateurs. Le type `number` l'est
[un peu plus](http://caniuse.com/#search=number). Vous pouvez constater quelques différences d'apparence dans votre formulaire suivant si vous êtes sur Chrome, Firefox, Internet Explorer ou Edge.

 * A propos du mot de passe, remarquez que ce dernier
apparaît en clair dans l'URL si vous êtes en `get` lors de l'envoi via à
`sendToTpServer.php`.  Définitivement donc, un envoi avec `post` doit
être privilégié, même si cela n'augmente pas vraiment la sécurité puisque le mot
de passe transite toujours en clair sur le réseau (utilisez l'onglet Réseau
comme dans l'exercice 1 pour le voir).
 

## La balise `<select>`

Voyons maintenant un autre élément important d'un formulaire, correspondant à la balise [`<select>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/select).
Il permet de choisir parmi un ensemble de valeurs présentées par un menu déroulant.
Tout comme `<input>`, cet élément peut aussi être libellé via un `<label>`. La liste déroulante permet de base de ne sélectionner
qu'une option. Plusieurs options peuvent être sélectionnées si l'attribut `multiple` est ajouté à la balise `<select>`. Des groupes de choix peuvent être proposés avec la balise `<optgroup>`. 

<div class="exercise" id="exlabel">


 A l'aide de [developer.mozilla.org](https://developer.mozilla.org/fr/docs/Web/HTML/Element/select) :

 1. Ajoutez un `<select>` libellé "Pays d'origine" qui prend comme valeur de pays `U.S.A` , `France`, `Chine` et `Viêt Nam`, les `values` associées ne doivent pas dépendre de la langue du formulaire (la `value` associée à `France` doit être `fr` par exemple). L'utilisateur ne peut pas sélectionner plusieurs valeurs, le pays sélectionné par défaut est la France (indépendamment de l'ordre des balises `<option>` dans le HTML).

 1. Ajoutez à la suite de ce champ un autre sélecteur libellé "Arts-martiaux préférés". Les valeurs sont "Kung fu" , "Karaté" et "Full-contact". L'utilisateur peut sélectionner plusieurs valeurs.
</div>

## La balise `<textarea>`


La balise [`<textarea>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Textarea)
permet de proposer une grande zone de texte pour que l'utilisateur puisse
s'exprimer.

<div class="exercise" id="exlabel">

 1.  A l'aide de [developer.mozilla.org](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Textarea), ajoutez un champ à votre formulaire libellé "Message pour Chuck" associé à un `<textarea>` sur lequel l'utilisateur peut s'épancher.
</div>

## La balise `<fieldset>`

La balise [`<fieldset>`](https://developer.mozilla.org/fr/docs/Web/Guide/HTML/Formulaires/Comment_structurer_un_formulaire_HTML#les_%C3%A9l%C3%A9ments_%3Cfieldset%3E_et_%3Clegend%3E) permet de regrouper visuellement différents champs `<input>`.


<div class="exercise" id="exfield">
A l'aide de [cette page](https://developer.mozilla.org/fr/docs/Web/Guide/HTML/Formulaires/Comment_structurer_un_formulaire_HTML#les_%C3%A9l%C3%A9ments_%3Cfieldset%3E_et_%3Clegend%3E),
regroupez les champs sur ces trois grands axes suivant :

* "Informations personnelles" (contenant "Nom", "Prénom", "Email", etc.),
* "Les sports de combat" (contenenant "Sport de combat préféré"" et "Niveau en karaté"),
* "Inscription" (contenant "Message personnel à Chuck", "Mot de passe", la coche "J'ai bien lu..", "Niveau d'engagement', etc.).


</div>


## Champs obligatoires, ergonomie et convivialité

### Champs obligatoires

Il est possible de rendre un champ **obligatoire**. 
Cela signfiie que le formulaire ne sera pas envoyé si l'utilisateur ne complète pas le champ.
Pour rendre un champ obligatoire, il suffit de rajouter l'attribut `required` dans la balise du champ (`<input>`, `<select>`, `<textarea>`, etc...) **sans aucune valeur associée** (pas de =).
Vous pouvez regarder [le code de cet exemple](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Input).

<div class="exercise" id="extab">
  1. Rendre la coche "J'ai bien lu les clauses que je n'ai pas lues" obligatoire. Vérifiez si l'envoi du formulaire est bien impossible alors.
  1. Rendre aussi les champs "Nom" "Mot de passe" et "Email" obligatoires.
  1. Par convention d'usage, le nom des champs obligatoires est suivi d'une "*". Ajoutez la aux labels des `<input>` obligatoires.
</div>


### Navigation

Pour les utilisateurs avancés, la navigation à l'aide de la touche “tabulation”
permet de parcourir très vite le formulaire. L'attribut “autofocus” permet de
spécifier au navigateur quel élément du formulaire doit avoir le focus quand la page est chargée. L'attribut [`tabindex`](https://developer.mozilla.org/fr/docs/Web/HTML/Attributs_universels/tabindex) permet de spécifier l'ordre
dans lequel les éléments sont parcourus en appuyant sur “tabulation”.

<div class="exercise" id="extab">
 * Vérifiez que vous pouvez accéder à tous les champs avec la touche tabulation. Modifier l'ordre de tabulation avec l'attribut `tabindex`.
</div>

### Convivialité

Quelques attributs permettent d'améliorer la convivialité des champs de votre formulaire :

* `placeholder` : permet d'afficher une ligne de texte dans le champ qui disparaît
  dès lors que l'utilisateur tape une information. Cela permet de donner à
  l'utilisateur des renseignements sur le contenu attendu. À utiliser
  impérativement avec les champs pour lesquels vous avez spécifié un “pattern”,
  sous peine de cause une extrême frustration à l'utilisateur. Vous devez alors
  utiliser l'attribut `placeholder` pour spécifier le format attendu, les
  caractères interdits/autorisés, etc.

   ex :  placeholder=“Entrez votre nom ici."

* `checked` / `selected` : pour les types “radio” et “checkbox”, et pour `<option>`
respectivement. Cet attribut permet de spécifier que l'option en question est
sélectionnée/cochée par défaut. Utile quand vous savez que l'une des options
sera utilisée beaucoup plus fréquemment que les autres. Vous épargnez alors du
temps à l'utilisateur.

<div class="exercise" >

 1. Ajoutez un placeholder de valeur “yourmail@domain.com” au champ Email.
 1. Ajoutez un attribut `placeholder` dans le `<textarea>` avec le texte suivant "Un inscrit sera tiré au sort, et verra son message transmis à Chuck Norris."
 <!-- 1. Faite en sorte que le pays sélectionné par défaut dans "Pays d'origine" soit la France (et cela indépendamment de l'ordre des balises `<option>` dans le HTML). -->
</div>


**Note :** Il existe depuis peu un pseudo attribut css `::placeholder`, mais celui-ci est [moins](http://caniuse.com/#search=placeholder%20css) bien supporté que 
l'[attribut](http://caniuse.com/#search=placeholder%20attribute).

<!---
Intéressant, mais pas adapté à NSI
### Contrôle du contenu

La sécurité de votre serveur et de vos utilisateurs impose que vous contrôliez
toujours au niveau du serveur les données entrées (cf. cours l'an
prochain). Toutefois, le contrôle par le serveur demande que les données soient
envoyées, que le serveur teste, puis réponde ; l'opération peut être longue.

Afin d'éviter une attente inutile aux utilisateurs de votre formulaire, vous
pouvez demander au navigateur d'effectuer directement certains tests de validation, afin de prévenir 
les erreurs courantes (ex : mauvais numéro de téléphone, mauvaise date...). 
Attention : cela ne vous dispense quand même pas de procéder aux vérifications côté serveur !  Deux attributs permettent
de vérifier le contenu du formulaire :

* `required` : spécifie que le champ doit être obligatoirement rempli. Attribut à
  ajouter à tous les champs dont la légende comporte une *
* `pattern` : attribut spécifique aux champs “libres”, il permet de spécifier une
  [expression régulière](http://www.rexegg.com/). Cette chaîne de caractère au
  [format particulier](http://www.rexegg.com/regex-quickstart.html#ref) indique
  au navigateur tous les formats d'entrée autorisés pour le champ et le
  navigateur refusera d'envoyer le formulaire si un champ n'est pas correctement
  rempli. Par exemple, un “pattern” égal à `0[1-9](\.\d{2}){4}` permettra de
  s'assurer qu'un numéro de téléphone respecte bien les règles de numérotation
  françaises, tandis que le pattern `[a-z0-9._-]+@[a-z0-9.-]+\.[a-z]{2,4}`
  bloquera les erreurs d'adresse email les plus grossières. Vous trouverez de
  nombreux exemples de patterns utilisables sur le site
  [HTML5pattern](http://html5pattern.com/).  
  **Note :** les patterns HTML sont automatiquement évalués sur la totalité de
  l'entrée. Il est donc inutile de les encadrer entre ^ et $ comme une
  expression régulière classique.

<div class="exercise" id="regulex" >
 1. Rendre la coche "J'ai bien lu les clauses que je n'ai pas lues" obligatoire. Vérifiez si l'envoi du formulaire est bien impossible alors.
 1. Rendre aussi les champs "Nom" "Mot de passe" et "Email" obligatoires.
 1. Par convention d'usage, le nom des champs obligatoires est suivi d'une "*". Ajoutez la aux labels des `<input>` obligatoires.
 1. Ajoutez au champ password un pattern pour que ne soient acceptés que des caractères de l'alphabet latin ou numériques.
 1. Faites en sorte que le mot de passe acceptable soit d'une longueur de 8 caractères minimum.
 <!-- 1. (optionnel) Ajoutez un pattern au champ mot de passe afin que celui-ci contienne obligatoirement 8 ou plus caractères avec au moins un chiffre, une lettre majuscule et une lettre minuscule.

</div>

<!--
**Note :** Pour être toujours protégé contre les bugs lorsque vous cogitez sur une expression régulière, ne sortez jamais sans votre [Regulex](https://jex.im/regulex). Regulex, le visualisateur de machine d'état qu'il vous faut pour vos expressions régulières.
-->

## Menu de navigation

Nous allons maintenant ajouter un **menu de navigation** sur la page `inscription.html` et `index.html` pour nous permettre de naviguer entre ces deux pages.

<div class="exercise">

**Rappel** : [Structuration d'une page HTML](tp1.html#structure)

Pour **les deux pages**, répétez les instructions suivantes :

1. Ajoutez de nouvelles balises `<header></header>` à l'intérieur des balises `<body></body>`, au tout début.
2. Placez tout ce qui reste dans la balise `<body></body>` (après le header), dans des balises `<main></main>`.
3. Ajoutez des balises `<nav></nav>` à l'intérieur des balises `<header></header>`.
4. A lintérieur du bloc `<nav>...</nav>` ajoutez deux liens hypertextes à l'aide des balises `<a>...</a>` :
	* Un lien `Home` dont l'attribut `href` pointe vers `index.html`.
	* Un lien `Inscription` dont l'attribut `href` pointe vers `inscription.html`.
	
Vous devriez obtenir un menu de navigation permettant de passer d'une page à l'autre!
</div>
