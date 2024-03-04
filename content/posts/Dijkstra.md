---
title: "[Algorithme] - Dijkstra"
subtitle: ""
date: 2024-01-20
draft: true
author: "Baptiste"
description: "Analyse de l'algorithme de Dijkstra"

tags: ["Algorithme", "Dijkstra", "Plus court chemin", "Théorie des Graphes"]
categories: ["Alogrithme", "Théorie des Graphes"]

image: "dijkstra/dijkstra_wallpaper.png"
featuredImage: ""
featuredImagePreview: ""
--- 
# Introduction
Dans cet article, nous allons nous intéresser à un des algorithmes les plus connus de la théorie des graphes c'est à dire **l'algorithme de Dijsktra**.  
La théorie des graphe permet d'étudier les relations entre plusieurs objects. Ceux-ci sont représentés par des points, que l'on appelle des "nœuds" ou "sommet", et les relations entre eux sont représentées par des lignes, que l'on appelle des "arêtes".  
**L'algorithme de Dijkstra** aussi appelé **l'algorithme du plus court chemin** consiste, à partir d'un réseau de nœuds et d'arêtes distinger les plus court chemin qui permet d'aller d'un point A à B le plus rapidement possible.   

Nous verrons dans cet article, des cas d'utilisations dont un relatif à la cybersécurité. Puis nous nous intéresseront à son implémentation en Python.

# Cas d'utilisation
De nombreuses fois, je me suis demandé comment réussir à optimiser ce que j'étais entrain de faire afin de gagner du temps. Cependant, en fonction de la tâche en court, il est des fois impossible de réussir à l'optimiser correctement sans l'aide d'une machine capable d'effectuer un grand nombre d'opérations. Nous allons alors nous intéresser à plusieurs cas d'utilisation de l'algorithme de **Dijkstra**:

- **Choix du meilleur itinéraire**: En prenant cet exemple en compte, nous pouvons schématiser un plan routier avec cet algorithme. Les villes seront représenter par les nœuds et les routes par les arêtes. Cela nous permettra de savoir quel sera les plus court et le plus rapide grâce aux informations fournis par les arêtes. Nous pouvons même imaginer que ces informations se mettent automatiquement à jour en fonction de la circulation.   
> ℹ️ Il faut aussi noter que cela peut très bien être appliqué pour tout problème nécessitant de trouver le plus court chemin comme de l'optimisation sur un ensemble de production par exemple.

- **Modélisation de connexion sur les réseaux sociaux**: Un autre utilisation serait sur la connexion des utilisateurs des réseaux sociaux. Nous pouvons très bien nous imaginer que les amis d'une personnes sont représenter par les nœuds et que leur niveau d'amitié soit caractérisé par les arêtes. En fonction de cela, il serait possible de trouver comment faire devenir 2 personnes amis en se basant sur les informations fournis par notre algorithme.
    
- **Détermination des chemins d'attaques les plus optimales pour l'attaquant**: Le dernier cas d'utilisation que nous allons observer est l'implémentation de l'algorithme de **Dijkstra** afin de déterminer quel serait le chemin d'attaque le plus optimal qui nous permetterait de compromettre une machine depuis un endroit définit préalablement. Il est vrai que pour réussir à implémenter cela, il faut avoir une extrême bonne gestion de son parc informatique afin de connaitre toutes ses machines, les version et types d'OS (système d'exploitation), les services exposés, les vulnérabilités devant être exploités, ... 


# Implémentation
Nous allons maintenant nous intéresser au fonctionnement de cet algorithme. Nous verrons alors dans un premier temps ce qu'est concrètement cet algorithme. Nous continurons par écrire l'algorithme. Puis nous finirons par l'implémenter en Python en y ajoutant quelques fonctionnalités utiles.

## Définition
Comme mentionné précédemment, l'algorithme de **Dijkstra** utilise des concepts tels que les "nœuds" et les "arêtes". Les nœuds représentent les points d'intersection, et ils ne contiennent qu'un identifiant unique sans autre information. Les arêtes sont les liens qui permettent de connecter deux nœuds. Pour évaluer la complexité du chemin à parcourir d'un point à un autre, on associe à chaque arête un poids indiquant le niveau de difficulté de la connexion. 
Prenons par exemple un trajet Paris vers Lyon. 
![DIJKSTRA Illustration](dijkstra/image_dijkstra.png)  
Nous pouvons nous rendre compte que plusieurs chemins nous permettre de notre rendre à Lyon en partant de Paris. Cependant, la complexité (ici le temps), est différentes en fonction des chemins pris. En appliquant cet algorithme, nous pourrons alors savoir plus facilement quel chemin prendre.  


## Ecriture

## Implémentation
# Conclusion

# Sources
- https://fr.wikipedia.org/wiki/Théorie_des_graphes
- https://fr.wikipedia.org/wiki/Algorithme_de_Dijkstra