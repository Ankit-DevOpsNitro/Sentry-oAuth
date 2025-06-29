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

