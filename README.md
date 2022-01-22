![Langage Python](https://img.shields.io/badge/language-python-blue.svg)
![Langage JavaScript](https://img.shields.io/badge/language-javascript-blue.svg)
![Langage HTML](https://img.shields.io/badge/language-HTML-blue.svg)
![Langage CSS](https://img.shields.io/badge/language-CSS-blue.svg)
[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)



# PROJET
L'objectif du projet est de monter un site de dashboarding en utilisant le micro-framework python Flask et un capteur de températue de type DTH.  
Ce projet est juste un POC pour tester Flask et donner un backbone pour construire son propre site de Dashboarding.  
  
  
## LE MATERIEL NECESSAIRE (optionnel)

 * Un RASPBERRY
 * Un capteur de temprature, humidité DTH ([DTH11](https://www.robotshop.com/eu/fr/capteurs-temperature-humidite-dth11-dfrobot-gravity.html  "lien vers un site de revente"), DTH21, ...)
  
Afin de ne pas bloquer pour une question de materiels, le modèle intègre un simulateur de données. 

## STRUCTURE DU PROJET


## Le CHOIX DU FRAMEWORK BACKEND PYTHON 
En terme de framework web python, plusieurs possibilités sont disponibles avec parfois peu de différence.
Parmi ces frameworks, nous pouvons en citer deux qui ont retenu mon attention :
* DJANGO
* FLASK

## ZOOM SUR FLASK

### La base de données
Pour la base de données, j'ai fait le choix d'utiliser le système *sqlite* car du fait de sa simplicité de mise en place (un simple fichier avec l'extension .sqlite)  
FLASK à un petit défaut (ou pas d'ailleurs) car en tant que bon micro-framework, il ne possède pas d'interface d'administration de base de données comme peut l'avoir Django.
Il peut donc vite s'avérer diffcicile de manager ces bases si l'on n'a pas de connaissance de SQL. Rassurez-vous, plsuieurs solutions de contournements à ce petit souci.

* Un add-on à flask comme [flask-admin](https://flask-admin.readthedocs.io/en/latest/)
* [La console SQLite](https://sqlite.org/cli.html) 
* Un utilitaire comme [DB Browser for SQLite](https://sqlitebrowser.org/)
  
Pour ma part, j'ai fait le choix d'utiliser la 3eme méthode car notre base et peu complexe et cela ne necessite pas nécessairement un sytème intégré à l'outils.
L'avantage toutefois de la première méthode est que cela s'adapte à d'autres type de technologie 

### Le système d'autentification 


