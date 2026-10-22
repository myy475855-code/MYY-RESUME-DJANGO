# Django Project Structure

## Recommended layout

``` text
resume_creator/
├── manage.py
├── config/
│   ├── __init__.py
│   ├── settings/
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── development.py
│   │   └── production.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── apps/
│   ├── accounts/
│   ├── resumes/
│   ├── documents/
│   ├── jobs/
│   ├── ats/
│   ├── cover_letters/
│   └── ai_services/
├── templates/
│   ├── base.html
│   ├── accounts/
│   ├── dashboard/
│   ├── resumes/
│   ├── templates_gallery/
│   ├── ats/
│   ├── cover_letters/
│   └── jobs/
├── static/
│   ├── css/
│   ├── js/
│   └── images/
├── media/                 # Development only; production files use private storage
├── tests/
├── requirements/
│   ├── base.txt
│   ├── development.txt
│   └── production.txt
├── .env.example
└── README.md
```

## Suggested app responsibilities

### `accounts`

-   Profile model.
-   Account settings and deletion workflow.
-   Registration and authentication views.

### `resumes`

-   Resume and ResumeVersion models.
-   Forms for personal details and repeatable sections.
-   Resume ownership checks.
-   Template selection and preview.
-   Dashboard list and resume CRUD.

### `documents`

-   Upload model and upload forms.
-   File validation and text extraction.
-   Import review flow.
-   PDF export service.

### `jobs`

-   JobDescription and JobApplication models.
-   Tracker views, filters, status changes, and follow-up dates.

### `ats`

-   Deterministic checks and keyword matching.
-   Report model and report UI.
-   Optional AI-assisted semantic analysis.

### `cover_letters`

-   CoverLetter model.
-   Editing and export views.
-   Service to request AI drafts.

### `ai_services`

-   Provider client.
-   Prompt templates.
-   Structured response validation.
-   Timeouts, usage limits, retries, and error normalization.

## Coding guidelines

-   Keep views small; move complex logic into `services.py` modules.
-   Use `select_related` and `prefetch_related` to avoid unnecessary
    queries.
-   Use UUIDs for externally referenced records where appropriate, but
    always check ownership.
-   Use Django Forms for server-rendered forms.
-   Add DRF only when an API is genuinely needed.
-   Use named URL patterns and reverse URLs instead of hard-coded paths.
-   Store configuration in environment variables.
-   Create the custom user model before running the first production
    migration if one is required.
