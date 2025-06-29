# 📄 Google SSO Integration for Self-Hosted Sentry (Docker Compose)

## 📑 Overview

This document outlines the step-by-step process to enable **Google Single Sign-On (SSO)** for a **self-hosted Sentry instance deployed via Docker Compose**. The integration uses OAuth2 via Google Cloud and Sentry’s social authentication backend.

---

## 📌 Prerequisites

- A working self-hosted Sentry instance (Docker Compose-based).
- Access to [Google Cloud Console](https://console.cloud.google.com/apis/credentials) to create OAuth credentials.
- Permissions to modify `config.yml`, `sentry.conf.py`, and restart Docker containers.

---

## ✅ Setup Process

### 1️⃣ Create Google OAuth Credentials

1. Visit [Google Cloud Console](https://console.cloud.google.com/apis/credentials).
2. Create a new project (or use an existing one).
3. Go to **APIs & Services → Credentials**.
4. Click **Create Credentials → OAuth Client ID**.
5. Select **Web application**.
6. Add the following redirect URI:
    "https://sentey.getnitro.co.in/auth/sso/"
7.Save the generated Client ID and Client Secret — you’ll need them in later steps.

### Configure Sentry for Google SSO
Sentry uses the "social-auth-app-django" backend internally for social logins. Configuration is done via "config.yml" and "sentry.conf.py".

📄 Update config.yml

In your self-hosted Sentry repository directory, edit the sentry/config.yml file:
    auth.providers:
              - google

📄 Update sentry.conf.py

Open sentry/sentry.conf.py and add or update the following configurations:

from sentry.conf.server import *

SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = '<your-client-id>'
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = '<your-client-secret>'
SOCIAL_AUTH_GOOGLE_OAUTH2_SCOPE = ['email']
SOCIAL_AUTH_GOOGLE_OAUTH2_WHITELISTED_DOMAINS = ['yourdomain.com']  # Optional

AUTHENTICATION_BACKENDS = (
    'social_core.backends.google.GoogleOAuth2',
    *AUTHENTICATION_BACKENDS,
)

### 3️⃣ Rebuild and Restart Sentry

After applying the configuration changes:

# Navigate to your self-hosted sentry directory
cd /path/to/sentry-self-hosted

# Stop containers
docker-compose down

# Build containers to pick up config changes
docker-compose build

# Start containers in detached mode
docker-compose up -d



