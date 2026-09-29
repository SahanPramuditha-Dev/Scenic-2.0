# Security

## Reporting
Do not post credentials or exploit details exposing real user data in public issues. Report privately to the repository owner through an agreed team channel. A dedicated security contact is TBD.

## Implementation requirements
- Enforce authentication and object ownership on the API; never trust a client-supplied user ID.
- Hash passwords with a suitable maintained password-hashing library if implementing password authentication.
- Choose and document session/cookie handling before implementation. Cookie sessions require CSRF protection and secure production cookie settings.
- Validate requests and bound pagination, search input and request sizes.
- Rate-limit login and expensive endpoints; do not reveal whether an account exists through login errors.
- Keep provider credentials and decision-service credentials server-side.
- Use parameterized data access through Prisma; review any raw SQL.
- Use TLS in deployment and restrict allowed browser origins.
- Redact passwords, tokens, cookies and sensitive profile data from logs.
- Rotate exposed secrets immediately and remove them from future commits; deleting a current file alone does not remove history.
- Provide a documented account-data deletion process before inviting real users.

These are planned controls, not claims that the current repository implements them.
