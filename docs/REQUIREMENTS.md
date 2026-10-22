# Software Requirements Specification

## 1. Purpose

Define the MVP requirements for the Django-based AI Resume Creator.

## 2. Actors

-   **Guest:** Views public pages and templates.
-   **Registered user:** Creates resumes, uses AI tools, uploads files,
    analyzes jobs, and tracks applications.
-   **Administrator:** Manages templates, monitors service health, and
    handles support. Admin access must not imply unnecessary access to
    private resume contents.
-   **External AI provider:** Processes approved prompts sent by the
    backend.

## 3. Functional requirements

### Authentication

-   FR-001: Users can register, log in, log out, and reset passwords.
-   FR-002: Private pages require authentication.
-   FR-003: Users can request account deletion.

### Resume management

-   FR-010: Users can create, view, edit, duplicate, archive, and delete
    resumes.
-   FR-011: Resume content is stored in a structured, validated format.
-   FR-012: Users can select a template without losing content.
-   FR-013: Users can reorder sections and manage repeatable entries.
-   FR-014: The application shows save status and prevents silent data
    loss.
-   FR-015: Users can restore a saved version if version history is
    enabled.

### Documents

-   FR-020: Users can upload supported PDF and DOCX files.
-   FR-021: Uploads are subject to size, extension, MIME, and content
    validation.
-   FR-022: Extracted content is presented for user review before
    becoming a saved resume.
-   FR-023: Users can export a resume to PDF.
-   FR-024: PDF output supports selectable text, correct page size, and
    clickable links where appropriate.

### AI writing

-   FR-030: Users can request summary suggestions.
-   FR-031: Users can improve experience bullet points using facts they
    provide.
-   FR-032: Users can accept, edit, regenerate, or reject suggestions.
-   FR-033: AI output must not be inserted silently.
-   FR-034: Requests must have rate limits, timeouts, and usage
    accounting.

### ATS and job matching

-   FR-040: Users can save a job description.
-   FR-041: The system identifies relevant keywords and potential gaps.
-   FR-042: The report explains its findings and limitations.
-   FR-043: The system does not guarantee passing an employer's ATS.

### Cover letters

-   FR-050: Users can generate a cover letter from selected resume
    content and a job description.
-   FR-051: Users can edit, save, duplicate, and export a cover letter.

### Job tracker

-   FR-060: Users can create and update job applications.
-   FR-061: Applications support statuses such as saved, applied,
    interview, offer, rejected, and withdrawn.
-   FR-062: Users can record application dates, notes, and follow-up
    dates.
-   FR-063: Users can filter applications by status and date.

## 4. Non-functional requirements

-   NFR-001: All private objects require server-side ownership checks.
-   NFR-002: Secrets must not be committed to source control or sent to
    the browser.
-   NFR-003: Uploads must be stored privately and processed safely.
-   NFR-004: The interface must work on common desktop and mobile screen
    sizes.
-   NFR-005: Forms must provide clear validation errors.
-   NFR-006: Critical workflows must have automated tests.
-   NFR-007: The system must record operational errors without
    unnecessarily logging personal resume content.
-   NFR-008: Users must be able to export and delete their data under
    the published policy.

## 5. MVP acceptance criteria

-   A new user can register and create a resume.
-   A user can edit and reload resume data without loss.
-   A user can switch templates without losing content.
-   A user can download a readable PDF.
-   A user can upload a supported document and review extracted text.
-   AI suggestions are editable and never silently overwrite content.
-   ATS findings show actionable reasons, not only a score.
-   A user can create a cover letter and track an application.
-   One user cannot access another user's private records by changing an
    ID in a URL.
-   Invalid or oversized files are rejected safely.
