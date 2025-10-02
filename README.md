# Scoros - Basketball Scoreboard

**Version 2.0.0**  
Application web de tableau de bord pour matchs de basketball amateurs

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-2.0.0-green.svg)

## Description

Scoros est une application web de scoreboard pensée pour les matchs de basketball en salle. Elle permet de gérer les scores, le chronomètre, et offre des effets audio/visuels personnalisables pour dynamiser l'ambiance pendant les matchs.

Conçue initialement pour le **Toulouse Basket Club (TBC)** - Équipe Loisirs.

## Fonctionnalités

### Score & Timer
- Affichage des scores HOME et VISITOR en temps réel
- Chronomètre avec contrôles +1min / -1min
- Boutons d'incrémentation : +1, +2, +3 points
- Boutons de décrémentation : -1 point
- Fonction undo pour annuler la dernière action
- Reset complet du match

### Effets & Animations
- Overlay GIF plein écran lors des paniers marqués
- Sons personnalisables par action
- Buzzer de fin de match (synthétique ou audio)
- Animations de victoire
- Feedback visuel sur les boutons

### Contrôles
- Interface clavier avec raccourcis configurables
- Interface tactile/souris
- Mode plein écran (double-clic sur score ou timer)
- Panel debug (F2) et historique des actions (F1)

### Personnalisation
- Configuration complète via fichier JSON externe
- Noms d'équipes personnalisables
- Logo personnalisable
- Couleurs et polices configurables
- Sons et GIFs par action

## Installation

### Prérequis
- Un navigateur web moderne (Chrome, Firefox, Edge, Safari)
- Un serveur web local pour le développement (optionnel mais recommandé)

### Démarrage rapide

1. **Télécharger les fichiers**
```bash
git clone https://github.com/votre-repo/scoros.git
cd scoros
```

2. **Lancer l'application**

Option A - Serveur Python (recommandé) :
```bash
python -m http.server 8000
```
Puis ouvrir http://localhost:8000

Option B - Ouvrir directement le fichier HTML :
```bash
# Double-clic sur scoros_app.html
# Note: Le fichier config.json ne sera pas chargé en mode file://
```

## Configuration

### Structure des fichiers

```
scoros/
├── scoros_app.html        # Application principale
├── config.json            # Configuration (optionnel)
└── assets/               
    ├── sounds/            # Fichiers audio
    ├── gifs/              # Animations GIF
    ├── tbc-logo.png       # Logo du club
    └── basketball-pattern.jpg
```

### Fichier config.json

Créez un fichier `config.json` à la racine pour personnaliser l'application :

