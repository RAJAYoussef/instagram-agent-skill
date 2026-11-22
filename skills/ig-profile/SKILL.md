---
name: ig-profile
description: >-
  Noter un profil Instagram sur 100 selon une grille en 12 points et réécrire
  ce qui fait perdre des points : champ nom, bio, lien, stories à la une, les
  trois épinglés, la grille. À utiliser quand l'utilisateur dit « optimise mon
  profil », « corrige ma bio », « note mon Instagram », « pourquoi les gens ne
  s'abonnent pas », ou colle son profil et demande ce que ça donne.
---

# ig-profile

Presque tout le monde optimise la mauvaise chose ici. Le profil n'est pas une
vitrine qu'on parcourt. C'est un **écran de décision**, atteint depuis un seul
reel, et il a environ trois secondes pour répondre à une question : est-ce
qu'il y en a d'autres comme ça ici, et est-ce que c'est pour moi.

## Entrée

Demande à l'utilisateur de coller ou de faire une capture de : le champ nom,
le pseudo, la bio, la destination du lien, les noms des stories à la une, ce
qui est épinglé, et les neuf premières couvertures de la grille. Une capture
du haut du profil plus les deux premières rangées de la grille suffit pour un
premier passage.

Ne te connecte pas à Instagram à sa place.

## La note

Lis `rubric.json` dans ce dossier (en anglais : traduis en notant). Douze
critères, 100 points, chacun avec ce qu'est la note maximale et comment il
échoue d'habitude. Note chaque critère, montre le tableau, donne le total. Sois
honnête. La plupart des profils tombent entre 30 et 49 au premier passage, et
une note généreuse ne sert à rien.

```
NOTE DU PROFIL  38/100

  champ nom          2/12   juste le prénom, aucun mot que quelqu'un recherche
  bio, ligne 1       3/12   trois noms communs et un émoji café
  les trois épinglés 0/10   rien d'épinglé
  à la une           2/8    « Divers », « Vie », « 2023 »
  lisibilité grille  4/8    six couvertures sur neuf : un visage en pleine phrase
  ...
```

## Puis réécris, dans cet ordre

Corrige par ordre décroissant de points perdus. Ne réécris pas tout d'un coup,
l'utilisateur doit vraiment aller changer chacun de ces éléments.

**1. Le champ nom (30 caractères).** La ligne en gras sous la photo, pas le
pseudo. C'est le champ que la recherche Instagram compare, et la plupart des
comptes y mettent un nom et rien d'autre. Format qui marche :
`{Nom} | {ce que tu fais, avec les mots recherchés}`. Donne trois options.

**2. La première ligne de bio.** Pour qui c'est et ce qui change. Pas un
intitulé de poste, pas des adjectifs, pas une liste d'identités séparées par
des barres. Le reste des 150 caractères porte une preuve ou une offre simple.

**3. Les trois épinglés.** Trois emplacements, trois rôles : la meilleure
preuve, l'explication la plus claire de l'offre, la meilleure présentation de
la personne. C'est la correction la plus rentable de tout le profil et elle
prend quatre taps. Une grille sans épinglé montre la dernière publication, ce
qui revient à jouer à pile ou face.

**4. Les stories à la une.** Quatre à six, nommées d'après les questions que
pose un acheteur : Prix, Résultats, Comment ça marche, Qui suis-je. Pas
« Divers ». Supprime le reste.

**5. Le lien.** Une destination qui correspond à ce que la bio vient de
promettre. Cinq sont autorisés ; deux, c'est déjà un menu, et un menu convertit
moins bien qu'une porte.

**6. Les couvertures de la grille.** Les neuf premières en miniature. Les
couvertures de reels se choisissent, on ne laisse pas la première image par
défaut. Quatre mots de texte sur une couverture rendent la grille lisible en un
coup d'œil.

## Sortie

Le tableau des notes, puis les réécritures en blocs prêts à copier dans l'ordre
des corrections, chacune passée dans `/ig-human`. Renote à la fin et montre
l'écart honnêtement. Si la réécriture atteint 84 et pas 98, dis 84, et dis ce
qu'il manque, qui est en général une grille, une habitude de stories et une
publication épinglée qui n'existe pas encore. Rien de tout ça n'est une
réécriture.

Ce skill n'enregistre rien sur Instagram. L'utilisateur modifie chaque champ.
