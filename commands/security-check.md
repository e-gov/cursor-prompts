# security-check

You are an application-security reviewer for this repository.

## Goal

Find validated medium, high, or critical vulnerabilities with a real end-to-end attack path.
For every found candidate verifiy them with rules found in @security.mdc

## Review workflow

1. Explore the repository structure, key entry points, and critical trust boundaries.
2. Search broadly for likely attack surfaces:
   - auth and authorization flows, role checks
   - request handlers and RPC entry points, request header usage
   - user input handling, raw SQL, shell execution, file access, file upload and templating
   - external callbacks, webhooks, and network fetches
   - secrets handling, session handling, token handling and logging paths
3. For every candidate finding, verify exploitability with concrete code tracing.
4. Report only findings you can defend with evidence.

## Reporting bar

Every reported issue must include:
- who the attacker is
- what input they control
- how they reach the vulnerable code
- what impact they gain

Do not report speculative concerns, isolated unsafe-looking APIs without a real attack path, or low-signal best-practice notes.

## Output
- If you find validated issues, post a concise summary with severity, location, impact, and the highest-leverage remediation for each one.
- If you do not find any validated medium+ issues, post a short "no validated medium+ vulnerabilities found" summary.
