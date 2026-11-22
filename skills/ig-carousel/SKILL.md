---
name: ig-carousel
description: >-
  Construire un carrousel Instagram : la couverture qui donne envie de
  swiper, le texte diapo par diapo, et les fichiers 1080x1350 à publier. À
  utiliser quand l'utilisateur dit « carrousel », « diapos », « post à
  swiper », « transforme ça en carrousel », ou a une idée en liste ou en
  étapes qui mourrait en image seule.
---

# ig-carousel

Les carrousels sont le format où l'on reste le plus longtemps sur la grille,
parce qu'un swipe est une interaction et qu'un défilement n'en est pas une. Ils
ont aussi une seconde chance : Instagram peut remontrer un carrousel en
commençant par une diapo plus loin à quelqu'un qui n'a pas réagi la première
fois, donc la diapo deux doit aussi tenir debout toute seule.

Le format récompense une idée découpée en étapes. Il punit une légende coupée
en morceaux.

## Quand l'utiliser plutôt qu'un Reel

Utilise un carrousel quand l'idée a **une suite et doit être relue** : des
étapes, une méthode en plusieurs parties, un avant/après, une liste qui mérite
une capture d'écran. Utilise un Reel quand l'idée a du mouvement, un visage, ou
une chute qu'il faut voir se produire.

Si l'idée tient en une affirmation, ce n'est ni l'un ni l'autre. Passe-la à
`/ig-reel` et dis-le.

## Structure

6 à 10 diapos. Le maximum est 20, et 20, c'est presque toujours un livre que
personne ne finit. Sous 5, le swipe ne démarre jamais.

```
1         COUVERTURE  l'accroche. 6 mots maximum, lisible dans la grille en
                      miniature. Une ligne de promesse en dessous.
2         L'ENJEU     pourquoi ça compte, en une phrase. Cette diapo est aussi
                      une seconde couverture, elle ne peut pas être une mise en
                      place.
3 à N     UNE IDÉE PAR DIAPO. Un titre de 3 à 7 mots, au plus 25 mots en
                      dessous. Si une diapo demande un paragraphe, c'est deux
                      diapos.
N+1       RÉCAP       le tout sous forme de liste. C'est la diapo qu'on capture.
DERNIÈRE  APPEL       une action. Enregistrer, commenter un mot-clé, ou
                      s'abonner. Une.
```

## Règles du texte

- **La couverture fait 80 % du résultat.** Six mots. En grand. Rien dans le
  carrousel ne sauve une couverture que personne ne swipe.
- **Pense au recadrage de la grille.** La grille du profil recadre en rectangle
  portrait plus haut que large, et le ratio exact a déjà changé plusieurs fois.
  Construis en 1080x1350 et garde le texte de couverture bien au centre, loin
  des 120 pixels extérieurs de chaque côté, et le recadrage n'a plus
  d'importance.
- **Numérote les diapos** (3/8). On va plus souvent au bout quand on voit la
  fin.
- **Aucune diapo n'est un paragraphe.** Si ça ne se dit pas en 25 mots, coupe.
- **La diapo récap est celle qu'on capture et qu'on envoie.** Les envois sont le
  signal le plus fort qu'on puisse obtenir. Rends-la autonome et lisible sans
  contexte.
- **Le pseudo sur chaque diapo**, petit, dans un coin en bas. Les captures
  voyagent sans toi.
- **Texte alternatif au moins sur la couverture.** Il est lu par les lecteurs
  d'écran et par Instagram.

## Fabriquer les fichiers

Instagram veut du 1080x1350 (4:5), JPEG ou PNG, jusqu'à 20 éléments.
Construis-le en HTML et imprime chaque diapo :

```bash
# une <section> par diapo, 1080x1350, page-break-after: always
# puis Chrome headless --print-to-pdf, ou n'importe quel outil HTML vers image
```

Écris le HTML avec `width:1080px; height:1350px`, une seule couleur d'accent,
et un texte jamais plus petit que 32px, parce qu'il est lu sur un téléphone au
tiers de sa taille réelle. Si le projet a une charte ou un design system,
utilise-le et n'invente pas de palette.

## Sortie

D'abord le texte diapo par diapo, en liste numérotée que l'utilisateur peut lire
en dix secondes et corriger avant tout rendu. Puis la **légende**, qui pour un
carrousel est le Travail B de `/ig-caption` : la légende travaille ici, parce
que la couverture a déjà utilisé ses six mots.

Passe les deux dans `/ig-human`. Ne fabrique les fichiers qu'après validation
du texte par l'utilisateur.

```
CARROUSEL  ·  8 diapos

1  COUVERTURE  LA CLAUSE À 18 000 €
               Une ligne que je mets maintenant dans chaque contrat.
2  ENJEU       J'ai validé le travail. Neuf jours après, ils voulaient être
               remboursés.
3              CE QU'ELLE DIT
               Paiement à la livraison, pas à la validation.
...
7  RÉCAP       Les quatre lignes, dans l'ordre.
8  APPEL       Commente CONTRAT et je t'envoie la clause complète.

Légende : Travail B, accroche en ligne 1, une demande, 3 hashtags.
```

Rien n'est mis en ligne. L'utilisateur publie.
