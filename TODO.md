# Trackr — TODO

Version actuelle : **0.2.1** (la 0.2.2 est prête : `package.json` et `CHANGELOG.md` à jour, reste à publier). Priorité = valeur produit et fiabilité. Difficulté = estimation, pas une durée garantie.

## À vérifier en priorité

- [ ] **Publier la 0.2.2** : `npm test`, `npm run release`, publier le brouillon GitHub, puis tester une **vraie mise à jour
  en un clic** depuis la 0.2.1 (le bouton doit télécharger, fermer Trackr, installer et relancer). *Faible*
- [ ] Overlay en **plein écran exclusif** : toujours invisible sur l'écran du jeu (injection interdite). Contournement ajouté :
  Trackr s'ouvre sur un second écran au lancement de la partie (Réglages → Partie en cours → Écran). À valider en réel
  avec deux écrans. *Moyenne*
- [ ] Écrans multiples, résolutions variables et changements de fenêtre pendant une session (l'overlay couvre la zone de
  travail de l'écran principal, sans la barre des tâches). *Moyenne*

## Priorité haute

- [ ] Stats d'usage : au-delà de ~200 utilisateurs actifs par jour, la limite d'écriture du plan gratuit KV est
  atteinte (passer à un ping par jour ou au plan payant) ; ajouter une protection contre les faux pings. *Faible*
- [ ] **Rapport de fin de partie actionnable** : comparer ton build et tes runes au build le plus joué
  du champion. *Moyenne*
- [ ] Diagnostics de dépannage Riot / LCU / fichiers manquants : messages explicites, retry ciblés. *Moyenne*
- [ ] Benchmarks par durée de partie ou par minute, en plus des moyennes de fin de partie. *Élevée*
- [ ] Événements multi-kill, Ace et First Blood dans les noms et filtres de clips. *Moyenne*
- [ ] Revalider les timers d'objectifs à chaque évolution importante du jeu. *Faible*

## Builds et données

- [ ] Choix de la plateforme et du rang dans l'onglet Builds ; ajouter Emerald+ pour plus de volume. *Moyenne*
- [ ] Builds par patch, avertissement si les stats ont plus d'un patch, mention « peu fiable » sous le seuil. *Faible*
- [ ] **Matchups** : runes et objets conseillés selon l'adversaire de lane. *Élevée*
- [ ] **Builds situationnels** : objets 4–6 selon l'équipe adverse (AP/AD, tanks, soins). *Élevée*
- [ ] Suivi du pipeline : taille de `build-state.json`, parties par champion, alerte après plusieurs échecs. *Faible*

## Priorité moyenne

- [ ] Suivi manuel des sorts d'invocateur ennemis avec compte à rebours. *Moyenne*
- [ ] Raccourcis clavier globaux (afficher/masquer l'overlay, démarrer un clip). *Moyenne*
- [ ] Notifications Windows : partie trouvée, build mis à jour, nouvelle version. *Faible*
- [ ] Rich Presence : bouton « rejoindre » (pas fait : il faut relayer une invitation de lobby via le client League, jugé trop fragile). *Faible*
- [ ] Profils d'overlay distincts selon le mode de jeu. *Élevée*
- [ ] Partage de clips vers Discord et conversion MP4 optionnelle. *Élevée*
- [ ] Capture audio et choix de l'écran pour les clips et l'overlay. *Élevée*
- [ ] Support d'autres régions dans l'app (profil, benchmarks, builds). *Moyenne*
- [x] Traduction de l'interface (anglais), sélecteur Langue / Language dans Réglages → Application, changement à chaud

## Priorité basse

- [ ] Certificat de signature reconnu pour supprimer l'avertissement Windows SmartScreen. *Faible*

## Terminé

### Application
- [x] Logo de la barre des tâches : problème côté Windows (cache d'icônes), réglé, rien à changer dans le code.
- [x] **Mise à jour en un clic** : le bouton cherche, télécharge, ferme Trackr, installe et relance sans second clic
  (annulé en cas d'erreur, ignoré en développement). À valider en réel.
- [x] **Trackr sur un second écran en partie** : choix de l'écran dans Réglages → Partie en cours, Trackr s'ouvre dessus
  au lancement de la partie sans prendre le focus. À valider avec deux écrans.
- [x] `build-automation/` : la collecte ne tourne plus dans le vide quand il n'y a plus de nouvelles parties (test passé de
  60 s à quelques ms, plus aucun appel Riot inutile en production).
- [x] Dépendances : jsdom ajouté en devDependency, `npm audit --omit=dev` sans vulnérabilité.
- [x] Worker de télémétrie déployé (`npx wrangler deploy`) et nouveau tableau de bord vérifié (5 onglets, Workflows).
- [x] Après le refactor : app parcourue en réel (accueil, clips, builds, fin de partie, overlay, réglages), sans régression.
- [x] Secrets du `.env` partagé changés (Riot, GitHub, jeton admin du Worker).
- [x] **Rich Presence** : le mode de jeu s'affiche en file, en sélection et en partie (ex. « En file d'attente · Classée
  Solo/Duo »). Le rang n'est volontairement jamais affiché.
- [x] **Tests d'interface** sur Live, Accueil/historique, Fin de partie et Clips (jsdom, 27 tests, ignorés si `npm install`
  n'a pas été fait).
- [x] **Aide aux compétences** : au level up, la compétence à monter brille sur la barre de sorts (ordre le plus joué du
  champion, ultime aux niveaux 6/11/16), position réglable et testable. Validée en vraie partie.
- [x] **Réglages réorganisés** en 7 catégories avec menu latéral (Général, Compte, Overlay en jeu, Partie en cours,
  Automatisation, Clips, Données et infos), dernière catégorie mémorisée.
- [x] **Tableau de bord de télémétrie refait** : 5 onglets (vue d'ensemble, utilisateurs, produit, releases, workflows),
  rétention, engagement, cycle de vie, cohortes, santé du pipeline, thème clair/sombre.
- [x] **Refactor complet** sans commentaires : code formaté, doublons retirés, `home.js` découpé, tests et rendu identiques.
- [x] Historique de l'accueil : filtres par file, « Voir plus », archive locale (300 parties par compte), parties perso exclues.
- [x] Gestion des erreurs 429 de l'API Riot (pause et limite de concurrence).
- [x] Statistiques d'usage anonymes (désactivables) + tableau de bord privé sur Cloudflare Workers (déployé et vérifié) :
  utilisateurs actifs, versions, options, téléchargements, état des workflows.
- [x] Icônes de champion des clips fiabilisées (joueur retrouvé par Riot ID, fiche complétée en début de partie, image de secours).
- [x] Bruit de logs supprimé : l'API de jeu répond 404 avant le début de partie, ce n'est plus loggé comme une erreur.
- [x] Clips et Fin de partie rangés par compte : filtre par compte dans Clips, sélecteur de compte dans Fin de partie,
  registre des comptes détectés. Les anciens clips sont classés « Compte inconnu ». À valider avec deux comptes.
- [x] Détection du client League, état d'attente, profil, rang Solo/Duo et Flex (bascule animée).
- [x] Champ select et partie en cours : équipes, rangs, maîtrises, runes, statistiques.
- [x] Ouverture de la bonne vue selon la phase, sans reprendre l'onglet à l'utilisateur.
- [x] Fin de partie, historique filtrable (session, champion, file, résultat), comparaison de sessions.
- [x] Overlay configurable : CS/min, gold/min, KP, vision/min, timers d'objectifs.
- [x] Gold diff précis avec les prix réels Data Dragon.
- [x] Clips : capture et bibliothèque ; correctif `clipboard.writeImage()` sous Electron 44.
- [x] Profil joueur : avatar, badges de rang, animations ; écussons redimensionnés.
- [x] Réglages : état du client, compte, version, date et patch des benchmarks.
- [x] Splash avec avancement et attente du client.

### Builds et automatisation
- [x] Champ select : carte « Importer les runes / Créer le set d'objets / Tout importer » dès que ton champion
  est verrouillé (rôle détecté, build le plus joué en haut elo). À valider en réel.
- [x] Pipeline de builds : run complet avec les seuils par défaut (25 / 15 parties).
- [x] Set d'objets (boutique en partie) et alerte de tilt testés avec un vrai client League.
- [x] Site `trackr-website` mis à jour et poussé, captures de l'onglet Builds ajoutées.
- [x] Onglet Builds façon u.gg : rôles, pick/win rate, niveaux 1–18, runes, objets, sorts.
- [x] Refonte de l'onglet : mur de champions avec recherche et récents, bannière, taux de victoire animé.
- [x] Import des runes (manuel et automatique, sans écraser les pages du joueur) et création du set d'objets.
- [x] Auto-accept de la partie trouvée, sans écraser une réponse manuelle (testé avec un vrai client).
- [x] Import des runes testé avec un vrai client League (pages recommandées et page « Trackr »).
- [x] Pipeline GitHub Actions des builds (Match-V5 + timeline), toutes les 8 h, publication robuste avec retry ; premier run réussi, stats publiées sur `gh-pages` et affichées dans l'onglet Builds.
- [x] Benchmarks Master+ par rôle publiés sur `gh-pages` et mis en cache localement.

### Confort et fiabilité
- [x] Release 0.1.9 publiée (signature avec retry, création de la release GitHub).
- [x] Discord Rich Presence : phase, champion, chronomètre, version, bouton vers le site (testé en réel).
- [x] Alerte de tilt (notification et bandeau en fin de partie), désactivable.
- [x] Export / import des réglages, avec validation du fichier.
- [x] Release de production : signature Windows (avec retry), auto-update, logs de diagnostic,
  checklist `RELEASE_CHECKLIST.md`.
- [x] Tests : transitions de phase, IPC, benchmarks, réglages, tilt, builds, UI du dashboard.
- [x] Site `trackr-website` : fonctionnalités, Builds et guide d'installation.
- [x] Documentation d'installation et README.