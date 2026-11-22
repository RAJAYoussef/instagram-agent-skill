---
name: ig-caption
description: >-
  Écrire la légende Instagram : la ligne qui survit à la coupure « ... plus »,
  le corps, la demande unique, les mots de recherche et les quelques hashtags,
  puis la vérifier avant publication. À utiliser quand l'utilisateur dit
  « écris la légende », « fais la description », « qu'est-ce que je mets en
  description », a un reel ou un carrousel prêt et a besoin du texte, ou pose
  une question sur les hashtags.
---

# ig-caption

Un outil est dans ce dossier et il tourne :

```bash
python3 caption.py caption.txt
python3 caption.py caption.txt --keywords "révisions maths,fractions 6e"
```

Il affiche la légende comme le fil l'affiche : les 125 premiers caractères dans
un cadre, tout le reste derrière le « plus ». Lis ce cadre avant de relire quoi
que ce soit d'autre. Il comprend les demandes en français (« commente MOT »,
« enregistre-le », « écris-moi »…). Ses messages sont en anglais : traduis-les
pour l'utilisateur.

## D'abord, décide quel travail fait cette légende

C'est la décision qui ruine les légendes quand on la saute.

**Travail A : la vidéo les a déjà accrochés.** Un Reel porte sa propre accroche
dans les deux premières secondes, parlée et à l'écran. La légende n'est pas une
seconde accroche, et concurrencer la vidéo, c'est perdre les deux. Son travail :
la demande, le contexte qui rend la demande logique, et les mots que les gens
recherchent.

**Travail B : la légende est le contenu.** Une photo, une image seule, une
couverture de carrousel qui ouvre une boucle. Ici la première ligne est
l'accroche et elle fonctionne exactement comme une accroche de Reel : concrète,
courte, coupée sur un suspense plutôt qu'au milieu d'une proposition.

Demande-toi lequel tu écris. Si l'utilisateur a un Reel avec une accroche
forte, écris A et dis pourquoi.

## La forme

```
Ligne 1     125 caractères visibles. Travail A : la demande, simplement.
            Travail B : l'accroche.
            Jamais de bonjour, jamais de hashtag, jamais d'émoji en premier
            caractère.
Corps       paragraphes courts, une ligne vide entre chacun. Deux à six.
            C'est là que vivent les mots de recherche.
La demande  une seule. Commenter un mot-clé, enregistrer, ou écrire en DM. Une.
Hashtags    cinq au maximum, sur leur propre ligne en bas, ou aucun.
```

La limite est de 2 200 caractères et presque rien n'en a besoin. Une légende qui
mérite le clic puis livre 600 caractères bat celle qui en livre 1 800.

## Les hashtags, honnêtement

Les hashtags ne sont plus un levier de portée, et la plateforme l'a dit par un
changement de produit. **Instagram a limité les hashtags à cinq par publication
le 18 décembre 2025**, contre trente avant, en expliquant aux créateurs
qu'« utiliser moins de hashtags (jusqu'à 5), plus ciblés, plutôt que beaucoup de
génériques » fonctionne mieux. Adam Mosseri avait déjà dit en février 2025 que
les hashtags n'augmentent pas la portée : ce sont des étiquettes, pas un levier
de diffusion.

Donc : cinq au maximum, précis, comme étiquettes de sujet. Si l'utilisateur a
un bloc de vingt hashtags dans ses notes, ce bloc est maintenant du poids mort
et le vérificateur le refusera.

`#viral`, `#fyp`, `#explorepage`, `#foryou`, `#pourtoi` ne décrivent rien.
Coupe-les.

## Les mots de recherche comptent plus que les hashtags

La recherche Instagram lit le texte de la légende. Donc l'expression sur
laquelle l'utilisateur veut être trouvé va dans la légende, telle qu'un humain
la taperait, dans une phrase qui se lit normalement. « Révisions de maths »
écrit en toutes lettres en ligne trois, pas « #revisionsmaths » dans un bloc en
bas.

Demande deux ou trois de ces expressions, puis passe-les au vérificateur :

```bash
python3 caption.py brouillon.txt --keywords "révisions maths,brevet maths"
```

## Règles

- **Pas de lien dans la légende.** Les légendes ne sont pas cliquables. Une URL
  dans le corps, c'est du texte mort qui dit « je n'utilise pas cette
  plateforme ». Bio ou DM.
- **Une seule demande.** Deux demandes, c'est comme aucune. `caption.py` les
  compte.
- **La demande par mot-clé exige un mot facile à taper.** Un mot, sans espace,
  sans émoji, et dis-le aussi à voix haute dans la vidéo. `Commente FRACTION`
  marche. `Commente « le guide des fractions »`, non.
- **Écris le premier commentaire à part** s'il y a un lien. Dis-le dans le
  récapitulatif.
- **L'émoji sert de ponctuation, pas de décoration.** Le vérificateur signale
  tout ce qui dépasse 4 pour 100 caractères.
- **Le texte alternatif vaut 20 secondes.** Pour les carrousels et les photos,
  écris-le. Il est lu par les lecteurs d'écran et par Instagram.

## La boucle de travail

1. Décide Travail A ou Travail B et dis lequel.
2. Rédige.
3. Passe-le dans `/ig-human`. Les légendes sont courtes, donc le remplissage
   s'entend plus fort ici que partout ailleurs dans le pack.
4. Lance `caption.py` avec les mots de recherche de l'utilisateur. Corrige
   chaque FAIL. Tranche chaque WARN à voix haute plutôt qu'en silence.
5. Affiche le bloc prêt à copier, puis le récapitulatif :

```
LÉGENDE PRÊTE
travail :     A, le reel porte l'accroche
visible :     118 caractères sur 125 avant la coupure
demande :     une, commente FRACTION
hashtags :    3
recherche :   « révisions maths » en ligne 3, « brevet maths » en ligne 5
vérif :       READY
```

Rien n'est publié. L'utilisateur colle la légende.
