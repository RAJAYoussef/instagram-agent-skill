---
name: ig-audit
description: >-
  Bilan de ce que l'utilisateur a déjà publié : quels reels ont vraiment
  marché, pourquoi, et quoi arrêter. À utiliser quand l'utilisateur colle ses
  statistiques Instagram ou ses anciennes publications et demande « qu'est-ce
  qui marche », « pourquoi ça a fait un flop », « lis mes stats », « audite mon
  contenu », ou veut savoir quoi faire davantage.
---

# ig-audit

La seule source honnête de ce qui marche pour un compte, c'est ce compte. Chaque
règle de chaque guide Instagram, y compris celles de ce pack, est une
hypothèse de départ. Les 30 dernières publications de l'utilisateur sont la
preuve.

## Entrée

Demande ce que l'utilisateur a :

- Les statistiques par publication : vues, couverture, interactions, durée de
  visionnage, enregistrements, partages, abonnements, et la part de couverture
  hors abonnés. Les captures conviennent.
- Ou la courbe de rétention de ses meilleurs et pires reels récents. Cette
  seule capture vaut plus que tout le reste réuni.
- Ou juste les publications et leur nombre de vues, ce qui suffit pour un
  premier passage.

Lis aussi `~/.claude/instagram/log.md` s'il existe, puisqu'il note quelle
formule d'accroche chaque publication a utilisée.

## Ce qu'il faut vraiment mesurer

Les vues brutes sont le chiffre le moins utile de la page, parce qu'elles
dépendent surtout du nombre de gens qui suivent déjà le compte. Calcule plutôt
ceci et montre le calcul :

| indicateur | calcul | ce qu'il dit |
| --- | --- | --- |
| **Multiple d'écart** | vues / médiane des vues du compte | si c'était un vrai succès ou une journée normale |
| **Couverture hors abonnés** | % de la couverture venant de non-abonnés | si ça a voyagé tout court |
| **Rétention à 3 s** | spectateurs encore là à 3 s / spectateurs qui ont commencé | si l'accroche a marché. C'est la note de l'accroche. |
| **Durée moyenne de visionnage** | directement dans les stats | si le milieu a marché |
| **Envois par couverture** | partages / couverture | le signal le plus fort qu'on puisse obtenir. Un envoi, c'est quelqu'un qui engage son nom. |
| **Abonnements par couverture** | abonnements / couverture | si le profil a converti l'attention |

Classe par multiple d'écart et par envois par couverture, pas par vues. Un reel
à 4 000 vues et 90 envois a battu celui à 60 000 vues et 11 envois.

## Puis trouve le motif

Avec les cinq meilleurs et les cinq pires côte à côte, cherche ce qui les
sépare, et accepte de conclure quelque chose que l'utilisateur n'aimera pas :

- **Rétention à 3 secondes.** Si le haut et le bas diffèrent ici, c'est
  l'accroche et rien d'autre, et tout ce qui vient après est une distraction.
- **Formule d'accroche.** Quels identifiants de `ig-reel/hooks.json` sont dans
  le top cinq ?
- **Format.** Reel, carrousel, image seule.
- **Durée.** Groupe en moins de 15 s, 15 à 30 s, 30 à 60 s, plus de 60 s.
- **Thème.**
- **Si l'utilisateur a répondu aux commentaires dans la première heure.**
- **Jour et heure.** Vérifie ça **en dernier**, et seulement si le reste ne
  montre rien. Ce n'est presque jamais la cause, et c'est là que les gens
  voudraient qu'elle soit.

Énonce le résultat comme une affirmation avec la preuve jointe, et dis à quel
point tu en es sûr. Avec 30 publications, on voit un motif. Avec 6, non, et le
dire vaut mieux qu'en inventer un.

## La distinction qui fait gagner des mois

**Un reel qui fait des vues mais aucun abonnement n'est pas un reel raté, c'est
un problème de profil.** Un reel qui ne fait pas de vues est un problème
d'accroche. Sépare les deux avant de recommander quoi que ce soit. Si la
couverture hors abonnés est haute et les abonnements par couverture bas, arrête
de réécrire les accroches et passe à `/ig-profile`.

## Sortie

```
AUDIT  ·  31 publications  ·  12 juin - 5 sept  ·  médiane 4 100 vues

TOP 5 PAR MULTIPLE D'ÉCART
  18,2x  #3  Personne ne te dit   74 600 vues  62 % hors abonnés  rét.3s 71 %  128 envois
   6,4x  #1  Confession du coût   26 300 vues  48 % hors abonnés  rét.3s 64 %   71 envois
  ...

BAS 5
   0,3x  #11 Liste avec favori     1 200 vues   9 % hors abonnés  rét.3s 31 %    2 envois
  ...

CE QUE DISENT LES DONNÉES
1. La rétention à 3 secondes explique tout. Le top cinq est à 66 % en
   moyenne, le bas cinq à 33 %. Tout ce qui t'inquiète d'autre dépend des deux
   premières secondes.
2. Les publications où c'est toi qui avais tort : 8,1x en moyenne contre 0,9x
   pour le reste. n=5. Le signal le plus fort ici, et de loin.
3. Les listes d'outils font des vues et rien d'autre. Grande couverture, pas
   d'envois, pas d'abonnements. Trois de tes cinq pires.
4. Le jour de la semaine ne montre rien. Tes moyennes du mardi et du vendredi
   sont dans le bruit. Arrête de l'optimiser.

ARRÊTE : les listes.
FAIS PLUS : celles avec un coût que tu as payé et un chiffre à l'appui.
```

Puis passe les conclusions à `/ig-plan` pour que la semaine suivante repose sur
les preuves de l'utilisateur plutôt que sur des réglages par défaut, et à
`/ig-viral` pour que le swipe file soit filtré sur les formules qui marchent
pour ce compte précisément.
