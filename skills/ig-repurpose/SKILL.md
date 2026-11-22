---
name: ig-repurpose
description: >-
  Transformer un long contenu (vidéo YouTube, podcast, live, newsletter,
  article de blog, appel client) en une semaine de reels et de carrousels. À
  utiliser quand l'utilisateur dit « recycle ça », « transforme ça en reels »,
  « j'ai une vidéo / un podcast / une transcription », « découpe ça », ou colle
  quelque chose de long qu'il veut sur Instagram.
---

# ig-repurpose

Un bon contenu long contient quatre à six publications. La plupart des gens en
tirent une et jettent le reste.

## Entrée

Une transcription, un article, une newsletter, un script, un résumé d'appel, un
live. Si l'utilisateur donne une URL et que cette session a un outil de
transcription, utilise-le ; sinon demande-lui de coller le texte. Lis tout
avant d'extraire quoi que ce soit.

Si la source est une vidéo qui appartient à l'utilisateur, demande aussi le
fichier. Un Reel construit sur ses propres images bat un Reel où il relit ses
propres mots.

## Extraire, pas résumer

Le résumé d'une vidéo n'est pas un Reel. Personne ne veut le résumé. Parcours
le contenu et sors ce qui tient debout tout seul :

| à extraire | ce que c'est |
| --- | --- |
| **Affirmations** | chaque phrase qui lancerait un débat |
| **Chiffres** | chaque nombre, coût, durée, pourcentage |
| **Histoires** | chaque moment avec une personne, une scène et un coût |
| **Mécanismes** | chaque « en fait, ça marche comme ça… » |
| **Erreurs** | chaque aveu de quelque chose qui a mal tourné |
| **Phrases** | chaque phrase déjà citable telle quelle |

Liste ce que tu as trouvé, avec les comptes, avant d'écrire quoi que ce soit.
Si le contenu donne moins de quatre éléments, il est maigre, et quatre
publications tirées de là le seront aussi. Dis-le.

## Puis choisis le format par extrait

Tout n'est pas un Reel.

- **Affirmation, erreur, histoire** vers un Reel. Il leur faut une voix et un
  visage.
- **Mécanisme, liste numérotée** vers un carrousel. Il faut les relire.
- **Une phrase citable** vers une image de story, pas une publication.

## Puis construis la semaine

Chaque extrait devient une publication, et chaque publication tient debout
toute seule. Le spectateur n'a pas vu la source et ne la verra jamais. N'écris
jamais « comme je le disais dans ma dernière vidéo ». La publication est la
chose.

Attribue à chacune une formule d'accroche de `ig-reel/hooks.json` et varie-les.
Cinq publications tirées d'une source avec la même forme d'accroche, ça se lit
comme une usine à contenu, parce que c'en est une.

Si la source est la vidéo de l'utilisateur, **utilise les vraies images**. Le
passage où il dit la chose, avec la vraie réaction, bat une nouvelle prise à
chaque fois. Coupe sur la phrase, pas sur la respiration.

Ordonne la semaine pour que l'affirmation la plus forte passe en premier,
l'histoire au milieu de la semaine, et le mécanisme en dernier, quand ceux qui
ont aimé les précédents l'attendent.

## Sortie

```
SOURCE : « Pourquoi on a arrêté les fiches de révision » (podcast 42 min, 8 900 mots)

TROUVÉ  5 affirmations, 9 chiffres, 3 histoires, 4 mécanismes, 2 erreurs, 7 phrases citables

SEMAINE
MAR  REEL       #2  Ordre négatif       Arrête de recopier tes cours
                                        utiliser l'extrait à 14:20, elle rit à la fin
MER  CARROUSEL  légende Travail B       Les 4 questions qui remplacent la fiche
VEN  REEL       #21 Départ en pleine phrase « …et là, il a eu 16 au contrôle »
DIM  REEL       #5  Temps écrasé        Deux heures de révision gagnées par semaine

Dis « écris mardi » et je le rédige.
```

Puis rédige à la demande, une à la fois, chacune via `/ig-reel` et `/ig-human`.
Ne livre pas quatre scripts finis d'un coup. Ils sonneront tous pareil et
l'utilisateur n'en tournera aucun.
