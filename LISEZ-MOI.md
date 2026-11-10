# Atelier de jetons

L'Atelier de jetons transforme vos portraits de personnages (PNG, WebP, JPG) en **jetons ronds encadrés**, prêts pour une table virtuelle (Foundry VTT, Roll20, Owlbear Rodeo…). Pour chaque image, il place un rond sur le visage, pose un cadre, puis écrit deux fichiers WebP : le portrait et le jeton. Vous ajustez tout à la souris.

Il marche pour tous les jeux de rôle : le ou la MJ y prépare ses PNJ, le joueur ou la joueuse son personnage.

## Installer

1. Dézippez l'archive **dans un dossier où vous pouvez écrire**, par exemple `Documents\Atelier de jetons`. Évitez `C:\Program Files`, où l'Atelier ne pourrait pas enregistrer ses réglages.
2. Ouvrez le dossier, puis double-cliquez sur **Atelier de jetons.exe**.

Il n'y a rien à installer : l'Atelier apporte son propre Python (dossier `python`). Ne déplacez pas les fichiers du dossier les uns sans les autres ; déplacez le dossier entier si besoin.

Windows peut afficher « Windows a protégé votre ordinateur » : le programme n'est pas signé. Cliquez sur **Informations complémentaires**, puis sur **Exécuter quand même**.

**Au premier lancement**, l'Atelier vous demande trois dossiers :
- **Cadres** : les cadres de jeton (PNG ou WebP). Celui proposé contient déjà plus de 200 cadres.
- **Portraits à traiter** : vous y déposez vos images.
- **Jetons fabriqués** : les portraits et les jetons finis (les jetons dans le sous-dossier `tokens`).

Les dossiers proposés sont à côté du programme et conviennent très bien : cliquez **Commencer**. Le bouton **Dossiers…**, en haut, permet de les changer plus tard.

## Fabriquer ses jetons, pas à pas

