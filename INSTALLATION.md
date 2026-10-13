# Installation de Trackr

Trackr fonctionne sous **Windows 10/11** avec le client **League of Legends** installé.
Aucun Node.js ni `npm` n'est nécessaire pour l'utiliser.

## Installer

1. Ouvre la [dernière release](https://github.com/KIZAFOX/trackr-release/releases/latest).
2. Télécharge `Trackr-Setup-x.y.z.exe`.
3. Lance l'installateur :
   - choisis le **dossier d'installation** (*Parcourir…*) ;
   - choisis le **style de « Partie en cours »** : Duel, Cartes ou Tableau (aperçu en direct) ;
   - clique sur **Installer**.
4. Ouvre Trackr depuis le menu Démarrer.
5. Laisse le client League ouvert : Trackr détecte ton compte et les phases de jeu tout seul.

> Windows peut afficher un avertissement SmartScreen tant que l'application n'a pas de certificat
> reconnu. Télécharge toujours l'installateur depuis la page de release officielle.

## Premiers pas

- **Accueil** : profil, rang Solo/Duo et Flex, dernières parties.
- **Builds** : choisis un champion pour voir runes, objets et sorts les plus joués en haut elo.
  Boutons d'import des runes et de création du set d'objets (le client doit être ouvert).
- **Réglages** : overlay, clips, auto-accept, import automatique des runes, alerte de tilt,
  Discord Rich Presence, export / import des réglages.

## Clé Riot (facultative)

Sans clé, le dashboard, l'historique et les builds fonctionnent ; seuls les rangs et maîtrises
détaillés des autres joueurs sont absents. La clé reste **locale** et n'est jamais publiée.
Ne partage jamais une clé Riot ni un fichier `riot-key.json`.

## Mises à jour

Clique sur **Mettre à jour Trackr** : la release GitHub est vérifiée et la nouvelle version
téléchargée. Quand le bouton affiche **Redémarrer**, clique dessus : Trackr se ferme, installe
la mise à jour et se relance. Ne lance pas un second installateur pendant ce temps.

Si une installation reste bloquée, fais un clic droit sur l'icône Trackr près de l'horloge,
choisis **Quitter**, puis recommence.

## Changer de PC

**Réglages → Application → Exporter** crée un fichier de réglages, **Importer** le recharge sur
l'autre machine. Le dossier des clips n'est pas repris (il dépend du PC).

## Données et dépannage

| Élément | Emplacement |
| --- | --- |
| Préférences et historique | `%APPDATA%\Trackr` |
| Journal de diagnostic | `%APPDATA%\Trackr\logs\trackr.log` |
| Clips | `Vidéos\Trackr Clips` (modifiable) |

Rien de tout cela n'est envoyé sur GitHub.

- **Client non détecté** : ouvre League, puis relance Trackr (détection via `LeagueClientUx.exe`).
- **Rangs ou maîtrises vides** : clé Riot absente ou invalide, ou mauvaise région dans les réglages.
- **« Stats pas encore publiées » dans Builds** : le champion n'a pas atteint le seuil de parties
  du dernier calcul ; réessaie après la prochaine mise à jour des données (toutes les 8 h).
- **Set d'objets introuvable** : lis le journal, cherche `[builds] set d'objets impossible (étape : …)`.
- **Signalement de bug** : joins les dernières lignes de `trackr.log` après avoir vérifié
  qu'elles ne contiennent rien de personnel.

## Développement

Prérequis : Node.js 20+ et npm.

```powershell
npm ci
npm start
npm test
```

Copie `.env.example` vers `.env` (ignoré par Git, jamais embarqué dans l'installateur) :

| Variable | Usage |
| --- | --- |
| `RIOT_API_KEY` | Statistiques Riot enrichies en développement |
| `DEFAULT_REGION` | Région par défaut (`euw1`) |
| `GH_TOKEN` | Publication GitHub (mainteneur) |
| `CSC_LINK` / `CSC_KEY_PASSWORD` | Certificat de signature `.pfx` (mainteneur) |

## Publier une release (mainteneur)

À lancer depuis Windows.

1. Incrémenter `version` dans `package.json` et `package-lock.json`.
2. Lancer `npm test`.
3. Fermer Trackr (installé ou en développement) et supprimer `dist/` si un build précédent a échoué.
4. `npm run dist` : installateur local, sans publication ; tester l'installation.
5. `npm run release` : build, signature et publication sur `KIZAFOX/trackr-release`.
6. Sur une machine de test, installer l'ancienne version puis vérifier la mise à jour.

Problèmes fréquents :

- **« The file is being used by another process »** pendant la signature : un processus (antivirus,
  ancien Trackr) bloque le fichier. Ferme Trackr, supprime `dist/`, ajoute une exclusion Defender.
  Le script de signature réessaie déjà 6 fois.
- **422 « Published releases must have a valid tag »** : le token `GH_TOKEN` doit avoir
  *Contents : Read and write* sur `trackr-release`, et le dépôt doit avoir une branche par défaut
  avec au moins un commit. À défaut, crée un brouillon de release `vX.Y.Z` à la main puis relance.

Checklist complète : [RELEASE_CHECKLIST.md](RELEASE_CHECKLIST.md).