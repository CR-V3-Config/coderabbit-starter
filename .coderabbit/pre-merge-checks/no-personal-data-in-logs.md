---
# AGENT: example check. Rewrite the list of personal data in the body to the fields this product actually
# handles (for example patient id, account number, device id), and name the logging, analytics and error
# reporting helpers this repository uses. Delete this document if the repository handles no personal data.
# Warning mode: it reports in the walkthrough and never blocks a merge.
id: no-personal-data-in-logs
name: No personal data in logs
mode: warning
report: coderabbit
---

Pass when the change adds no personal data to a place it can leak from. Fail when the change writes any of these to a log line, an error message, an analytics or telemetry event, a URL or query string, or a test fixture: an email address, a phone number, a full name together with another identifier, a postal address, a date of birth, a government id, payment card or bank details, an access token or a session id. Also fail when a new field holding one of these is stored or returned by an API without the masking or access check that neighbouring fields have. List each file and line, and name the field.
