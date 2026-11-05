### Issue for this PR

Closes #62024

### Type of change

- [x] Bug fix

### What does this PR do?

The Go and Zen routes now use the same flex layout and icon padding for the header Download link as the working landing page. The icon and label stay on one line inside the 80px header. No feature flag: this corrects the existing button layout.

### How did you verify your code works?

Ran the real local website at `/de/go` and `/de/zen` in Chromium, dark mode, 1470×956:

- Before: inline, 78px high, no gap.
- After: flex, 40px high, 8px gap, padding 8px 16px 8px 10px.
- At 800px both buttons remain hidden, as before.
- Prettier and the repository pre-push lint/typecheck hook passed.

### Visual

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="240" height="72" viewBox="0 0 240 72"><g fill="none" stroke="currentColor"><rect x="8" y="8" width="224" height="56" rx="6" opacity=".3"/><rect x="100" y="22" width="118" height="28" rx="4"/><path d="M114 29v12m-4-4 4 4 4-4"/></g><text x="126" y="40" fill="currentColor" font-size="12">Download</text><path d="M8 63h224" stroke="currentColor" opacity=".2"><animate attributeName="opacity" values=".2;.7;.2" dur="2s" repeatCount="indefinite"/></path></svg>
```

### Screenshots / recordings

| Route | Before | After |
| --- | --- | --- |
| Go | ![Before](https://raw.githubusercontent.com/caseclose/opencode/download-button-visuals/go-before.png) | ![After](https://raw.githubusercontent.com/caseclose/opencode/download-button-visuals/go-after.png) |
| Zen | ![Before](https://raw.githubusercontent.com/caseclose/opencode/download-button-visuals/zen-before.png) | ![After](https://raw.githubusercontent.com/caseclose/opencode/download-button-visuals/zen-after.png) |

### Checklist

- [x] I have tested my changes locally
- [x] I have not included unrelated changes in this PR
