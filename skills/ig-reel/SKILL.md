---
name: ig-reel
description: >-
  Écrire un Reel Instagram à partir d'une idée brute : des accroches tirées de
  26 formules, le script parlé, le texte à l'écran et un découpage minuté, dans
  la voix de l'utilisateur et notés avant le tournage. À utiliser dès que
  l'utilisateur veut un Reel, un script de vidéo courte, une accroche, une voix
  off, « fais un reel sur X », « qu'est-ce que je dis dans cette vidéo », ou
  s'apprête à tourner sans avoir sa première phrase.
---

# ig-reel

Transforme une idée brute en un Reel que les gens regardent jusqu'au bout.

Deux outils sont dans ce dossier et ils tournent vraiment. Utilise-les. Ne juge
pas l'accroche à l'œil et ne devine pas la durée.

```bash
python3 hookscore.py hooks.txt              # classer tes accroches
python3 hookscore.py --hook "une phrase"    # noter une seule accroche
python3 beats.py script.txt --target 30     # découpage minuté avant le tournage
```

Les outils comprennent le français et l'anglais. Leurs messages sont en
anglais : traduis-les pour l'utilisateur quand tu lui montres le résultat.

## Avant d'écrire

1. Lis `~/.claude/instagram/voice.md` s'il existe. C'est le profil de voix de
   l'utilisateur : comment il parle face caméra, ce qu'il ne dit jamais, à qui
   il s'adresse. S'il n'existe pas, demande **trois de ses propres reels**,
   transcris-les ou lis-les, déduis la voix et écris le fichier. Un script dans
   la mauvaise voix est inutilisable, parce qu'il faut le dire à voix haute.
2. Lis `hooks.json` dans ce dossier. 26 formules, chacune avec un modèle, un
   exemple rempli, la version à l'écran, son usage et la façon dont on la
   rate. Chaque formule a aussi sa version française (`nom_fr`, `modele_fr`,
   `exemple_fr`, `ecran_fr`). Quatre d'entre elles sont là parce qu'elles
   revenaient sans cesse dans de vraies accroches, pas pour compléter un
   motif.
3. Si l'idée est maigre, ne la gonfle pas. Pose une seule question groupée :
   que s'est-il passé, à qui, et qu'est-ce que ça a coûté ou rapporté. Un Reel
   a besoin d'une chose vraie et précise. Obtiens-la avant d'écrire.
4. Si `~/.claude/instagram/swipe.md` existe, lis-le. `/ig-viral` écrit ce
   fichier, et c'est la preuve de l'utilisateur sur les formules qui marchent
   dans sa niche en ce moment. Il passe avant les réglages par défaut de ce
   fichier.

## La forme

Un Reel se joue dans les deux premières secondes et se garde dans les cinq
suivantes.

```
0:00 - 0:02   ACCROCHE    l'affirmation. Phrase parlée et phrase à l'écran,
                          écrites séparément. Du mouvement dès la première
                          image, pas un visage figé.
0:02 - 0:07   L'ENJEU     pourquoi ça compte pour la personne qui regarde.
                          Une phrase.
0:07 - ...    LE CORPS    une idée par temps, et le plan change à chaque temps.
3 DERN. s     LA CHUTE    tenir la promesse de l'accroche, puis une seule
                          demande.
DERN. PHRASE  LA BOUCLE   reprendre un mot de l'accroche pour que le replay
                          s'enchaîne proprement.
```

Durée : 15 à 45 secondes, c'est la zone utile. Les Reels peuvent durer
3 minutes et presque personne ne devrait s'en servir. Sous 7 secondes, les
boucles gonflent les compteurs et rien d'autre.

## La boucle de travail

**1. Choisis trois accroches, pas une.** Passe l'idée dans `hooks.json`,
choisis trois formules qui lui vont vraiment et écris pour chacune la phrase
parlée et la phrase à l'écran. Trois formules différentes, pas trois
réécritures de la même.

**2. Note-les.** Mets les trois phrases parlées dans un fichier, une par
ligne, et lance `hookscore.py`. Montre le classement à l'utilisateur. Si la
première est sous 50, tu n'as pas encore l'accroche, et aucune retouche n'y
changera rien.

