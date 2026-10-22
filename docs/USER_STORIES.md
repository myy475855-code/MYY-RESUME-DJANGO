# User Stories and Acceptance Criteria

## Resume creation

**As a job seeker,** I want to create a resume from a guided form so I
can focus on my experience instead of formatting.

Acceptance criteria: - The editor contains personal details, summary,
experience, education, skills, projects, and certifications. -
Repeatable sections can be added and removed. - Required fields are
validated with helpful messages. - The resume can be saved and reopened.

## Template switching

**As a user,** I want to switch templates without re-entering
information.

Acceptance criteria: - Template changes affect presentation only. -
Resume content remains unchanged. - A preview is available before
export.

## AI writing

**As a user,** I want help improving my writing while keeping it
accurate.

Acceptance criteria: - The user supplies the original text and optional
context. - Suggestions are displayed separately from the original. - The
user can accept, edit, regenerate, or reject a suggestion. - The AI is
instructed not to invent facts or metrics.

## Upload and import

**As a user,** I want to import an existing resume to avoid retyping it.

Acceptance criteria: - Supported file types and size limits are clearly
displayed. - Extracted content is shown for review. - Uncertain fields
are not silently treated as verified. - Unsupported, encrypted,
corrupted, or oversized files receive a clear error.

## ATS analysis

**As a user,** I want to compare my resume with a job description so I
can make relevant improvements.

Acceptance criteria: - The report lists matched and missing terms. -
Recommendations are grounded in the provided job description and
resume. - The user can choose which recommendations to apply. - The
report explains that the analysis is an estimate.

## Cover letter

**As a user,** I want to generate a cover letter for a specific role.

Acceptance criteria: - The user selects a resume and provides a job
description. - The generated letter is editable. - The system does not
claim experience absent from the source resume. - The letter can be
saved and exported.

## Job tracking

**As a user,** I want to record applications and follow-up dates.

Acceptance criteria: - The user can add a company, role, job URL,
status, dates, and notes. - Status can be updated. - Applications can be
filtered. - Private notes are not accessible to other users.

## Privacy

**As a user,** I want my documents and resume data to remain private.

Acceptance criteria: - Access is restricted to the owner. - Uploaded
files are stored privately. - The user can delete resumes and request
account deletion. - Logs do not contain full resume contents or secrets
by default.
