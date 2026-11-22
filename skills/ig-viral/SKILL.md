---
name: ig-viral
description: >-
  Aller chercher les reels qui marchent vraiment en ce moment dans la niche de
  l'utilisateur, les classer selon à quel point chacun a dépassé son propre
  compte, nommer la formule d'accroche de chacun et en faire un fichier
  d'inspiration (swipe file) prêt à tourner. À utiliser quand l'utilisateur
  dit « trouve des vidéos virales », « qu'est-ce qui marche en ce moment »,
  « qu'est-ce que les gens postent dans ma niche », « décortique ce compte »,
  « fais-moi un swipe file », « pourquoi ce reel cartonne », ou demande quoi
  faire ensuite sans preuve pour y répondre.
---

# ig-viral

Le skill de recherche. Tous les autres écrivent ; celui-ci va regarder. Lance-le
une fois par mois, pas tous les jours. Les formules durent une saison.

Un outil est dans ce dossier et il tourne :

```bash
python3 swipe.py captured.tsv --out ~/.claude/instagram/swipe.md
```

Il reconnaît les accroches en français et en anglais. Ses messages sont en
anglais : traduis-les pour l'utilisateur.

## L'idée qui rend ce travail utile

**Les vues brutes ne sont pas une preuve.** Un compte de deux millions
d'abonnés qui fait 400 000 vues a eu un mardi tranquille. Un compte de quatre
mille abonnés qui fait 400 000 vues a trouvé quelque chose, et ce quelque chose
se copie.

Donc tout ici se classe sur le **multiple d'écart** : les vues divisées par la
médiane récente du compte lui-même. Au-dessus de 3x, c'est un signal. Sous
1,5x, c'est une journée normale pour ce compte et ça ne t'apprend rien, aussi
gros que paraisse le chiffre.

Choisis des comptes **à moins de 10x environ de la taille de l'utilisateur**.
Une formule qui marche à 2 M d'abonnés marche souvent parce qu'elle est à 2 M
d'abonnés.

## Étape 1 : choisir les comptes

Demande à l'utilisateur 6 à 12 comptes, ou propose-les et fais-les valider :

- **4 directs** : même niche, même offre, un peu en avance.
- **4 voisins** : autre niche, même public. C'est là qu'on emprunte des formats
  avant que quiconque dans la niche les ait.
- **2 à 4 géants** : des comptes bien plus gros, pour le format seulement,
  jamais pour le rythme ou le ton.

Demande-lui aussi d'ouvrir sa propre **collection Enregistrements**. C'est le
corpus le plus rapide et le plus pertinent qui existe, déjà filtré par ses
goûts.

## Étape 2 : aller regarder

Utilise l'outil de navigation dont cette session dispose vraiment : un
navigateur intégré, une extension reliée au Chrome de l'utilisateur, ou un
outil de contrôle de l'ordinateur. Il n'y a pas d'API pour ça et il n'en faut
pas, le volume est assez petit pour être lu.

**Règles non négociables :**

- **Ne te connecte jamais à Instagram à la place de l'utilisateur et ne demande
  jamais de mot de passe.** Si une page demande une connexion, c'est
  l'utilisateur qui est déjà connecté. Pilote son navigateur en sa présence, ou
  demande-lui de coller le contenu.
- **On lit, on n'aspire pas.** Dix comptes, une douzaine de reels chacun, à
  vitesse humaine. La collecte automatisée en volume viole les conditions
  d'utilisation d'Instagram et fait bloquer les comptes. Ne construis pas de
  robot d'exploration, n'utilise pas de service de scraping, et ne fais pas
  tourner ça en arrière-plan.
- **Copie la formule, jamais la vidéo.** La forme de l'accroche, la structure,
  la durée, le rythme des coupes. Pas leur script, pas leur voix, pas leur
  montage. Attribue chaque ligne du swipe file au compte d'où elle vient.

**Ce qu'il faut relever par reel**, dans les mots du créateur :

| champ | notes |
| --- | --- |
| account | le pseudo |
| followers | depuis le profil |
| median | regarde les 12 derniers reels et prends le nombre de vues du milieu |
| views | ce reel |
| hook | la première phrase, parlée ou à l'écran, mot pour mot, fautes comprises |
| on-screen | le premier carton de texte, s'il est différent |
| length | secondes |
| cta | ce qu'ils demandent à la fin |

