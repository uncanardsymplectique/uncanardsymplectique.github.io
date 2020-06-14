---
title: "Plus de mots, plus de nuages."
date: 2020-06-13
# last_modified_at: 2020-05-19T16:20:02-05:00
categories:
  - blog
  - (méta-)maths
  - projets python
tags:
  - arXiv
  - Géométrie symplectique
  - nuages de mots
excerpt: "Suite directe du précédent, de mon exploration des métadonnées d'articles publiés sur arXiv, et de mes errances dans WordCloud. Où l'on essaie de voir s'il est possible de faire dire quelque chose aux nuages de mots. Et à défaut, aux sucettes. "
# à retirer quand il y aura plus de page :
# permalink: /metamaths/
author_profile: true
layout: metamaths
classes: wide
annexe: "Galerie de l'évolution"
annexe_url: /annexes/2020-06-13-annexe-galerie-de-l-evolution
---



Depuis mon premier nuage de mots, j'ai pas mal lu à leur sujet et l'opinion qui se dégage très nettement de mes lectures peut être résumée en un

**Principe général :** Les nuages de mots _**ne sont pas**_ des outils d'analyse de textes. (Même s'ils _peuvent_ être esthétiques.)
{: .notice}

Les arguments principaux (compressés) sont les suivants.
+ Représenter l'importance d'un concept par l'_aire des mots_ utilisés pour l'exprimer est une erreur parce qu'en général l'aire d'un truc est difficile à appréhender à l'oeil nu et que, dans le cas des mots, le nombre de lettres de chacun va biaiser encore un peu plus la lecture puisqu'à importance égale un mot plus court sera plus large et vice versa.
+ Le contexte manque cruellement. Par exemple, dans les discours d'investiture respectifs d'Obama et de Trump, "America" est dans les trois mots pertinents les plus utilisés mais, de mon point de vue subjectif, ils n'ont pas le même sens quand ils sont remis dans le contexte (i.e. dans la bouche de chacun des deux présidents).

Ce second point est moins handicapant dans le cadre dans lequel je me place (titres et résumés d'articles de maths) surtout si l'on autorise les paires de mots successifs fréquentes, ce que j'arrive beaucoup mieux à faire depuis mon [chamadaire symplectique](/metamaths/2020-05-19-le-chameau-symplectique#finalement--créer-le-nuage-de-mots) qui lui n'en contenait pas. Il faut juste être un peu soigneux, puisque l'on trouve par exemple des "Witten invariants" qui sont en fait des "Gromov--Witten invariants", que l'on peut corriger de sorte que "Gromov--Witten" soit la paire retenue.

{% include figure image_path="/assets/images/metamaths/galerie_evolution/arXiv_SG_2019_All.png" alt="La sphère symplectique (2019)" width="200px" %}{: .align-right .width-third}
Le résultat est ci-contre.

**Remarque.** Un clic droit sur le dessin puis _ouvrir l'image dans un autre onglet_ vous le montrera en vraie grandeur i.e. en plus gros. Idem pour les gifs ci-dessous.
{: .notice--info .width-third}

J'ai retiré sciemment les mots mathématiquement et symplectiquement trop basiques ("manifold", "submanifold", "dimension", "symplectic", "$2n$", etc.). Il reste encore pas mal de travail pour parfaire le tout (il y a entre autres des "equivalent to" et des "equal to" qu'il faudrait éliminer) mais bon il fallait bien s'arrêter quelque part (j'ai un _vrai_ travail, je suis enseignant-à-distance--chercheur).

Bref. C'est joli mais reste le premier point... il n'est pas aisé par exemple d'ordonner "invariant", "Hamiltonian", "Lagrangian", et "Floer homology". Ceci tend à confirmer le **principe général** énoncé ci-dessus : il est assez _difficile_ de représenter des données dans les nuages de mots de manière réellement informative.

Comme difficile n'est pas impossible, je me suis dit qu'il fallait pousser un peu et qu'avec un petit effort ... on pouvait rendre la chose parfaitement impossible.

###### Du nuage à la capsule météo du journal de 20h
{% include figure image_path="/assets/images/metamaths/Everything.gif" alt="Les mots les plus utilisés (2002-2019)" width="200px" %}{: .align-right .width-third}

