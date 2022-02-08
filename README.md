[Doc en cours de rédaction]

![Langage Python](https://img.shields.io/badge/language-python-blue.svg)
![Langage JavaScript](https://img.shields.io/badge/language-javascript-blue.svg)
![Langage HTML](https://img.shields.io/badge/language-HTML-blue.svg)
![Langage CSS](https://img.shields.io/badge/language-CSS-blue.svg)
[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)

# Sommaire
  
* [I) CAHIER DES CHARGES DU PROJET](#i)-cahier-des-charges-du-projet)
* [II) LE MATERIEL NECESSAIRE (optionnel)](#ii)-le-materiel-necessaire-(optionnel))
* [III) Rentrons un peu dans la technique](#iii)-rentrons-un-peu-dans-la-technique) 
	- [III)1 Le CHOIX DU FRAMEWORK BACKEND PYTHON](#III)1-le-choix-du-framework-backend-python)
	- [Get Sub-items of the Item](#get-sub-items-of-the-item)
	- [Magic Where Methods](#magic-where-methods)
* [Referring to Menu Objects](#referring-to-menu-instances)
* [HTML Attributes](#html-attributes)
* [Manipulating Links](#manipulating-links)
	- [Link's Href Property](#links-href-property)
* [Active Item](#active-item)
	- [URL Wildcards](#url-wildcards)
    - [Check for Active Children](#check-for-active-children) 
* [Inserting a Separator](#inserting-a-separator)
* [Append and Prepend](#append-and-prepend)
* [Meta Data](#meta-data)
* [Manipulating The Items](#manipulating-the-items)
* [Sorting the Items](#sorting-the-items)
* [Rendering](#rendering)
    - [Built-in Renderers](#built-in-renderers)
        - [Render As UL](#render-as-ul)
        - [Render As OL](#render-as-ol)
        - [Render As Div](#render-as-div)
	- [Custom Renderers](#custom-renderers)
* [Authorization](#authorization)
* [Configuration](#configuration)

# I) CAHIER DES CHARGES DU PROJET
L'objectif du projet est de monter un site de dashboarding en utilisant le micro-framework python Flask et un capteur de températue de type DTH.  
Ce projet est juste un POC pour tester Flask et donner un backbone pour construire son propre site de Dashboarding.  
  
Afin de pousser un peu plus loin l'utilisation de Flask, une base de données sera utilisé et un système d'autentification sera rajouté en plus.
  
  
# II) LE MATERIEL NECESSAIRE (optionnel)

 * Un RASPBERRY
 * Un capteur de temprature, humidité DTH ([DTH11](https://www.robotshop.com/eu/fr/capteurs-temperature-humidite-dth11-dfrobot-gravity.html  "lien vers un site de revente"), DTH21, ...)
  
Afin de ne pas bloquer pour une question de materiels, le modèle intègre un simulateur de données. 

# III) Rentrons un peu dans la technique
## III)1 Le CHOIX DU FRAMEWORK BACKEND PYTHON 
En terme de framework web python, plusieurs possibilités sont disponibles avec parfois peu de différence.
Parmi ces frameworks, nous pouvons en citer deux qui ont retenu mon attention :
* DJANGO
* FLASK  

Inutile de refaire un comparatif qui à été réalisé de nombreuses fois. Je vous invite donc à lire cette [article](https://www.monocubed.com/flask-vs-django/).  
Pour donner mon avis personnel, je dirais que la force de Flask est ce qui en fait aussi sa faiblesse. C'est le projet qui doit vous orienter vers tel technologie ou l'autre.  
Flask a pour avantage en effet de très rapidement pouvoir démarrer un service web puisqu'en tant que micro-framework, il n'embarque pas toutes les composants que l'on retouve dans Django (ORM, Admin, ...). C'est en partie pour cela que Flask est tres interessant pour créer des applications monopages ou de Dashboarding qui ne necessite pas necessairement de bases, de gestions d'utilisateurs, ...  
Toutefois, il serait réducteur de croire que Flask est *simple d'utilisation*. En outre, il est tout à fait possible de se rapprocher d'un structure proche de DJANGO avec l'ajout de *add-on* comme un ORM, un gestionnaire de Session, ... Cela complexifie le projet d'autant que la doc n'est pas toujours aussi bien fournie (il sera necessaire de faire quelques recherches en plus).  
Sur ce point, même si Flask a une bonne communauté, Django est excellent avec une documentation unique trés bien fournie. 
  
Et qui dit liberté sur la structure, dit aussi difficulté à maintenir si la rigueur n'est pas là. Pour un débutant, il est judicieux au préalable de maitriser la [philosophie MVC | MVT](https://www.geeksforgeeks.org/difference-between-mvc-and-mvt-design-patterns/). 
  
Pour ma part, après m'être froté à Django, j'apprécie fortement la liberté de FLASK mais en appliquant certains concept de Django. Mes projets de type POC ou Monopage justifient aussi mon attirance pour ce Framework.

## III)2 ZOOM SUR [FLASK](https://flask.palletsprojects.com/ "se rediriger vers site du framework")

Pour installer flask, commencer par installer la biblioteque necessaire par la commande qui suit :  
```python -m pip install Flask```   
*Nota : ke préconise l'utilisation d'un environnement virtuel*
  
Le meilleurs moyen d'illuster Flask, c'est d'en montrer son apparente simplicité via le "Hello  World" de cette technologie :
Dans un fichier nommé *run.py*, saisir le code suivant, puis enregister.
```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
    
if __name__ == "__main__":
    app.run()
    
```  
Dans votre invit de commande préfére, saisir au niveau du répertoire contenant votre fichier *run.py* la commande suivante :  
```python run.py```  
  
Votre serveur est désormé lancé en local sur votre PC et est accesible à l'url suivante : http://127.0.0.1:5000/ ou http://localhost:5000/.

### III.2.a - FLASK : la base de données
Pour la base de données, j'ai fait le choix d'utiliser le système *sqlite* car du fait de sa simplicité de mise en place (un simple fichier avec l'extension .sqlite)  
FLASK à un petit défaut (ou pas d'ailleurs) car en tant que bon micro-framework, il ne possède pas d'interface d'administration de base de données comme peut l'avoir Django.
Il peut donc vite s'avérer diffcicile de manager ces bases si l'on n'a pas de connaissance de SQL. Rassurez-vous, plusieurs solutions de contournements à ce petit souci.

* Un add-on à flask comme [flask-admin](https://flask-admin.readthedocs.io/en/latest/)
* [La console SQLite](https://sqlite.org/cli.html) 
* Un utilitaire comme [DB Browser for SQLite](https://sqlitebrowser.org/)
  
Pour ma part, j'ai fait le choix d'utiliser la 3eme méthode car notre base et peu complexe et cela ne necessite pas nécessairement un sytème intégré à l'outils.
L'avantage toutefois de la première méthode est que cela s'adapte à d'autres types de technologies SQL. 

![utilitaire SQL](https://github.com/Enoarch/dash_flask/blob/main/readme_files/DBBrowser1.png)
![utilitaire SQL](https://github.com/Enoarch/dash_flask/blob/main/readme_files/DBBrowser2.png)

### III.2.b - L'ORM 
Dans le cadre de manipulation d'une base de type SQL, il est normalement necessaire de maitriser le SQL en plus de langage utilisé pour la création de l'application. Heureusement, Python permet de faire le lien entre le code et la base directement sans apprendre le SQL via un type de programme que l'on appelle un [ORM](https://fr.wikipedia.org/wiki/Mapping_objet-relationnel).
Contrairement à Django, Flask n'embarque pas nativement d'[ORM](https://fr.wikipedia.org/wiki/Mapping_objet-relationnel) et il est donc necessaire d'ajouter un add-on pour pouvoir l'intégrer au projet.   
  
Pour l'ORM, je vous conseille d'utiliser comme moi [SQLalchemy](https://www.sqlalchemy.org/) qui est simple d'utilisation et qui possede certaine fonctionalitée plutôt interessante.

### III.2.C - Gestion de Session et Système d'autentification 
> blabla

# RESUME DE LA STRUCTURE DU PROJET

# Comment lancer le projet ?  
Pour commencer, veuillez vous prémunir d'avoir bien python en version minimal de 3.6 installé sur votre PC.
J'ai pour habitude de travailler via des environnements virtuels pour mes projets en Python et je vous invite donc à le faire aussi.  
Pour ma part, j'utilise Virtualenv mais Venv fourni de base avec Python fait tres bien l'affaire.

A la racine du projet précédemment téléchargé, saisir la commande suivante dans votre invite de commande préféré :  
* ```python -m pip install -r requirements.txt```  
> Cette commande va permettre de charger les biblioteques necessaires au projet directement dans votre environnement virtuel.  

* ```python run.py```  
>  Commande pour lancer le serveur Flask

Vous pouver maintenant ouvrir votre application à l'adresse suivante : http://localhost:5000/
![Page de connexion](https://github.com/Enoarch/dash_flask/blob/main/readme_files/connection.png)
