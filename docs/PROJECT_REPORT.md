# Project Report: AI-Powered Resume Creator Using Django

## 1. Title

**AI-Powered Resume Creator and Job Application Management System**

## 2. Abstract

The AI-Powered Resume Creator is a web application designed to help
users create, customize, export, and manage professional resumes. The
system uses Django as its main web framework and PostgreSQL as its
relational database. Users can build resumes from structured forms,
choose templates, upload existing PDF or DOCX resumes for text
extraction, request AI-assisted writing improvements, compare resume
content with a job description, generate cover letters, and track job
applications.

The platform is intended to reduce the time and design effort required
to produce a clear resume. AI suggestions are presented as editable
recommendations, not as facts. The ATS analysis provides explainable
checks and keyword coverage estimates; it does not promise that a resume
will pass every employer's applicant tracking system.

## 3. Introduction

A resume is a key document in the job search process, but creating one
can be difficult for people who lack design experience or who need to
tailor their experience to different positions. Existing document
editors often require users to manage formatting manually. Job seekers
may also find it difficult to identify relevant keywords, write
achievement-oriented bullet points, and keep track of applications.

This project combines resume authoring, template rendering, document
export, AI writing assistance, job-description analysis, cover letters,
and application tracking in one web platform.

## 4. Problem statement

Job seekers commonly face these problems:

-   Resume formatting takes time and can break during editing or export.
-   Users may not know how to describe their experience clearly.
-   Existing resumes may be difficult to reuse for different job
    applications.
-   Important requirements in a job description can be overlooked.
-   Creating a matching cover letter adds extra work.
-   Job applications and follow-up dates can become disorganized.
-   Uploaded resume data may be sensitive and needs appropriate
    protection.

## 5. Proposed solution

The proposed system provides a guided resume editor, reusable templates,
PDF/DOCX import, PDF export, AI writing suggestions, explainable
ATS-style checks, cover letter generation, and a job application
tracker. Django handles authentication, business rules, database access,
file processing, and server-side AI requests.

## 6. Objectives

### Primary objectives

1.  Provide a simple interface for creating and editing resumes.
2.  Save resume data securely and allow users to manage multiple
    versions.
3.  Produce readable, consistently formatted PDF resumes.
4.  Extract editable content from uploaded PDF and DOCX files.
5.  Offer AI writing support without inventing user qualifications.
6.  Compare resume content with a target job description.
7.  Generate editable cover letters.
8.  Track applications and follow-up dates.

### Secondary objectives

-   Support mobile and desktop layouts.
-   Offer free and paid plans after validating demand.
-   Maintain an architecture that can support additional templates and
    features.
-   Provide data export and account deletion.

## 7. Project scope

### Included in the initial release

-   User registration, login, logout, password reset.
-   User dashboard.
-   Resume create, read, update, delete, duplicate, and version history.
-   Personal details, summary, work experience, education, skills,
    projects, and certifications.
-   Three to five templates.
-   Live or near-live preview.
-   PDF export.
-   PDF/DOCX upload and extracted-text review.
-   AI summary and bullet-point suggestions.
-   Basic resume/job-description analysis.
-   Cover letter creation.
-   Job application tracking.
-   Basic account and privacy controls.

### Excluded from the initial release

-   Automated job applications.
-   Guaranteed ATS passing.
-   Scraping restricted job boards.
-   Social networking.
-   Recruiter marketplace.
-   Complex enterprise administration.
-   AI interview simulation.
-   Native mobile applications.

## 8. Intended users

-   Students and fresh graduates.
-   Experienced professionals changing roles.
-   Freelancers and contractors.
-   People returning to work.
-   Career coaches and, in a later phase, university career centers.

## 9. Functional requirements

1.  The system shall allow users to register and authenticate.
2.  The system shall allow an authenticated user to create and manage
    multiple resumes.
3.  The system shall allow a user to edit structured resume sections.
4.  The system shall render resume content using a selected template.
5.  The system shall export a resume to PDF.
6.  The system shall accept supported PDF and DOCX uploads within
    configured limits.
7.  The system shall extract text from uploaded documents and allow the
    user to review it.
8.  The system shall generate AI suggestions from user-provided facts.
9.  The system shall analyze a resume against a user-provided job
    description.
10. The system shall generate and save cover letters.
11. The system shall allow users to track job applications and their
    statuses.
12. The system shall enforce access control for private records and
    files.
13. The system shall allow users to delete their account and associated
    data according to the retention policy.

## 10. Non-functional requirements

-   **Security:** Authentication, authorization, CSRF protection, secure
    cookies, upload validation, and secret management.
-   **Privacy:** Minimize collected personal data and explain how files
    and AI requests are processed.
-   **Reliability:** Autosave should provide clear save status and
    handle transient failures.
-   **Usability:** Resume editing should be understandable to
    non-technical users.
-   **Performance:** Common dashboard and editor actions should feel
    responsive; heavy parsing and AI tasks may run asynchronously.
-   **Accessibility:** Use semantic HTML, keyboard-accessible controls,
    labels, and sufficient contrast.
-   **Maintainability:** Keep Django apps separated by domain and cover
    business rules with tests.
-   **Portability:** Use environment-based configuration and documented
    deployment steps.

