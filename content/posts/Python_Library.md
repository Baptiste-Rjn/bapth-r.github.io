---
title: "[Programmation] - Création et publication d'une librairie python"
subtitle: ""
date: 2024-03-03
draft: false
author: "Baptiste"
description: "Explication de la création de la librairie python"

tags: ["Programmation", "Pip", "Librairie"]
categories: ["Programmation"]

links:
  - title: GitHub
    description: Le projet
    website: https://github.com/Bapth-R/check_library
    image: github.png

image: "Pip/python-pip.png"
---

# Introduction
Depuis quelque temps, lors des développement Python que je fais, je perds du temps à vérifier si de nouvelles versions des librairies que j'utilise sont disponibles. Cela peut s'avérer fastidieux, surtout lorsque je dois consulter régulièrement mon fichier `requirements.txt` où sont répertoriées les bibliothèques utilisées par le projet. Dans cet article, je vais vous expliquer la création de mon projet permettant de rechercher et de mettre à jour le fichier requirements.txt avec les dernières versions des dépendances python et cela de manière automatique. Ce projet se base sur le site : https://pypi.org/, qui centralise toutes les bibliothèques Python.

# Développement 

Dans cette partie, nous allons nous intéresser au développement de notre code nous permettant de récupérer les dernières versions des librairies sur le site : [https://pypi.org/](https://pypi.org/). Bien entendu, le code sera écrit en Python 3 (version 3.12).

Dans un premier temps, nous cherchons à trouver la méthode la plus simple pour qu'une personne puisse vérifier si ses dépendances sont à jour et monter de version celles qui ne le sont pas. Nous avons opté pour qu'avec une seule commande, les bibliothèques se mettent à jour. Il faudra alors écrire la commande suivante en ajoutant des arguments optionnels afin de spécifier au code d'effectuer certaines actions :

```bash
check-library
```

Après nous être intéressés à l'interaction utilisateur, nous devons savoir comment aller chercher les dernières versions des bibliothèques utilisées. Pour cela, nous allons parcourir le fichier où sont stockées les bibliothèques utilisées (par défaut, le fichier requirements.txt). Dans un second temps, nous allons utiliser le flux RSS, un type de format Web facilement compréhensible par un bot, des librairies utilisées dans le projet afin de déterminer si ces bibliothèques possèdent des versions supérieures à celles utilisées dans le projet. À la fin de ce processus, cela créera un nouveau fichier nommé `requirement-output.txt` avec les nouvelles versions des dépendances. Voici un schéma explicatif de tout le processus :
![Schema PIP](/Pip/Schema_Lib.png#center)

Nous avons également ajouté par défaut une partie "verbose" nous indiquant si la bibliothèque scannée est à jour ou non. Nous détaillerons dans la partie "Utilisation" toutes les possibilités de personnalisation de ce code afin que ce programme soit apprécié par le plus grand nombre.

Pour finir, voici un exemple d'utilisation de la bibliothèque :
![Example check lib](/Pip/check-library_example.png#center)

# Publication
Après nous être assurés que notre programme est correct, nous devons le publier sur le site : https://pypi.org/. Nous allons alors vous expliquer comment procéder.

## Ajout d'un fichier setup.py
Dans un premier temps, nous devons créer un fichier nommé `setup.py` dans lequel nous allons spécifier toutes les caractéristiques de notre programme. Voici celui que j'ai utilisé :
```py
from setuptools import setup

setup(
    name='check_library',
    version='1.0.4',
    author='Bapth',
    description='Check and update libraries in a requirements file ',
    long_description=open('README.md').read(),
    long_description_content_type='text/markdown',
    url='https://github.com/Bapth-R/check_library.git',
    py_modules=['check_library'],
    license = 'Apache License, Version 2.0',
    install_requires=[
        'requests',
    ],
    classifiers=[
        'Programming Language :: Python :: 3',
        'Operating System :: OS Independent',
    ],
    entry_points={
        'console_scripts': [
            'check_library=check_library:main',
        ],
    },
)
```

Ici, nous spécifions le nom du projet, la version, l'auteur, la documentation, la licence, ... Toutes ces informations sont publiques et peuvent être récupérées en faisant, après avoir installé la librairie, la commande suivante :
```bash
>>> pip3 show check_library

# Output
Name: check-library
Version: 1.0.4
Summary: Check and update libraries in a requirements file 
Home-page: https://github.com/Bapth-R/check_library.git
Author: Bapth
Author-email: None
License: Apache License, Version 2.0
Location: /home/debian/.local/lib/python3.9/site-packages
Requires: requests
Required-by: 
```

## Création d'un compte sur le site PyPI
Afin de publier une nouvelle librairie Python, nous devons nous inscrire sur le site PyPI, ce qui est très simple.
Ensuite, il faudra créer un token nous permettant de nous authentifier lorsque nous souhaitons effectuer une modification sur la librairie. Pour cela, il faut se rendre sur l'URL : https://pypi.org/manage/account/token/ et générer un token. Le format doit être le suivant : `pypi-{170}`. Une fois généré, il faut mettre ce token dans le fichier `.pypirc` qui doit être présent à la racine du projet. Le format de celui-ci doit être (le seul élément à modifier est le mot de passe) :
```bash
[distutils]
index-servers =
  pypi

[pypi]
repository: https://upload.pypi.org/legacy/
username:__token__
password:pypi-*********
```

Une fois créé, il est judicieux de créer un fichier `.gitignore` qui permettra de spécifier certains fichiers à ne pas publier sur Github, comme le fichier où est présent le token. Voici le mien :
```bash
venv/
.pypirc
.DS_Store/
__pycache__
dist/
build/
*.pyc
*.pyo
*.pyd
*.egg-info/
```

Une fois toutes ces étapes effectuées, nous avons créé un dépôt GitHub afin d'y stocker notre code et que tout le monde puisse voir quelles sont les actions effectuées par le script.

Après la création du repo et le push du code, nous devons publier notre code afin qu'il soit téléchargeable en utilisant uniquement la commande : `pip3 install check-library`. Pour cela, il faut exécuter la commande : `python3 setup.py sdist bdist_wheel` qui va créer trois dossiers :

- build
- check_library.egg-info
- dist
Une fois fait, nous devons utiliser la commande permettant de publier notre bibliothèque : `python3 -m twine upload dist/*`. Pour avoir la certitude que notre bibliothèque a bien été publiée, nous pouvons aller sur le site PyPI : https://pypi.org/project/check-library/
![PyPI](/Pip/pypl.png)

# Utilisation
Dans cette avant-dernière partie, nous allons voir comment utiliser la bibliothèque. La documentation est déjà présente sur mon GitHub : https://github.com/Bapth-R/check_library, cependant, je vais la synthétiser ici.

Comme nous l'avons vu au début de cet article, cette librairie se veut la plus simple d'utilisation possible. Pour cela, vous pouvez l'utiliser sans avoir besoin d'être expert. Il suffit de saisir la commande : `check_library`dans un terminal. Cela va prendre toutes les librairies présentes dans le fichier `requirements.txt`, récupérer leurs dernières versions, et créer un fichier nommé `requirement-output.txt`, qui sera le fichier requirements.txt mis à jour.

Cependant, nous pouvons personnaliser cette librairie afin qu'elle puisse répondre à toutes les attentes. Elle peut :
- Modifier le nom du fichier `requirements.txt` si le fichier utilisé pour stocker ses librairies possède un autre nom grâce à l'option `-p` ou `--path` suivie du nom du fichier.
- Modifier le nom du fichier de destination. Par défaut, il sera nommé `requirement-output.txt`, mais nous pouvons modifier le nom donné par défaut grâce à l'option `-o` ou `--output` suivie du nom du fichier.

- Enlever l'option verbose. Cela n'affichera plus les librairies dans le terminal, mais uniquement le message : `Requirements file updated` quand le programme aura terminé. Pour cela, il faut utiliser l'option `-v` ou `--verbose`.
- Écraser le fichier d'origine. Afin de ne pas avoir plusieurs fichiers requirements, l'option `-f` ou `--force` permet d'écraser le fichier d'input avec les nouvelles versions des librairies.
- L'option `-h` ou `--help` permet de connaître les personnalisations du script et comment l'exécuter.
## Exemple d'utilisation
Nous allons maintenant voir quelques exemples d'utilisation afin que cela soit plus clair.

### Exemple 1 
Dans cet exemple, nous voulons mettre à jour nos librairies depuis le fichier `config/requirements.txt`. Nous souhaitons que le fichier de sortie soit : `config/requirements-output`.txt. Pour cela, nous devons exécuter la commande suivante :
```bash
>>> check_library -p config/requirements.txt -o config/requirement-output.txt
```

### Exemple 2
Dans cet exemple, nous voulons mettre à jour nos librairies depuis le fichier `requirements.txt` (par défaut) et que les versions à jour des bibliothèques se remettent dans ce fichier. Pour cela, nous devons utiliser la commande suivante :
```
>>> check_library -f
```
En effet, comme le fichier par défaut d'input est `requirements.txt`, nous n'avons pas eu besoin de spécifier le chemin du fichier d'origine. De plus, nous souhaitons écraser ce fichier afin de le mettre à jour. Il faut alors utiliser l'option `-f` qui va forcer l'écrasement du fichier.


# Améliorations
Nous allons maintenant nous intéresser aux différentes améliorations que nous pouvons implémenter sur ce programme afin de le rendre plus complet.

## Découverte de CVE
Pour chaque librairies obsolète, nous pouvons vérifier si entre la version marquée dans le fichier contenant les dépendances utilisées par le projet et celles actuelles, des vulnérabilités ont été découvertes. Si oui, donner le score CVSS de chaque vulnérabilité.

## Publication automatique 
Pour chaque modification du code source publiée sur Github, un workflow pourrait être mise en place afin de publier automatiquement la nouvelle version sur le site PyPI après avoir effectué des tests unitaires au préalable.

## Découverte automatique des librairies utilisées
Une dernière amélioration pourrait être de découvrir automatiquement les librairies utilisées par le projet, puis de générer/modifier le fichier répertoriant les bibliothèques utilisées.

# Conclusion
En conclusion, la réalisation de ce projet m'a permis de ne plus avoir à me préoccuper des versions de mes librairies Python, car le script le fait pour moi. De plus, cela m'a permis de comprendre le processus de publication de librairies Python. Si vous trouvez ce projet intéressant, n'hésitez pas à aller "starrer" le projet sur Github :)

