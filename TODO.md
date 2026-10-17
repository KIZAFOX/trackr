# Trackr : TODO

Version publiée : **0.2.6** (16/10/2026 : recherche d'un joueur, Stats perso refaite,
synchronisation de l'overlay, recette du prochain objet, cartes du salon, Changelog dans les réglages, Classement refait
avec podium et carte du joueur, Données et stockage, rejoindre depuis Discord, courbe de rang plus lisible, résumé en image
remis en vue, stats d'usage des pages). Ce qui
est sorti est décrit dans `CHANGELOG.md`, ce fichier ne garde que ce qui reste à faire. Priorité = valeur produit et fiabilité.
Difficulté = estimation, pas une durée garantie.

Rangé du plus important au moins important : d'abord ce qui reste à vérifier en conditions réelles, puis les priorités,
puis le reste. Dans chaque section, le plus important est en haut. Rien ne bloque la publication de la 0.2.7.

## 1. À vérifier en conditions réelles

Codé et testé, mais demande une situation qu'on ne peut pas créer seul.

- [ ] **Contre-picks** dans Draft en direct : essayer le panneau dans une vraie sélection (poste attribué, picks adverses un
  par un). *Faible*
- [ ] **Esport** : rechargement toutes les minutes pendant un direct. Vu le 17/10 (Mondial, FUR - C9) : la page se recharge
  seule chaque minute avec le score de l'API. Reste à voir le score changer et le match passer dans Derniers résultats à
  la fin. Pendant le même direct, déplier « Détail des parties » : la partie en cours doit se mettre à jour avec la page
  (vu seulement sur des matchs terminés). *Faible*
- [ ] **Esport, bans des parties** : lolesports.com ne les donne pas (ni le flux livestats). Source possible : Leaguepedia
  (API Cargo, contenu CC BY-SA, à créditer), à associer aux parties par équipes et date. *Moyenne*
- [ ] **Stats d'usage** : déployer le Worker (`cd telemetry-worker` puis `npx wrangler deploy`) pour activer la limite par
  adresse et le plafond de nouveaux postes, puis vérifier dans le tableau de bord que les actifs du jour restent cohérents
  (un poste n'écrit plus qu'une fois par jour quand rien ne change). La page Confidentialité du site dit déjà que l'adresse IP
  sert à cette limite : c'est vrai seulement une fois le Worker déployé. *Faible*
- [ ] **Bot Discord, article sur le site** : créer le jeton GitHub (`discord-bot/SETUP.md`, partie 9), publier un brouillon
  avec `DRY_RUN=false` et ouvrir la page `notes/<version>.html` en ligne, puis le lien dans l'annonce et le tweet. Vérifier
  aussi que la version arrive en tête de `notes/` et que la pastille « Nouveau » de l'accueil passe dessus. *Faible*
- [ ] **Bot Discord, détection des versions** : bot lancé pendant la sortie de la 0.2.7, le brouillon doit arriver seul dans
  `#validation` dans les 15 minutes (partie 10). *Faible*
- [ ] **Clips, en partie** : codé et testé hors jeu, à voir dans de vraies parties. Multi-kill, Ace et First Blood (le clip
  doit prendre le nom du plus fort, « penta » plutôt que « kill ») ; raccourci de clip (Alt+C par défaut, à activer dans
  Réglages → Clips) en clips courts et en partie entière ; son du PC et micro mélangés ; écran choisi sur un PC à deux écrans ;
  place maximale atteinte pendant une partie entière (les anciennes vidéos partent, pas celle en cours). *Moyenne*
- [ ] **Clips depuis l'historique** : sur une partie filmée après cette version, cliquer un kill du déroulé doit ouvrir le clip
  (ou la partie entière) à ce moment. Vérifié sur ton enregistrement du 17/10 (Sion) par le calcul seulement : le kill à 26:49
  tombe 5 s avant le repère de l'enregistrement. *Faible*
- [ ] **Maîtrises d'un profil consulté** : lues dans le client (`/lol-collections/v1/inventories/{summonerId}/champion-mastery`,
  résumé `top` puis liste complète), codé et testé sans client. À voir sur un vrai profil, client ouvert. *Faible*
- [ ] **Recherche client fermé** (clé Riot) : profil, 20 dernières parties, détail et timeline via l'API Riot, testé avec des
  réponses simulées. À essayer avec une vraie clé, client fermé. *Faible*