**3. Écris le script** sur l'accroche gagnante. Langue parlée simple, comme
l'utilisateur parle vraiment. Élisions et oral (« t'as », « y'a » si c'est sa
voix). Phrases courtes. Aucune phrase qu'il faudrait répéter avant de la dire.

**4. Minute-le.** Lance `beats.py script.txt --target {durée}`. Corrige chaque
alerte : une accroche de plus de 3 secondes, un temps de plus de 4 secondes,
une suite de temps sans rien de concret, pas de boucle. Relance jusqu'à ce que
ce soit propre.

**5. Humanise-le.** Passe le script dans `/ig-human` avant de le montrer. Une
phrase qui sonne écrite se remarque dès qu'on la dit à voix haute.

**6. Affiche le bloc.** Le script dans un bloc de code, le texte à l'écran en
liste séparée avec les minutages, puis :

```
REEL PRÊT
accroche :    #3 Personne ne te dit, note 86 FORTE
durée :       28,4 s sur 9 temps à 165 mots/min
à l'écran :   6 cartons
humaniseur :  4 artefacts retirés, score humain 81 OK
légende :     lance /ig-caption ensuite

Réponds « oui » pour l'enregistrer, ou dis-moi quoi changer.
```

**7. Ne publie jamais.** Ce skill produit un script. L'utilisateur le tourne et
le publie. Sur « oui », ajoute à `~/.claude/instagram/log.md` la date, la
formule d'accroche utilisée et la première phrase, pour que `/ig-audit` ait un
historique plus tard.

## Le texte à l'écran est un script à part

Écris-le séparément, à chaque fois. Il est lu avant d'être entendu.

- **Six mots maximum par carton.** Il est lu à bout de bras par quelqu'un qui
  n'écoute pas encore.
- **Le carton d'accroche est là dès la première image**, pas après un temps de
  silence.
- **Reste dans la zone sûre.** Sur une image 1080x1920, rien au-dessus de
  y=230 ni en dessous de y=1440, et garde libres les 230 pixels de droite.
  L'interface recouvre tout ce qui sort de ce cadre : la légende, la colonne
  d'actions, la bande audio.
- **Ne mets jamais l'accroche là où se trouve la légende.** C'est le bas de
  l'image et il est recouvert.
- **Incruste les sous-titres pour le corps.** La plupart des gens regardent
  d'abord sans le son.

## Les règles qui font la différence

- **Une idée par Reel.** Si le script en a deux, tu as deux Reels. Dis-le.
- **Des chiffres plutôt que des adjectifs.** « 4 200 € » bat « beaucoup ». Si
  l'utilisateur n'a pas donné de chiffre, demande-le plutôt que d'écrire
  autour du trou.
- **Coupe l'intro.** Pas de bonjour, pas de « dans cette vidéo », pas de nom,
  pas de jingle avec le logo. La vidéo commence à la phrase qu'on atteindrait
  normalement à la sixième seconde.
- **Change de plan à chaque temps.** Un plan fixe de 8 secondes, c'est là que
  les gens partent, et `beats.py` le signalera.
- **Une seule demande à la fin.** Commenter un mot-clé, enregistrer, ou
  s'abonner. Une.
- **N'invente jamais rien.** Pas de chiffres, de clients, de revenus ou de
  résultats inventés au nom de l'utilisateur, même comme exemple provisoire.
  S'il faut un chiffre inconnu, laisse `{{ton chiffre}}` dans le script et
  signale-le.
- **N'écris pas un script autour d'un son tendance que l'utilisateur ne peut
  pas utiliser.** Si l'idée a besoin de la voix de l'utilisateur, dis-le.

## Exemple

```
/ig-reel on est passés de 5 heures à 20 minutes par devis avec un seul modèle
```

```
ACCROCHES  (notées)
  86  FORTE  #5  Temps écrasé         « Un devis me prenait cinq heures. Maintenant, vingt minutes. »
                                      à l'écran : 5 HEURES -> 20 MIN
  71  FORTE  #1  Confession du coût   « J'ai facturé quatre heures de mise en page par semaine. Pendant deux ans. »
                                      à l'écran : 2 ANS PERDUS
  54  OK     #9  Le vol               « Vole le modèle de devis qui a tout changé. »
                                      à l'écran : VOLE ÇA

On tourne la #5 : le rapport est crédible, il se lit en un coup d'œil à
l'écran, et le chiffre est le tien.
```
