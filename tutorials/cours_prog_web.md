---
title: Notions complémentaires &ndash; Programmation web côté serveur
subtitle:
layout: tutorial
---

## Le fonctionnement du World Wide Web

<section>

### Client / Serveur

* Le *client* : C'est le visiteur d'un site Web. Il demande la page Web au
  serveur. En pratique, vous êtes des clients quand vous surfez sur le Web.  
  Plus précisément c'est votre *navigateur Web* (Firefox, Chrome, Safari, IE,
  Edge, ...) qui est le client car c'est lui qui demande la page Web.

* Le *serveur* : Ce sont les ordinateurs qui délivrent les sites Web aux
  internautes, c'est-à-dire aux clients.

<br>

<p style="text-align:center">
![Mécanisme client/serveur]({{site.baseurl}}/assets/ClientServeur.png)
<br>
Le client fait une *requête* au serveur, qui répond en donnant la page Web
</p>

</section>
<section>

### Protocole de communication : HTTP

**HTTP** (*HyperText Transfer Protocol*) est un protocole de communication
entre un client et un serveur développé pour le Web. L'une de ses fonctions
principales est ainsi de récupérer des pages Web.

**À quoi ressemble une requête HTTP ?**

La requête HTTP la plus courante est la requête GET. Par exemple pour demander
la page Web
[https://mgasquet.github.io/ProgWeb-NSI/index.html](https://mgasquet.github.io/ProgWeb-NSI/index.html)
:

```http
GET /ProgWeb-NSI/index.html HTTP/1.1
Host: mgasquet.github.io

```

 La réponse est alors:

```http
HTTP/1.1 200 OK
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Mon, 08 Feb 2021 01:55:10 GMT

<html><head><meta charset="utf-8" />...</head>
<body>...</body></html>(contenu de index.html)
```

</section>
<section>

### Le navigateur comme client HTTP


Quand on ouvre une URL en `http://`, le navigateur va agir comme un client
HTTP. Il va donc envoyer une *requête HTTP*.

Le client HTTP reçoit la réponse du serveur HTTP qui contient la page Web
demandée.

Le navigateur interprète alors la page Web et l'affiche.


<p style="text-align:center">
![Requête HTTP]({{site.baseurl}}/assets/RequeteHTTP.png)
</p>

<!-- Je vous ai montré ce qui se passe quand je demande une page Web -->
<!-- en tapant une URL dans la barre d'adresse -->
**Que se passe-t-il quand on clique sur un lien hypertexte `<a>` ?**
<div class="incremental">
<div>
Cliquer sur un lien fait pareil que demander une page Web par la barre
d'adresse, cela envoie une requête HTTP.

</div>
</div>

</section>
<section>

### Qu'est-ce qu'un serveur HTTP ? 

Un *serveur* **HTTP** est un logiciel qui répond à des requêtes HTTP.  
Il est souvent associé au port 80 de la machine hôte.

**Quelques exemples de serveurs HTTP ?**

* Apache HTTP Server : classique, celui que l'on utilisera
* Apache TomCat : évolution pour Java (J2EE)
* IIS (Internet Information Services) : Microsoft
* Node.js : codé en JavaScript.

**En pratique** lors du [TP4](tp_php.html), nous utiliserons un serveur **HTTP** Apache grâce au logiciel **Uwamp**, que vous installerez sur vos machines.

**Résumé :**

* Un serveur Web = un serveur **HTTP**

</section>

## Pages Web statiques ou dynamiques
<section>

### Différence entre page statique/dynamique

* Les sites *statiques* :  
  Sites réalisés uniquement à l'aide de HTML/CSS.  
  Ils fonctionnent très bien mais leur contenu ne change pas en fonction du client.  
  Les sites statiques sont donc bien adaptés pour réaliser des sites «vitrine»
  C'est ce que vous avez fait jusqu'ici, avec les TPs précédents.

<p style="text-align:center">
![Requête HTTP]({{site.baseurl}}/assets/RequeteHTTP.png)
</p>

* Les sites *dynamiques* :  
  Leur contenu change en fonction du client.
  Ils utilisent d'autres langages tels que PHP pour générer du HTML et CSS.  
  La plupart des sites Web que vous visitez sont dynamiques.

**Fonctionnalités typiques de sites dynamiques :**  
Un espace membres, un forum, un compteur de visiteurs, des actualités, une
newsletter

</section>
<section>

### Mécanisme de génération des pages dynamiques

<!-- Voir l'un puis l'autre -->

**Rappel :**

* Site statique :  
  1. le client demande au serveur à voir une page Web (requête HTTP) ;
  2. le serveur lui répond en lui envoyant la page réclamée (réponse HTTP).
  
  <!-- déjà vu -->
  
<p style="text-align:center">
![Requête HTTP]({{site.baseurl}}/assets/RequeteHTTP.png)
</p>

</section>
<section>

<!-- PHP : recette pour créer page HTML -->

* Site dynamique :  
  1. le client demande au serveur à voir une page Web (requête HTTP) ;
  2. le serveur crée la page spécialement pour le client (en suivant les instructions du PHP) ;
  3. le serveur répond au client en lui envoyant la page qu'il vient de générer (réponse HTTP).

<p style="text-align:center">
![Génération PHP]({{site.baseurl}}/assets/RolePHP.png)
</p>

</section>
<!-- <section> -->

<!-- ## Où intervient le PHP ? -->

<!-- Un module PHP (mod_php5) est intégré au serveur HTTP Apache. -->

<!-- Quand le serveur Web reçoit une requête d'un fichier .php, il génère -->
<!-- dynamiquement la page Web en exécutant le code PHP de la page. -->

<!-- La page généré est ensuite renvoyée dans la réponse HTTP. -->

<!-- **C'est ce que l'on appelle une page dynamique.** -->

<!--
 La création du document advient au moment de la requête
 Le serveur peut
 o Compiler le document à la volée (comme dans la génération statique),
 o Interagir avec d’autres serveurs (authentification, API, …),
 o Interroger des bases de données.
-->

<!-- <br> -->

<!--  <p style="text-align:center"> -->
<!--  ![Rôle du PHP]({{site.baseurl}}/assets/RolePHP.png) -->
<!--  </p> -->


<!-- </section> -->
<section>

### Le langage de création de page Web : PHP

<div style="display:flex;align-items:center;">
<div style="flex-grow:1">
Le rôle de PHP est justement de générer du code HTML.

C'est un langage que seuls les **serveurs** comprennent et qui permet de rendre
votre site dynamique.
</div>
<div style="flex-grow:1">
<p style="text-align:center">
<img src="{{site.baseurl}}/assets/ElePHPant.svg" style="width:200px" alt="Mascotte PHP">  
L'éléPHPant, la mascotte de PHP
</p>
</div>
</div>

<br>

<div class="incremental">
<div>
**Attention :** Les clients (navigateur) sont incapables de comprendre le code PHP : ils ne
connaissent que le HTML et le CSS.

<p style="text-align:center;">
<img src="{{site.baseurl}}/assets/OpenPHPInBrowser.jpg" alt="Quand on ouvre un .php directement dans le navigateur">
</p>
</div>
</div>
</section>