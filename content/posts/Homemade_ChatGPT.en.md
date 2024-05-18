---
title: "[Artificial Intelligence] - Build a home"
subtitle: ""
date: 2024-01-27
draft: false
author: "Baptiste"
description: "Analyse du groupe LAPSUS$"

tags: ["CTI", "LAPSUS$"]
categories: ["CTI"]

image: "LAPSUS.webp"
---
# Syllabus 
J'ai essayé de rendre ce document le plus accessible possible en évitant les termes trop techniques. Cependant, à certains moments, ce document entrera plus en détail dans l'hébergement d'une intelligence artificielle. À ce moment-là, j'essaierai de fournir des explications afin que tout le monde puisse comprendre cet article.


---

# Introduction 

**LAPSUS$**, également connu sous le nom de **SaudeGroup**, est un groupe de cybercriminels apparu à la fin de l'année 2021. Ils communiquent principalement en anglais et en portugais lors de leurs échanges avec les entreprises. Ils se sont rapidement fait connaître en divulguant des données confidentielles de plusieurs entreprises connues telles que **Microsoft**, **NVIDIA**, ainsi que des entités gouvernementales comme le **ministère de la santé du Brésil**. Contrairement aux groupes actuels de cybercriminels, LAPSUS$ ne déploie pas de ransomware après leurs attaques, à l'exception de celle dirigée contre le ministère de la santé du Brésil qui en a subit un.

Il est également à noter que LAPSUS$ n'est ni affilié ni sponsorisé par un État, comme ils le répètent souvent sur leur Telegram. Ils piratent et divulguent des données contre de l'argent ou des suppressions de limitations matérielles, comme nous le verrons dans le cas de NVIDIA.

Dans ce rapport, nous examinerons le groupe LAPSUS$ afin d'essayer de comprendre les motivations de ses membres en effectuant une recherche plus approfondie sur le créateur de ce groupe. Ensuite, nous nous intéresserons aux différentes attaques menées par ce groupe en nous renseignant préalablement sur les techniques, outils et méthodes utilisés par les hackers pour atteindre leurs objectifs. Nous conclurons ce document en nous penchant sur l'arrestation et la prétendue fin du groupe LAPSUS$.

# Création du groupe

LAPSUS$ est un groupe de cybercriminels assez récent spécialisé dans le **vol de données d'entreprise**. Il a été créé il y a environ 3 ans par un individu nommé **Arion Kurtaj**, également connu sous les pseudonymes de **Whitedoxbin**, **Breachbase**, **Oklaqq**, et **White**. Pour des raisons de simplicité, nous l'appellerons dans la suite de ce document uniquement par l'un de ses pseudonymes : **White**.  
Nous allons voir dans la suite de cette partie le principal protagoniste du groupe.

## Arion Kurtaj alias White

