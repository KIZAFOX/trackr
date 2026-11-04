# Trackr : TODO

Version publiée : **0.2.8** (25/10/2026 : overlay en classée Solo/Duo et Flex seulement, lancement et page Clips plus rapides).
Prochaine version : **0.2.9** (logo sur les clips partagés, kill et doublé dans un seul clip, santé de l'app dans les statistiques d'usage). Ce qui
est sorti est décrit dans `CHANGELOG.md`, ce fichier ne garde que ce qui reste à faire. Priorité = valeur produit et fiabilité.
Difficulté = estimation, pas une durée garantie.

Rangé du plus important au moins important : d'abord les priorités, puis le reste. Dans chaque section, le plus important est en haut.

## 1. Priorité haute

- [x] **Page Esport : suisse et tableau final en grand** (demande du 05/11/2026, sauvegarde : `D:\Dev\TrackR - 0.1.1\trackr-backup-esport-bracket-2026-11-05`) :
  - [x] `core/esportsTournament.js` : phases du tournoi en cours déduites du calendrier (suisse rejoué match par match, tableau, saison, listes) ;
  - [x] interface : onglets de phase, plateau suisse relié, tableau final en miroir, classement de saison, détail d'un match dans une fenêtre, cartes de ligue plus compactes ;
  - [x] tests, traductions, CHANGELOG, DESIGN.md ;
  - [x] vérification visuelle sur le vrai calendrier en cache (Mondial 2026, LEC), thèmes sombre et clair.
  - Choix faits : pas de nouvel appel réseau, tout vient de `getSchedule` déjà chargé (le suisse se recalcule à partir des résultats, et si le rejeu ne tombe pas juste la phase s'affiche en simple liste au lieu d'un plateau faux) ; plateau sombre dans les deux thèmes car les logos d'équipe sont prévus pour fond sombre ; l'appariement des quarts non joués suit l'ordre du calendrier et une mention le dit sur la page.
  - [ ] regarder la page avec `npm start` sur un match en direct (les données testées venaient du cache, sans réseau).

