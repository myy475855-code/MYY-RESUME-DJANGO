# Security and Privacy Plan

## Security baseline

-   Keep Django, Python, and dependencies patched.
-   Set `DEBUG=False` in production.
-   Configure `ALLOWED_HOSTS`, HTTPS, secure cookies, and trusted
    origins correctly.
-   Use Django CSRF protection and Django's password hashing.
-   Store secrets in environment variables or a secrets manager.
-   Use a dedicated database user with least privilege.
-   Run `python manage.py check --deploy` before release.
-   Configure security headers and HTTPS at the application host or
    reverse proxy.

## Authorization

Every user-owned object must be checked server-side. For example,
retrieve a resume through the current user's queryset rather than
retrieving it globally and trusting the submitted UUID.

Example pattern:

``` python
resume = get_object_or_404(
    Resume.objects.filter(user=request.user),
    pk=resume_id,
)
```

Use this pattern for resumes, versions, uploaded documents, ATS reports,
cover letters, and applications.

## Upload security

-   Permit only supported file formats.
-   Set strict upload size and processing time limits.
-   Verify file content rather than trusting filename extensions alone.
-   Use randomized storage keys.
-   Keep uploads in private storage.
-   Do not execute uploaded files or render them as trusted HTML.
-   Consider malware scanning for production.
-   Isolate parsing tasks and handle malformed files safely.
-   Do not fetch arbitrary user-supplied URLs without SSRF protections.

## AI security

-   Call the AI provider from the backend only.
-   Never expose provider API keys in HTML or JavaScript.
-   Treat uploaded text as untrusted content.
-   Limit input size and output size.
-   Apply quotas, throttling, and abuse monitoring.
-   Validate structured output.
-   Avoid including more personal information than the feature requires.
-   Do not log full prompts and completions by default.

## Privacy

-   Publish a clear privacy policy before public launch.
-   Explain what data is sent to AI providers and under what terms.
-   Set retention rules for uploads, extracted text, generated reports,
    and logs.
-   Provide user data export and account deletion workflows.
-   Restrict staff/admin access and audit privileged operations where
    appropriate.
-   Use private object storage and expiring download links when
    supported.
-   Avoid storing unnecessary personal information.

## Data deletion

When a user deletes a resume, remove related versions and derived files
according to the documented policy. Account deletion should address
database rows, storage objects, queued tasks, and any third-party
retention obligations. Backups may have separate expiration schedules,
which should be disclosed.

## Security testing checklist

-   Anonymous user cannot open private pages.
-   User A cannot read or change User B's objects.
-   Invalid UUIDs and manipulated form fields are rejected safely.
-   CSRF protection is enabled for state-changing browser requests.
-   Upload size/type/content validation works.
-   AI endpoints enforce quotas and input limits.
-   Errors do not expose stack traces or secrets in production.
-   Account deletion removes the expected records and files.
