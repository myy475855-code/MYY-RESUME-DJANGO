# API and URL Design

The MVP can use Django views and forms without a separate REST API. If a
JavaScript frontend or mobile client is added, Django REST Framework can
expose a versioned API.

## Server-rendered URL proposal

  Method     URL                                  Purpose
  ---------- ------------------------------------ -----------------------
  GET/POST   `/accounts/signup/`                  Registration
  GET/POST   `/accounts/login/`                   Login
  POST       `/accounts/logout/`                  Logout
  GET        `/app/`                              Dashboard
  GET/POST   `/app/resumes/new/`                  Create resume
  GET/POST   `/app/resumes/<uuid>/edit/`          Edit resume
  POST       `/app/resumes/<uuid>/duplicate/`     Duplicate resume
  POST       `/app/resumes/<uuid>/delete/`        Delete resume
  GET        `/app/resumes/<uuid>/preview/`       Preview
  GET        `/app/resumes/<uuid>/download.pdf`   PDF export
  GET/POST   `/app/documents/upload/`             Upload document
  GET/POST   `/app/documents/<uuid>/review/`      Review extracted data
  GET/POST   `/app/resumes/<uuid>/analyze/`       ATS analysis
  GET/POST   `/app/cover-letters/new/`            Create cover letter
  GET        `/app/jobs/`                         Application tracker
  GET/POST   `/app/jobs/new/`                     Add application

Use POST for state-changing operations and protect forms with CSRF.

## Optional REST API

Prefix API routes with `/api/v1/`.

-   `GET /api/v1/resumes/`
-   `POST /api/v1/resumes/`
-   `GET /api/v1/resumes/{id}/`
-   `PATCH /api/v1/resumes/{id}/`
-   `DELETE /api/v1/resumes/{id}/`
-   `POST /api/v1/resumes/{id}/duplicate/`
-   `POST /api/v1/resumes/{id}/export-pdf/`
-   `POST /api/v1/documents/`
-   `POST /api/v1/documents/{id}/parse/`
-   `POST /api/v1/ats/analyze/`
-   `POST /api/v1/ai/rewrite-summary/`
-   `POST /api/v1/ai/rewrite-bullets/`
-   `POST /api/v1/cover-letters/`
-   `GET /api/v1/applications/`
-   `POST /api/v1/applications/`

## API behavior

-   Validate all request bodies and uploaded files.
-   Return stable error codes and helpful field-level messages.
-   Apply authentication, object ownership checks, throttling, and
    quotas.
-   Do not accept user IDs from the client as proof of ownership.
-   Do not return private storage paths or secrets.
-   Limit AI input size and validate the provider response before saving
    it.
-   Use pagination for list endpoints.
-   Consider idempotency for expensive actions such as generation or
    export.
