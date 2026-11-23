# Sudoku Elo — appli Android

Plateforme de sudoku hors ligne inspirée de chess.com : défis du jour (problème + grille, identiques pour tous),
série de jours, missions et XP, duels contre 7 bots, problèmes classés, Rush de 3 minutes, leçons de techniques,
badges et bilan de partie (précision, coups Brillant / Excellent / Imprécision / Gaffe). Classements Elo séparés :
solo, duel et problèmes.
Le jeu tourne dans une WebView à partir de `app/src/main/assets/index.html`.
Ton Elo, ton historique et la partie en cours sont stockés dans le stockage privé de l'appli.

## Obtenir l'APK sans rien installer (GitHub Actions)

1. Crée un dépôt **privé** sur GitHub (par ex. `sudoku-elo`) et envoie-y tout le contenu de ce dossier,
   y compris le dossier caché `.github/`.
2. Chaque push sur `main` lance la compilation (onglet **Actions**, environ 3 à 4 minutes).
3. L'APK apparaît dans **Releases** sous le nom `sudoku-elo.apk` : ouvre la page depuis ton téléphone,
   télécharge, puis autorise l'installation depuis le navigateur si Android le demande.

Les mises à jour s'installent par-dessus l'ancienne version sans perdre ton Elo :
le numéro de version augmente à chaque compilation et la signature reste la même.

## Compiler sur ton ordinateur

- Android Studio : *Open* sur ce dossier, puis *Build > Build APK(s)*.
- En ligne de commande (Android SDK installé) : `./gradlew assembleRelease`
  → `app/build/outputs/apk/release/app-release.apk`

## Signature (important pour les mises à jour)

Le dépôt est public : la clé de signature n'est pas versionnée. Ajoute deux secrets dans
**Settings > Secrets and variables > Actions** :

- `SIGNING_KEYSTORE_B64` : le fichier `.jks` encodé en base64
- `SIGNING_PASSWORD` : son mot de passe (alias `sudokuelo`)

Sans ces secrets, l'APK est signée avec une clé de debug qui change à chaque compilation :
chaque mise à jour demande alors de désinstaller l'appli (et efface ton Elo).

## Notes

- Désinstaller l'appli efface ton Elo et ton historique.
- Pour modifier le jeu : édite `app/src/main/assets/index.html`, puis pousse ; une nouvelle APK est compilée.
