# Trackr : TODO

Version publiée : **0.2.5** (14/10/2026). La **0.2.6** est prête à publier (recherche d'un joueur, Stats perso refaite,
synchronisation de l'overlay, recette du prochain objet, cartes du salon, Changelog dans les réglages, Classement refait
avec podium et carte du joueur, Données et stockage, rejoindre depuis Discord, courbe de rang plus lisible, résumé en image
remis en vue, stats d'usage des pages). Ce qui
est sorti est décrit dans `CHANGELOG.md`, ce fichier ne garde que ce qui reste à faire. Priorité = valeur produit et fiabilité.
Difficulté = estimation, pas une durée garantie.

## À faire pour la 0.2.6

- [x] Version 0.2.6 (`package.json`, `package-lock.json`, badge du README), section datée dans `CHANGELOG.md`,
  `release-notes.md` régénéré, README à jour (fonctionnalités, plus de splash).
- [x] Adresses passées à `KIZAFOX/trackr` et `kizafox.github.io/trackr` dans l'app, le Worker, le crawler et le site.
- [x] **Déménagement sur GitHub** : `trackr-release` renommé en `trackr`, site sur la branche `website` (Pages actif,
  kizafox.github.io/trackr). `trackr-website` supprimé : son ancienne adresse reste en 404 pour les 0.2.5 installées.
  Ne jamais recréer de dépôt `trackr-release` : les 0.2.5 passent par sa redirection pour les mises à jour et le crawler.
- [x] `CHANGELOG.md` complété avec tout ce qui a été fait depuis (overlay synchronisé, touches des sorts, recette du
  prochain objet, cartes du salon, onglet Changelog, longues vidéos, barres de défilement), `release-notes.md` régénéré.
- [ ] Relancer Trackr et essayer les nouveautés avec un vrai client avant de publier : Synchroniser l'overlay et la
  recette du prochain objet en partie, cartes du salon en groupe (vues jusqu'ici avec des données simulées), Classement
  (podium, carte du joueur), Données et stockage, bouton « Copier le résumé en image » du détail d'une partie. Le détail
  de chaque point est dans « À vérifier en conditions réelles ». Hors partie : une instance de dev lancée pendant une
  partie enregistre la partie et met à jour la présence Discord. *Faible*
- [ ] Redéployer le Worker (`npx wrangler deploy` dans `telemetry-worker`) : il accepte alors les pages ouvertes, et l'onglet
  Produit du tableau de bord affiche les cartes « Pages ouvertes » et « Onglets du détail d'une partie ».
- [ ] Crawler : commiter ses changements et le relancer, puis vérifier une publication sur `crawler-data` de `trackr`.
  Le fichier du classement a maintenant un champ `podium` (icône et champion favori des 3 premiers de chaque palier,
  `src/trackr-community.js` et `topChampion` dans `src/leaderboard.js`, test dans `test/trackr.test.js`) : sans relance,
  les cartes du podium restent sur leur fond de repli tant que le client League est fermé. Ces fichiers sont mélangés à
  d'autres changements en cours du crawler : les inclure dans le commit.
- [ ] **Publier la 0.2.6** : mettre la date de publication sur la section `## [0.2.6]` du `CHANGELOG.md` (encore au
  15/10), `dist\` vidé, `npm run release`, signature Windows vérifiée, publier le brouillon GitHub.
- [ ] Après publication : annonce avec le bot Discord (`/annonce version:0.2.6`).

## Hors application (pas lié à une version)

- [x] **Bot Discord**, étapes 1 à 3 : `/ping`, circuit de validation dans `#validation`, rédaction des annonces (gratuite par
  défaut, Claude en option). Code de capture des teasers commencé (`discord-bot/src/teaser`).

## À vérifier en conditions réelles

Codé et testé en jsdom, mais demande une configuration qu'on n'a pas encore eue sous la main.

- [ ] **Deux écrans** : Trackr ouvert sur le second écran au lancement de la partie (League en plein écran exclusif) et
  raccourci `Alt + N` pendant une partie. *Faible*
- [ ] **Deux comptes sur le même PC** : instantané (icône, niveau, rangs), archive hors connexion, retour en direct quand le
  compte consulté se connecte. *Faible*
- [ ] **Salon à plusieurs** dans Draft en direct : postes choisis, chef du groupe, rangs des membres, fond de profil et
  écusson de chaque membre. *Faible*
- [ ] **Synchroniser l'overlay** sur plusieurs résolutions et tailles d'interface du jeu, avec et sans minimap trouvée. *Faible*
- [ ] **Touches des sorts** sur le surlignage avec un clavier AZERTY et des touches changées dans le jeu. *Faible*
- [ ] **Recette du prochain objet** sur une partie entière : composants cochés, alerte d'or pour le composant puis
  l'assemblage. *Faible*
- [ ] **Rôles d'après la position** sur une vingtaine de parties Solo/Duo et Flex, dont des roams et des swaps de lane. *Faible*
- [ ] **Recherche de joueur** : Riot ID avec accents ou espaces, tag à 5 caractères, joueur d'une autre région. *Faible*
- [ ] **Rejoindre depuis Discord** : codé et testé sans Discord ni client réels. À essayer avec deux PC (deux comptes League
  amis, deux comptes Discord amis, Trackr et la présence Discord activés des deux côtés). Ouvrir le salon dans le client
  (groupe ouvert), vérifier que Discord affiche bien « Rejoindre » pour une application non vérifiée, puis cliquer chez l'ami.
  Vérifier aussi le refus quand le salon est plein ou refermé. Si Discord n'affiche pas le bouton, regarder le journal
  (`[discord] Discord a refusé …`). *Moyenne*
- [ ] **Classement refait** : vu sur captures avec le vrai fichier EUW et des illustrations d'exemple, pas dans l'app
  lancée. À regarder en vrai : après relance du crawler, splash du champion favori et icône des trois cartes du podium,
  client fermé et sur une autre région ; client ouvert, fond de profil exact à la place (route `get-player-art`, Riot ID
  avec accents ou espaces, joueur introuvable) ; couronnes, lueurs et faisceaux, survol des cartes, fenêtre étroite.
  Carte du joueur : retournement à l'ouverture, inclinaison et reflet à la souris, « Voir son profil ». *Faible*
- [ ] **Données et stockage** : vu dans l'app avec les vraies tailles, mais boutons Vider et Effacer cliqués seulement en jsdom.
  À essayer hors partie : vider les journaux pendant que Trackr écrit dedans, effacer l'historique puis ouvrir Fin de partie,
  effacer les comptes puis ouvrir le sélecteur de comptes. *Faible*

## Priorité haute

- [ ] **Matchups** (entrée grisée « bientôt ») : ton champion contre un adversaire → winrate, nombre de parties, runes et objets
  les plus gagnants (données du crawler, déjà lues par le panneau Menaces). *Moyenne*
- [ ] **Champions** (entrée grisée « bientôt ») : tier list par rôle et par rang (winrate, pickrate, banrate) à partir de
  `champions/index.json` du crawler, clic → fiche Builds. *Moyenne*
- [ ] **Profils depuis Pros** : un clic sur un compte pro ouvre son profil, avec la route `find-player`. Fait pour le
  Classement (bouton « Voir son profil » de la carte du joueur), à reprendre pour Pros. *Faible*
- [ ] **Archiver le détail et la timeline** des parties des comptes enregistrés, pour que le détail (équipes, KP, déroulé) marche
  hors connexion. Taille à surveiller (une timeline ≈ 100 Ko). *Moyenne*
- [ ] **Rapport de fin de partie actionnable** : ton build et tes runes face au build le plus joué du champion ; morts avant
  10 min, écart de CS à 10 et 15 min (la timeline est déjà lue). *Moyenne*
- [ ] **Audit antislop du 14/10** (`anti-slop/audit-001-2026-10-14.md`), rien n'est encore corrigé : focus invisible sur les
  interrupteurs des Réglages, gris trop pâles (contraste AA), tirets cadratins dans l'interface, fond animé et carte profil
  chargés, animations infinies sans `prefers-reduced-motion`, couleurs sans variables CSS. *Faible à Moyenne*
- [ ] Affiner la **note** des parties (repères par rôle, poids des critères), maintenant que les rôles sont fiables. *Faible*
- [ ] Éditeur de position de l'overlay : deux blocs posés au même endroit se cachent l'un l'autre. *Faible*
- [ ] Stats d'usage : au-delà de ~200 utilisateurs actifs par jour, limite d'écriture du plan gratuit KV atteinte ; ajouter une
  protection contre les faux pings. *Faible*
- [ ] Diagnostics de dépannage Riot / LCU / fichiers manquants : messages explicites, retry ciblés. *Moyenne*

## Bot Discord

- [ ] Étapes suivantes prévues dans `discord-bot/SETUP.md` : visuels (bannière et teaser vidéo), Typefully, article, détection
  automatique d'une nouvelle version. *Moyenne*
- [ ] **Ouvrir le serveur Discord** : mettre l'invitation dans `core/socialLinks.js` et transformer l'icône grisée de la barre
  latérale en bouton. *Faible*

## Idées (à trier)

### Recherche et profils
- [ ] **Suggestions dans la barre de recherche** pendant la frappe : champions, comptes détectés, joueurs consultés récemment,
  avec flèches + Entrée. *Moyenne*
- [ ] **Recherche sans client League** : avec une clé Riot, passer par account-v1 (`by-riot-id`) puis match-v5 quand le client
  est fermé. *Moyenne*
- [ ] **Joueurs suivis** : épingler un profil consulté (duo, ami, rival) pour le retrouver en un clic et voir ses dernières
  parties. *Moyenne*
- [ ] **Déjà croisé** : sur un profil consulté, en Draft ou en partie, les parties que tu as jouées avec ou contre ce joueur
  (archive locale) et le bilan. *Moyenne*
- [ ] **Comparer deux profils** côte à côte (toi et un joueur consulté, ou deux de tes comptes). *Moyenne*
- [ ] Profil consulté : maîtrises de champion du joueur (via le client) dans le panneau Champions. *Faible*

### Analyse de partie (la timeline LCU donne positions, évènements et or minute par minute)
- [ ] **Carte des morts** : où tu meurs sur la carte (évènements `CHAMPION_KILL`), sur une partie ou sur les 20 dernières, avec
  les morts « évitables » (seul, loin de ton équipe). *Moyenne*
- [ ] **Carte des balises** : où tu poses tes wards et tes pinks (`WARD_PLACED` n'a pas toujours la position : à vérifier). *Moyenne*
- [ ] **Courbe de CS et d'or face à ton adversaire de lane**, minute par minute, dans l'onglet Détails. *Faible*
- [ ] **Timeline lisible au survol** : ligne verticale qui suit la souris et affiche l'écart d'or et le score à cette minute. *Faible*
- [ ] **Phases de jeu** (panneau « bientôt » de Draft) : winrate du champion selon la durée de partie, à calculer dans le crawler. *Élevée*
- [ ] **Jungle pathing** (panneau « bientôt » de Draft) : premiers camps des junglers d'après les positions des timelines du
  crawler, chemin le plus fréquent par champion. *Élevée*

### Progression
- [ ] **Duo / groupe** : winrate avec chaque joueur avec qui tu joues souvent (archive des parties). *Moyenne*
- [ ] **Objectifs personnels** : un objectif choisi (CS/min, morts, vision) suivi partie après partie, rappel en fin de partie. *Moyenne*
- [ ] **Bilan de la semaine** : parties, LP, meilleur champion, tendance des indicateurs, en notification ou à l'ouverture. *Faible*
- [ ] **Courbe de LP sur 30 jours** dans le Tableau de bord (la courbe de rang existe déjà dans Fin de partie). *Faible*
- [ ] **Série en cours** dans l'en-tête du Tableau de bord : proposer une pause après 3 défaites, en lien avec l'alerte de tilt. *Faible*

### Sélection et partie
- [ ] **Draft en direct sans clé Riot** : champion le plus joué de chaque adversaire, son winrate dessus et « one trick » (déjà
  affichés avec une clé, via les maîtrises), à lire dans l'historique du client dès que le pseudo est visible. *Moyenne*
- [ ] **Groupes adverses** : signaler les joueurs ennemis qui jouent ensemble (parties communes dans leur historique). *Moyenne*
- [ ] Suggestion de **bans** selon tes matchups les plus durs dans ton rôle principal. *Faible*
- [ ] Suivi manuel des sorts d'invocateur ennemis avec compte à rebours. *Moyenne*
- [ ] Profils d'overlay distincts selon le mode de jeu. *Élevée*

### Replays et clips
- [ ] **Replays** (entrée du menu, aujourd'hui = clips) : lister les fichiers `.rofl` et relancer un replay via le client
  (`/lol-replays`). *Moyenne*
- [ ] Déclencheurs de clips multi-kill, Ace et First Blood (aujourd'hui : kill, assist, mort), dans les noms et les filtres. *Moyenne*
- [ ] Raccourci clavier global pour démarrer un clip (réutiliser `accelerator` et l'enregistrement de raccourci existants). *Faible*
- [ ] Partage d'un clip vers Discord en un clic (les clips sont déjà en MP4). *Moyenne*
- [ ] Capture audio (choix de la source, micro) et choix de l'écran de capture. *Élevée*

### Données et builds
- [ ] Choix de la plateforme et du rang dans l'onglet Builds ; ajouter Emerald+ pour plus de volume. *Moyenne*
- [ ] Builds par patch, avertissement si les stats ont plus d'un patch, mention « peu fiable » sous le seuil. *Faible*
- [ ] **Builds situationnels** : objets 4 à 6 selon l'équipe adverse (AP/AD, tanks, soins). *Élevée*
- [ ] Benchmarks par durée de partie ou par minute, en plus des moyennes de fin de partie. *Élevée*
- [ ] Suivi du pipeline : taille de `build-state.json`, parties par champion, alerte après plusieurs échecs. *Faible*
- [ ] Revalider les timers d'objectifs à chaque évolution importante du jeu. *Faible*
- [ ] Support d'autres régions dans l'app (profil, benchmarks, builds, classement). *Moyenne*

### Confort
- [ ] Notifications Windows en plus du tilt et du plein écran : partie trouvée, build mis à jour, nouvelle version. *Faible*
- [ ] Liste des raccourcis clavier (Ctrl + K, `Pseudo#TAG`, retour/suivant, boutons de souris, `Alt + N`) dans Réglages. *Faible*
- [x] Rich Presence : bouton « Rejoindre » sur Discord pour un salon ouvert dans le client (voir « À vérifier en conditions réelles »).
- [x] Fin de partie : repères tous les 50, 25 ou 10 LP sur l'axe du graphique de rang quand les LP bougent peu.

## Dette technique

- [x] Fichiers trop longs découpés : `matches.js` (810 → 475, modèle dans `match-model.js`, LP, rangs et KP dans
  `match-enrich.js`), `session.js` (devenu `champ-select.js` + `end-of-game.js`), `runes-tab.js` (706 → 480, HTML sans état
  dans `runes-html.js`), `clips.js` (697 → 344, réglages dans `settings-clips.js`, lecteur et découpe dans `clip-player.js`).
- [x] Traductions : 9 doublons retirés de `en.js` (`{n} partie(s)`, séries d'affilée, `File classée`), aucune traduction
  affichée ne change. `test/i18n.test.js` échoue désormais si une clé apparaît deux fois.
- [x] Télémétrie : Draft en direct, Stats perso, Classement, Pros, profil consulté, recherche de joueur et chaque onglet du
  détail sont comptés (ouverts par le joueur, pas l'ouverture automatique de Draft en direct). Le Worker doit être redéployé
  pour les accepter (voir « À faire pour la 0.2.6 »).
- [ ] Traductions anglaises incomplètes, vues en refaisant le Classement : les noms de rang avec division
  (« Émeraude III ») ne sont traduits nulle part dans l'app, et les pourcentages gardent la virgule (« 54,7 % ») en
  anglais. *Faible*
- [ ] `end-of-game.js` fait encore 532 lignes : la comparaison de sessions et la courbe de rang peuvent en sortir. *Faible*
- [ ] Retirer le commentaire `TODO` des entrées « bientôt » dans `index.html` une fois Champions et Matchups livrés. *Faible*
- [ ] Certificat de signature reconnu pour supprimer l'avertissement Windows SmartScreen (l'empreinte du certificat auto-signé
  est épinglée dans `updateSignature.js` ; avant de le renouveler en octobre 2027, publier une version avec les deux empreintes). *Faible*
