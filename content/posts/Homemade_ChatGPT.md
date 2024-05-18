---
title: "[Intelligence Artificielle] - Construction d'un ChatGPT hébergé en local "
subtitle: ""
date: 2024-05-18
draft: false
author: "Baptiste"
description: "Construction d'un ChatGPT hébergé en local"

tags: ["Artificial Intelligence"]
categories: ["IA"]

image: "IA.png"
---
# Syllabus 
J'ai essayé de rendre ce document le plus accessible possible en évitant les termes trop techniques. Cependant, à certains moments, ce document entrera plus en détail dans l'hébergement d'une intelligence artificielle. À ce moment-là, j'essaierai de fournir des explications afin que tout le monde puisse comprendre cet article.
---

# Introduction 

Depuis le 30 novembre 2022, le modèle de langage d'OpenAI, ChatGPT (Chat Generative Pre-Trained Transformer), a été rendu accessible à tous gratuitement, ce qui a marqué un tournant dans l'utilisation de l'IA dans le monde. En effet, nous pouvons constater que le nombre de modèles sur le site Hugging Face (une entreprise française proposant des modèles d'IA en open source) a augmenté de manière significative depuis 2023. Grâce au site Wayback Machine, nous constatons que le 16 mai 2023, c'est-à-dire il y a un an, le nombre de modèles disponibles était de 202 865. Maintenant, le 18 mai 2024, 660 531 modèles sont disponibles sur ce site. Nous pouvons trouver des modèles permettant d'analyser des images, de générer du texte, de générer des voix humaines, etc.



Avec cette évolution du nombre de models disponibles, des entreprises se sont spécialisé dans la création de models comme l'entreprise Mistral, une entreprise francaise qui développe des models rivalisant avec ceux de ChatGPT et de Meta. Voici un graphique mesurant la compréhention de des plus gros models. 
![Mistral comparaison](images/ia/Mistral_comparaison.jpeg)

Nous allons alors dans cet article héberger un model permettant de pouvoir converser comme nous faisons avec ChatGPT. Pour cela, nous utiliserons comme hardware RaspberryPi 4B (1Go RAM) ainsi que mon MacBook Pro M1 (16Go RAM) permettant d'héberger les models utilisés. Afin de contruire cela, je me suis inspiré de la vidéo de NetworkChuck (host ALL your AI locally).  

# Explication des models utilisés

Nous utiliserons différents LLM (Large Language Model) afin de contruire notre ChatGPT local. Un LLM est un model d'apprentissage automatique permettant de comprendre et de produire du texte de manière cohérente et ordonné comme peut le faire ChatGPT. Les LLM se caractérisent par: 
- Leur taille: Le nombre de paramètres (tokens) que ces models peuvent comprendre. Cependant, nous ne pouvons pas dire que un langage est meilleur qu'un autre juste en ce basant sur ce paramètre. 
- Leur capacité de compréhension: Les déductions qu'il peut faire en fonction du texte donné, l'analyse sémantique afin de comprendre la signification du texte et non seulement des mots. 
- Leur technique d'apprentisage: Le traitement en parallèle de mots afin de mieux comprendre le sens général du texte fourni ainsi que le fine-tuning, une technique utilisé après l'apprentisage initial afin de rendre le LLM plus performant dans un sujet donnée en créant un focus sur un sujet précis. 

