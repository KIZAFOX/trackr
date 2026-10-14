# Trackr — TODO

Version publiée : **0.2.4**. La **0.2.5** est prête à publier (Classement, Pros, comptes détectés, profil d'un joueur, rangs
dans l'historique, Fin de partie refaite, prochain objet, clips MP4). Priorité = valeur produit et fiabilité. Difficulté = estimation, pas une durée garantie.

## À faire pour la 0.2.5

- [x] **Changelog 0.2.5** et version passée à 0.2.5 (`package.json`, `package-lock.json`, badge du README).
- [ ] **Publier la 0.2.5** : `npm test`, `dist\` vidé, `npm run release`, signature Windows vérifiée, publier le brouillon.

## À valider en réel (codé et testé en jsdom, jamais vu avec un vrai client)

- [ ] **Barre de titre intégrée** : boutons natifs Windows (réduire, agrandir, fermer) bien alignés, zone de glisser, fenêtre
  agrandie au démarrage. *Faible*
- [ ] **Démarrage sans écran d'attente** : la fenêtre s'ouvre tout de suite (événement `ready-to-show`), accueil « League of Legends
  n'est pas lancé », compte détecté sans redémarrage. *Faible*
- [ ] **Salon dans Draft en direct** : noms des champs du lobby (`gameName`, `gameTag`, `firstPositionPreference`…) et rangs des
  membres via `/lol-ranked/v1/ranked-stats/{puuid}`. *Faible*
- [ ] **Draft en direct en sélection** : champions ennemis visibles malgré les pseudos masqués, illustrations, panneau Menaces,
  ouverture automatique. *Faible*
- [ ] **Rôles d'après la position** (minutes 2 à 13 de la timeline) : vérifier sur une vingtaine de parties Solo/Duo et Flex,
  dont des parties avec roams et des swaps de lane. *Faible*
- [ ] **Détail d'une partie** : timeline LCU (`/lol-match-history/v1/game-timelines`), phase de lane, déroulé, ordre des
  compétences. Sorts lancés et pings avec une clé Riot (format `EUW1_<gameId>` de match-v5). *Moyenne*
- [ ] **Profil d'un autre joueur** : `/lol-summoner/v2/summoners/puuid`, `/lol-match-history/v1/products/lol/{puuid}/matches`
  (historique visible ? limité ?). *Faible*
- [ ] **Comptes détectés** : avec deux comptes, vérifier l'instantané (icône, niveau, rangs), l'archive hors connexion et le
  retour automatique en direct quand le compte consulté se connecte. *Faible*
- [ ] Overlay en **plein écran exclusif** : toujours invisible sur l'écran du jeu (injection interdite). Contournement : Trackr
  s'ouvre sur un second écran au lancement de la partie. À valider avec deux écrans. *Moyenne*
- [ ] **Raccourci global pour ouvrir Trackr** : pendant une partie (focus, fond sombre au-dessus du jeu en sans bordure), avec deux
  écrans, raccourci déjà pris. *Faible*
- [ ] **Enregistrement « partie complète »** sur une longue partie ; récupérer les fichiers `.part` laissés par un plantage au
  prochain démarrage. *Faible*
- [ ] Import automatique des runes : `HTTP 400` sur `matches/by-puuid` (puuid du client au format UUID). Retrouver le puuid
  côté Riot à partir du Riot ID si ça se reproduit. *Moyenne*

## Priorité haute

- [ ] **Matchups** (page « bientôt ») : choisir ton champion et l'adversaire → winrate, nombre de parties, runes et objets les
  plus gagnants dans ce matchup (données du crawler, déjà utilisées par le panneau Menaces). *Moyenne*
- [ ] **Champions** (page « bientôt ») : tier list par rôle et par rang (winrate, pickrate, banrate) à partir de
  `champions/index.json` du crawler, clic → fiche Builds. *Moyenne*
- [ ] **Recherche d'invocateur** dans la barre de titre : Riot ID → puuid via le client (`/lol-summoner/v1/alias/lookup`) → profil
  consulté. La recherche ne trouve aujourd'hui que des champions. *Faible*
- [ ] **Archiver le détail et la timeline** des parties des comptes enregistrés, pour que le détail (équipes, KP, déroulé) marche
  aussi hors connexion. Taille à surveiller (une timeline ≈ 100 Ko). *Moyenne*
- [ ] **Rapport de fin de partie actionnable** : comparer ton build et tes runes au build le plus joué du champion ; morts avant
  10 min, écart de CS à 10 et 15 min (la timeline est déjà lue). *Moyenne*
- [ ] Affiner la **note** des parties (repères par rôle, poids des critères), maintenant que les rôles sont fiables. *Faible*
- [ ] Éditeur de position de l'overlay : deux blocs posés au même endroit se cachent l'un l'autre. *Faible*
- [ ] Stats d'usage : au-delà de ~200 utilisateurs actifs par jour, limite d'écriture du plan gratuit KV atteinte ; ajouter une
  protection contre les faux pings. *Faible*
- [ ] Diagnostics de dépannage Riot / LCU / fichiers manquants : messages explicites, retry ciblés. *Moyenne*

## Idées (à trier)

### Analyse de partie (la timeline LCU donne positions, évènements et or minute par minute)
- [ ] **Carte des morts** : où tu meurs sur la carte (positions des évènements `CHAMPION_KILL`), sur une partie ou sur les 20
  dernières, avec les morts « évitables » (seul, loin de ton équipe). *Moyenne*
- [ ] **Carte des balises** : où tu poses tes wards et tes pinks (`WARD_PLACED` n'a pas toujours la position : à vérifier). *Moyenne*
- [ ] **Courbe de CS et d'or face à ton adversaire de lane**, minute par minute, dans l'onglet Détails. *Faible*
- [ ] **Timeline lisible au survol** : ligne verticale qui suit la souris et affiche l'écart d'or et le score à cette minute. *Faible*
- [ ] **Phases de jeu** (panneau « bientôt » de Draft) : winrate du champion selon la durée de partie, à calculer dans le crawler. *Élevée*
- [ ] **Jungle pathing** (panneau « bientôt » de Draft) : premiers camps des junglers d'après les positions des timelines du
  crawler, chemin le plus fréquent par champion. *Élevée*

### Profil et progression
- [ ] **Duo / groupe** : winrate avec chaque joueur avec qui tu joues souvent (à partir de l'archive des parties). *Moyenne*
- [ ] **Comparer deux profils** côte à côte (toi et un joueur consulté, ou deux de tes comptes). *Moyenne*
- [ ] **Objectifs personnels** : un objectif choisi (CS/min, morts, vision) suivi partie après partie, rappel en fin de partie. *Moyenne*
- [ ] **Bilan de la semaine** : parties, LP, meilleur champion, tendance des indicateurs, en notification ou à l'ouverture. *Faible*
- [ ] Stats perso : graphique de LP sur 30 jours (les rangs mémorisés + l'historique de fin de partie suffisent). *Faible*
- [ ] Profil consulté : maîtrises de champion du joueur (via le client) dans le panneau Champions. *Faible*

### Sélection et partie
- [ ] **Draft en direct** : afficher pour chaque adversaire son champion le plus joué et son winrate dessus (dès que son pseudo
  est visible ou en partie), et signaler un « one trick ». *Moyenne*
- [ ] Suggestion de **bans** selon tes matchups les plus durs dans ton rôle principal. *Faible*
- [ ] Suivi manuel des sorts d'invocateur ennemis avec compte à rebours. *Moyenne*
- [ ] Profils d'overlay distincts selon le mode de jeu. *Élevée*

### Replays et clips
- [ ] **Replays** (entrée du menu, aujourd'hui = clips) : lister les fichiers `.rofl` et relancer un replay via le client
  (`/lol-replays`). *Moyenne*
- [ ] Événements multi-kill, Ace et First Blood dans les noms et filtres de clips. *Moyenne*
- [ ] Raccourci clavier global pour démarrer un clip (réutiliser `accelerator` et l'enregistrement de raccourci existants). *Faible*
- [ ] Partage de clips vers Discord et conversion MP4 optionnelle. *Élevée*
- [ ] Capture audio (choix de la source, micro) et choix de l'écran de capture. *Élevée*

### Données et builds
- [ ] Choix de la plateforme et du rang dans l'onglet Builds ; ajouter Emerald+ pour plus de volume. *Moyenne*
- [ ] Builds par patch, avertissement si les stats ont plus d'un patch, mention « peu fiable » sous le seuil. *Faible*
- [ ] **Builds situationnels** : objets 4–6 selon l'équipe adverse (AP/AD, tanks, soins). *Élevée*
- [ ] Benchmarks par durée de partie ou par minute, en plus des moyennes de fin de partie. *Élevée*
- [ ] Suivi du pipeline : taille de `build-state.json`, parties par champion, alerte après plusieurs échecs. *Faible*
- [ ] Revalider les timers d'objectifs à chaque évolution importante du jeu. *Faible*
- [ ] Support d'autres régions dans l'app (profil, benchmarks, builds). *Moyenne*

### Confort
- [ ] Notifications Windows restantes : partie trouvée, build mis à jour, nouvelle version. *Faible*
- [ ] Liste des raccourcis clavier (Ctrl + K, retour/suivant, souris) dans Réglages. *Faible*
- [ ] Rich Presence : bouton « rejoindre » (relayer une invitation de lobby via le client, jugé fragile). *Faible*
- [ ] Fin de partie : repères intermédiaires sur l'axe du graphique de rang quand les LP bougent peu. *Faible*

## Dette technique

- [ ] `session.js` mélange sélection, Fin de partie et navigation : sortir Fin de partie dans son propre fichier. *Faible*
- [ ] `matches.js` dépasse 700 lignes (liste, enrichissement, rôles, en-tête) : séparer le modèle de partie et l'enrichissement. *Moyenne*
- [ ] Traductions : doublons anciens dans `en.js` (`{n} parties`, séries d'affilée) à dédoublonner, test qui vérifie qu'aucune clé
  n'est en double. *Faible*
- [ ] Télémétrie : compter l'usage des nouvelles pages (Draft en direct, Stats perso, profils consultés, détail Détails/Runes). *Faible*
- [ ] Certificat de signature reconnu pour supprimer l'avertissement Windows SmartScreen (l'empreinte du certificat auto-signé
  est épinglée dans `updateSignature.js` ; avant de le renouveler en octobre 2027, publier une version avec les deux empreintes). *Faible*

## Terminé

### 0.2.4 (prête à publier)
- [x] **Nouvelle interface** : barre de titre intégrée (retour/suivant, actualiser, recherche de champion Ctrl + K, état du client,
  réglages, boutons natifs Windows), barre latérale groupée (Analyse, Outils) façon RIFT/OS avec icônes Lucide, réductible et
  mémorisée, compte connecté en bas (icône, pseudo, rang, états fermé / connexion / erreur).
- [x] **Tableau de bord** refait : en-tête aux couleurs du rang (suit le filtre de file), 20 dernières, 8 indicateurs avec courbe et
  écart avec la période précédente, menu Indicateurs, files, 10/20/30 parties, lignes à plat avec les deux équipes.
- [x] **Détail d'une partie** : onglets Général / Détails / Runes, joueur analysé au choix, phase de lane à 15 min, vision, par
  minute, déroulé par lignes (écart d'or, combats, objectifs), ordre des compétences, runes, sorts lancés et pings (clé Riot).
- [x] **Rôles** fiables : position sur la carte (timeline), Châtiment, objet de support, élimination dans l'équipe.
- [x] **Draft en direct** : plateau 5 contre 5 ouvrable à tout moment, salon (postes choisis, chef, rangs), sélection en direct
  avec illustrations, panneau Menaces (matchups du crawler), clic → fiche Builds.
- [x] **Stats perso** : page avec l'ancien profil détaillé (Aperçu, Champions, Rôles, Forme).
- [x] **Fin de partie** refaite : filtres compacts, dernière partie et bilan sans carte imbriquée, rang en français, comparaison à
  plat, liste à plat.
- [x] **Comptes détectés** (sélecteur à côté du logo) : profil mémorisé de chaque compte (icône, niveau, rangs), consultable hors
  connexion avec ses parties archivées.
- [x] **Profil d'un joueur** : clic sur un joueur dans le détail d'une partie → son profil lu dans le client, Retour en chaîne,
  panneau Champions.
- [x] Écran d'attente au démarrage supprimé ; journal LCU sans répétition quand le client est fermé.

### 0.2.3
- [x] **Mise à jour automatique** : signature vérifiée par empreinte du certificat épinglée (le certificat auto-signé faisait
  échouer la vérification d'electron-updater). Testée de 0.2.3 vers une 0.2.4 de test.
- [x] **Raccourci global pour ouvrir Trackr** (`Alt + N` par défaut) : module `appHotkey`, fond sombre `backdrop`, réglages.
- [x] **Statistiques de l'accueil par file** (sélecteur Solo/Duo – Flex).
- [x] **Plantage de l'enregistreur** en mode « partie complète » : écriture sur disque au fil de l'eau.
- [x] **Accueil** : bloc profil, statistiques à onglets, cartes de parties avec note, KP et adversaire de lane.
- [x] Trackr s'ouvre agrandi ; pseudos abîmés (UTF-8) corrigés ; bandeaux de Partie en cours ; position de l'overlay ; Rich
  Presence des modes spéciaux ; clips regroupés par compte.

### Application (avant)
- [x] Diagnostic : l'historique de l'accueil affiche sa raison quand il échoue, erreurs de l'interface recopiées dans le terminal.
- [x] **0.2.2 publiée** ; mise à jour en un clic ; Trackr sur un second écran en partie.
- [x] `build-automation/` : la collecte ne tourne plus dans le vide.
- [x] Dépendances : jsdom en devDependency, `npm audit --omit=dev` sans vulnérabilité.
- [x] Worker de télémétrie déployé et tableau de bord vérifié.
- [x] Secrets du `.env` partagé changés (Riot, GitHub, jeton admin du Worker).
- [x] **Rich Presence** : mode de jeu en file, en sélection et en partie (rang jamais affiché).
- [x] **Tests d'interface** jsdom sur toutes les pages.
- [x] **Aide aux compétences** au level up, validée en vraie partie.
- [x] **Réglages réorganisés** en 7 catégories.
- [x] **Tableau de bord de télémétrie** refait.
- [x] **Refactor complet** sans commentaires inutiles.
- [x] Historique : archive locale (300 parties par compte), parties perso exclues.
- [x] Gestion des erreurs 429 de l'API Riot.
- [x] Statistiques d'usage anonymes (désactivables).
- [x] Icônes de champion des clips fiabilisées ; bruit de logs 404 de l'API de jeu supprimé.
- [x] Clips et Fin de partie rangés par compte.
- [x] Détection du client, profil, rangs ; champ select et partie en cours ; ouverture de la bonne vue selon la phase.
- [x] Fin de partie, historique filtrable, comparaison de sessions.
- [x] Overlay configurable ; gold diff précis ; clips ; profil joueur ; réglages.
- [x] ~~Splash avec avancement et attente du client~~ (supprimé en 0.2.4).

### Builds et automatisation
- [x] Champ select : carte « Importer les runes / Créer le set d'objets / Tout importer ».
- [x] Pipeline de builds (Match-V5 + timeline) toutes les 8 h, stats publiées sur `gh-pages`, benchmarks Master+ par rôle.
- [x] Onglet Builds façon u.gg, mur de champions, import des runes et set d'objets, auto-accept.
- [x] Site `trackr-website` mis à jour.

### Confort et fiabilité
- [x] Discord Rich Presence, alerte de tilt, export / import des réglages.
- [x] Release de production : signature Windows, auto-update, logs, `RELEASE_CHECKLIST.md`.
- [x] Tests : transitions de phase, IPC, benchmarks, réglages, tilt, builds, UI du dashboard.
- [x] Documentation d'installation et README.
