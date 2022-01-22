![Langage Python](https://img.shields.io/badge/language-python-blue.svg)
![Langage JavaScript](https://img.shields.io/badge/language-javascript-blue.svg)
![Langage HTML](https://img.shields.io/badge/language-HTML-blue.svg)
![Langage CSS](https://img.shields.io/badge/language-CSS-blue.svg)
[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)



# CAHIER DES CHARGE DU PROJET
L'objectif du projet est de monter un site de dashboarding en utilisant le micro-framework python Flask et un capteur de températue de type DTH.  
Ce projet est juste un POC pour tester Flask et donner un backbone pour construire son propre site de Dashboarding.  
  
Afin de pousser un peu plus loin l'utilisation de Flask, une base de données sera utilisé et un système d'autentification sera rajouté en plus.
  
  
# LE MATERIEL NECESSAIRE (optionnel)

 * Un RASPBERRY
 * Un capteur de temprature, humidité DTH ([DTH11](https://www.robotshop.com/eu/fr/capteurs-temperature-humidite-dth11-dfrobot-gravity.html  "lien vers un site de revente"), DTH21, ...)
  
Afin de ne pas bloquer pour une question de materiels, le modèle intègre un simulateur de données. 

## Le CHOIX DU FRAMEWORK BACKEND PYTHON 
En terme de framework web python, plusieurs possibilités sont disponibles avec parfois peu de différence.
Parmi ces frameworks, nous pouvons en citer deux qui ont retenu mon attention :
* DJANGO
* FLASK

## ZOOM SUR FLASK
!["Flask Image"](https://upload.wikimedia.org/wikipedia/commons/3/3c/Flask_logo.svg?uselang=fr)
### La base de données
Pour la base de données, j'ai fait le choix d'utiliser le système *sqlite* car du fait de sa simplicité de mise en place (un simple fichier avec l'extension .sqlite)  
FLASK à un petit défaut (ou pas d'ailleurs) car en tant que bon micro-framework, il ne possède pas d'interface d'administration de base de données comme peut l'avoir Django.
Il peut donc vite s'avérer diffcicile de manager ces bases si l'on n'a pas de connaissance de SQL. Rassurez-vous, plsuieurs solutions de contournements à ce petit souci.

* Un add-on à flask comme [flask-admin](https://flask-admin.readthedocs.io/en/latest/)
* [La console SQLite](https://sqlite.org/cli.html) 
* Un utilitaire comme [DB Browser for SQLite](https://sqlitebrowser.org/)
  
Pour ma part, j'ai fait le choix d'utiliser la 3eme méthode car notre base et peu complexe et cela ne necessite pas nécessairement un sytème intégré à l'outils.
L'avantage toutefois de la première méthode est que cela s'adapte à d'autres types de technologies SQL. 

![utilitaire SQL](https://github.com/Enoarch/dash_flask/blob/main/readme_files/DBBrowser1.png)
![utilitaire SQL](https://github.com/Enoarch/dash_flask/blob/main/readme_files/DBBrowser2.png)

### L'ORM 
Dans le cadre de manipulation d'une base de type SQL, il est normalement necessaire de maitriser le SQL en plus de langage utilisé pour la création de l'application. Heureusement, Python permet de faire le lien entre le code et la base directement sans apprendre le SQL via un type de programme que l'on appelle un [ORM](https://fr.wikipedia.org/wiki/Mapping_objet-relationnel).
Contrairement à Django, Flask n'embarque pas nativement d'[ORM](https://fr.wikipedia.org/wiki/Mapping_objet-relationnel) et il est donc necessaire d'ajouter un add-on pour pouvoir l'intégrer au projet.   
  
Pour l'ORM, je vous conseille d'utiliser comme moi [SQLalchemy](https://www.sqlalchemy.org/) qui est simple d'utilisation et qui possede certaine fonctionalitée plutôt interessante.


### Le système d'autentification 


# RESUME DE LA STRUCTURE DU PROJET