La médiane est la plus importante. Sans elle, tu reviens à classer par nombre
d'abonnés, ce que ce skill existe justement pour empêcher.

**Quand Instagram ne montre pas assez :** la même grammaire d'accroche tourne
sur YouTube Shorts, où les vues et les transcriptions sont publiques et sans
connexion. C'est un second corpus légitime, et l'accroche parlée y est plus
facile à récupérer :

```bash
# nombre de vues des shorts d'une chaîne
python3 -m yt_dlp --flat-playlist --playlist-end 40 -J \
  "https://www.youtube.com/@PSEUDO/shorts" > channel.json

# la première phrase parlée d'un short, depuis les sous-titres auto
python3 -m yt_dlp --skip-download --write-auto-subs --sub-langs "fr.*" \
  --sub-format json3 -o hook "https://www.youtube.com/watch?v=ID_VIDEO"
```

Prends chaque mot des sous-titres horodaté avant 3,0 secondes. C'est
l'accroche, telle qu'elle est dite, pas telle qu'elle est écrite.

## Étape 3 : classer

Remplis un fichier séparé par des tabulations avec une ligne d'en-tête (garde
les noms de colonnes en anglais, le script les attend) et lance le script :

```
account	followers	median	views	hook
@quelquun	48000	11000	412000	personne ne te dit que tes 30 premiers reels sont censés faire un flop
```

```bash
python3 swipe.py captured.tsv --out ~/.claude/instagram/swipe.md
```

Il calcule le multiple d'écart, nomme la formule d'accroche avec les mêmes 26
formules que `/ig-reel`, note chaque accroche avec `hookscore.py`, et affiche
ce qui sépare le tiers du haut du tiers du bas.

## Étape 4 : dire ce que ça veut dire, prudemment

Rapporte trois choses, pas plus :

1. **Quelles formules sont sur-représentées** dans le tiers du haut, avec les
   comptes. Deux formules qui apparaissent quatre fois chacune sur six comptes,
   c'est un résultat. Une qui apparaît deux fois, non.
2. **Ce que le tiers du haut a en commun dans sa structure** et que le tiers du
   bas n'a pas : longueur de l'accroche, chute visuelle ou non, première image
   en mouvement ou non, place de la demande.
3. **Les lignes non classées.** Chaque accroche que le classeur n'a pas su
   nommer est soit du bruit, soit une formule qui n'est pas encore dans
   `hooks.json`. Lis-les à la main. C'est la colonne la plus précieuse de la
   sortie, et c'est pour ça que le script en affiche le nombre.

Puis donne la taille de l'échantillon et le niveau de confiance en mots
simples. Quarante reels sur six comptes soutiennent une affirmation. Douze,
non, et le dire fait la différence entre de la recherche et un horoscope.

## Étape 5 : en faire quelque chose à tourner

Pour les trois meilleures formules, écris **la version de l'utilisateur** : sa
propre histoire, son propre chiffre, dans la forme qui marche. Passe chacune à
`/ig-reel` avec l'identifiant de formule déjà choisi.

Ne rends jamais « fais un reel comme celui-là ». Rends une phrase d'accroche
qu'il pourrait dire demain.

## Sortie

```
SWIPE  ·  38 reels  ·  7 comptes  ·  référence : médiane du compte

ÉCARTS (au-dessus de 3x)
  38,4x  accroche 86  #3  Personne ne te dit   @compte_a   412 000  (médiane 10 700)
  11,2x  accroche 79  #9  Le vol               @compte_c   180 000  (médiane 16 100)
  ...

CE QUI EST SUR-REPRÉSENTÉ
  #3 Personne ne te dit   x5 dans le tiers du haut, 0 en bas
  #2 Ordre négatif        x4
  longueur médiane        8 mots en haut, 19 en bas

NON CLASSÉES (6)
  Deux d'entre elles ont la même forme et elle n'est pas dans hooks.json :
  une accroche qui commence par lire à voix haute le commentaire de
  quelqu'un. À ajouter.

TA VERSION
  #3  « Personne ne te dit que tes 20 premiers devis sont censés être perdus. »
  ...
```

Écris le swipe file dans `~/.claude/instagram/swipe.md`. `/ig-reel` et
`/ig-plan` le lisent tous les deux, et c'est tout l'intérêt : après un premier
passage, le reste du pack travaille sur les preuves de l'utilisateur plutôt que
sur des réglages par défaut.

Ce skill ne publie, ne suit, n'aime et n'envoie rien. Il lit.
