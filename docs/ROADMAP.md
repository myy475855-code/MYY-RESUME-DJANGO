# Implementation Roadmap

Planning estimate: around 6--8 weeks for a developer working
consistently on a focused MVP. The schedule is not a guarantee and
should be adjusted to the available hours and quality bar.

## Phase 1 --- Foundation (Week 1)

-   Create Django project and settings.
-   Choose built-in or custom user model before initial migrations.
-   Configure PostgreSQL and environment variables.
-   Implement registration, login, logout, and password reset.
-   Create the base layout and dashboard shell.
-   Add CI and initial tests.

**Exit criteria:** authentication works and private views require login.

## Phase 2 --- Resume editor (Weeks 2--3)

-   Create Resume, ResumeVersion, and template configuration.
-   Implement structured resume forms.
-   Add repeatable experience, education, skills, and project sections.
-   Implement create/edit/delete/duplicate workflows.
-   Add autosave or explicit save feedback.
-   Build three initial templates and a preview.
-   Test ownership permissions.

**Exit criteria:** users can create, edit, reload, and preview resumes.

## Phase 3 --- PDF and import (Week 4)

-   Select PDF rendering engine.
-   Implement print CSS and page-break handling.
-   Add PDF export.
-   Implement PDF/DOCX text extraction.
-   Build import review and correction workflow.
-   Add upload validation and private storage.

**Exit criteria:** exported PDFs are readable and supported uploads can
be reviewed safely.

## Phase 4 --- AI writing and cover letters (Week 5)

-   Create server-side AI client.
-   Add summary and bullet rewriting.
-   Add output schema validation and user review controls.
-   Add cover-letter generation and editing.
-   Implement quotas, timeouts, and error handling.
-   Mock AI responses in tests.

**Exit criteria:** AI features are safe to test with a limited beta
group.

## Phase 5 --- ATS and job tracker (Week 6)

-   Create JobDescription and JobApplication models.
-   Add job-description entry and editing.
-   Implement keyword coverage and basic formatting checks.
-   Add explanatory reports.
-   Implement application statuses, notes, and follow-up dates.

**Exit criteria:** a user can tailor a resume to a job and track the
application.

## Phase 6 --- Launch readiness (Weeks 7--8)

-   Run security and permission tests.
-   Test mobile and keyboard accessibility.
-   Test PDF edge cases and file parsing failures.
-   Add monitoring, analytics, privacy policy, and support contact.
-   Conduct user interviews and beta testing.
-   Fix high-impact usability issues.
-   Deploy and monitor a limited launch.

**Exit criteria:** critical security tests pass and the primary workflow
is reliable.

## Prioritization rule

If behind schedule, preserve the resume editor, safe persistence,
template preview, PDF export, and privacy controls. Release AI and
tracker features in smaller increments rather than rushing a fragile
document workflow.
