# AI-Powered Resume Creator

A Django-based resume creation platform for students, job seekers,
freelancers, and experienced professionals. Users can create resumes,
choose templates, import existing resumes, improve content with AI,
analyze resume-to-job-description alignment, generate cover letters,
export PDFs, and track job applications.

## Product goals

-   Make professional resume creation accessible to non-designers.
-   Help users tailor truthful resumes to specific job descriptions.
-   Provide transparent resume checks rather than guaranteeing ATS
    success.
-   Keep personal data and uploaded documents private.
-   Validate the product with a focused MVP before expanding.

## Core features

1.  Authentication and user dashboard.
2.  Structured resume editor with live preview.
3.  Three to five resume templates.
4.  PDF export.
5.  PDF/DOCX resume upload and parsing.
6.  AI-assisted summaries and achievement bullets.
7.  Resume/job-description keyword and formatting analysis.
8.  Cover letter generation and editing.
9.  Job application tracker.
10. Resume duplication, version history, and account deletion.

## Recommended stack

-   Python 3.12+
-   Django 5.2 LTS or another currently supported Django release
-   Django templates for the initial server-rendered UI; add
    HTMX/Alpine.js or a React frontend later if needed
-   PostgreSQL
-   Django authentication and permissions
-   Django REST Framework only if a separate API is needed
-   Celery + Redis for long-running document parsing and AI jobs, when
    scale requires it
-   OpenAI API accessed only from server-side code
-   `pypdf` or PDF.js-compatible extraction workflow for PDFs
-   `python-docx` or Mammoth.js-compatible pipeline for DOCX parsing
-   Playwright/Chromium or WeasyPrint for PDF rendering, selected after
    layout testing
-   pytest + pytest-django for tests

## Documentation index

-   [Project report](docs/PROJECT_REPORT.md)
-   [Requirements specification](docs/REQUIREMENTS.md)
-   [User stories and acceptance criteria](docs/USER_STORIES.md)
-   [System architecture](docs/ARCHITECTURE.md)
-   [Database design](docs/DATABASE_DESIGN.md)
-   [Django app structure](docs/DJANGO_STRUCTURE.md)
-   [API design](docs/API_DESIGN.md)
-   [AI and ATS design](docs/AI_ATS_DESIGN.md)
-   [Security and privacy](docs/SECURITY_PRIVACY.md)
-   [Testing plan](docs/TESTING.md)
-   [Deployment guide](docs/DEPLOYMENT.md)
-   [Implementation roadmap](docs/ROADMAP.md)
-   [Business model](docs/BUSINESS_MODEL.md)
-   [Risks and mitigations](docs/RISKS.md)

## Suggested build order

1.  Project setup, authentication, settings, and database.
2.  Resume CRUD and structured editor.
3.  Template rendering and PDF export.
4.  Upload parsing and review workflow.
5.  AI writing and cover letters.
6.  ATS checks and job tracker.
7.  Security review, testing, analytics, and beta launch.

## Important product principles

-   Never fabricate a user's credentials, employment, education, or
    achievements.
-   Clearly label ATS scores as estimates based on disclosed checks.
-   Keep API secrets on the server.
-   Enforce object ownership and permissions on every user-owned
    resource.
-   Validate uploads and avoid serving uploaded files as executable
    content.