- [ ] **Partie en cours, groupes et déjà croisé** : les 10 joueurs viennent de `/lol-gameflow/v1/session` (`teamOne`,
  `teamTwo`, puuid), testé avec une session simulée. Vérifier en vraie partie que les puuid y sont et que les groupes
  repérés sont justes ; et en Draft, que le champion le plus joué des alliés s'affiche sans clé Riot. *Faible*
- [ ] **Profils d'overlay par mode** : régler l'ARAM à part dans Réglages → Overlay, lancer une ARAM puis une partie en
  Faille et vérifier que les blocs changent de place. *Faible*
- [ ] **Données du crawler** (phases de jeu, ouverture en jungle, build Émeraude+, objets 4 à 6 selon l'équipe adverse,
  benchmarks par minute et par serveur, classement de chaque serveur collecté) : codé et testé des deux côtés, mais rien
  n'est publié tant que le démon de `lol-crawler` n'a pas redémarré. Les ouvertures en jungle et les benchmarks par
  minute ne viennent que des timelines récupérées après le redémarrage : vérifier les fichiers publiés après quelques
  jours, puis l'onglet Builds, le panneau Phases de jeu et Jungle de Draft, et la ligne « repère à 15 min » de
  l'overlay. *Faible*
- [ ] **Partager sur Discord** : Ctrl+V dans une conversation après le bouton du lecteur de clip (copie du fichier vérifiée dans
  le presse-papiers Windows, pas le collage dans Discord). *Faible*
- [ ] **Replays** : « Regarder » lance bien le replay depuis le client (liste et état vus sur les vrais replays du PC, pas le
  lancement). *Faible*
- [ ] **Notifications Windows** : partie trouvée, builds d'un nouveau patch (au prochain patch du crawler), nouvelle version
  (à la sortie de la 0.2.7). *Faible*

## 2. Priorité haute

- [ ] **Pages légales du site** (`website/aide/`, contenu dans `discord-bot/src/site/infoPages.js`) : ajouter le téléphone de
  l'hébergeur (GitHub) dans les mentions légales, demandé par la loi française, et faire relire confidentialité, conditions et
  mentions légales. *Faible*
- [ ] **Détail hors connexion** : vérifier en vrai, client League fermé, qu'une partie déjà préchargée s'ouvre (détail, déroulé,
  rapport). Testé en jsdom et la mise en cache vue dans l'app (17 parties, 220 Ko), mais pas l'ouverture client fermé. *Faible*
- [ ] **Note des parties** : les repères de dégâts par poste ne viennent pas du crawler (il ne publie pas les dégâts par
  minute). Les ajouter à `benchmarks.json` pour caler aussi ce critère sur les vraies moyennes. *Faible*
- [ ] **Éditeur de position de l'overlay** au clavier : les blocs ne se déplacent qu'à la souris (flèches à ajouter). *Faible*

## 3. Plus tard (à surveiller)

- [ ] Certificat de signature reconnu pour supprimer l'avertissement Windows SmartScreen (l'empreinte du certificat auto-signé
  est épinglée dans `updateSignature.js` ; avant de le renouveler en octobre 2027, publier une version avec les deux empreintes). *Faible*
- [ ] **Site, pages d'aide** : la FAQ et la confidentialité décrivent ce que fait l'app (stats d'usage, données gardées, services
  contactés, clé Riot). Les mettre à jour à chaque changement de ce côté (`npm run site:pages` puis `tools\push-website.bat`). *Faible*
- [ ] **Site, pied de page en double** : écrit dans `website/index.html` et dans le gabarit `discord-bot/src/targets/websiteArticle.js`
  (notes et aide). Le générer à un seul endroit si on le modifie souvent. *Faible*

## 4. Idées (à trier)

Groupes rangés par intérêt pour le joueur, les idées les plus utiles et les moins chères en haut de chaque groupe.

### Données et builds
- [ ] Revalider les timers d'objectifs à chaque évolution importante du jeu. Vu le 18/10/2026 : Baron à 20:00 confirmé par
  Riot (/dev saison 2026, Atakhan retiré) ; le Héraut est à 14:00 dans `objectiveTimers.js`, une source non officielle dit
  15:00 : à chronométrer en partie avant de changer. *Faible*
