---
title: "Des chiffres, des graphes, un camembert et une boîte à moustache."
date: 2020-06-14
# last_modified_at: 2020-05-19T16:20:02-05:00
categories:
  - blog
  - (méta-)maths
  - projets python
tags:
  - arXiv
  - Géométrie symplectique
excerpt: "Où l'on essaie finalement (!) de faire dire quelque chose d'informatif aux métadonnées extraites d'arXiv."
author_profile: true
layout: metamaths
classes: wide
annexe: "math.SG is a real category (or not)"
annexe_url: /(méta-)maths/blog/humour/english/SG-is-a-category/
---

Après deux épisodes nuageux, et pour éviter la dépression du même adjectif, je propose d'autres graphes, plus informatifs concernant les métadonnées des articles d'arXiv en `math.SG` ou en référence croisée (cross-listed).

Promis, après je passe à autre chose.

![dépôts cumulés 1997-2020](/assets/images/metamaths/depots_cumules.png){: .align-right}
###### De plus en plus de prépublications

Le nombre total de prépublications déposées sur arXiv ayant `math.SG` comme catégorie primaire _ou_ secondaire a passé les 7 000 cette année. Curieusement (?), la proportion de prépublications en `math.SG` (primaire) est sensiblement équivalente à la proportion d'articles en référence croisée (secondaire), même si cette dernière diminue sans discontinuer depuis fin 2007.

Au 30 avril 2019 il y avait donc 3 659 articles en `math.SG` (+ 20 articles mensuels en moyenne tous les mois depuis 2013 -- voir le graphe ci-dessous). Pour comparaison, la catégorie `math` toute entière est constituée de 32 sous-catégories et a connu 3 269 dépôts pour le seul mois d'avril 2019. L'inégalité (très) stricte $32 \times 20 < 3 \ 269$, démontre donc :

**Proposition.** La catégorie `math.SG` n'est pas la sous-catégorie de `math` où l'on publie le plus... #HaBenÇaAlors #CestPasLaTailleQuiCompte
{: .notice--danger}

La moyenne annuelle du nombre de prépublications déposées mensuellement n'a cessé quant à lui d'augmenter depuis la création d'arXiv pour atteindre 38 en 2019. Le maximum global du nombre d'articles déposés mensuellement est de 63 et a été atteint en octobre 2019.

![dépôts mensuels 1997-2020](/assets/images/metamaths/depots_mensuels.png)

