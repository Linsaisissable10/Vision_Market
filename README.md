# Market Watch — Analyste V5.2

## Ce qui change
- Interface réorganisée en Vue d'ensemble, Calendrier, Analyste, Data & sources, Contexte & structure, Réglages.
- Calendrier plus large, filtres d'impact/zone/recherche/période, inspecteur latéral, précédent/consensus/réel/révision si fournis.
- Moteur analytique spécialisé **local et explicable**, sans API de génération de texte : surprise réel vs consensus, catégorisation de certains indicateurs macro, mapping de la devise publiée à la paire, confluence avec le contexte structurel saisi et signalement des données manquantes/conflits.
- Parcours événementiel : cliquer sur une publication dans le calendrier ouvre son inspecteur; le bouton « Analyser avec MW » lance ensuite l’analyse. Le formulaire de publication manuelle a été retiré de l’écran Analyste.
- Aucun événement de démonstration, aucun prix inventé. Si un fournisseur est indisponible, l'interface l'indique.
- Backend `/api/analyze` utilise aussi des règles et n'appelle pas d'API d'IA externe.

## Important sur le mot « IA »
Cette V5 est un système expert/règles métier, pas un grand modèle de langage et pas encore un modèle prédictif entraîné sur les données historiques. C'est volontaire : elle est explicable et gratuite à exécuter. Pour une vraie modélisation statistique, il faut collecter un historique horodaté (surprises macro, prix, spreads, taux, volatilité), définir une cible, entraîner puis évaluer hors-échantillon et éviter les fuites de données. Les scores actuels ne sont pas des probabilités et ne sont pas calibrés.

## Sources
- Calendrier : Helious Economic Calendar (`https://api.helious.io/v1/calendar`). Les champs et la fraîcheur dépendent du fournisseur, de ses quotas et de son offre. Le calendrier peut être indisponible; aucun fallback fictif n'est utilisé.
- Forex : Frankfurter, taux de référence quotidiens, pas de flux intraday ni de bid/ask.
- Crypto : endpoint public CoinGecko; quotas et fraîcheur dépendent de l'accès. Optionnel `COINGECKO_DEMO_API_KEY` côté serveur.
- Matières premières : pas de prix de marché connectés dans cette version.
- Forex Factory : lien pour consultation manuelle, pas de scraping ni d'import non autorisé.

## GitHub Pages + backend
GitHub Pages sert uniquement le frontend. Il ne lance pas Node.js.
1. Déployer le dossier `backend` sur un hébergeur Node compatible.
2. Variables facultatives sur le serveur : `ALLOWED_ORIGIN`, `COINGECKO_DEMO_API_KEY`, `PORT`.
3. Dans `config.js`, définir `window.MARKET_WATCH_API_BASE = 'https://URL-DU-BACKEND';`.
4. Mettre à jour le site GitHub Pages. Ne jamais ajouter un `.env` avec des secrets au dépôt.
5. Tester `https://URL-DU-BACKEND/health`, `/api/events?days_ahead=7`, `/api/markets`.

## Démarrage local
- `cd backend && npm install && npm start`
- Servir le dossier parent avec un serveur statique local et mettre `config.js` sur `http://localhost:8787`.

## Limites
- Les données de calendrier peuvent être retardées, limitées ou absentes; vérifie les sources officielles.
- La saisie de contexte structurel est manuelle et n'est pas une lecture automatique du graphique.
- Les règles de sémantique ne couvrent pas tous les indicateurs et ne remplacent pas une validation empirique.
- Aucun prix cible, probabilité prédictive ou amplitude en pips n'est fournie.


## Utilisation de l’analyse d’un événement
1. Ouvrir **Calendrier**.
2. Cliquer sur la ligne d’une publication. Son inspecteur s’ouvre à droite (ou sous la liste sur mobile).
3. Vérifier précédent, consensus, réel, source et horodatage.
4. Cliquer sur **Analyser avec MW →**. L’application ouvre l’espace Analyste et affiche les faits, le biais conditionnel, les scénarios et les données manquantes.

## Héberger le backend (à faire une seule fois)
Le backend est un serveur Node.js distinct : GitHub Pages ne l’exécute pas. Sur un hébergeur compatible Node.js, créer un nouveau service depuis le dépôt GitHub `Vision_Market`, en indiquant le dossier racine `backend` comme **Root Directory**, la commande de build `npm install` et la commande de démarrage `npm start`. Le service doit fournir une URL HTTPS publique. Ensuite, dans l’application, ouvrir **Réglages**, coller cette URL dans le champ API backend, puis enregistrer. Tester d’abord `/health`, puis `/api/events?days_ahead=7` et `/api/markets`.

Le moteur MW n’appelle aucune API d’IA générative et ne nécessite donc aucune clé OpenAI. Les fournisseurs de données externes peuvent néanmoins appliquer des quotas, retards ou changements d’API. Les cours de matières premières restent indisponibles tant qu’un fournisseur adapté n’est pas connecté.