À l'âge de **16 ans**, White se fait connaître sur Internet en vendant et achetant des **0days**, c’est-à-dire des vulnérabilités impactant des services informatiques qui n'ont fait l'objet d'aucune publication ou qui n'ont aucun correctif public connu. Grâce à cette activité, il réussit à accumuler une somme estimée à environ **14 millions** de dollars en bitcoin (BTC). Afin de garantir un minimum d'anonymat, tous ses échanges sont effectués avec un compte Telegram ou une adresse e-mail (`dox[***]te@pr[***]om` et [`https://t.me/doxbinwhite`](https://t.me/doxbinwhite)). Pour trouver ses acheteurs, il utilise de nombreux forums, notamment celui nommé : **RAIDForums** qui a été fermé par le FBI depuis.

![RaidForum Image](images/lapsus/raidforum.png)


En plus de cela, **White** est un membre fondateur du groupe nommé **Infinity Recursion**, ayant comme domaine de prédilection le **SIM-Swapping** et le **Swatting**, 2 techniques que le groupe **LAPSUS$** utilisera pour commenttre ses actes de piratages.  

Explorons maintenant la définition de ces deux termes :
- Le **SIM-Swapping** permet de voler le numéro de téléphone de quelqu’un afin de pouvoir s’authentifier à ses comptes protégés par le 2FA (2 Factor Authentication) .
- Le **swatting** est une pratique de canular téléphonique visant à tromper les services de police de manière anonyme, en simulant une situation d'urgence, généralement chez un individu particulier, dans le but de lui causer des problèmes.

Sur ce site, il utilise un nouveau pseudo : **Everlynn**.


Pour continuer ses activités criminelles, **White** est également un membre actif sur le site `doxbin[.]com` dont il devient le propriétaire pour **75 000$** en BTC, mais se retrouve contraint de revendre le site peu de temps après vers janvier 2022 pour **20 000$**, car il n'est pas apprécié au sein de la communauté. Juste avant de le rendre, il divulgue l'intégralité du site pour se venger sur Telegram.

![Doxbin leak download](images/lapsus/doxbin_download.png)

Une analyse des articles sur https://flashpoint.io/blog/doxbin-leak/ et https://cyble.com/blog/sensitive-information-exposed-through-doxbin-data-leak/ a révélé que la fuite de données contient les informations de **41 544 utilisateurs uniques** dans lesquelles sont présentes :   
- les noms d'utilisateur
- les adresses e-mail 
- les mots de passe

Il faut aussi noter que dans la fuite de données, nous pouvons notamment trouver le mot de passe de White que nous ne divulguerons pas.   
![Doxbin leak White password ](images/lapsus/doxbin_password.png)  
Afin de se venger, les membres du forum l'ont par la suite doxxé, c'est-à-dire qu'ils ont révélé ses informations personnelles. Voici une capture d'écran montrant certaines données personnelles de White, bien entendu masquées.  
![Doxbin leak White](images/lapsus/doxbin_white_leak.png)  
Dans ce leak, nous pouvons retrouver des photos de lui enfant, ainsi que des adresses e-mail, des mots de passe, des informations sur sa famille, et bien d'autres détails personnels.  Par ailleurs, voici une image de lui enfant que nous pouvons retrouver dans ces données :  
![Doxbin leak img White](images/lapsus/doxbin_white2.png)  

Même en étant découvert et possédant toutes ces informations personnelles sur Internet, White est resté comme nous allons le voir un membre actif du groupe **LAPSUS$**. Interessons nous alors à ce groupe afin de connaitre ses revendications ainsi que ses différents piratages.

# Activités du groupe LAPSUS$
## Découverte du groupe 

**LAPSUS$** est un groupe de cybercriminel composé de personnes jeunes dont des mineurs (-18 ans). Ils se sont fait connaitre en **décembre 2021** et sont à l'origine de nombreuses fuites de données d'entreprises de renommé mondiales comme **NVIDIA**, **Microsoft** et même **Ubisoft**. Nous allons voir dans le suite de ce document les méthodes utilisées par ce groupe, puis les différentes attaques qu'ils ont ménées.


## Méthodes utilisées par ce groupe

**LAPSUS$** utilise une large diversité de tactiques, techniques et procédures, cependant, ils préfèrent utiliser des failles humaines afin de réussir à arriver à leur objectif ce qui ne nécessite pas de techniques avancées en sécurité informatique. Nous pouvons en effet, retrouver un message sur leur Telegram essayant de recruter des personnes travaillant dans une des sociétés qu'ils avaient pour cible afin qu'ils leurs fournissent un accès initial : 
![Telegram hire](images/lapsus/telegram_hire.png)  


Comme nous venons de le voir, le principal canal de communication est Telegram et une adresse mail:
- **t[.]me/min...r** (Ouvert) — Salon de revendication d’attaque
- **t[.]me/s…t** (Supprimé) — Salon permettant de discuter avec la communauté et faire des sondages permettant de décider quel sera le prochain leak.
- **sa...up@ct...ar.com**

Après avoir découvert leurs moyens de communication, nous allons nous intéresser aux différentes attaques qu'ils ont menées.

## Attaques menées
Nous allons maintenant nous intéresser aux différentes attaques perpétrées par ce groupe dans un ordre chronologique. Nous allons nous appercevoir qu'en seulement 2 mois, de nombreuses entreprises ont subi des attaques et ont perdu des données précieuses. 

### Ministère de la santé du Brésil
>⚠️ Un lien est présent sur leur Telegram permettant de télécharger des données du ministère

Leur première attaque connue a été faite et revendiquée le **10 décembre 2021**, prenant pour cible le ministère de la santé du Brésil. Bien que peu relayée médiatiquement, cette attaque a permis au groupe d'attaquants de dérober environ **50 To de données**. Pour conclure sur cette attaque, le site du ministère a également été effacé, exposant ainsi le message suivant:  
![MOH](images/lapsus/message_MOH_web.png)  
Une communication a été faite par la suite sur leur Telegram annoncant cette compromission. Cela a été leur première communication : 
![MOH Telegram](images/lapsus/telegram_moh.png)  

### Claro et Embratel
>ℹ️ Aucun lien n'est présent sur leur Telegram permettant de télécharger les données

Quatorze jours plus tard, le groupe revendique deux autres attaques, affirmant avoir réussi à pirater les entreprises **Claro** et **Embratel** le **24 décembre 2021**. Dans ces cas également, le groupe demande une somme d'argent afin de ne pas divulguer des informations sur les sociétés, représentant une taille de **10 000 To de documents confidentiels**.  
![Claro Telegram](images/lapsus/telegram_claro.png)  

### Impresa
>ℹ️ Nous n'avons pas réussi à avoir un lien nous permettant de télécharger les données

Dans la suite de ces attaques, le 1er janvier 2022, l'entreprise **Impresa** a subi une attaque du groupe **LAPSUS$**, lors de laquelle le groupe a pris le contrôle des actualités, envoyé des e-mails de phishing à tous les abonnés d’Impresa, et rédigé un tweet sous le nom d’Expresso (un média dont Impresa est propriétaire) revendiquant le groupe LAPSUS$ comme le nouveau président du Portugal :     
![Tweeter Expresso](images/lapsus/twitter_expresso.png)  

### Localiza
>ℹ️ Aucun lien n'est présent sur leur Telegram permettant de télécharger les données

Après l'attaque impactant Impressa, il n'a pas fallu attendre plus de 10 jours pour que le groupe revendique une autre attaque sur l'entreprise **Localiza**. Afin de prouver l'attaque aux yeux de tout le monde et pour faire le plus de bruit possible, ils ont redirigé le site de l'entreprise de location de voitures vers un site pour adultes, en se vantant de leur exploit sur Telegram :  
![Localiza Telegram](images/lapsus/telegram_localiza.png)  

### Vodafone
>ℹ️ Aucun lien n'est présent sur leur Telegram permettant de télécharger les données

Le **8 février 2022**, le groupe refait parler de lui après l’attaque réussie contre **Vodafone**.
Le 11 février, le groupe affirme sur leur Telegram qu’ils ont réussi à voler environ 500Gb de données. On apprendra le 7 mars que ces données représentent environ 5000 repository Github.   
![Vodafone Telegram](images/lapsus/telegram_vodafone.png)  
Cette fuite de donnée fait suite au sondage qu'ils ont fait sur leur Telegram, où ils demandaient quelles informations leurs followers voulaient voir divulguées. C'est l'entreprise Vodafone qui a malheureusement "remporté" le sondage:  
![Sondage Telegram](images/lapsus/telegram_sondage.png)  

### NVIDIA
>⚠️ Un lien est présent sur leur Telegram permettant de télécharger des données de NVIDIA

Le groupe a par la suite fait une "pause" de 17 jours avant de rendre publique leur attaque sur **NVIDIA** le 25 février 2022. Par rapport aux autres attaques, celle-ci a pris plus d'ampleur. Le PDG de NVIDIA à l'époque, **Jensen Huang**, a été interviewé sur la chaîne Yahoo Finance afin de parler du piratage que subissait son entreprise :  
[PDG NVIDIA vidéo](https://finance.yahoo.com/video/nvidia-ceo-says-lapsus-hack-134523585.html?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAMvftKOX8Nc4klL14WRJTEYnUg05xbz4drEwNYKqn0DqHxUac5DIXr3dPjudT1OcdSx6nX99btWMSbuIu4VCV4IQ4TU7IdbGvhnIlWNSOPUr-j8G1tX8KyNTA7UvGs2-LCoYU0Ogx5yEiFrhc1Le9ltn_erkcTPcbe2Tv0IsYt5I).

Par rapport aux autres attaques, les pirates avaient de réelles revendications afin de ne pas révéler les informations qu'ils avaient réussi à voler. Au total, environ 1 To de données ont été exfiltrées. Cela comprenait, selon LAPSUS$ :
- Schéma de cartes
- Drivers
- Firmwares
- ...
 

Le 28 février, LAPSUS$ publie ce message sur son Telegram revendiquant l'attaque.   
![NVIDIA 1 Telegram](images/lapsus/telegram_nvidia1.png)  
Quelques heures après, le premier leak est partagé sur leur Telegram, et ils demandent par la même occasion de désactiver la limitation LHR (une protection contre le minage de cryptomonnaies) pour les cartes NVIDIA, ce qui réjouit certaines personnes sur Reddit.  
![Meme NVIDIA](images/lapsus/meme_nvidia.png)  

---

![NVIDIA leak](images/lapsus/telegram_nvidia_torrent.png)  
Dans les informations révélées, des certificats de signature de code de NVIDIA ont permis à des malwares d'être signés par NVIDIA, contournant ainsi les antivirus.

Deux jours après, le 1er mars, le groupe LAPSUS$ demande à NVIDIA que les drivers des GPU pour Windows, MacOS et Linux soient désormais open source pour toujours. Cependant, NVIDIA ne répondra pas. À cause de cela, une fuite de données de 71 000 comptes d'employés est révélée.  
![NVIDIA 2 Telegram](images/lapsus/telegram_nvidia2.png)  

Quelques jours avant cette dernière revendication, NVIDIA a contre-attaqué le groupe en implantant un ransomware sur les machines de LAPSUS$. Le groupe a confirmé ces propos sur leur second canal Telegram :  
![NVIDIA Hackback](images/lapsus/hackback_nvidia.png)  

### Samsung
>⚠️ Un lien est présent sur leur Telegram permettant de télécharger des données de Samsung

Le 4 mars 2022, le groupe revendique une attaque contre Samsung, affirmant avoir volé de nombreuses informations et mettant à leur habitude un fichier torrent contenant au moins une partie des informations dérobées.  
![Samsung Telegram](images/lapsus/telegram_samsung.png)

### Ubisoft
>ℹ️ Aucun lien n'est présent sur leur Telegram permettant de télécharger les données

Le 12 mars, le groupe revendique une attaque sur Ubisoft, mais aucune donnée n'est fournie. Les informations à ce sujet sont minimes.  
![Ubisoft Telegram](images/lapsus/telegram_ubisoft.png)

### Microsoft
>⚠️ Un lien est présent sur leur Telegram permettant de télécharger des données de Microsoft

Microsoft est le prochain à subir une fuite de données le 20 mars, mais la plupart des informations relatives au piratage ont été supprimées de leur Telegram. Cependant, nous avons réussi à récupérer plusieurs publications avant la suppression, dans lesquelles ils disaient avoir :

- 90% du code source de Bing Maps
- 45% du code source de Cortana et Bing
- Corrompu un Azure DevOps  

![Microsoft Telegram](images/lapsus/torrent_microsoft.png)

### LG  
>⚠️ Un lien est présent sur leur Telegram permettant de télécharger des données de LG

Deux jours après, le 22 mars, LG subit une fuite de données. Sur la publication de revendication, le groupe LAPSUS$ se moque de la compagnie en disant qu'en seulement 1 an, le groupe a subit 2 cyberattaques. Les criminels publient alors une liste de tous les hash des employés et services de LG.  

![LG Telegram](images/lapsus/torrent_lg.png)

![LG Leak](images/lapsus/leak_lg.png)

### Okta
>⚠️ Un lien est présent sur leur Telegram permettant de télécharger des données de Okta

Le 22 mars, le même jour que la divulgation des données de LG, le groupe publie un message revendiquant une attaque contre Okta. Ils partagent de nombreuses captures d'écran où on les voit comme administrateurs.  
![Okta 1 Telegram](images/lapsus/telegram_okta1.png)

Cependant, le même jour, Okta publie un article expliquant qu'ils n'ont pas subi d'attaque : [Okta Statement](https://www.okta.com/blog/2022/03/updated-okta-statement-on-lapsus/). Ces informations ont été démenties et mal prises par le groupe LAPSUS$.  
![Okta 2 Telegram](images/lapsus/telegram_okta2.png)  
Un jour plus tard, Okta publie un nouveau communiqué dans lequel ils expliquent avoir été victimes d'une attaque, mais que l'impact est faible : [Okta's Investigation of the January 2022 Compromise](https://www.okta.com/blog/2022/03/oktas-investigation-of-the-january-2022-compromise/).  

### Globant
>⚠️ Un lien est présent sur leur Telegram permettant de télécharger des données de Globant

La dernière revendication d'attaque a été faite le **30 mars** sur l'entreprise Globant, où **70 Go** de données ont été volées et publiées, ainsi que des accès sur GitHub, Jira, Crucible et Confluence.  
![Okta 2 Telegram](images/lapsus/telegram_globant.png)


Voici un récapitulatif des attaques menées par Lapsus$ provenant d’un rapport de Intrinsec :   
![Frise](images/lapsus/frise.png)

---

## Arrestations
Le 21 mars, le FBI publie un article afin de solliciter des informations sur le groupe LAPSUS$ en vue de les arrêter, suite à la fuite de données que l'entrepirse Microsoft a subie.
![Fbi](images/lapsus/fbi.png)

Deux jours après la publication du FBI, le 23 mars, le groupe annonce sur Telegram qu'il prend une semaine de vacances :  
![Telegram Vacation](images/lapsus/telegram_vacation.png)  
Cependant, cette information coincide avec un article de la BBC paru le **24 mars 2022** annonçant que 7 adolescents affiliés au groupe LAPSUS$ ayant entre 16 et 21 ans ont été arrêtés (dont White): https://www.bbc.com/news/technology-60864283 

Cependant, une semaine après, le **30 mars**, des messages ont été publié sur leur Telegram revendiquant l’attaque de Globant. Après cela, leur Telegram n’a plus été actif. 

La dernière apparition de LAPSUS$ a été avec le leak de GTA 6, en **septembre 2022**, cependant nous soupçonnons **White** d’avoir agit tout seul et non avec le groupe. De plus leur Telegram n’a pas revendiqué ce leak.

## Conclusion
En conclusion, nous avons observé que le groupe **LAPSUS$** a mené des attaques contre de nombreuses entreprises ainsi qu'une entité gouvernementale brésilienne. Leur approche repose souvent sur l'ingénierie sociale et le phishing, des méthodes qui ne nécessitent pas nécessairement des compétences techniques avancées. Les 0days sont rarement utilisés, privilégiant plutôt des méthodes visant à élever leurs privilèges après avoir obtenu un accès initial.

Nous avons également noté la rapidité d'action du groupe, ayant réussi en seulement 3 mois à compromettre et divulguer massivement des données d'entreprises telles que **Microsoft**, **Ubisoft** et **NVIDIA**.

Enfin, même après les arrestations et la dissolution du groupe, le fondateur de LAPSUS$, White, a réussi à faire fuiter une partie du code source de GTA 6. Cela remet en lumière le groupe, suscitant des inquiétudes quant à une éventuelle résurgence et la possibilité qu'il continue à semer la terreur pendant des mois.

## Sources
https://www.cisa.gov/sites/default/files/2023-08/CSRB_Lapsus%24_508c.pdf

https://www.intrinsec.com/analysis-of-lapsus-intrusion-set/

https://unit42.paloaltonetworks.com/lapsus-group/

https://www.theverge.com/22998479/lapsus-hacking-group-cyberattacks-news-updates

https://www.lemonde.fr/pixels/article/2023/12/22/lapsus-un-pirate-a-l-origine-du-hack-de-gta-vi-place-a-l-hopital-par-la-justice-britannique_6207274_4408996.html  

https://securityboulevard.com/2022/03/hackers-gaining-power-of-subpoena-via-fake-emergency-data-requests/ 

https://www.theverge.com/2022/3/23/22993731/lapsus-hacking-group-teenager-mastermind 

[L’étonnant profil du groupe cybercriminel LAPSUS$ - Next](https://next.ink/1973/letonnant-profil-groupe-cybercriminel-lapsus/) 

https://www.usine-digitale.fr/article/le-ministere-de-la-sante-bresilien-victime-d-une-cyberattaque-les-donnees-de-vaccination-ciblees.N1168357

https://revistaoeste.com/politica/grupo-hacker-invade-outros-sites-do-governo-federal-e-xinga-bolsonaro/ 

https://www.databreachtoday.asia/lapsus-attacks-localiza-redirects-users-to-porn-site-a-18286 

https://www.silentpush.com/blog/lapsus-group-an-emerging-dark-net-threat-actor/ 

https://www.intrinsec.com/wp-content/uploads/2022/03/INTRINSEC-LAPSUS-Intrusion-Set-20220324.pdf 

https://www.youtube.com/watch?v=tyg7fCPneWk 

https://www.wired.com/story/lapsus-hacking-group-extortion-nvidia-samsung/

https://www.databreaches.net/nvidia-breached-by-attackers-who-seem-shocked-by-hack-back/

https://twitter.com/vxunderground/status/1497484483494354946