<div align="center">

<img src="assets/icon.png" alt="Trackr" width="120" />

# Trackr

**Connais ta game avant qu'elle commence.**

Overlay et dashboard pour League of Legends : sélection des champions, stats en partie,
bilan de fin de partie, builds high-elo, clips et bien plus, au même endroit.

![Version](https://img.shields.io/badge/version-0.2.6-blueviolet)
![Plateforme](https://img.shields.io/badge/plateforme-Windows-0078D6)
![Electron](https://img.shields.io/badge/Electron-44-47848F)
![Licence](https://img.shields.io/badge/licence-propriétaire-lightgrey)

[**Télécharger**](https://github.com/KIZAFOX/trackr/releases/latest) ·
[Site officiel](https://kizafox.github.io/trackr/) ·
[Guide d'installation](docs/INSTALLATION.md) ·
[Roadmap](TODO.md)

</div>

---

## Aperçu

Trackr se connecte au client League of Legends (lecture seule) et affiche ce qui compte,
au moment où ça compte : qui tu affrontes, comment tu joues, ce que tu devrais acheter,
et comment ta session se déroule.

## Fonctionnalités

### Profil et statistiques
- **Tableau de bord** : rang, bilan des dernières parties et 8 indicateurs avec leur courbe, parties avec note, KP et les deux équipes.
- **Stats perso** : progression de chaque indicateur partie après partie, champions et rôles, par file et sur 10 à 30 parties.
- **Détail d'une partie** : phase de lane, déroulé, ordre des compétences, runes et rang de chaque joueur.
- **Recherche d'un joueur** (`Pseudo#TAG`) et clic sur un joueur d'une partie pour ouvrir son profil.
- **Comptes détectés** : chaque compte connecté sur ce PC reste consultable, même hors connexion.
- **Classement** Challenger, Grand Maître et Maître, et **Pros** avec leurs comptes SoloQ.

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

1. Télécharge `Trackr-Setup-x.y.z.exe` depuis la [dernière release](https://github.com/KIZAFOX/trackr/releases/latest).
2. Lance l'installateur, choisis le dossier et le style de l'écran « Partie en cours ».
3. Ouvre Trackr depuis le menu Démarrer, laisse le client League ouvert.

Les données sont stockées dans `%APPDATA%\Trackr`, les logs dans `%APPDATA%\Trackr\logs\trackr.log`.
Détails, mises à jour et dépannage : [docs/INSTALLATION.md](docs/INSTALLATION.md).

> Une clé Riot API est **optionnelle** et reste locale. Sans elle, le dashboard et les infos
> de base fonctionnent ; les rangs et maîtrises détaillés ne sont pas disponibles.

## Données et automatisation

Le crawler de Trackr analyse des parties classées Solo/Duo et publie ses données sur la branche
`crawler-data` de [`KIZAFOX/trackr`](https://github.com/KIZAFOX/trackr) :

- **Benchmarks** (`benchmarks.json`) : moyennes par rôle et par rang, affichées dans l'overlay.
- **Champions** (`champions.json`, `champions/<id>.json`) : stats par rôle, matchups, synergies et builds,
  utilisés par l'onglet Builds et l'aide aux compétences.

Trackr télécharge ces fichiers, les met en cache localement et continue de fonctionner hors ligne.

## Statistiques d'usage anonymes

Trackr envoie, au plus toutes les 6 h, un ping anonyme (identifiant aléatoire, version, système, région, options
activées, pages ouvertes sans ce qu'elles affichent) pour que le développeur sache combien de personnes l'utilisent. Jamais de pseudo, de parties, de clips ni de
clé API. Désactivable dans **Réglages → Statistiques d'usage anonymes**.

## Respect du jeu et de Riot

Trackr reste en **lecture seule** vis-à-vis du jeu : pas d'injection, pas de lecture mémoire,
uniquement le client local et les API officielles Riot.

*Trackr n'est pas affilié à Riot Games et n'est ni approuvé ni sponsorisé par Riot Games.
League of Legends et Riot Games sont des marques déposées de Riot Games, Inc.*

---

<div align="center">

Fait par **KIZAFOX** · [kizafox.github.io/trackr](https://kizafox.github.io/trackr/)

</div>
