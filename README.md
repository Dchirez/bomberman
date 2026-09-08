# Bomberman

Bomberman complet jouable dans le navigateur : **[dchirez.fr/bomberman](https://dchirez.fr/bomberman/)**

Campagne solo de 8 niveaux, duel local à deux, IA de poursuite, bonus cachés, réactions en chaîne.
Un seul fichier `index.html`, aucune dépendance, aucune image, aucun fichier son.

## Commandes

| Action | Solo | Duel — J1 | Duel — J2 |
| --- | --- | --- | --- |
| Déplacement | Flèches ou ZQSD | ZQSD | Flèches |
| Poser une bombe | Espace | Espace | Entrée |
| Pause | Échap ou P | | |
| Couper le son | M | | |

Sur mobile, une croix directionnelle et un bouton de bombe s'affichent sous le plateau.

## Le jeu

**Campagne solo** — huit niveaux générés à la volée : trame de piliers indestructibles, murs
cassables semés aléatoirement, et une sortie dissimulée sous l'un d'eux. Le niveau est terminé
quand tous les ennemis sont éliminés *et* que la sortie est atteinte. Le chronomètre écoulé ne tue
pas : il fait apparaître des fantômes qui traversent les murs.

**Duel à deux** — deux joueurs sur le même clavier, arène régénérée à chaque manche, trois manches
gagnantes.

**Cinq familles d'ennemis**, du promeneur au traqueur :

| Ennemi | Comportement | Points |
| --- | --- | --- |
| Balloom | déplacements au hasard | 100 |
| Oneal | se dirige parfois vers le joueur | 200 |
| Doll | rapide et erratique | 300 |
| Minvo | poursuite par parcours en largeur | 400 |
| Pontan | traverse les murs cassables | 800 |

**Cinq bonus** cachés sous les murs, détruits par une flamme s'ils ne sont pas ramassés à temps :
bombe supplémentaire, souffle allongé, vitesse, coup de pied dans les bombes, vie supplémentaire.

## Sous le capot

- **Rien n'est chargé depuis le disque.** Décors, personnages et explosions sont dessinés au trait
  sur un `<canvas>` ; les bruitages sont des formes d'onde calculées à l'ouverture (balayages,
  bruit blanc filtré, arpèges) via l'API Web Audio.
- **Poursuite prudente.** Les ennemis traqueurs calculent leur chemin par un parcours en largeur
  sur la grille qui écarte les cases déjà menacées par une mèche allumée.
- **Déplacement confortable.** L'entité est recentrée en continu sur l'axe perpendiculaire à sa
  marche : c'est ce détail qui évite de rester bloqué aux angles.
- **Traversée de sa propre bombe.** Chaque bombe retient les entités qui la chevauchent encore : on
  s'échappe de la case où l'on vient de poser, mais on ne peut plus y revenir.
- **Moteur séparé du rendu**, ce qui permet de le simuler sans afficher quoi que ce soit — la
  campagne, les manches du duel et les chaînes de mort ont été vérifiées ainsi.

## Version desktop

Ce jeu est le portage web d'une version **Java 21 / JavaFX** :
[Dchirez/bomberman-javafx](https://github.com/Dchirez/bomberman-javafx).

---

Damien Chirez — [dchirez.fr](https://dchirez.fr)