1. Déposez vos portraits dans le dossier des portraits à traiter (bouton **Ouvrir le dossier des images**), puis cliquez **Actualiser**.
2. **À gauche**, la liste des images. Texte clair : à faire ou à refaire. Gris : déjà fabriqué. Orange : à regarder (par exemple, une tête qui touche l'anneau).
3. **Au centre**, l'image et son **rond** : ce qui sera dans le jeton.
   - Glissez le rond pour le **déplacer**.
   - **Molette** au-dessus de l'image, ou petite **poignée** carrée du rond : l'agrandir ou le réduire.
   - Le cercle en pointillé est la proposition automatique, centrée sur le visage. **Revenir à l'automatique** la reprend.
   - **Cadrage** : « Buste » pour un personnage, « Sujet entier » pour une créature ou un véhicule.
4. **À droite**, le jeton fini, en grand, puis en petit (100 px) pour juger de son allure sur la carte à un zoom ordinaire. Le fichier lui-même est fabriqué à la résolution choisie en haut (256 px par case par défaut).
5. **Cadres** : cliquez un cadre pour l'appliquer. Si la case **Appliquer aussi aux variantes** est cochée, toutes les versions de la même image (`-v1`, `-v2`…) le prennent aussi. **Cadre automatique** rend le choix à l'outil. Le champ de recherche filtre la galerie.
6. **Teinte du cadre**, **Saturation**, **Luminosité** : changent la couleur du cadre seul ; le portrait ne bouge pas. **Réinitialiser** rend au cadre ses couleurs. **Enregistrer comme nouveau cadre** écrit le cadre recoloré en nouveau fichier, à côté de l'original, sans jamais rien écraser.
7. **Fabriquer cette image** ou **Tout fabriquer**. **Voir la planche** montre tous les jetons d'un coup d'œil.

Chaque réglage est enregistré tout de suite : rien à sauvegarder. Vos images déposées ne sont jamais modifiées. Un jeton remplacé est gardé dans `fabrique\_controle\_remplaces\`.

**Résolution**, en haut : la taille du jeton, en pixels par case de votre scène (256 par défaut ; 512 pour zoomer plus net).

## Ajouter ses propres cadres

Un cadre est une image **PNG ou WebP carrée** : l'anneau est opaque, et le centre est **transparent** (c'est là que le portrait apparaît). Les cadres fournis sont en WebP sans perte, plus légers que le PNG pour la même image.

- **Ajouter des cadres…** (au-dessus de la galerie) : choisissez un ou plusieurs fichiers. Ils sont **copiés** dans le dossier des cadres ; vos originaux restent où ils sont. Si un nom est déjà pris, la copie prend le premier numéro libre (`TF - Nain 2.png`, puis `3`…) : rien n'est jamais écrasé. La galerie se met à jour toute seule.
- **Ouvrir le dossier des cadres** : vous pouvez aussi y déposer vos fichiers à la main, puis cliquer **Actualiser**.

### Les nommer pour qu'ils soient reconnus

N'importe quel nom est accepté : un cadre mal nommé n'est jamais refusé, il forme simplement une famille à lui seul. Mais ce modèle range vos cadres en **familles** :

```
TF - <Thème> (<Variante>) <N>.png      (ou .webp)
```

- Le nom commence par `TF - `.
- Le **thème** vient d'abord : c'est le mot qui servira aux règles (Nain, Elfe, Magie, Chevalier…).
- La **variante** (couleur, matière, style) se met entre parenthèses, si le thème en a plusieurs.
- Le **numéro** vient **tout à la fin, seul**. Un cadre unique porte aussi le numéro 1, pour que le suivant s'ajoute sans rien renommer.

L'Atelier retire `TF - `, les parenthèses et les tirets pour lire le nom : `TF - Nain (Bronze) 2.png` devient **Nain Bronze 2**, de la famille **Nain Bronze**. Les cadres `TF - Nain (Bronze) 1`, `2` et `3` forment donc une famille : un PNJ de cette famille en reçoit un, toujours le même. Un numéro placé ailleurs (`TF - Nain 2 (Bronze).png`) isole le cadre. Les majuscules et les accents ne comptent pas, mais l'orthographe compte.

### Les cadres attribués tout seuls : `cadres.csv`

Le fichier `fabrique\cadres.csv` (à ouvrir avec le Bloc-notes) choisit le cadre d'après le **nom de l'image**. Une ligne = une règle ; la **première** règle qui correspond gagne.

```
mot;dwarf|nain|naine;TF - Nain*
```

Cette ligne dit : si le nom de l'image contient « dwarf », « nain » ou « naine », prendre un cadre dont le nom commence par `TF - Nain`. Le `*` remplace n'importe quelle suite de lettres.

**Exemple fantasy.** La section « Fantasy » de `cadres.csv` contient déjà des règles en attente pour les elfes, les nains, les orques, les chevaliers, les clercs, les voleurs et les morts-vivants. Une règle dont le cadre n'existe pas encore est simplement sautée. Pour vos nains :
1. Ajoutez votre cadre sous le nom `TF - Nain 1.png` (bouton **Ajouter des cadres…**).
2. Nommez vos portraits `nain-forgeron.png`, `naine-guerriere-v1.png`…
3. Cliquez **Actualiser** : vos nains reçoivent ce cadre, sans rien faire d'autre.

Pour une race ou un rôle qui n'a pas encore de règle, ajoutez une ligne **au-dessus** de la ligne `defaut` (la dernière), par exemple :

```
mot;gobelin|goblin;TF - Gobelin*
```

La dernière ligne, `defaut;;TF - (Cyberpunk - Chrome) Street sam*`, donne le cadre « Street sam » à tout personnage qu'aucune règle ne reconnaît : remplacez ce qui suit `defaut;;` par le début du nom de votre cadre préféré (par exemple `defaut;;TF - Nain*`).

Les autres sortes de règles (`nom`, `dossier`, `cadrage`, `mot-entier`) sont expliquées en tête du fichier. Une image peut aussi prendre le cadre d'un **sous-dossier** : déposez-la dans un sous-dossier `Nain Bronze` du dossier des portraits, et elle prend un cadre de cette famille. Enfin, un cadre cliqué dans la galerie passe toujours avant les règles.

## Si quelque chose ne va pas

- Un message **orange**, en bas, dit ce qui manque.
- **Détection des visages** : l'Atelier se sert du détecteur intégré à Windows. S'il ne marche pas sur votre PC, l'Atelier le dit en orange et place le rond au centre, en haut de l'image : placez-le à la souris, tout le reste fonctionne.
- `Atelier de jetons - diagnostic.cmd` lance l'Atelier avec ses messages dans une fenêtre noire, utile si quelqu'un vous aide.

## Limites

- **Windows 10 ou 11, 64 bits, seulement.** Ni macOS ni Linux.
- Le dossier de l'Atelier doit être modifiable (pas dans `Program Files`).
- Le programme n'est pas signé : voir « Installer » pour l'avertissement de Windows.

## Crédits et licences

- Code de l'Atelier de jetons : © DjamZ, licence MIT (voir `LICENCE.txt`).
- Cadres de jeton fournis : © DjamZ, licence [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/deed.fr). Vous pouvez les partager et les modifier en citant DjamZ, mais pas en faire un usage commercial.
- Programme construit avec [Godot Engine](https://godotengine.org) (licence MIT). Images traitées par [Pillow](https://python-pillow.org) (licence MIT-CMU), avec [Python](https://www.python.org) (licence PSF), fournis dans le dossier `python`. Détection des visages : Windows (Windows.Media.FaceAnalysis).

---

## In English (short)

**Atelier de jetons** (Token Workshop) turns character portraits into framed round tokens for virtual tabletops. Windows 10/11 64-bit only; nothing to install.

1. Unzip anywhere you can write (e.g. `Documents`, not `Program Files`) and run **Atelier de jetons.exe**. If Windows SmartScreen warns you, click *More info* → *Run anyway* (the program is not signed).
2. On first launch, keep the three suggested folders (frames, portraits to process, finished tokens) and click **Commencer** (Start).
3. Drop your portraits in the portraits folder, click **Actualiser** (Refresh). Drag the circle to move it, mouse wheel to resize. Click a frame in the gallery; adjust its hue / saturation / brightness. Click **Tout fabriquer** (Make all).
4. Add your own frames with **Ajouter des cadres…**: square PNG or WebP with a transparent centre, named `TF - <Theme> (<Variant>) <N>.png` (number alone at the end). Rules in `fabrique\cadres.csv` assign frames from words in the image file name, e.g. `mot;dwarf|nain;TF - Nain*`.
5. Face detection uses Windows' built-in detector; if it fails, the circle is centred and everything else still works.

Licences: code under MIT; the bundled frames © DjamZ under CC BY-NC 4.0 (share and adapt with credit, no commercial use). See `LICENCE.txt`.
