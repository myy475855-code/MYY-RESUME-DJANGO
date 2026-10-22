# Testing Plan

## Tools

-   pytest
-   pytest-django
-   Django test client
-   unittest.mock or pytest monkeypatch for external API calls
-   Playwright for end-to-end browser tests if the budget permits

## Unit tests

### Models

-   Required fields and default values.
-   Valid application statuses.
-   Version snapshots preserve prior resume content.
-   Deletion behavior matches the documented policy.

### Forms and validation

-   Valid resume content is accepted.
-   Malformed JSON structures are rejected.
-   Unsupported file types and oversized files are rejected.
-   Empty or oversized job descriptions are rejected.

### Services

-   ATS keyword coverage is calculated consistently.
-   AI responses are schema-validated.
-   PDF export handles missing optional fields.
-   Parsing errors produce safe, actionable messages.

## Permission tests

-   Anonymous users cannot access private records.
-   User A cannot read, update, delete, or export User B's resume.
-   User A cannot access User B's uploads, reports, cover letters, or
    applications.
-   IDs supplied in request data do not override the authenticated user.

## Integration tests

-   Register, log in, and create a resume.
-   Edit a resume, reload it, and verify persistence.
-   Switch templates and confirm content is preserved.
-   Upload a valid document and review extracted text.
-   Generate a PDF and verify a non-empty document is returned.
-   Mock AI generation and verify the suggestion can be accepted or
    rejected.
-   Analyze a resume against a job description.
-   Create a cover letter and a job application.
-   Verify account deletion behavior.

## PDF quality checks

Test: - One-page and multi-page resumes. - Long names, long job titles,
and large skill lists. - Unicode characters and non-English text. - Page
breaks and orphaned headings. - Embedded or available fonts. - Clickable
links. - Selectable text and reading order. - Layout in the target
deployment environment.

## End-to-end smoke test

1.  Sign up.
2.  Create a resume.
3.  Add experience and education.
4.  Select a template.
5.  Preview and download a PDF.
6.  Save a job description.
7.  Run analysis.
8.  Create a cover letter.
9.  Add an application to the tracker.
10. Sign out and confirm private pages require authentication.

## Release gate

Do not launch publicly until critical authorization tests pass,
production settings are secure, PDF export works in the deployment
environment, and upload/AI failure states are understandable.
