# HowMuch?

Jeu mobile d'estimation chiffrée : 50 niveaux, défi du jour, duel et mode en ligne jusqu'à 4 joueurs. Tout tient dans un seul fichier, `index.html` (HTML, CSS et JavaScript, sans dépendance).

## Mode en ligne

- Un joueur crée un salon et partage son code de 4 lettres, les autres le rejoignent (4 joueurs maximum), chacun avec son prénom.
- **Survie** : capital de départ de 150, 300 ou 500 points, le dernier joueur qui a encore des points gagne.
- **Précision** : 5, 10 ou 20 questions, le joueur le plus précis gagne.
- Questions tirées au hasard dans toute la base. Dès la première réponse, les autres ont 15 secondes ; sans réponse, pénalité maximale (100 points).
- Si l'hôte part, le plus ancien joueur encore connecté prend le relais.

Le mode en ligne utilise Firebase Realtime Database (`howmuch-aeb9e`) via son API REST, sans clé ni SDK. Règles à coller dans la console Firebase (Realtime Database, onglet Règles) :

```json
{
  "rules": {
    "rooms": {
      "$code": {
        ".read": true,
        ".write": true,
        ".validate": "$code.length === 4"
      }
    }
  }
}
```

Seuls les salons sont lisibles et modifiables ; le reste de la base reste fermé.