Comme nous l'avons vu précédament, nous utiliserons plusieurs langage:
- Mistral 7B [Mistral Model](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2): Le model de Mistral de 7 milliards de token.
- Llama-3 8B [Lama Model](https://huggingface.co/meta-llama/Meta-Llama-3-8B): Le dernier model de Meta rivalisant avec ChatGPT-4.
- Dolphin-2.9.1-llama-3-8b [Dolphin Llama](https://huggingface.co/cognitivecomputations/dolphin-2.9.1-llama-3-8b): Le dernier model de Meta ayant moins de restrictions.

## Installation des models

Apres avoir définis les modes utilisés, nous allons maintenant définir l'architecture de notre projet.
![Architecture schema](images/ia/Schema_Architecture.png)


Après avoir définis les models utilisés, nous allons devoir installer Ollama, un framework permettant d'exécuter des LLM en local. J'ai voulu installer ollama dans un docker. Pour cela, j'utilise docker desktop car je suis sur Mac mais vous pouvez très facilement utiliser docker (Explication d'installation: https://docs.docker.com/engine/install/debian/). 

Apres l'installation de docker, nous devons installer l'image docker. Pour cela, n'ayant pas de GPU Nvidia, j'ai lancé l'image grâce à la commande suivante:
```txt
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```
Cependant, si vous avez une carte Nvidia, vous pouvez utiliser cette commande afin d'utiliser votre GPU:
```txt
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

Après, nous devons exécuter les 3 modèles ci-dessus pour cela, nous devons faire la commande:

```txt
docker exec -it ollama ollama run llama3
docker exec -it ollama ollama run mistral
docker exec -it ollama ollama run dolphin-llama3:8b-256k
```

Après avoir fait toutes ces étapes, vous devez normalement avoir accès à ollama en local. Pour s'assurer que tout fonctionne bien, regardez si vous avez une réponse quand vous allez sur l'url: http://<your-local-ip>:11434 si vous avez comme retour `Ollama is running` cela signifie que Ollama a bien démarré correctement. 


## Installation de OpenWebUI

Nous allons maintenant installer OpenWebUI afin d'avoir une interface graphique à Ollama. Pour cela, j'ai utilisé mon RasbperryPi qui doit bien entendu être sur le même réseau que l'instance Ollama. 
Après avoir installer docker sur le raspberry, nous devons lancer l'image OpenWebUI grâce à la commande suivante:
```txt
sudo docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://<server-ip>:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

On a maintenant raccordé Ollama avec une interface graphique. Cependant, nous ne pouvons pas accéder à l'instance web depuis n'importe quel appareils dans notre réseau. Pour cela, nous allons utiliser nginx afin qu'il prenne le rôle de reverse proxy. Pour cela, nous l'installons : `sudo apt install nginx`. 

Après cela, nous modifions la configuration comme expliqué ci-dessous:
```txt
server {
    listen 80;
    server_name 192.168.0.190;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
Puis appliquons notre configuration en redémarrant le service: `sudo systemctl restart nginx`

## Configuration de OpenWebUI

Après avoir configurer le reverse proxy, nous pouvons accéder à la plateform en allant sur l'url: http://<raspberry-ip>. On nous demande de nous connecter. Le premier compte créer sera le compte d'admin. 
Voici l'interface après la connection:
![WebUI first](images/ia/WebUI.png)

En allant dans la partie Modelfiles, nous pouvons configurer notre instance afin que les réponses soient plus adapté à notre besoin. De mon coté, je défini l'instance pour qu'elle soit plus compétente en programmation. Pour cela, je lui définis un content particulier et j'adapte la catégorie à 'Programming' et 'Education'. Cela permettra au model d'avoir plus de contexte et ainsi mieux me répondre. 

En allant dans la partie Documents, nous pouvons donner aux LLMs des fichiers textes. Grâce à cela, les LLMs peuvent récupérer des informations présentes dans les documents fournis et ainsi améliorer leurs réponses. 

Pour finir, nous pouvons donner à chaque prompt un tag ce qui nous permet de mieux classer et ainsi retrouver nos prompts. Une partie de recherche a aussi été intégrée ce qui facilite aussi amplement la recherche d'ancien prompts.

## Utilisation de différents models

Nous allons nous interesser dans cette dernière partie la différence concrète des différents models. Nous pouvons en effet nous rendre rapidement compte que le model de llama et mistral sont quasiment identique dans leurs réponses. Cependant, le model dolphin est très interessant. Il nous permet de poser tout type de questions sans aucune restriction. Je lui ai par exemple demander de m'expliquer en détail avec des exemples le principe d'injections SQL un sujet que ChatGPT n'aurait pas voulu traiter. Ainsi, le fait d'héberger ses models en local en complément de ChatGPT est un bonne alternative quand nous souhaitons discuter de sujets précis.

## Conclusion

Même si les réponses générés par nos LLMs en local sont moins rapide que ChatGPT, nous pouvons garder nos données en local ce que je trouve est un élément majeur. De plus la possiblilité d'utiliser le model que nous voulons est aussi un élément déterminant. En effet, avec le model dolphin, nous pouvons poser tout type de questions au model sans avoir de limitation ce qui peut être très avantageux dans le domaine de la cybersécurité. 