---
name: ig-comment
description: >-
  Écrire des commentaires sous les publications et reels des autres qui se
  lisent comme ceux d'une personne avec un avis, pas d'un robot. À utiliser
  quand l'utilisateur colle une publication ou un reel et veut un commentaire,
  dit « commente ça », « interagis avec ça », « qu'est-ce que je dis ici », ou
  veut une série pour sa tournée d'interactions du jour.
---

# ig-comment

Commenter, ce sont les vingt minutes les plus rentables d'Instagram, et les plus
faciles à mal faire. Un commentaire en haut d'un reel à 40 000 vues est vu par
plus de monde que la plupart des publications d'un compte, et c'est le seul
endroit où un inconnu peut aller directement sur un profil d'un tap.

Un commentaire générique est pire que rien. Il coûte un tap qui ne mène nulle
part, et il range le compte parmi les comptes de « pods d'engagement » aux yeux
de la seule personne dont l'avis comptait : le créateur.

## Entrée

L'utilisateur colle le texte de la publication ou du reel, ou une capture, avec
le nom du compte. S'il donne une URL que tu ne peux pas ouvrir, demande-lui de
coller le contenu. N'utilise pas d'outil de navigation pour aspirer le fil et ne
publie rien.

## Les neuf types de commentaires

Choisis selon ce qu'est vraiment la publication. Ne prends jamais le type 1 par
défaut.

| # | type | quand | forme |
| --- | --- | --- | --- |
| 1 | **Ajouter une donnée** | la publication affirme quelque chose que tu peux appuyer d'un chiffre | « Pareil chez nous : 40 % des… » |
| 2 | **Ajouter le cas manquant** | la publication a raison mais elle est incomplète | « Vrai, jusqu'à ce que {condition}. » |
| 3 | **Désaccord respectueux** | tu penses vraiment que c'est faux | nomme d'abord l'accord, puis la bifurcation |
| 4 | **Prolonger une phrase** | une phrase dedans est la bonne | cite-la, construis dessus |
| 5 | **Poser la vraie question** | la publication a sauté la partie difficile | une question, précise |
| 6 | **Le vécu** | tu as fait ce qu'ils décrivent | ce qui s'est passé, en deux phrases |
| 7 | **La correction** | il y a une erreur factuelle | aie raison, sois bref, gentil et sûr |
| 8 | **Le recadrage** | bons faits, mauvais cadre | « Une autre façon de le lire : » |
| 9 | **La phrase unique** | la publication n'a besoin de rien, tu veux être présent | moins de 10 mots, drôle ou vrai |

## Règles

- **Une à trois phrases.** Les commentaires Instagram se lisent dans une
  colonne étroite sous une vidéo. Un paragraphe est replié derrière « plus » et
  personne ne tape dessus.
- **N'ouvre jamais par** « Super post », « J'adore », « Trop vrai », « Ça 👏 »,
  « J'avais besoin de lire ça », ou le prénom du créateur avec un point
  d'exclamation. Tous sont invisibles.
- **Pas de commentaire uniquement en émojis** et pas d'émoji en premier
  caractère.
- **Ne résume jamais le reel.** Tous ceux qui le lisent viennent de le
  regarder.
- **Une idée.** Un commentaire avec deux points ressemble à un détournement.
- **Dis la chose précise.** Si le commentaire pouvait aller sous n'importe
  quelle publication sur le sujet, ce n'est pas un commentaire, c'est du bruit.
- **Jamais de démarchage.** Ni l'offre, ni le lien, ni « va voir ma page ».
  C'est le moyen le plus rapide de se faire bloquer par la personne même qu'on
  voulait toucher.
- **Être tôt compte plus ici qu'ailleurs.** Un commentaire posté dans la
  première heure d'un reel qui décolle voyage avec lui.

## Sortie

Donne **deux options de types différents**, étiquetées, plus une ligne sur celle
que tu publierais et pourquoi. Passe les deux dans `/ig-human` d'abord : les
commentaires sont courts, donc un tiret cadratin ou une formule toute faite s'y
entend proportionnellement plus fort que dans une légende.

```
OPTIONS DE COMMENTAIRE  (sur le reel de @compte à propos des devoirs)

[6 · Le vécu]
Ma fille a arrêté de pleurer sur les fractions le jour où on les a coupées
en vraies parts de pizza. Trois semaines, et elle les explique à son frère.

[3 · Désaccord respectueux]
D'accord sur la régularité. Là où je ne te suis pas, c'est le chrono : chez
nous, minuter les exercices a fait monter le stress, pas les notes.

Publie le premier. Il a un détail vrai et un chiffre.
```

## Mode série

Pour une tournée d'interactions, demande les 5 à 10 publications en texte collé
dans un seul message, rends un commentaire pour chacune dans un seul bloc, et
tiens une note dans `~/.claude/instagram/log.md` des comptes commentés cette
semaine. Commenter les trois mêmes comptes tous les jours se voit, et ça
ressemble exactement à ce que c'est.

## Jamais

Ne publie pas automatiquement, n'automatise pas les commentaires, et n'utilise
pas d'outil de navigation pour publier à la place de l'utilisateur.
L'interaction automatisée viole les conditions d'utilisation d'Instagram et
fait bloquer les comptes. Ce skill écrit le commentaire. L'utilisateur le
publie.
