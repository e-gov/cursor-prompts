# Code Review Guide

## Objective

Ensure every change is checked against the workspace's full rule set so issues are found early, fixes are targeted, and merges remain low-risk.

## When to Run This Checklist

- A user explicitly requests a review (e.g., “Enter Code Review Mode: …”).
- A feature branch is ready for feedback before merge or release.
- You discover unexpected changes and need to assess their safety.

## Review Workflow

1. **Confirm Scope**
   - Ask which files/commits to inspect; default to all current changes (`git diff --name-only HEAD`).
   - Note each file's role (source, config, doc, test, infra) to understand which rules will apply.

2. **List Applicable Rules**
   - Collect all rule sources: always-applied rules, `.cursor/rules/**/*.mdc`, team guidelines, coding standards.
   - Build a quick checklist grouped into standards, architecture, framework usage, performance, security, testing, documentation.

3. **Inspect Each File**
   - For every applicable rule, decide: compliant, partial, or non-compliant.
   - Capture references (line numbers, behaviors) for both strengths and issues.
   - Assign severity:
     - **Critical** – security/correctness/data loss.
     - **High** – significant standard violations or likely bugs.
     - **Medium** – maintainability, clarity, missing tests.
     - **Low** – style or minor consistency improvements.

4. **Summarize Findings**
   - Use a concise per-file summary such as:
     ```markdown
     ### File: path/to/file.ext

     - Overall: Minor issues
     - Critical: 0, High: 1, Medium: 2, Low: 0
       **Key Findings**
     - [High] Architecture – Direct API call from component (rule 010-architecture)
     - [Medium] Testing – No regression test for new branch
       **Suggested Fixes**

     1. Move API call into existing service layer.
     2. Add unit test covering the new edge case.
     ```
   - Reference the exact rule or guideline behind each issue.

5. **Propose or Apply Fixes**
   - Prioritize fixes in impact order (critical → low).
   - Keep changes minimal and focused; avoid refactors unless requested.
   - When authorized to edit, run available linters/tests and report results.

6. **Close the Review**
   - Deliver the final summary and ordered fix list (or confirm all fixes were applied and retested).
   - Document any new recurring lesson in `rules/ai-tools/agent-memory.mdc` if it's broadly useful.

## Collaboration Tips

- Ask clarifying questions before assuming requirements.
- Label issues as **must-fix** vs **nice-to-have** so the user can prioritize.
- Provide “what + why + how” for each recommendation.
- Offer small code samples when they help illustrate the fix.

## Exit Criteria

A review is complete when every in-scope file has been checked against the relevant rules, issues are documented with severity and references, and the user can clearly decide on the next actions (fix now, defer, or approve).
