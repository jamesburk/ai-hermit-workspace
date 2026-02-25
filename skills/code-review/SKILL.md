# Skill -- Code Review

Reviews code diffs, PRs, or selected code blocks with structured feedback.

## Commands

- `/review` -- Review staged changes (git diff --cached) in the current project
- `/review <file>` -- Review a specific file
- `/review pr <number>` -- Review a pull request by number (requires gh CLI)

## Behavior

1. Read the full diff or file before commenting -- understand context first
2. Focus on correctness and security over style
3. Flag OWASP top 10 risks (injection, XSS, auth bypass, etc.) with severity
4. Keep feedback actionable -- suggest the fix, not just the problem
5. Note positive patterns worth keeping -- review is not just criticism

## Output Format

```markdown
## Review: <target>

### Issues
- **[severity]** file:line -- description. Suggested fix: `...`

### Observations
- Things that look good or are worth noting

### Summary
One-line verdict: approve / request changes / needs discussion
```

## Severity Levels

- **critical** -- Security vulnerability, data loss risk, crash
- **warning** -- Bug likely, logic error, performance issue
- **suggestion** -- Style, readability, minor improvement
