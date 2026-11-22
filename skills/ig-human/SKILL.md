---
name: ig-human
description: >-
  Retirer l'empreinte machine de n'importe quel brouillon (tirets cadratins,
  mots creux typiques de l'IA, caractères invisibles de filigrane) et le noter
  sur un panel de cinq contrôles avant publication. À utiliser dès qu'un texte
  doit sonner humain, quand l'utilisateur dit « humanise », « est-ce que ça
  fait IA », « enlève les tirets », « ça sonne ChatGPT », ou avant de montrer
  à l'utilisateur toute légende, tout script, commentaire, réponse ou DM.
---

# ig-human

Deux outils sont dans ce dossier et ils tournent vraiment. Utilise-les. Ne fais
pas ça à l'œil.

```bash
python3 humanize.py brouillon.txt --report       # nettoyer, montrer les changements
python3 detect.py brouillon.txt                   # noter, cinq contrôles
python3 detect.py avant.txt apres.txt             # prouver l'écart
```

Les deux lisent `slop.json` : des mots et expressions toutes faites en anglais
et en français avec leurs remplacements simples, 18 classes de caractères
invisibles, 11 substitutions typographiques et des tics de structure. Le
dernier bloc de chaque liste est propre à Instagram, le vocabulaire qu'on ne
trouve que dans les légendes et les voix off. Le fichier est fait pour être
modifié. Si l'utilisateur emploie toujours un mot que le lexique retire,
enlève-le du fichier.

Les messages des outils sont en anglais : traduis-les pour l'utilisateur.

## Pourquoi c'est plus important sur Instagram qu'il n'y paraît

Les légendes sont courtes et les scripts se disent à voix haute. Une phrase qui
sonne écrite pèse plus lourd dans une légende de 600 caractères que la même
phrase dans un long article, et une voix off que personne ne pourrait dire
naturellement s'entend dès la première prise. Le problème n'est pas un
détecteur qui signale la publication. Le problème, c'est quelqu'un qui fait
défiler un texte qui sonne comme une marque, ou un créateur qui bute sur son
propre script.

## Ce qui est corrigé automatiquement

**1. Les caractères invisibles.** Espaces et liants de largeur nulle,
séparateurs de mots, traits d'union conditionnels, indicateurs d'ordre des
octets, caractères Unicode d'étiquette, séparateurs invisibles, espaces
insécables et fines. Un clavier ne produit pas ça. Ils survivent au
copier-coller, sont invisibles dans tous les éditeurs, et sont la chose la plus
mécanique d'un texte généré. `humanize.py` les supprime tous, y compris tout
caractère de format Unicode qu'il ne sait pas nommer.

Attention, en français : l'espace insécable avant « : ; ! ? » et dans
« 18 000 € » est de la typographie normale. L'outil la remplace par une espace
simple, ce qui reste correct sur Instagram.

**2. La typographie.** Tiret cadratin en virgule, tiret demi-cadratin en trait
d'union, guillemets courbes en droits, points de suspension en trois points,
puces en tirets. Le passage sur le tiret cadratin est celui qui compte : il
remplace le tiret par une virgule puis nettoie la double ponctuation et les
points orphelins qui restent.

**3. Le lexique creux.** En anglais : delve, leverage, robust, seamless… En
français : « plonger dans », « dans un monde en constante évolution »,
« véritable game changer », « il est essentiel de », « en somme »… plus le bloc Instagram : « arrête de scroller », « dans la vidéo
d'aujourd'hui », « abonne-toi pour plus de contenu », « identifie quelqu'un qui
a besoin de ça », « l'algorithme adore ». Chacun est remplacé par un mot simple
ou supprimé, en gardant les majuscules et sans toucher aux URL.

## Ce qui n'est PAS corrigé automatiquement

Les tics de structure sont **signalés, pas réécrits**, parce que changer la
forme d'une phrase demande du jugement :

- « Ce n'est pas juste X, c'est Y » et « non seulement X mais aussi Y »
- Les triades en série de trois
- Les questions rhétoriques d'un mot : « Le résultat ? »
- Le préambule vidéo : « dans cette vidéo je vais vous montrer »
- Les listes à puces en émojis
- Trois mots en majuscules ou plus à la suite
- Les murs de hashtags
- Les appâts réflexes : « abonne-toi pour plus », « identifie quelqu'un qui »,
  « double tap si »
- « N'hésite pas à… » (le supprimer casserait la phrase : réécris-la en ordre
  direct)

Chaque texte est d'abord identifié comme français ou anglais, et seul le
lexique de sa langue s'applique : une légende française ne reçoit jamais de
remplacement en anglais.

Cette liste, c'est ton travail. Réécris chaque ligne signalée à la main en
gardant le sens, puis relance `detect.py`. C'est ce qui fait passer la note de
REVIEW à PASS, et c'est ce qu'un script ne peut pas faire.

## Les cinq contrôles

`detect.py` note cinq signaux de 0 à 100, plus c'est haut plus c'est humain :

| contrôle | ce qu'il mesure | à quoi ressemble la machine |
| --- | --- | --- |
| BURSTINESS | variation de longueur des phrases | toutes les phrases font la même longueur |
| SPECIFICITY | chiffres, noms, repères concrets pour 100 mots | noms abstraits, aucun chiffre |
| SLOP DENSITY | occurrences du lexique pour 100 mots | vocabulaire tout fait |
| FINGERPRINT | caractères invisibles, tirets cadratins, guillemets courbes pour 1 000 caractères | typographie parfaite |
| VOICE | élisions orales, personne, tics de structure | aucune forme orale, révélations mises en scène |

Le verdict pondère la moyenne à 60 % et le **contrôle le plus faible** à 40 %,
parce qu'un seul signal suffit. PASS exige un total de 70 ou plus sans aucun
contrôle sous 55.

## Dis-le honnêtement

Ce sont cinq heuristiques locales calquées sur les signaux qu'utilisent les
détecteurs publics. Elles tournent entièrement sur la machine de
l'utilisateur et rien n'est envoyé. Ce ne sont **pas** GPTZero, Originality,
Copyleaks, Winston ou Turnitin, elles n'appellent pas leurs API, et elles ne
peuvent pas promettre leurs verdicts. Corriger ce qu'elles mesurent fait en
général bouger ces chiffres-là, parce qu'elles mesurent les mêmes choses de
fond. C'est tout ce qu'on peut affirmer. Ne promets rien de plus au nom de
l'utilisateur, et ne lui dis jamais que son texte est indétectable.

## Ordre des opérations

1. `humanize.py brouillon.txt -o propre.txt --report`
2. Lis les signalements de structure. Réécris ces lignes toi-même.
3. `detect.py brouillon.txt propre.txt` pour montrer l'avant et l'après.
4. Si le verdict n'est pas PASS, corrige le contrôle le plus faible indiqué
   dans la sortie et recommence. Deux tours, c'est normal. Cinq, ça veut dire
   que le brouillon a été écrit à la chaîne, et la solution est un autre
   brouillon, pas plus de passages.
5. Montre à l'utilisateur le texte nettoyé et la note. Jamais la note seule.
