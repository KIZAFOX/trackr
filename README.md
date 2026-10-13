<div align="center">

<img src="assets/icon.png" alt="Trackr" width="120" />

# Trackr

**Connais ta game avant qu'elle commence.**

Overlay et dashboard pour League of Legends : sélection des champions, stats en partie,
bilan de fin de partie, builds high-elo, clips et bien plus, au même endroit.

![Version](https://img.shields.io/badge/version-0.1.9-blueviolet)
![Plateforme](https://img.shields.io/badge/plateforme-Windows-0078D6)
![Electron](https://img.shields.io/badge/Electron-44-47848F)
![Licence](https://img.shields.io/badge/licence-propriétaire-lightgrey)

[**Télécharger**](https://github.com/KIZAFOX/trackr-release/releases/latest) ·
[Site officiel](https://kizafox.github.io/trackr-website/) ·
[Guide d'installation](docs/INSTALLATION.md) ·
[Roadmap](docs/TODO.md)

</div>

---

## Aperçu

Trackr se connecte au client League of Legends (lecture seule) et affiche ce qui compte,
au moment où ça compte : qui tu affrontes, comment tu joues, ce que tu devrais acheter,
et comment ta session se déroule.

## Fonctionnalités

### Avant la partie
- **Sélection des champions** : rang, maîtrise et winrate des joueurs des deux équipes.
- **Runes en un clic** : import automatique des runes recommandées dès le champ select.
- **Accept auto** de la partie trouvée.

### Pendant la partie
- **Overlay en jeu** : CS/min, gold/min, participation aux kills, vision/min.
- **Timers d'objectifs** et estimation de la différence de gold.
- **Styles d'affichage** : Duel, Cartes ou Tableau.

### Après la partie
- **Bilan de fin de partie** : résultat, statistiques, LP gagnés ou perdus.
- **Alerte de tilt** : détecte les séries de défaites et te prévient une fois par partie.
- **Historique** filtrable par session, champion, file et résultat, avec comparaison entre sessions.

### Builds
- **Onglet Builds** : runes, objets, ordre de montée des sorts et winrates par champion et par rôle.
- **Données high-elo** (Master, Grandmaster, Challenger) générées automatiquement toutes les 8 h.
- **Set d'objets** créé directement dans la boutique du jeu.

### Outils
- **Clips** : capture d'événements ou de parties entières, lecture dans le dashboard.
- **Discord Rich Presence** : affiche l'état de ta partie, la version de Trackr et un lien vers le site.
- **Export / import des réglages** pour changer de machine sans tout reconfigurer.
- **Mises à jour automatiques** depuis l'application.

## Installation

1. Télécharge `Trackr-Setup-x.y.z.exe` depuis la [dernière release](https://github.com/KIZAFOX/trackr-release/releases/latest).
2. Lance l'installateur, choisis le dossier et le style de l'écran « Partie en cours ».
3. Ouvre Trackr depuis le menu Démarrer, laisse le client League ouvert.

Les données sont stockées dans `%APPDATA%\Trackr`, les logs dans `%APPDATA%\Trackr\logs\trackr.log`.
Détails, mises à jour et dépannage : [docs/INSTALLATION.md](docs/INSTALLATION.md).

> Une clé Riot API est **optionnelle** et reste locale. Sans elle, le dashboard et les infos
> de base fonctionnent ; les rangs et maîtrises détaillés ne sont pas disponibles.

## Développement

Prérequis : Windows, Node.js 20+ et npm.

```powershell
npm ci
npm start
```

Copie `.env.example` vers `.env` pour renseigner `RIOT_API_KEY` et `DEFAULT_REGION`
(fichier ignoré par Git, jamais embarqué dans l'installateur).

| Commande | Rôle |
| --- | --- |
| `npm start` | Lance l'application en développement |
| `npm test` | Lance les tests (`node --test`) |
| `npm run dist` | Construit l'installateur dans `dist/`, sans publication |
| `npm run release` | Build, signature et publication GitHub (`GH_TOKEN`, `CSC_LINK`, `CSC_KEY_PASSWORD`) |

Incrémente `version` dans `package.json` avant une release. Checklist complète : [docs/RELEASE_CHECKLIST.md](docs/RELEASE_CHECKLIST.md).

## Architecture

```text
src/
  main/       Process principal Electron (cycle de vie, réglages, fenêtres, IPC, mises à jour)
  preload/    Ponts sécurisés renderer <-> main
  core/       Logique métier sans Electron, testable seule (client LCU, runes, builds, tilt...)
  shared/     Modules UMD utilisés par Node et par les pages
  renderer/   Interfaces : dashboard, overlay, splash, recorder
assets/       Icône de l'application
build/        Icône Windows et script NSIS
tools/        Signature Windows, vérification de release
test/         Tests automatisés
docs/         Installation, release, clips, thèmes, roadmap
```

## Données et automatisation

Deux dépôts d'automatisation (GitHub Actions) alimentent l'application, publiés sur la branche
`gh-pages` de [`KIZAFOX/trackr-release`](https://github.com/KIZAFOX/trackr-release) :

- **Builds** : collecte de parties Ranked Solo/Duo de joueurs high-elo via Match-V5, toutes les 8 h,
  avec seuils minimaux de parties par champion et par rôle.
- **Benchmarks** : moyennes par rôle régénérées chaque semaine.

Trackr télécharge ces fichiers, les met en cache localement et continue de fonctionner hors ligne.

## Documentation

- [Installation](docs/INSTALLATION.md)
- [Checklist de release](docs/RELEASE_CHECKLIST.md)
- [Clips](docs/CLIPS.md)
- [Thèmes](docs/THEMES.md)
- [Roadmap](docs/TODO.md)

## Respect du jeu et de Riot

Trackr reste en **lecture seule** vis-à-vis du jeu : pas d'injection, pas de lecture mémoire,
uniquement le client local et les API officielles Riot.

*Trackr n'est pas affilié à Riot Games et n'est ni approuvé ni sponsorisé par Riot Games.
League of Legends et Riot Games sont des marques déposées de Riot Games, Inc.*

---

<div align="center">

Fait par **KIZAFOX** · [kizafox.github.io/trackr-website](https://kizafox.github.io/trackr-website/)

</div>