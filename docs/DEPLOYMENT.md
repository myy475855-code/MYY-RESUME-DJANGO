# Deployment Guide

This is a deployment checklist. Exact commands depend on the chosen host
and package versions.

## Environments

Maintain separate development, test, and production settings. Do not use
production data in development unless it has been appropriately
anonymized.

## Required production configuration

Typical environment variables:

``` text
DJANGO_SETTINGS_MODULE=config.settings.production
DJANGO_SECRET_KEY=<strong-secret>
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=example.com
DATABASE_URL=<managed-postgres-url>
OPENAI_API_KEY=<server-side-secret>
DEFAULT_FROM_EMAIL=<verified-sender>
```

Use a secrets manager where available. Never commit real values to Git.
Parse environment variables safely and fail startup if required
production settings are missing.

## Database

-   Provision managed PostgreSQL.
-   Configure encrypted connections where supported.
-   Use least-privilege credentials.
-   Run migrations as a controlled release step.
-   Back up the database and test restoration.
-   Monitor connection limits and query performance.

## Static files and uploads

-   Collect and serve static assets through the hosting platform or a
    suitable static server/CDN.
-   Store private user uploads in private object storage.
-   Do not rely on a public static directory for private resumes.
-   Use expiring, access-controlled links for downloads where supported.
-   Configure deletion and retention policies.

## Application server

-   Run Django with a production WSGI or ASGI server.
-   Configure HTTPS, secure cookies, allowed hosts, and trusted origins.
-   Set request and upload size limits.
-   Configure timeouts appropriate for web requests.
-   Move slow parsing and AI work to background jobs if it exceeds web
    request limits.

## Pre-launch checks

1.  Install production dependencies.
2.  Set production environment variables.
3.  Run database migrations.
4.  Run `python manage.py collectstatic`.
5.  Run `python manage.py check --deploy`.
6.  Run automated tests.
7.  Verify login, resume CRUD, file upload, PDF export, and account
    deletion.
8.  Verify logs and error monitoring.
9.  Verify backups and restoration procedures.
10. Test from a non-admin account.

## Monitoring

Monitor: - HTTP error rates and latency. - Database availability and
query latency. - Upload and PDF generation failures. - AI latency,
errors, and estimated costs. - Queue length if background jobs are
used. - Storage growth and deletion failures.

Avoid logging full resume content, passwords, tokens, or provider
secrets.
