# Market Watch V4 backend

Node.js 20+ conseillé. GitHub Pages ne lance pas ce serveur : il faut un hébergeur Node séparé.

## Endpoints
- `GET /health` : état de configuration.
- `GET /api/events?days_back=1&days_ahead=7` : calendrier réel Helious; renvoie `unavailable` en cas d'échec, sans données de remplacement.
- `GET /api/markets` : taux de référence quotidiens Frankfurter + prix crypto CoinGecko. Les matières premières sont marquées indisponibles tant qu'aucun fournisseur n'est configuré.
- `POST /api/analyze` : analyse IA OpenAI (clé serveur uniquement).

## Configuration
Copier `.env.example` en `.env`. Renseigner `OPENAI_API_KEY` si l'analyse IA est voulue. `COINGECKO_DEMO_API_KEY` est facultative. Définir `ALLOWED_ORIGIN` à l'origine exacte du frontend en production.

Ne jamais commiter `.env` ni publier une clé. La clé gratuite CoinGecko peut être obtenue sur le portail développeur officiel; les quotas et conditions peuvent changer.
