### Issue for this PR

Closes #62031

### Type of change

- [x] Bug fix

### What does this PR do?

Sanitized session exports now redact assistant-level native data, structured error messages and response bodies, and current/previous paths in location-switch messages. This covers assistant failures/retries, tool failures, failed compactions and idle failures while retaining error type, HTTP status and retry duration.

Ordinary exports retain the original data. The old compaction-error assertion now expects redaction only for the sanitized export. No feature flag: this fixes the existing `--sanitize` contract.

### How did you verify your code works?

- Added a regression through the real SessionTransfer service and SQLite. It failed before the fix, passes afterward, and passed 10 consecutive runs.
- The test encodes the exported transfer schema, checks that private markers disappear, verifies structured diagnostic fields, and confirms ordinary exports remain unchanged after sanitization.
- All 48 session-create/transfer tests passed. Root lint and all 35 typecheck tasks passed.
- Full core suite: 7,288 passed, 27 skipped, four unrelated process/lifetime cases failed in the minimal container. The MCP failure also reproduces on untouched `dev`; with a user-local Bun launcher and Linux subreaper, all five selected rechecks pass on both baseline and this branch. No test assertions or timeouts were relaxed.

### Visual

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="240" height="72" viewBox="0 0 240 72"><g fill="none" stroke="currentColor"><rect x="8" y="8" width="224" height="56" rx="6" opacity=".3"/><path d="M20 23h78m-78 13h62m-62 13h70" opacity=".5"/><path d="m108 36 14-8v16Z"/></g><text x="137" y="40" fill="currentColor" font-size="12">[redacted]<animate attributeName="opacity" values=".5;1;.5" dur="2s" repeatCount="indefinite"/></text></svg>
```

### Screenshots / recordings

Not applicable; this changes the JSON produced by `session export --sanitize`.

### Checklist

- [x] I have tested my changes locally
- [x] I have not included unrelated changes in this PR
