# Documentation Technique - Jeu de Taquin (15-Puzzle)

Ce document explique en détail le fonctionnement du code source `taquin.c`, sa structure, la logique de jeu implémentée, ainsi que l'interface utilisateur graphique réalisée avec la bibliothèque SDL2.

## 1. Structure Globale du Code

Le projet est contenu dans un fichier unique en C utilisant la bibliothèque **SDL2** pour la gestion de la fenêtre, du rendu graphique et des événements (clavier/souris).

### Bibliothèques et Constantes
- **Bibliothèques** :
  - `<SDL2/SDL.h>` : Pour l'interface graphique.
  - `<stdbool.h>`, `<stdio.h>`, `<stdlib.h>`, `<time.h>` : Pour les types standards.
- **Macros et Configuration** :
  - `MAX_GRID_SIZE 5` : Taille maximale supportée pour la grille.
  - `TILE_SIZE 150` : Taille en pixels des tuiles.
  - `GAP 5` : Espace entre les tuiles.
  - `UI_HEIGHT 60` : Hauteur de la barre d'interface en bas de l'écran.

### Structures de Données
- **`GameState`** : Structure stockant l'état du jeu.
  - `grid[MAX_GRID_SIZE][MAX_GRID_SIZE]` : Plateau de jeu.
  - `empty_x`, `empty_y` : Position de la case vide.
  - `size` : Taille actuelle de la grille (3, 4 ou 5).
- **`AppState` (Enum)** : `STATE_MENU` ou `STATE_PLAYING`.

---

## 2. Analyse des Fonctions

### Fonctions Logiques
- **`init_game`** / **`shuffle_game`** : Gestion de l'initialisation et du mélange adaptatif selon la taille.
- **`check_win`** : Vérifie la condition de victoire.

### Fonctions Graphiques
- **`draw_number`** : Rendu des chiffres 7-segments.
- **`draw_home_icon`** : Dessine une icône de maison vectorielle pour le bouton de retour.

### Boucle Principale
Intègre une machine à états et gestion des zones de clic :
- **Zone de Jeu** : Clics convertis en coordonnées de grille `(y / TILE_SIZE)`.
- **Zone UI** : Clics en bas de l'écran (`y >= size * TILE_SIZE`) déclenchent le retour au menu.

---

## 3. L'Interface Utilisateur (UI)

### Menu Principal
L'écran d'accueil propose les tailles 3, 4 et 5. La fenêtre redimensionne automatiquement.

### En Jeu
Une **barre d'outils (grise)** est ajoutée en bas de la fenêtre.
- **Bouton Home** : Une icône de maison au centre permet de quitter la partie actuelle et revenir au menu principal pour choisir une autre grille.
- **Raccourcis** : La touche `ESC` permet également de revenir au menu.