Par exemple, on peut produire des nuages de mots annuels -- mettons des 500 (paires de) mots les plus utilisés chaque année depuis 2002, année où le nombre d'articles publiés en `math.SG` a dépassé 200 --, que l'on peut ensuite assembler en un gif. Idéalement trop rapidement pour que l'on puisse lire quoique ce soit.
Réussi, non ?

**Remarque inconsciente.** Moi, ça m'évoque une animation satellitaire type capsule météo journal-de-20-heuresque. J'ai hésité à coller un mini Alain Gillot-Pétré à gauche expliquant que la dépression hamiltonienne était là pour durer... #3615Freud
{: .notice--danger}

Pour automatiser le processus, il est plus facile de créer les nuages de mots avec le même masque (ici une sphère, symplectique évidement) via un script sensiblement identique à celui utilisé pour le chamadaire et une simple boucle sur les années. Ensuite, on peut ajouter la date sur chaque image avec `ImageDraw` de la librairie `PIL`. Finalement, on réalise le gif avec la fonction `mimsave` de `imageio`.

En fait, suivre ces indications ne conduirait pas au résultat présenté. Le problème vient du fonctionnement par défaut de `WordCloud`.

###### "Quand même, c'est joli toutes ces couleurs." -- Un daltonien.

En fait, on ne comprend pas grand-chose sur le _comment_ de `WordCloud` en parcourant les docs qui ne sont, si je n'ai rien raté, qu'un ensemble d'exemples que je trouve (et là ce n'est que mon opinion) mal choisis. Le traitement des couleurs par défaut par exemple produit un résultat assez esthétique (toujours de mon point de vue de daltonien bien biaisé) mais selon un processus qui semble aléatoire. Faire ce que je décrivais ci-dessus produit donc une série de nuages dont les couleurs ne sont pas cohérentes d'une année à l'autre.

Heureusement, il y a un exemple dans la "doc" de `WordCloud` expliquant comment modifier les couleurs choisies par défaut, en invoquant la méthode `recolor` sur un objet `WordCloud`. Cette méthode mange une fonction couleur et recolorise _mot par mot_ le nuage engendré au préalable. Il suffit donc de produire une telle fonction couleur. Celle utilisée au-dessus ressemble à ça
```python
def recoloriage(word, font_size, position, orientation, random_state=None, **kwargs):
    couleur = fonction_ad-hoc(font_size)
    return f'hsl({couleur}, 95%, 40%)'
```
et retourne une couleur au format `hsl`: teinte (hue), saturation, luminosité ; la partie importante ici étant qu'elle choisit une couleur pour chaque mot (la variable `word`) en fonction de son "importance" dans le nuage, cette importance étant quantifiée par la taille de la police (la variable `font_size`) utilisée par `WordCloud` pour représenter le mot.

La `fonction_ad-hoc` elle-même n'a aucun intérêt même si j'ai passé quelques heures dessus (satanées couleurs !). En fait, choisir un certains nombres de règles pour que les différentes années soient comparables entre elles, tout en gardant un ensemble esthétique, sans trop perdre en lisibilité n'est pas chose aisée.
Pour cela, j'ai beaucoup appris sur la roue des couleurs et _la **B**onne_ façon de produire des couleurs foncées (augmenter la saturation, réduire la luminosité) grâce à [ce blog][couleurs] à ~~opinions colorées~~ couleurs opinionées. Et donc après quelques heures d'essais divers (une seule couleur et changement de tons, passage lent du vert au bleu, etc.) je me suis résigné un peu plus à privilégier l'esthétique sur la lisibilité (trois passages successifs à travers toute la roue des couleurs -- Blam !).


###### "Quand on élimine le hasard, on a plus de contrôle." --- Captain Obvious
Le gros avantage de contrôler la distribution des couleurs c'est que cela ouvre la porte à toute sorte de variations. Comme rendre quasi-invisibles certains mots.

{% include figure image_path="/assets/images/metamaths/New.gif" alt="Les nouveaux mots les plus utilisés" width="200px" %}{: .align-right .width-third}
Dans cet exemple, j'ai recolorié comme précédemment uniquement les 50 mots (ou paire de mots) les plus fréquents chaque année, s'ils n'avaient pas déjà fait le top 10 lors d'une année antérieure et j'ai quasi-invisibilisé les autres.

