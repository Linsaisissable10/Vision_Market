# EUR/USD Watch V2 — mobile-first
## Sur Windows
Décompresse l'archive, ouvre PowerShell dans le dossier contenant `index.html`, puis lance `py -m http.server 8000` (ou `python -m http.server 8000`). N'ajoute pas `bash` devant la commande. Ouvre http://localhost:8000.
## Sur téléphone
Pour l'installer sur un vrai téléphone, héberge le dossier en HTTPS (GitHub Pages, Cloudflare Pages ou Netlify selon les conditions du service), puis ouvre l'URL sur le téléphone. Android/Chrome : menu ⋮ puis Installer/Ajouter à l'écran d'accueil. iPhone/Safari : Partager puis Sur l'écran d'accueil. Autorisations propres à chaque appareil.
## Inclus
Interface mobile-first, onglets événements/analyse/saisie/réglages, tentative de connexion au calendrier public, exemples fictifs en secours, règles quantitatives explicables, liens source, notifications locales, PWA et cache.
## Limites
IA non connectée; backend/ contient un squelette uniquement. Pas de collecte continue de news géopolitiques. Les notifications de rappel sont côté client et ne sont pas fiables lorsque l'app est fermée. Pas d'amplitude en pips sans backtest. La connexion au calendrier doit être vérifiée : si l'API échoue, l'app bascule en démo.
## Architecture cible
PWA → backend sécurisé → calendrier/news → moteur quantitatif → IA serveur → historique/backtests → Web Push. Aucune exécution d'ordre. Une clé API reste côté serveur.
