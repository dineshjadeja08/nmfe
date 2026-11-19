# NammaPros frontend

This repository contains the customer web app (`apps/web`), admin app (`apps/admin`), and the shared packages they use. The API, mobile app, database credentials, and backend deployment files are in the separate backend repository.

## Local setup

Use Node.js 22 and npm 10. Run `npm ci` at the repository root. Copy each app's `.env.example` to `.env.local` for local development. The Firebase App Hosting configurations contain the public production API and Firebase client settings.

- `npm run build:web` builds the customer app.
- `npm run build:admin` builds the admin app.

## Firebase App Hosting

Connect this GitHub repository to two App Hosting backends in the existing Firebase project `nammapro-api`, using branch `main` and automatic rollouts:

| Backend | Root directory |
| --- | --- |
| Customer web | `apps/web` |
| Admin | `apps/admin` |

Each app has its own `package-lock.json` and `apphosting.yaml` because App Hosting installs dependencies from the selected app root. Set `NEXT_PUBLIC_SITE_URL` for the customer app to its final HTTPS domain before launch. Allow the deployed frontend domains in the API's CORS and CSRF settings. Firebase Phone Authentication also requires the provider and authorized domains in Firebase and backend verification to be enabled before customer OTP login can work; the current backend has phone auth disabled.

Do not add private keys or database URLs to `NEXT_PUBLIC_*` variables or commit `.env` files.