Oui mais euh... pourquoi ?

Parce que je peux. On réalise par exemple que l'expression "Gromov--Witten" entre dans le top 50 en 2005 et y reste jusqu'en 14 où elle fait le top 10 (yeah !) et disparaît donc ensuite. De même "Fukaya category" entre dans le top 50 en 2010 et dans le top 10 en 16. En 17, elle a disparu et apparaît alors un petit "wrapped Fukaya" des familles.

**Remarque orientée.** Au contraire, les expressions "Khovanov homology" et "Rabinowitz Floer" font le top 50 en 2009 et 2010 _respectivement_ et disparaissent dès l'année suivante sans être entrées dans le top 10. #HaBenÇaAlors
{: .notice--danger}



Pour faire ça, la difficulté provient encore du fait que je ne comprends rien à ce qui se passe dans l'algorithme qui engendre l'objet `WordCloud`. Je suis donc allé chercher les infos où je sais qu'elles apparaissent ... au moment du recoloriage des mots. (Je sais, c'est ignoble. Comment ai-je pu faire ça ?!)
```python
def recoloriage_funky(word, font_size, position, orientation,
                         random_state=None, **kwargs):
    global TOP10, RANG
    if (word not in TOP10) and (RANG < 50):
        luminosite = 40
	couleur = la_meme_fonction_ad-hoc(font_size)
        if RANG < 10: TOP10.append(word)
    else:
        luminosite, couleur = 97, 3
    RANG += 1
    return f"hsl({couleur}, 95%, {luminosite}%)" 
```

Les variables `TOP10` et `RANG` sont des variables globales (puisque j'ai besoin qu'elles sortent de la fonction) : `RANG` code la position du mot dans la liste des mots d'une année et `TOP10` construit au fur et à mesure la liste des mots apparus dans le top 10 du `WordCloud` années après années.

**Remarque auto-dérisionnelle.** La variable `RANG` permet _évidemment_ une meilleure quantification de l'importance d'un mot dans son `WordCloud` que le paramètre `font_size`. Il est donc clair que _si_ je n'étais pas fondamentalement fainéant, j'aurais modifié le code de ma `fonction_ad-hoc` initiale pour en tirer parti. Seulement voila... j'y ai pensé après et la condition précédente n'est pas vérifiée. #LeRangCEstImportant #PrivateJokeSorry
{: .notice--danger}

**Annexe.** Les deux séries d'images statiques utilisées pour les gifs sont visibles dans l'annexe que j'ai intitulée [galerie de l'évolution](/annexes/2020-06-13-annexe-galerie-de-l-evolution). #DoYouSeeWhatIDidThere?
{: .notice--info}


###### Un petit dernier pour la route...
{% include figure image_path="/assets/images/metamaths/Lagrangian_Legendrian.gif" alt="Comparaison " %}{: .align-right .width-third}

Bon évidemment, on peut décliner cela dans tous les sens mais je n'ai pas trouvé d'idée suffisamment intéressante pour pousser plus loin. Voici donc juste une dernière petite capsule météo montrant la prise d'importance années après années de la petite soeur de contact de la lagrangienne.

En fait, et à terme, j'espère pouvoir essayer l'[analyse de réseau de texte](https://infranodus.com/) qui semble un outil plus intéressant (et aussi très esthétique de mon point de vue) pour analyser des textes en gardant probablement partie du contexte. Mais ce sera pour plus tard donc, et avec une autre source de textes.

~~The end.~~

**Remarque intéressée (et politisée).** Du point de vue du mathématicien (ayant un boulot permanent dans une université française), il me semble que le contenu de cette page serait plus utile si les textes analysés étaient les textes des projets _financés_ par l'ANR et l'ERC puisque ces organismes sont en passe de devenir notre seule source de financement. Si quelqu'un a un outil permettant de concaténer efficacement ces textes, qu'il n'hésite pas à m'écrire.
#ViveLaLPPR #IlsOntToutCompris
{: .notice--danger}

The end.






[couleurs]: https://learnui.design/blog/the-hsb-color-system-practicioners-primer.html