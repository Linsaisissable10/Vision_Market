# Market Watch V3 — PWA multi-marchés

Application web installable sur Android/PC. Elle propose un sélecteur Forex / Crypto / matières premières, un calendrier de démonstration explicitement fictif, les champs réel / consensus / précédent / précédent révisé, des liens vers plusieurs sources, une lecture quantitative explicable et un adaptateur IA côté serveur.

## Important — ce qui est et n'est pas connecté
- Les événements affichés par défaut sont fictifs et servent à montrer l'interface. Ce paquet ne prétend pas fournir des données économiques en direct.
- Forex Factory est proposé comme source consultable. Le projet ne le scrape pas : configure un fournisseur autorisé pour les valeurs réelles, consensus et précédentes. Les sites officiels (BLS, BEA, Fed, BCE, EIA) permettent surtout de vérifier les chiffres publiés.
- L'IA ne fonctionne que lorsque le backend est déployé et qu'une clé privée est configurée côté serveur. GitHub Pages n'exécute pas le backend Node.
- Les actifs sélectionnables sont EUR/USD, GBP/USD, USD/JPY, GBP/JPY, AUD/USD, USD/CAD, USD/CHF, NZD/USD, BTC/USD, ETH/USD, SOL/USD, or, argent, WTI, Brent et gaz naturel. Les flux de prix ne sont pas encore connectés.
- Pas d'exécution d'ordres, pas de promesse de performance, pas de prédiction chiffrée en pips.

## Publier le site statique sur GitHub Pages
1. Décompresse l'archive et ouvre le dossier `eurusd_watch_v2`.
2. Dans le dépôt GitHub, remplace les fichiers du site par `index.html`, `styles.css`, `app.js`, `manifest.json`, `sw.js`, `icon.svg` et `README.md` (ils doivent être à la racine du dépôt). Tu peux aussi déposer le dossier `backend`.
3. Dans Settings → Pages, choisis `Deploy from a branch`, la branche `main`, le dossier `/(root)`, puis Save.
4. Attends le lien HTTPS publié par GitHub Pages puis ouvre-le dans Chrome Android et choisis `Installer l'application` ou `Ajouter à l'écran d'accueil`.

## Activer l'IA (déploiement backend séparé)
Voir `backend/README.md`. Déploie le backend sur un hébergeur Node compatible HTTPS, configure la clé API dans les variables privées de cet hébergeur et indique son URL HTTPS dans `API_BASE` au début de `app.js`. Ne mets jamais une clé API dans GitHub Pages.

## Données économiques
Pour les données live, configure `CALENDAR_API_URL` côté backend vers un fournisseur qui autorise l'usage et fournit un schéma compatible. La simple présence d'une URL ne garantit pas que les champs soient normalisés : mapper explicitement `date`, `country`, `name`, `impact`, `forecast`/`consensus`, `actual`, `previous`, `revised_previous`, `source` et `url`. Les prévisions consensuelles sont généralement fournies par un service spécialisé, pas par les organismes statistiques officiels.
