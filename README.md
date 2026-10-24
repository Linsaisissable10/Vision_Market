# Market Watch V4 — données réelles, sans démo

## Important
Cette version ne crée aucun événement de démonstration. Si un fournisseur échoue, l'interface affiche « indisponible » au lieu de valeurs fictives.

## Sources branchées dans le backend
- **Calendrier économique : Helious API** (`https://api.helious.io/v1/calendar`). La documentation annonce un accès sans clé, précédent/prévision/réel, mais le niveau sans clé est retardé d'environ une heure et limité à 50 crédits/mois partagés par adresse réseau. Un compte gratuit annoncé donne 100 crédits/mois et 7 jours d'historique; une demande `fresh=1` consomme 5 crédits selon leur documentation. Vérifier leurs conditions avant usage prolongé.
- **Forex : Frankfurter API v2**. Taux de référence quotidiens provenant de banques centrales/sources officielles, gratuits sans clé. Ce ne sont PAS des cotations intraday, bid/ask ou CFD adaptées à l'exécution/scalping.
- **Crypto : CoinGecko API**. Endpoint public essayé sans clé; peut être limité. Optionnel : `COINGECKO_DEMO_API_KEY` gratuite, soumise aux quotas et conditions du fournisseur.
- **Matières premières : pas encore de flux de cours branché.** L'application l'indique explicitement. Il faut choisir un fournisseur couvrant réellement or/argent/WTI/Brent/gaz, avec ses propres limites et conditions.
- **IA : OpenAI Responses API**, optionnelle, avec clé gardée uniquement dans le `.env` du backend. Sans clé ou sans backend, aucune analyse IA distante n'est prétendue active.

## Déploiement local
1. `cd backend`
2. `npm install`
3. Copie `.env.example` vers `.env`, puis renseigne `OPENAI_API_KEY` si tu veux l'analyse IA. Ne publie jamais `.env`.
4. `npm start` (port 8787 par défaut).
5. Sers le frontend depuis le dossier parent sur localhost et garde `config.js` avec `MARKET_WATCH_API_BASE = 'http://localhost:8787'` pour tester.

## Déploiement public
GitHub Pages héberge seulement les fichiers statiques, il n'exécute pas `backend/server.js`. Déploie `backend/` sur un hébergeur Node compatible (par exemple Render ou Railway), configure les variables d'environnement dans le tableau de bord du service, puis modifie `config.js` :
`window.MARKET_WATCH_API_BASE = 'https://URL-DE-TON-BACKEND';`
Commite ensuite `config.js` et les fichiers frontend sur GitHub Pages. Configure `ALLOWED_ORIGIN` avec l'origine GitHub Pages exacte pour limiter le CORS. N'ajoute aucune clé API à `config.js`.

## Limites fonctionnelles actuelles
- Pas de scraping Forex Factory : on n'extrait pas son site sans API/licence vérifiée.
- Le fournisseur de calendrier Helious peut être retardé d'une heure sur les offres gratuites. Le nombre d'événements dépend de sa couverture et de son quota.
- Frankfurter est quotidien, pas temps réel.
- Crypto dépend des quotas CoinGecko; matières premières en attente d'un fournisseur.
- Les données réelles ne garantissent pas que l'impact sur le prix soit prévisible. L'IA doit recevoir la donnée et son horodatage et peut signaler les limites; aucun rendement/pips n'est garanti.
- Les notifications locales ne sont pas des push fiables lorsque l'app est fermée.
