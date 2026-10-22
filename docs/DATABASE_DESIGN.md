# Database Design

This document is a proposed schema, not a migration file. Refine fields
and constraints during implementation.

## 1. User and profile

Use Django's built-in User model or a custom user model created at the
beginning of the project. If email is the primary login identifier,
decide that before the first migration.

### Profile

-   `user`: one-to-one relation to the user model.
-   `display_name`: optional display name.
-   `plan`: free/pro or a related subscription record.
-   `created_at`, `updated_at`.

## 2. Resume

Suggested fields: - `id`: UUID primary key. - `user`: foreign key to
user. - `title`: short user-facing title. - `content`: JSONField
containing structured resume data. - `template_key`: validated
identifier for a template. - `status`: draft or archived. -
`created_at`, `updated_at`.

The `content` field should be validated against an application schema.
JSONField flexibility does not replace validation.

Example:

``` json
{
  "personal_info": {
    "full_name": "",
    "email": "",
    "phone": "",
    "location": "",
    "linkedin": "",
    "portfolio": ""
  },
  "summary": "",
  "experience": [],
  "education": [],
  "skills": [],
  "projects": [],
  "certifications": [],
  "languages": [],
  "custom_sections": []
}
```

Each repeatable section should have a stable UUID or key. Do not use
list positions as persistent identifiers.

## 3. ResumeVersion

-   `id`: UUID primary key.
-   `resume`: foreign key to Resume.
-   `content_snapshot`: JSONField.
-   `template_key_snapshot`: optional string.
-   `created_at`.
-   `label`: optional user note.

Apply a retention limit so version history does not grow without bound.

## 4. ResumeTemplate

-   `key`: unique stable string.
-   `name`: display name.
-   `category`: professional, modern, minimalist, creative, etc.
-   `is_active`: Boolean.
-   `configuration`: JSONField for supported visual options.
-   `preview_image`: optional asset path.

Avoid allowing arbitrary user-provided template paths or code.

## 5. UploadedDocument

-   `id`: UUID.
-   `user`: foreign key.
-   `storage_key`: private storage identifier.
-   `original_filename`: sanitized display name.
-   `file_type`: PDF or DOCX.
-   `file_size`: integer.
-   `status`: uploaded, processing, review_required, imported, failed.
-   `extracted_text`: optional protected text field or separate
    processing artifact.
-   `created_at`, `processed_at`.

Delete temporary artifacts according to the retention policy.

## 6. JobDescription

-   `id`: UUID.
-   `user`: foreign key.
-   `title`, `company`, `description`, `job_url`.
-   `location`: optional.
-   `created_at`, `updated_at`.

Do not fetch arbitrary URLs from the server without SSRF protection. For
the MVP, prefer user-pasted descriptions.

## 7. ATSReport

-   `id`: UUID.
-   `user`: foreign key.
-   `resume`: foreign key.
-   `job_description`: optional foreign key.
-   `score`: optional numeric estimate.
-   `report_data`: JSONField.
-   `created_at`.

Keep a snapshot or content hash of the analyzed resume/job description
if historical reproducibility is required. Avoid storing unnecessary
copies of sensitive content.

## 8. CoverLetter

-   `id`: UUID.
-   `user`: foreign key.
-   `resume`: optional foreign key.
-   `job_description`: optional foreign key.
-   `title`, `content`.
-   `created_at`, `updated_at`.

## 9. JobApplication

-   `id`: UUID.
-   `user`: foreign key.
-   `job_description`: optional foreign key.
-   `resume`: optional foreign key.
-   `company`, `role_title`, `job_url`.
-   `status`: saved, applied, interview, offer, rejected, withdrawn.
-   `applied_at`, `follow_up_at`.
-   `notes`.
-   `created_at`, `updated_at`.

## 10. AIUsageRecord

-   `id`: UUID.
-   `user`: foreign key.
-   `feature`: summary, bullet_rewrite, ats, cover_letter.
-   `provider`, `model`: optional metadata.
-   `input_units`, `output_units`: token counts where available.
-   `estimated_cost`: optional internal estimate.
-   `created_at`, `status`.

Do not store full prompts or resume text in usage logs by default.

## Relationships

-   User has many resumes.
-   Resume has many versions.
-   User has many uploaded documents and job descriptions.
-   Resume can have many ATS reports.
-   User has many cover letters and job applications.
-   A job application can reference a resume and a job description.

## Indexes and constraints

-   Index `user_id` on all user-owned tables.
-   Index `status`, `follow_up_at`, and `updated_at` where frequently
    filtered.
-   Add database constraints for valid status values and required
    fields.
-   Use `on_delete` behavior intentionally and document data deletion
    cascades.
-   Test that ownership constraints are enforced in views/services; a
    UUID is not an authorization mechanism.