```json
{
  "app": {
    "name": "Scoros",
    "club": "Toulouse Basket Club",
    "team": "Équipe Loisirs",
    "matchDuration": 600
  },
  "teams": {
    "homeTeam": "TBC LOISIRS",
    "visitorTeam": "ADVERSAIRES"
  },
  "display": {
    "primaryColor": "#00ff00",
    "secondaryColor": "#ffff00",
    "feedbackColor": "#ff6b35",
    "feedbackDuration": 2000,
    "shortcutDisplay": {
      "enabled": true,
      "format": "({key})",
      "fontSize": "0.7rem",
      "color": "#888888"
    }
  },
  "assets": {
    "logo": "./assets/tbc-logo.png",
    "backgroundImage": "./assets/basketball-pattern.jpg"
  },
  "audio": {
    "globalVolume": 0.8,
    "sounds": {
      "buzzer": {
        "enabled": true,
        "files": ["./assets/sounds/buzzer.mp3"],
        "volume": 1.0
      }
    }
  },
  "actions": {
    "score2pt_home": {
      "sounds": ["./assets/sounds/panier.mp3"],
      "gifs": ["./assets/gifs/celebration1.gif"],
      "gifDuration": 2000,
      "volume": 0.8
    },
    "score3pt_home": {
      "sounds": ["./assets/sounds/three-pointer.mp3"],
      "gifs": [
        "./assets/gifs/three-point1.gif",
        "./assets/gifs/three-point2.gif"
      ],
      "gifDuration": 2500,
      "randomSelection": true,
      "volume": 0.9
    },
    "omg": {
      "sounds": ["./assets/sounds/omg.mp3"],
      "gifs": ["./assets/gifs/amazing.gif"],
      "gifDuration": 3000
    }
  },
  "keyboard": {
    "shortcuts": [
      { "key": "p", "action": "toggleTimer", "description": "Play/Pause" },
      { "key": "q", "action": "score1pt_home", "description": "HOME +1" },
      { "key": "w", "action": "score2pt_home", "description": "HOME +2" },
      { "key": "e", "action": "score3pt_home", "description": "HOME +3" },
      { "key": "a", "action": "minus_home", "description": "HOME -1" },
      { "key": "u", "action": "score1pt_visitor", "description": "VISITOR +1" },
      { "key": "i", "action": "score2pt_visitor", "description": "VISITOR +2" },
      { "key": "o", "action": "score3pt_visitor", "description": "VISITOR +3" },
      { "key": "j", "action": "minus_visitor", "description": "VISITOR -1" },
      { "key": "m", "action": "omg", "description": "OMG!" },
      { "key": "b", "action": "buzzer", "description": "Buzzer" },
      { "key": "r", "action": "resetGame", "description": "Reset" },
      { "key": "z", "action": "undoLastAction", "description": "Undo" },
      { "key": "t", "action": "addTime", "params": { "seconds": 60 }, "description": "+1min" },
      { "key": "y", "action": "addTime", "params": { "seconds": -60 }, "description": "-1min" }
    ]
  }
}
```

## Raccourcis clavier

### Actions de jeu (configurables)

| Touche | Action | Description |
|--------|--------|-------------|
| **Q** | HOME +1 | Ajoute 1 point à HOME |
| **W** | HOME +2 | Ajoute 2 points à HOME |
| **E** | HOME +3 | Ajoute 3 points à HOME |
| **A** | HOME -1 | Retire 1 point à HOME |
| **U** | VISITOR +1 | Ajoute 1 point à VISITOR |
| **I** | VISITOR +2 | Ajoute 2 points à VISITOR |
| **O** | VISITOR +3 | Ajoute 3 points à VISITOR |
| **J** | VISITOR -1 | Retire 1 point à VISITOR |
| **P** | Play/Pause | Démarre/Arrête le chronomètre |
| **T** | +1 minute | Ajoute 1 minute au chrono |
| **Y** | -1 minute | Retire 1 minute au chrono |
| **M** | OMG | Action spéciale "incroyable" |
| **B** | Buzzer | Déclenche le buzzer manuellement |
| **Z** | Undo | Annule la dernière action |
| **R** | Reset | Nouveau match (avec confirmation) |

### Touches de debug (fixes)

| Touche | Action |
|--------|--------|
| **F1** | Afficher/Masquer l'historique |
| **F2** | Afficher/Masquer le panneau debug |
| **F3** | Test manuel des raccourcis |
| **F5** | Recharger l'application |

### Interactions souris

- **Clic** sur les boutons : Exécute l'action
- **Double-clic** sur score ou timer : Passe en plein écran
- **Clic** sur overlay GIF : Ferme l'animation

## Utilisation en match

### Avant le match

1. Ouvrir l'application sur le PC de projection
2. Vérifier que les noms d'équipes sont corrects
3. Passer en plein écran (F11 ou double-clic)
4. Tester le son et les GIFs (F3 pour debug)

### Pendant le match

1. Utiliser les raccourcis clavier pour les actions rapides
2. Le chronomètre démarre avec **P**
3. Marquer les points avec **Q/W/E** (HOME) ou **U/I/O** (VISITOR)
4. Utiliser **M** pour les actions spectaculaires
5. **B** pour le buzzer de fin de période

### Après le match

1. Appuyer sur **R** pour réinitialiser
2. Les données sont automatiquement sauvegardées dans localStorage

## Affichage GIF

Les GIFs s'affichent en plein écran avec :
- Préservation des proportions (pas de déformation)
- Utilisation maximale de l'espace disponible
- Animation d'entrée/sortie fluide
- Fermeture automatique ou manuelle (clic)

