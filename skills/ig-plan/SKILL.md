---
name: ig-plan
description: >-
  Construire la semaine sur Instagram : quoi publier, sous quel format, quand,
  et avec qui interagir. À utiliser quand l'utilisateur dit « planifie ma
  semaine », « qu'est-ce que je publie », « calendrier de contenu », « je n'ai
  rien à publier », ou veut un planning de publication et une liste de comptes
  avec qui interagir.
---

# ig-plan

La salle de contrôle. Tout le reste du pack exécute ; celui-ci décide ce qui
est exécuté. Lance-le une fois par semaine, le même jour.

## Entrée

Si `~/.claude/instagram/voice.md`, `swipe.md` et `log.md` existent, lis-les.
Le swipe file est la preuve de l'utilisateur, tirée de `/ig-viral`, sur les
formules qui marchent dans sa niche en ce moment, et il passe avant tout ce qui
est dans ce fichier. Le journal évite que le plan répète un thème des deux
dernières semaines.

S'ils n'existent pas, demande quatre choses et note-les :

1. Ce que l'utilisateur vend, et à qui.
2. Les trois ou quatre thèmes pour lesquels il veut être connu.
3. Ce qui s'est réellement passé cette semaine : un appel client, un chiffre,
   une erreur, quelque chose qu'il a construit, un désaccord. C'est de là que
   viennent les publications.
4. Dix comptes auprès desquels il vaut la peine d'être visible.

## Quoi publier

Quatre à cinq publications par semaine, dont au moins trois Reels. Les Reels
sont le seul format d'Instagram qui atteint de façon fiable des gens qui ne
suivent pas le compte. Les carrousels approfondissent avec ceux qui suivent
déjà. Les stories sont quotidiennes et se planifient à part.

Mélange sur la semaine, jamais deux du même type à la suite :

| type | part | rôle |
| --- | --- | --- |
| **Preuve** | 1 par semaine | quelque chose qui s'est passé, avec un chiffre. Reel. |
| **Apprendre** | 1 à 2 par semaine | une chose que le spectateur peut faire aujourd'hui. Reel ou carrousel. |
| **Opinion** | 1 par semaine | une position qui pourrait te faire perdre des abonnés. Reel. |
| **Histoire** | 1 toutes les deux semaines | une scène qui a coûté quelque chose. Reel. |
| **Offre** | 1 toutes les deux semaines | ce que tu vends, dit simplement, sans t'excuser. Carrousel ou stories. |

Pour chaque créneau, donne : le thème, l'angle précis tiré de ce qui s'est
vraiment passé cette semaine, le format, et le numéro de formule d'accroche
dans `ig-reel/hooks.json`. Pas un sujet, un angle. « Les maths » n'est pas un
plan. « L'élève qui a compris les fractions avec une pizza en carton » est un
Reel.

## Quand publier

Publie quand le public de l'utilisateur est réveillé et pas au travail. Pour la
plupart des publics grand public, c'est en début de soirée heure locale ; pour
un public professionnel, tôt le matin. Pour des collégiens et lycéens : après
les cours (17 h-19 h) et le mercredi après-midi ; pour des parents, après le
dîner (20 h 30-21 h 30) ; pour des profs, le soir et le dimanche.

Mais dis-le clairement : **l'heure compte bien moins que les deux premières
secondes.** Instagram continue de montrer un Reel pendant des jours s'il
performe, et enterre un Reel bien minuté qui ne performe pas. Si l'utilisateur
optimise ses horaires avant que ses accroches marchent, il polit la mauvaise
chose, et tu dois le lui dire.

Cale les heures sur le fuseau du public, pas de l'utilisateur, s'ils diffèrent.

## La tournée d'interactions, qui n'est pas optionnelle

20 minutes par jour, avant de publier, pas après. Fais une liste de 10 :

- **5 portée** : des comptes avec le public que l'utilisateur veut, où un bon
  commentaire se voit. Commente tôt, avant que le fil ait 200 réponses.
- **3 pairs** : même taille, même domaine. C'est le groupe qui rend la pareille.
- **2 acheteurs** : des gens qui pourraient vraiment acheter. Commente pendant
  des semaines avant tout DM, et ne vends jamais dans un commentaire.

Passe la liste à `/ig-comment`.

## Sortie

```
SEMAINE DU 15 SEPT

LUN  interactions seulement  (20 min, liste ci-dessous)
MAR  19 h 30  REEL       PREUVE     #5  Temps écrasé       - devis de 5 h à 20 min
MER  stories seulement + interactions
JEU  19 h 00  CARROUSEL  APPRENDRE  légende Travail B      - la clause en 4 diapos
VEN  19 h 30  REEL       OPINION    #2  Ordre négatif      - arrête les appels découverte
SAM  -
DIM  18 h 00  REEL       HISTOIRE   #21 Départ en pleine phrase - le mail de remboursement

STORIES  tous les jours, 3 à 5 images, boîte à questions le jeudi.

INTERACTIONS  (5 portée / 3 pairs / 2 acheteurs)
  ...

Dis « écris mardi » et je le rédige.
```

Écris le plan dans `~/.claude/instagram/plan.md` pour que les autres skills
puissent le lire. Rien n'est programmé ni publié nulle part. C'est un plan, et
c'est l'utilisateur qui l'exécute.