## 11. Proposed technology

  -----------------------------------------------------------------------
  Layer                               Technology
  ----------------------------------- -----------------------------------
  Backend                             Django

  UI                                  Django templates, HTML, CSS,
                                      HTMX/Alpine.js if desired

  Database                            PostgreSQL

  Authentication                      Django authentication

  Forms and validation                Django Forms / ModelForms

  Optional REST API                   Django REST Framework

  Background jobs                     Celery + Redis, if needed

  AI                                  OpenAI API via server-side service

  PDF parsing                         pypdf or another maintained parser

  DOCX parsing                        python-docx

  PDF generation                      Playwright/Chromium or WeasyPrint

  Tests                               pytest, pytest-django

  Deployment                          Linux container or managed Python
                                      hosting; PostgreSQL and private
                                      object storage
  -----------------------------------------------------------------------

Select PDF rendering libraries only after checking operating-system
dependencies, fonts, CSS support, and deployment compatibility.

## 12. High-level architecture

The browser communicates with Django views. Django validates input,
checks permissions, applies business rules, and reads or writes
PostgreSQL records. Resume templates render structured resume data into
HTML. A PDF service converts the approved HTML into a downloadable
document. Upload processing extracts text into a review step. AI
requests are sent through a server-side service with timeouts, quotas,
and error handling. Private files are stored in access-controlled
storage.

## 13. Main database entities

-   User/Profile
-   Resume
-   ResumeVersion
-   ResumeTemplate
-   UploadedDocument
-   JobDescription
-   ATSReport
-   CoverLetter
-   JobApplication
-   AIUsageRecord

See [Database Design](DATABASE_DESIGN.md) for proposed fields and
relationships.

## 14. AI and ATS methodology

AI can help rewrite summaries, improve bullet points, and draft cover
letters. The system should pass only necessary information to the AI
provider and should ask the user to review generated content. The system
must not invent credentials or quantified results.

The ATS analyzer should combine deterministic checks with optional
AI-assisted semantic comparison. Examples include checking for contact
information, recognizable headings, selectable text, likely parsing
problems, and overlap between job requirements and resume skills. Any
score should be labeled as an estimate, and its components should be
disclosed.

## 15. Security and privacy

-   Use Django's authentication and CSRF protection.
-   Enforce ownership checks for every resume, report, cover letter,
    application, and upload.
-   Keep `SECRET_KEY`, database passwords, and AI keys in environment
    variables or a secrets manager.
-   Validate upload extension, MIME type, size, and file contents.
-   Use random storage keys and private file storage.
-   Do not trust user-supplied filenames or paths.
-   Apply rate limits and usage limits to AI endpoints.
-   Set retention and deletion rules for uploaded files and generated
    content.
-   Avoid logging full resumes, API keys, or other sensitive content.
-   Provide account deletion and privacy notices.

## 16. Testing strategy

Unit tests should cover models, validators, ownership rules, ATS
calculations, and AI response validation. Integration tests should cover
resume creation, editing, upload processing, AI failure cases, PDF
export, and application tracking. Browser tests should verify the main
user journey, keyboard navigation, responsive layouts, and PDF download
behavior. Security tests should attempt cross-user access and invalid
uploads.

## 17. Project plan

  Phase   Work                               Deliverable
  ------- ---------------------------------- --------------------------
  1       Setup, auth, database, base UI     Working foundation
  2       Resume editor and templates        Editable resume
  3       PDF rendering and import           Download/import workflow
  4       AI writing and cover letters       AI-assisted content
  5       ATS checks and job tracker         Job-targeted workflow
  6       Testing, security, beta feedback   Launch candidate

A focused MVP may take approximately 6--8 weeks for a developer working
consistently, but the schedule depends on available hours, template
quality, and document-processing complexity.

## 18. Risks and mitigation

  -----------------------------------------------------------------------
  Risk                                Mitigation
  ----------------------------------- -----------------------------------
  AI invents facts                    Require user review; preserve
                                      original content; never fabricate
                                      credentials

  ATS score misleads users            Explain scoring and label it an
                                      estimate

  PDF layout breaks                   Use template fixtures and visual
                                      regression tests

  Malicious uploads                   Validate, limit size, isolate
                                      processing, and keep files private

  AI costs grow                       Usage quotas, token limits, caching
                                      where appropriate, and monitoring

  Private data leaks                  Ownership checks, RLS where
                                      applicable, private storage, and
                                      access tests

  Users abandon editor                Autosave, guided onboarding, and a
                                      short first-run workflow
  -----------------------------------------------------------------------

## 19. Future enhancements

-   DOCX export.
-   Premium templates and customization.
-   Multiple job-targeted resume variants.
-   Portfolio website generation.
-   Interview practice.
-   Application reminders and calendar integration.
-   University or career-coach plans.
-   Additional languages and regional resume formats.

## 20. Conclusion

The AI-Powered Resume Creator combines resume editing, document
processing, AI writing support, job matching, cover letters, and
application tracking. Django provides a mature foundation for
authentication, database-backed business logic, forms, file processing,
and secure server-side integrations. The project should begin with a
dependable resume editor and PDF export, then expand through measured,
user-validated releases.