Les dimensions s'adaptent automatiquement :
- GIF large → occupe toute la largeur
- GIF haut → occupe toute la hauteur
- Toujours centré et proportionnel

## Personnalisation avancée

### Actions personnalisées

Vous pouvez définir des actions pour chaque type de panier :

```json
"actions": {
  "score3pt_home": {
    "sounds": [
      "./assets/sounds/crowd1.mp3",
      "./assets/sounds/crowd2.mp3"
    ],
    "gifs": [
      "./assets/gifs/curry1.gif",
      "./assets/gifs/curry2.gif",
      "./assets/gifs/curry3.gif"
    ],
    "gifDuration": 3000,
    "randomSelection": true,
    "volume": 0.9
  }
}
```

`randomSelection: true` choisira aléatoirement parmi les sons/GIFs fournis.

### Conditions de victoire

```json
"rules": {
  "victoryConditions": {
    "enabled": true,
    "minScore": 21,
    "scoreDifference": 2,
    "playVictorySound": true,
    "playVictoryAnimation": true
  }
}
```

## Dépannage

### Le fichier config.json n'est pas chargé

**Problème** : Mode `file://` détecté  
**Solution** : Utiliser un serveur web local
```bash
python -m http.server 8000
# ou
npx http-server
```

### Les raccourcis ne fonctionnent pas

1. Ouvrir la console (F12)
2. Chercher "KEYDOWN détecté" dans les logs
3. Vérifier que vous n'êtes pas dans un champ de saisie
4. Appuyer sur F3 pour tester les raccourcis

### Les GIFs ne s'affichent pas

1. Vérifier les chemins dans config.json
2. Vérifier que les fichiers existent dans `/assets/gifs/`
3. Ouvrir la console pour voir les erreurs
4. Formats supportés : GIF, PNG, JPG, WEBP

### Le son ne fonctionne pas

1. Vérifier le volume système
2. Autoriser la lecture automatique dans le navigateur
3. Vérifier `globalVolume` dans la config
4. Formats supportés : MP3, WAV, OGG

## Support navigateurs

| Navigateur | Version minimale | Support |
|------------|------------------|---------|
| Chrome | 90+ | Complet |
| Firefox | 88+ | Complet |
| Edge | 90+ | Complet |
| Safari | 14+ | Complet |

## Technologies utilisées

- HTML5
- CSS3 (Grid, Flexbox, Animations)
- JavaScript (ES6+)
- Web Audio API (buzzer synthétique)
- LocalStorage API (sauvegarde état)

## Développement

### Architecture

```
scoros_app.html
├── Configuration (config object)
├── État du jeu (gameState object)
├── Gestion des événements (keyboard, mouse)
├── Logique métier (scores, timer, actions)
├── Effets (audio, GIF, animations)
└── Interface (display, feedback)
```

### Fonctions principales

- `executeAction(actionName, params)` - Exécute une action
- `addScore(team, points)` - Modifie le score
- `toggleTimer()` - Démarre/Arrête le chrono
- `showGifOverlay(gifFile, duration)` - Affiche un GIF
- `setupKeyboardShortcuts()` - Configure les raccourcis

## Contribution

Les contributions sont les bienvenues ! Pour contribuer :

1. Fork le projet
2. Créer une branche (`git checkout -b feature/amelioration`)
3. Commit les changements (`git commit -m 'Ajout fonctionnalité'`)
4. Push vers la branche (`git push origin feature/amelioration`)
5. Ouvrir une Pull Request

## Licence

MIT License - Voir le fichier LICENSE pour plus de détails

## Auteurs

- **Développement initial** - Pour TBC Équipe Loisirs
- **Version 2.0** - Refonte complète avec système de configuration

## Remerciements

- Toulouse Basket Club pour le support
- La communauté du basket amateur
- Tous les contributeurs

## Contact

Pour toute question ou suggestion :
- Email : contact@example.com
- GitHub Issues : [Créer un ticket](https://github.com/votre-repo/scoros/issues)

---

**Vamos Toros! 🐂🏀**
