# Trackr : TODO

Version publiée : **0.2.7** (18/10/2026 : contre-picks dans Draft en direct, pages Esport, Champions, Matchups et
Replays, rapport de la partie, clips au raccourci et partage sur Discord, progression et objectif dans le Tableau de bord).
Prochaine version : **0.2.8** (overlay en classée Solo/Duo et Flex seulement). Ce qui
est sorti est décrit dans `CHANGELOG.md`, ce fichier ne garde que ce qui reste à faire. Priorité = valeur produit et fiabilité.
Difficulté = estimation, pas une durée garantie.

Rangé du plus important au moins important : d'abord les priorités, puis le reste. Dans chaque section, le plus important est en haut.
Avant de publier la 0.2.8 : vérifier en partie que l'overlay s'affiche en Solo/Duo et en Flex, et reste caché en normale et en ARAM.

## 1. Priorité haute

- [ ] **Mentions légales, téléphone de l'hébergeur** (`discord-bot/src/site/infoPages.js`, section Hébergement) : la loi
  française le demande, mais GitHub ne publie aucun numéro officiel (ses conditions disent « pas de support téléphonique »)
  et les annuaires en donnent plusieurs différents. À ajouter seulement avec une source sûre. Relecture de la
  confidentialité, des conditions et des mentions légales faite le 19/10/2026. *Faible*

## 2. Plus tard (à surveiller)

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
