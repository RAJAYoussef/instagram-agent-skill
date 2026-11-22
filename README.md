# Le skill agent Instagram (version française)

Treize skills Claude qui font tourner un compte Instagram. Gratuit, licence MIT,
sans inscription, sans clé d'API, rien à connecter.

L'un écrit tes Reels à partir de 26 formules d'accroche et note l'accroche avant
que tu perdes une prise dessus. Un autre va chercher les reels qui marchent
vraiment dans ta niche et les classe selon à quel point chacun a dépassé son
propre compte. Un autre écrit la légende et te montre exactement ce que le fil
affiche avant le « ... plus ». Un autre note ton profil sur 100 et réécrit ce
qui a perdu des points. Un autre planifie la semaine.

Et il y a l'humaniseur, la raison pour laquelle le reste est utilisable. Il
retire les tirets cadratins, le vocabulaire creux et les caractères invisibles
d'un brouillon, puis note ce qui reste sur un panel de cinq contrôles avant que
tu ne le voies.

**Rien n'est publié tant que tu n'as pas dit oui.** Ces skills écrivent. Tu
publies.

> Fork traduit de
> [Jakeschincariol/instagram-agent-skill](https://github.com/Jakeschincariol/instagram-agent-skill)
> (MIT). Voir [Ce qui change dans la version française](#ce-qui-change-dans-la-version-française).

## Installation

Colle ceci dans Claude :

```
https://github.com/RAJAYoussef/instagram-agent-skill

Installe ce skill, puis vérifie que /ig-reel fonctionne.
```

Ou fais-le toi-même, dans Claude Code :

```bash
git clone https://github.com/RAJAYoussef/instagram-agent-skill.git
cp -r instagram-agent-skill/skills/ig-* ~/.claude/skills/
```

Ou en plugin :

```
/plugin marketplace add RAJAYoussef/instagram-agent-skill
/plugin install instagram-agent
```

Pour un projet seulement plutôt que partout : copie les mêmes dossiers dans le
`.claude/skills/` de ton dépôt. Pas de Claude Code du tout ? Colle n'importe
quel `SKILL.md` en haut d'une conversation et il fonctionne comme un mode. Tu
perds les cinq outils Python, qui sont l'essentiel de `/ig-reel` et
`/ig-human`, mais le reste marche.

Ensuite, passe dix minutes sur `templates/voice.md`. Copie-le dans
`~/.claude/instagram/voice.md` et remplis-le, ou envoie à Claude trois de tes
propres reels en disant « écris mon voice.md à partir de ça ». Tous les skills
lisent ce fichier. Il compte plus ici qu'ailleurs, parce que les mots, il faut
les dire à voix haute.

## Les treize

| commande | ce qu'elle fait |
| --- | --- |
| `/ig-reel` | Une idée en Reel. Trois accroches tirées de [26 formules](skills/ig-reel/hooks.json), notées, puis le script, le texte à l'écran et un découpage minuté. |
| `/ig-viral` | Va voir ce qui marche dans ta niche, le classe par multiple au-dessus de la médiane de chaque compte, nomme la formule, écrit le swipe file. |
| `/ig-caption` | La légende, vérifiée. Te montre les 125 caractères que le fil affiche vraiment avant le tap. |
| `/ig-carousel` | Les posts à swiper. La couverture qui donne envie de swiper, le texte des diapos, et les fichiers 1080x1350. |
| `/ig-story` | La séquence de stories du jour, quel sticker fait quel travail, et le tunnel vers les DM qui commence quand c'est eux qui bougent. |
| `/ig-profile` | Note ton profil sur une [grille en 12 points](skills/ig-profile/rubric.json) sur 100, puis réécrit en commençant par le plus urgent. |
| `/ig-plan` | La semaine. Quoi publier, sous quel format, quand, et les 10 comptes avec qui interagir. |
| `/ig-human` | L'humaniseur. Deux scripts qui tournent vraiment. Voir plus bas. |
| `/ig-comment` | Les commentaires sous les publications des autres. Neuf types, choisis selon ce qu'est vraiment la publication. Jamais « 🔥🔥🔥 ». |
| `/ig-reply` | Le fil sous ta propre publication. Trie en mot-clé / prospect / fond / question / soutien / bruit, puis écrit dans cet ordre. |
| `/ig-dm` | L'envoi après un mot-clé, le premier message, la proposition de collab, et les deux relances. Deux. |
| `/ig-repurpose` | Une vidéo, un podcast ou une newsletter en une semaine de reels et de carrousels qui tiennent chacun debout seuls. |
| `/ig-audit` | Le bilan de ce que tu as déjà publié. Classe par multiple d'écart et envois par couverture, pas par vues. |

## Les cinq outils qui tournent vraiment

Aucune dépendance, aucun réseau, rien n'est envoyé. Ils tournent sur ta machine,
sur ton texte, en français comme en anglais. Leurs messages sont en anglais ;
Claude te les traduit.

### Les accroches

```bash
python3 hookscore.py hooks.txt              # classer tes options
python3 beats.py script.txt --target 30     # minuter avant de tourner
```

```
HOOK RANKING
==============================================================================
->  81.4 STRONG  Arrête de recopier tes cours de maths. Dessine-les.
        weakest: STAKES (70)
    66.2 OK      68 % des élèves de 3e ne savent pas diviser une fraction.
        weakest: ADDRESS (35)
    53.0 OK      Personne ne te dit que les fractions, c'est juste des parts...
        weakest: SPECIFICITY (15)
    30.0 WEAK    Les maths, c'est important pour l'avenir.
        weakest: SPECIFICITY (15)
     0.0 WEAK    Salut tout le monde, dans cette vidéo je vais vous montrer ...
        weakest: FRONTLOAD (0)
        dealbreaker: Video preamble. Delete it and open on the payoff.
        dealbreaker: Greeting. Nobody came to the feed to be greeted.
```

`beats.py` estime combien de temps prend chaque phrase à dire, les empile en
minutage, et signale les quatre choses qui tuent un Reel au montage : une
accroche qui dépasse trois secondes, un temps assez long pour que le
spectateur parte, une suite de phrases sans rien de concret, et pas de boucle
vers la première phrase.

### La légende

```bash
python3 caption.py caption.txt --keywords "révisions maths,brevet"
```

Instagram donne à une légende environ 125 caractères dans le fil et cache le
reste derrière un tap. Presque toutes les légendes qui échouent échouent là.
Donc la première chose affichée est cette fenêtre, dans un cadre, comme la lit
un inconnu qui fait défiler.

Il applique la limite actuelle de hashtags, qui est de **cinq par
publication**, pas trente. Instagram l'a réduite le 18 décembre 2025.

### L'humaniseur

```bash
python3 humanize.py brouillon.txt --report      # nettoyer, montrer chaque changement
python3 detect.py brouillon.txt                  # noter, cinq contrôles
python3 detect.py avant.txt apres.txt            # prouver l'écart
```

**Ce qui part automatiquement :**

- **Les caractères invisibles.** Espaces et liants de largeur nulle, traits
  d'union conditionnels, marques d'ordre des octets, caractères d'étiquette
  Unicode, espaces insécables et fines. Ton clavier ne les produit pas.
- **La typographie.** Tiret cadratin en virgule, demi-cadratin en trait
  d'union, guillemets courbes en droits, points de suspension en trois points.
  En français, l'espace avant « ; : ! ? » est conservée.
- **Le lexique.** Des mots et expressions toutes faites en anglais et en
  français avec des remplacements simples, dont un bloc propre à Instagram :
  « arrête de scroller », « dans la vidéo d'aujourd'hui », « abonne-toi pour
  plus de contenu », « l'algorithme adore ». Il est dans
  [`slop.json`](skills/ig-human/slop.json) et il est fait pour être modifié.
  Chaque texte est identifié comme français ou anglais et seul le lexique de sa
  langue s'applique.

**Ce qui est signalé au lieu d'être corrigé :** « Ce n'est pas juste X, c'est
Y », « non seulement… mais aussi », les questions rhétoriques d'un mot, le
préambule vidéo, les listes à puces en émojis, trois mots en majuscules à la
suite, les murs de hashtags, les appâts réflexes, « n'hésite pas à… ». Changer
la forme d'une phrase demande du jugement.

### Le swipe file

```bash
python3 swipe.py captured.tsv --out ~/.claude/instagram/swipe.md
```

Les vues brutes ne sont pas une preuve. Un compte de 2 000 000 d'abonnés qui
fait 400 000 vues a eu un mardi tranquille. Un compte de 4 000 abonnés qui fait
400 000 vues a trouvé quelque chose. `swipe.py` classe sur le multiple
au-dessus de la médiane de chaque compte, nomme la formule d'accroche (en
français ou en anglais), et affiche ce qui sépare le tiers du haut du tiers du
bas.

## Ce qui a été mesuré

L'auteur d'origine a testé le noteur d'accroches sur **74 vraies accroches**
de vidéos courtes en anglais (YouTube Shorts, les 8 meilleures et 8 pires de
cinq chaînes).

1. **Il repère bien les mauvaises accroches** : AUC 0,83 contre des accroches
   écrites exprès pour être mauvaises.
2. **Il ne choisit pas les gagnantes** : séparer les succès d'un bon créateur
   de ses échecs donne une AUC de 0,56, où 0,50 est du pile ou face.
3. **Le classeur de formules** reconnaît environ la moitié des vraies
   accroches ; sur l'autre moitié il s'abstient, ce qui est correct.

La version française n'a pas été mesurée sur un corpus français. Les listes de
mots françaises suivent la même logique que les anglaises, mais traite les notes
comme un filtre contre les accroches faibles, pas comme une prédiction.
Utilise-le pour éliminer les accroches clairement faibles avant de tourner,
puis fais confiance à ta propre courbe de rétention.

## Les petites lignes, la partie honnête

**Ces skills ne publient pas sur Instagram.** Il existe une vraie API de
publication pour les comptes professionnels, mais elle demande une application
développeur Meta, une page liée, un jeton longue durée et une validation, ce
qu'un skill ne peut pas te fournir. Tout le reste de ce que les gens utilisent
pour automatiser la publication, les commentaires, les abonnements ou les DM,
c'est de l'automatisation de navigateur ou un outil tiers, et les deux violent
les [conditions d'utilisation d'Instagram](https://help.instagram.com/581066165581870)
et font bloquer les comptes. Donc chaque skill se termine pareil : un bloc prêt
à copier, et c'est toi qui publies.

La seule exception : les réponses automatiques par mot-clé en DM, qu'Instagram
prend en charge via ses propres outils et des partenaires agréés, et qui ne se
déclenchent qu'après que quelqu'un a commenté.

**`/ig-viral` lit, il n'aspire pas.** Dix comptes, une douzaine de reels
chacun, à vitesse humaine, avec toi aux commandes de ton propre navigateur. Il
ne demande jamais ton mot de passe et ne se connecte jamais à ta place.

**Les cinq contrôles de détection sont des heuristiques locales, pas des API de
détecteurs.** Ce ne sont pas GPTZero, Originality, Copyleaks, Winston ou
Turnitin. Personne ne peut honnêtement te vendre de l'« indétectable ».

**Rien n'est inventé.** Aucun chiffre, client ou résultat inventé ne passe sous
ton nom. Si un brouillon a besoin d'un chiffre que tu n'as pas donné, il revient
avec `{{ton chiffre}}` et une alerte, à chaque fois.

**Les chiffres de la plateforme vieillissent.** Si quelque chose ici contredit
ce que fait Instagram quand tu le lis, c'est Instagram qui a raison.

## Ce qui change dans la version française

- Les 13 `SKILL.md`, ce README et `templates/voice.md` sont traduits. Les noms
  de commandes (`/ig-reel`…), de dossiers et de fichiers sont inchangés.
- `hooks.json` : chaque formule a sa version française (`nom_fr`,
  `modele_fr`, `exemple_fr`, `ecran_fr`) et une expression `match_fr` pour que
  `swipe.py` reconnaisse les accroches en français.
- `hookscore.py`, `beats.py`, `caption.py`, `detect.py`, `swipe.py` : prise en
  charge des accents, des élisions (« j'ai », « c'est »), des montants en euros
  et des nombres à la française (« 18 000 », « 6e »), plus les listes de mots
  françaises (enjeux, chiffres dits à voix haute, ouvertures faibles,
  impératifs, demandes du type « commente MOT », « enregistre-le »).
- `slop.json` : un lexique français marqué `"lang": "fr"`, et des tics de
  structure français.
- Sur un texte en anglais, les outils donnent exactement les mêmes résultats
  que l'original.

## Fichiers

```
skills/ig-reel/hooks.json          26 formules d'accroche, en anglais et en français
skills/ig-reel/hookscore.py        le panel de notation d'accroche en cinq critères
skills/ig-reel/beats.py            du script au découpage minuté
skills/ig-caption/caption.py       l'aperçu de coupure et le vérificateur de légende
skills/ig-human/slop.json          le lexique, les caractères invisibles et les tics
skills/ig-human/humanize.py        les trois passes de nettoyage
skills/ig-human/detect.py          le panel à cinq contrôles
skills/ig-viral/swipe.py           classement par écart et reconnaissance des formules
skills/ig-profile/rubric.json      la note de profil sur 100
templates/voice.md                 ton profil de voix. À remplir en premier.
```

## Crédits

Créé par Jake Schincariol, [opusjake.ai](https://opusjake.ai). Version
française par RAJAYoussef.

Dépôt frère, même idée pour une autre plateforme :
[linkedin-agent-skill](https://github.com/Jakeschincariol/linkedin-agent-skill).

## Licence

MIT. Prends-le, modifie-le, publie-le.