- [x] **Refonte de la page Matchups, écran « versus » animé** (demande du 05/11/2026, sauvegarde : `D:\Dev\TrackR - 0.1.1\trackr-backup-matchups-2026-11-05`) :
  - [x] sélection : scène à deux splashs avec aperçu au survol, au focus et à la frappe, verrouillage animé, flèches du clavier ;
  - [x] duel : même scène, coupure en diagonale, bras de fer du winrate, chiffre qui défile depuis 50 % ;
  - [x] répartition de tous les adversaires sur un axe de winrate, cliquable ;
  - [x] traductions, CHANGELOG, DESIGN.md, tests ;
  - [x] rendu vérifié avec de fausses données dans un navigateur (sombre et clair, 1100 px de large).
  - [ ] regarder la fluidité des animations avec `npm start` et de vraies données (l'aperçu tournait au ralenti, panneau masqué ; mise en page sous 640 px non vue).
  - Choix faits : une seule scène à la fois (la sélection remplace le duel, « Retour au duel » ou Échap pour revenir) ; champion sans données : la grille se rouvre pour en choisir un autre, elle restait fermée sans issue.
- [x] **Nouvelle page de choix des Builds** (demande du 05/11/2026, sauvegarde : `D:\Dev\TrackR - 0.1.1\trackr-backup-builds-2026-11-05`) :
  - [x] champions récents en cartes illustrées, tuiles avec jauge de winrate, filtre par rôle et tri ;
  - [x] thèmes sombre et clair, états vide et erreur, clavier ;
  - [x] tests, traductions, CHANGELOG, DESIGN.md.
- [x] **Détail d'une partie dans sa propre fenêtre** (demande du 04/11/2026, sauvegarde : `D:\Dev\TrackR - 0.1.1\trackr-backup-detail-2026-11-04`) :
  - [x] clic sur une partie : fenêtre par-dessus la page, sans faire bouger le tableau de bord, Échap pour fermer ;
  - [x] en-tête avec le résumé de la partie, parties précédente et suivante ;
  - [x] onglet Général d'abord ; plus aucun bloc vide dans Détails (ARAM : pas de lane, de vision ni de CS par adversaire) ;
  - [x] tests, traductions, CHANGELOG.
  - [ ] regarder la fenêtre sur de vraies parties avec `npm start` (ARAM et classée).
- [x] **Thème clair / sombre pour toute l'app** (demande du 04/11/2026, sauvegarde : `D:\Dev\TrackR - 0.1.1\trackr-backup-theme-2026-11-04`) :
  - [x] réglage Sombre / Clair / Système dans Réglages → Général, sans flash au lancement, barre de titre comprise ;
  - [x] couleurs des feuilles de style passées sur des variables, feuille `theme.css` pour le clair ;
  - [x] pages vérifiées avec de fausses données (Classement, Pros, Esport, Matchups, fiche Build et Partie en cours restent à regarder avec de vraies données) ;
  - [x] traductions, CHANGELOG, DESIGN.md, tests.
  - Choix faits : sombre par défaut pour ne rien changer aux joueurs actuels ; l'overlay en jeu reste sombre ; la page Partie en cours, le lecteur de clips et les cartes posées sur une illustration restent sombres dans les deux thèmes, car leur texte se lit sur une image.
- [x] **Nouveau tableau de bord d'après le screen du 04/11/2026** (sauvegarde : `D:\Dev\TrackR - 0.1.1\trackr-backup-dashboard-2026-11-04`) :
  - [x] mise en page : carte de rang, historique compact, Clips, Favoris, Performance, Champions ;
  - [x] favoris : étoile sur un champion, un build, un matchup, une partie ou un clip, gardés dans les réglages ;
  - [x] carte Clips : les 2 derniers clips, ouverts dans le lecteur ;
  - [x] traductions, CHANGELOG, DESIGN.md, tests.
  - Choix faits : thème sombre gardé (DESIGN.md, le screen est clair) ; objectif, 7 jours, coéquipiers et joueurs suivis gardés sous la grille ; 5 indicateurs affichés par défaut comme sur le screen, les 3 autres via « Indicateurs » ; « Voir tout » et l'ouverture d'une partie passent l'historique en pleine largeur avec les lignes détaillées.
- [ ] **Publier la 0.2.9 avec les statistiques de santé** (lancement, plantages, erreurs, client League, parties, overlay ;
  Clips et Fin de partie comptés à l'ouverture). Code et tests faits le 26/10/2026, dans cet ordre :
  - [x] déployer le Worker (`cd telemetry-worker` puis `npx wrangler deploy`) avant la release : fait le 26/10/2026 ;
  - [ ] mettre le site à jour (`tools\push-website.bat`) : la confidentialité décrit les nouveaux compteurs ;
  - [ ] jouer une classée avec `npm start` et vérifier `telemetry-pending.json` dans `%APPDATA%\Trackr` (parties, overlay, client League, lancement) ;
  - [ ] publier la release, puis vérifier l'onglet Produit → Santé de l'app au premier ping d'un poste en 0.2.9.
- [ ] **Clips : vérifier en partie que le bon écran est filmé** (correction du 04/11/2026, deux écrans, choix « Automatique ») :
  - [x] attendre la fenêtre du jeu 15 s, puis filmer l'écran principal au lieu du premier de la liste ;
  - [x] ne reconnaître que la fenêtre « League of Legends (TM) » ;
  - [ ] jouer quelques parties avec `npm start` et lire `[clips] source filmée` dans `trackr.log`. Si « fenêtre League introuvable » revient, allonger l'attente.
- [ ] **Revoir les statistiques ~2 semaines après la 0.2.9** : rétention à 7 jours (17 % au 26/10), où les joueurs décrochent,
  puis choisir la suite (première partie mise en avant, Draft en direct proposé pendant la sélection). *Faible*
- [ ] **Mentions légales, téléphone de l'hébergeur** (`discord-bot/src/site/infoPages.js`, section Hébergement) : la loi
  française le demande, mais GitHub ne publie aucun numéro officiel (ses conditions disent « pas de support téléphonique »)
  et les annuaires en donnent plusieurs différents. À ajouter seulement avec une source sûre. Relecture de la
  confidentialité, des conditions et des mentions légales faite le 19/10/2026. *Faible*

## 2. Plus tard (à surveiller)

- [ ] **Sortir Trackr sur macOS et Linux** (code fait le 27/10/2026, retiré de la 0.2.9 faute de Mac et de Linux pour fabriquer
  et tester les fichiers). Le code reste dans l'app et ne change rien sous Windows : détection du client par `ps` (lockfile sur macOS),
  menu, Dock et overlay plein écran sur macOS, mise à jour qui ouvre la page des releases sur macOS (app non signée), copie du clip
  par `osascript`, son du Mac dans les clips (macOS 14.2+), lancement au démarrage sous Linux (`~/.config/autostart`),
  cibles `dmg`/`zip`/`AppImage`/`deb` et scripts `dist:mac`/`dist:linux`. Dans l'ordre :
  - [ ] fabriquer les fichiers Linux : WSL (`wsl --install` puis `npm run dist:linux`), ou AppImage seule sous Windows après avoir activé
    le mode développeur (l'essai du 27/10 n'a échoué que sur la création de liens symboliques) ;
  - [ ] fabriquer les fichiers Mac : GitHub Actions (runner macOS, sources dans un dépôt privé), Mac loué ou emprunté (`npm run dist:mac`) ;
  - [ ] version de test proposée aux joueurs Mac et Linux du Discord : détection du client, overlay en plein écran, son du Mac dans les
    clips (fonction Chromium `MacCatapLoopbackAudioForScreenShare` non vérifiée), ouverture d'une app non signée, démarrage auto sous Linux ;
  - [ ] entrée CHANGELOG (texte de départ dans `D:\Dev\trackr-backup-2026-10-27-macos-linux\round3\CHANGELOG.md`, section 0.2.9) ;
  - [ ] site : reprendre `home.html` et `infoPages.js` mis de côté dans `D:\Dev\trackr-backup-2026-10-27-macos-linux\site-mac-linux`
    (téléchargements, installation, FAQ « Le Mac refuse d'ouvrir Trackr », dossiers des données), `npm run site:pages`, et ne publier
    qu'une fois les fichiers Mac et Linux joints à la release ;
  - plus tard : barre de titre intégrée sur macOS (barre native pour l'instant), copie du clip sous Linux (`xclip`/`wl-copy`).
- [ ] Certificat de signature reconnu pour supprimer l'avertissement Windows SmartScreen (l'empreinte du certificat auto-signé
  est épinglée dans `updateSignature.js` ; avant de le renouveler en octobre 2027, publier une version avec les deux empreintes). *Faible*
- [ ] **Site, pages d'aide** : la FAQ et la confidentialité décrivent ce que fait l'app (stats d'usage, données gardées, services
  contactés, clé Riot). Les mettre à jour à chaque changement de ce côté (`npm run site:pages` puis `tools\push-website.bat`). *Faible*

## 3. Idées (à trier)

Groupes rangés par intérêt pour le joueur, les idées les plus utiles et les moins chères en haut de chaque groupe.

### Données et builds
- [ ] **Esport, bans des parties** : lolesports.com ne les donne pas (ni le flux livestats). Source possible : Leaguepedia
  (API Cargo, contenu CC BY-SA, à créditer), à associer aux parties par équipes et date. *Moyenne*
- [ ] Revalider les timers d'objectifs à chaque évolution importante du jeu. Vu le 18/10/2026 : Baron à 20:00 confirmé par
  Riot (/dev saison 2026, Atakhan retiré) ; le Héraut est à 14:00 dans `objectiveTimers.js`, une source non officielle dit
  15:00 : à chronométrer en partie avant de changer. *Faible*
