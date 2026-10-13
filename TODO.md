# Trackr — TODO

Version actuelle : **0.1.9**. Priorité = valeur produit et fiabilité. Difficulté = estimation, pas une durée garantie.

## À vérifier en priorité

- [ ] Release 0.1.9 : corriger la création de release GitHub (erreur 422 « valid tag »), publier, puis
  tester une **vraie mise à jour** 0.1.8 → 0.1.9. *Moyenne*
- [ ] Pipeline de builds : premier run complet avec les seuils par défaut (25 / 15 parties),
  `builds/<id>.json` présent sur `gh-pages`, affichage dans l'onglet Builds. *Faible*
- [ ] Tester avec un vrai client League : **création du set d'objets** (boutique en partie),
  import automatique des runes au champ select, alerte de tilt en situation réelle. *Faible*
- [ ] Pousser le site mis à jour (`trackr-website`) et ajouter les captures de l'onglet Builds. *Faible*
- [ ] Écrans multiples, résolutions variables et changements de fenêtre pendant une session. *Moyenne*

## Priorité haute

- [ ] **Rapport de fin de partie actionnable** : comparer ton build et tes runes au build le plus joué
  du champion. *Moyenne*
- [ ] **Proposition automatique au champ select** : page de runes et set d'objets du rôle détecté,
  confirmation en un clic. *Moyenne*
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
- [ ] Rich Presence : rang en option, état « en file » avec le mode, bouton de rejoindre. *Faible*
- [ ] Profils d'overlay distincts selon le mode de jeu. *Élevée*
- [ ] Partage de clips vers Discord et conversion MP4 optionnelle. *Élevée*
- [ ] Capture audio et choix de l'écran pour les clips et l'overlay. *Élevée*
- [ ] Support d'autres régions dans l'app (profil, benchmarks, builds). *Moyenne*
- [ ] Traduction de l'interface (anglais). *Moyenne*

## Priorité basse

- [ ] Étendre les tests d'interface aux autres onglets (live, historique, clips). *Moyenne*
- [ ] Certificat de signature reconnu pour supprimer l'avertissement Windows SmartScreen. *Faible*

## Terminé

### Application
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
- [x] Onglet Builds façon u.gg : rôles, pick/win rate, niveaux 1–18, runes, objets, sorts.
- [x] Refonte de l'onglet : mur de champions avec recherche et récents, bannière, taux de victoire animé.
- [x] Import des runes (manuel et automatique, sans écraser les pages du joueur) et création du set d'objets.
- [x] Auto-accept de la partie trouvée, sans écraser une réponse manuelle.
- [x] Pipeline GitHub Actions des builds (Match-V5 + timeline), toutes les 8 h, publication robuste avec retry.
- [x] Benchmarks Master+ par rôle publiés sur `gh-pages` et mis en cache localement.

### Confort et fiabilité
- [x] Discord Rich Presence : phase, champion, chronomètre, version, bouton vers le site.
- [x] Alerte de tilt (notification et bandeau en fin de partie), désactivable.
- [x] Export / import des réglages, avec validation du fichier.
- [x] Release de production : signature Windows (avec retry), auto-update, logs de diagnostic,
  checklist `RELEASE_CHECKLIST.md`.
- [x] Tests : transitions de phase, IPC, benchmarks, réglages, tilt, builds, UI du dashboard.
- [x] Site `trackr-website` : fonctionnalités, Builds et guide d'installation.
- [x] Documentation d'installation et README.