Notons que la proposition précédente serait toujours vraie, même avec un nombre de nouvelles prépublications de 63 par mois... (On se rapproche du cas d'égalité cela dit -- 102 !?)

Si l'on change de point de vue et que l'on considère plutôt la répartition _mensuelle_ des dépôts d'une année type (moyenne sur plusieurs années des dépôts du mois de janvier par exemple), il se dégage plusieurs changements saisonniers très clairs.
- _Un minimum global en août_. Mois pendant lequel l'enseignant-chercheur se repose, cherche et dort beaucoup mais n'écrit pas tandis que l'intermittent de la recherche fait ses cartons, déménage, s'adapte à une nouvelle ville, un nouveau pays. Il fait aussi pas mal de démarches administratives et dort s'il reste du temps. 
- _Un maximum global en octobre_. Mois pendant lequel l'enseignant-chercheur se remet de la course de la rentrée et peut finalement se permettre de finir d'écrire ce qu'il avait trouvé en août. Pendant ce temps, l'intermittent de la recherche peaufine son dossier pour décrocher un poste plus ou moins temporaire ailleurs pour l'année suivante : il se dépèche donc de mettre ses prépublications sur arXiv...

Ces changements saisonniers (et d'autres, pas nécessairement clairs) ne sont pas propres à `math.SG` et me semblent suffisamment intéressants pour faire l'objet d'une prochaine errance, prenant en compte tous les sous-domaines de `math`.

[//]: # (###### Répartition annuelle des prépublications)
[//]: # (![repartition mensuelle](/assets/images/metamaths/repartition_mensuelle.png))

###### Catégorie primaire vs catégories secondaires
L'ensemble des [catégories d'arXiv](https://arxiv.org/) présente quelques subtilités. D'abord `physics` est la seule discipline qui semble désigner une _sur_-catégorie dont fait partie la catégorie `physics` (elle-même contenant une tripotée de sous-catégories).

Ensuite, il existe des _alias_.

**Exemple.** La dénomination `math.MP` est en fait un alias pour `math-ph` (mathematical physics). Ça permet à cette catégorie cavalière (à tout le moins, "à cheval") de ne faire peur ni aux mathématiciens, ni aux physiciens... #Sneaky
{: .notice--danger}

![catégories primaires et secondaires](/assets/images/metamaths/all_categories.png){: .align-left}
Pour illustrer les liens entre `math.SG` et les autres catégories, on a représenté en bleu le nombre d'articles publiés dans une catégorie `cat` (e.g. `math.DG`) ayant `math.SG` comme catégorie secondaire et en vert le nombre d'articles publiés en `math.SG` ayant `cat` comme catégorie secondaire (dès que l'un de ces deux nombres valait au moins 15).
Par souci de lisibilité, on a supprimé le préfixe `math.` des sous-catégories de `math`.

Une remarque liminaire concernant le fait qu'il y ait "si peu" de catégories secondaires (la somme des catégories secondaires représentées en vert est de 2 834). Ceci vient en grande partie de la façon dont j'ai traité les données initiales. En effet, je n'ai conservé que les catégories spécifiques d'arXiv alors que les catégories listées viennent sous formes et nomenclatures diverses et variées.

En voici deux exemples typiques. La liste interminable de codes venant de la [classification des sujets mathématiques](https://mathscinet.ams.org/msc/pdfs/classifications2010.pdf) de MathSciNet :
```
math.DG; math-ph; math.AG; math.MP; math.SG;
14L24 14L30 17B63 17B65 17B66 17B81 17C36 17C37 17C40 17C70
32C20 32Q15 32S05 32S60 53D17 53D20 53D30 53D50 81S10
```

et si (comme moi) vous avez déjà dû fouiller la classification MathSciNet à la recherche d'une catégorie à indiquer dans les métadonnées d'un de vos articles, vous comprenez pourquoi j'hésite à me lancer dans l'analyse de cette partie des données... (Sinon, je ne saurais trop vous encourager à cliquer sur le lien ci-dessus et vous rendre compte par vous-même.)

La liste brutale de mots-clés :
```
math.RT; math-ph; math.AG; math.CT; math.GR; math.MP; math.NT; math.QA; math.SG; quant-ph;
Weil representation, chracteristic two, bigger group, canonical model
```

et là... c'est pire. Non seulement toute combinaison de mots existants peut devenir un mot-clé ("bigger group". Sérieusement ?!) mais apparemment les mots qui n'existent pas aussi ("chracteristic". Rien de moins.).

Bref. J'en suis resté aux sous-catégories d'arXiv et ça m'a déjà évoqué plusieurs observations / questions que je liste en partie ci-dessous et qui sont illustrées avec l'humour qui me caractérise dans [ce post]({% post_url 2020-06-03-SG-is-a-category %}).

+ `SG` est-elle une sous-catégorie de `math` (ou de `math.DG`) ?

Y a-t-il beaucoup d'articles de `SG` qui ne peuvent pas être considérés comme des articles de `DG` ?
Pourquoi un géomètre kählerien publie-t-il en `DG` quand un symplecticien publie en `SG` ? 

+ La physique ça existe. Et elle a encore des liens avec la géométrie symplectique. (Au moins _théoriquement_.)

Avant que je ne réalise que `math.MP` sert en fait d'alias à `math-ph`, je trouvais surprenant et très très suspect le fait que tant d'articles de `math-ph` citent `math.SG` en référence croisée alors qu'aucun article de `math.SG` n'indiquait `math-ph` en catégorie secondaire.
Maintenant que je suis rassuré concernant la Physique mathématique, je me demande si quelque chose de ce genre est aussi à l'origine du phénomène équivalent pour les catégories `hep-th` (High Energy Physics - Theory) et `quant-ph` (Quantum Physics) qui n'ont cependant pas d'alias.

+ Est-ce que mon collègue dynamicien a raison quand il affirme :

> Votre dynamique hamiltonienne, ce n'est pas de la dynamique hamiltonienne.

Sachant que je le soupçonne d'ajouter le second "hamiltonienne" pour ne pas trop me vexer.

+ Que sont les [Sciences non-linéaires](https://arxiv.org/archive/nlin) ?!

Et surtout : que sont les "Sciences linéaires" dans ce cas...


###### Nombres d'auteurs et de versions
![stats d'auteurs et de versionsprépublications retirées](/assets/images/metamaths/auteurs_versions.png){: .align-left}

Pour terminer avec les données "objectives", il est complètement futile de remarquer que le nombre d'articles déposés sur arXiv ayant $n$ auteurs est très similaire au nombre d'articles déposés en $n$ versions. Et ce, que l'on compare les articles spécifiquement déposés en `math.SG` ou ceux indiquant `math.SG` en catégorie primaire ou secondaire.

Sans être digne du site [Spurious correlations](http://www.tylervigen.com/spurious-correlations) (à éplucher !) ... on en vient quand même à s'interroger tel Mr Cyclopède :
> Étonnant, non ?



###### Fromage et ~~dessert~~ moustache

![le fromage (prépublications retirées) title="le fromage (prépublications retirées)"](/assets/images/metamaths/papiers_retires.png){: .align-right}
Pour boucler et finir avec quelque chose de mignon mais au contenu informatif très contestable, voici les raisons du retrait des 66 prépublications qui mentionnent le mot "withdrawn" (retiré) dans leur résumé ou le champ de commentaires (dont 43 pour lesquelles SG est la catégorie primaire).

Moi je trouve ça plutôt rassurant une quarantaine (34+3+3) de papiers _à retirer_ sur 7000+ articles, même si (encore une fois) ça ne dit pas grand-chose : qui n'a pas rencontré un papier qui ne devrait pas être là mais qui y est quand même, l'air de rien, sans mention particulière de sa dangerosité ?

Quarante articles donc, mentionnés comme "retirés". Je me suis demandé comment représenter les durées entre la date de dépôt sur l'archive et celle de "retrait" de l'article et je n'ai pas pu résister au plaisir de réaliser ma première [boîte à moustache](https://en.wikipedia.org/wiki/Box_plot) (l'article [en français](https://fr.wikipedia.org/wiki/Bo%C3%AEte_%C3%A0_moustaches) est beaucoup moins complet) avec Python :
![boite à moustache](/assets/images/metamaths/boite_a_moustache.png)

J'avoue que depuis que j'ai (appris et) enseigné ça à de très probablement futurs professeurs des écoles cette année j'ai un petit faible pour ce type de représentation de données.

**Fun fact.** Les trois articles représentés par les + à droite ont été retirés après une durée _aberrante_. (Ce n'est pas mon opinion, c'est [une définition](https://fr.wikipedia.org/wiki/Donn%C3%A9e_aberrante).) #ViveLaScience
{: .notice--danger}

The end.