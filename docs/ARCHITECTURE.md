# System Architecture

## Overview

Use a modular Django monolith for the MVP. This keeps deployment and
debugging simpler than starting with microservices.

``` text
Browser
  |
  | HTTPS
  v
Django views / forms / optional DRF API
  |
  +---- Authentication and authorization
  +---- Resume domain services
  +---- Template rendering
  +---- Upload and parsing service
  +---- ATS analysis service
  +---- AI integration service
  +---- PDF export service
  |
  +---- PostgreSQL
  +---- Private file/object storage
  +---- AI provider API
  +---- Optional Redis/Celery workers
```

## Django app boundaries

-   `accounts`: profile, account settings, deletion workflow.
-   `resumes`: resume data, versions, editor forms, template rendering.
-   `documents`: upload validation, extraction, import review, PDF
    export.
-   `jobs`: job descriptions and application tracker.
-   `ats`: keyword analysis, formatting checks, reports.
-   `cover_letters`: generation and saved letters.
-   `ai_services`: prompts, provider client, response validation,
    quotas.
-   `billing`: subscription and usage plans, introduced when needed.

## Request flow

1.  Browser sends a request to a Django URL.
2.  Middleware handles session, CSRF, and request security.
3.  View validates the request and authenticates the user.
4.  A service function applies business rules and checks ownership.
5.  The ORM reads or writes records.
6.  Templates or JSON serializers produce a response.
7.  Long-running parsing or AI operations may be queued when a task
    queue is configured.

## Architectural principles

-   Keep business rules out of large view functions.
-   Use Django Forms or serializers for validation.
-   Use service modules for AI, parsing, ATS scoring, and PDF
    generation.
-   Use transactions for multi-record updates.
-   Treat AI and uploaded text as untrusted input.
-   Avoid coupling resume content to a specific visual template.
-   Use feature flags or settings to disable external AI calls during
    tests.
-   Add asynchronous workers only when task duration or traffic
    justifies them.

## Rendering strategy

Store a canonical structured resume representation. Each template maps
that representation to HTML and CSS. The PDF service renders the same
template or a dedicated print variant. Test page breaks, font embedding,
Unicode, links, and text extraction.

## Deployment topology

For the first release: - One Django web service. - Managed PostgreSQL. -
Private object storage for uploads. - External AI provider called
server-side. - Optional Redis/Celery workers for background jobs. -
HTTPS termination at the hosting platform or reverse proxy.
