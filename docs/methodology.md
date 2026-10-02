# Methodology

## 1. Scope first

Before testing, record:

- in-scope assets
- out-of-scope assets
- allowed techniques
- prohibited techniques
- rate limits
- automation restrictions
- disclosure rules

No testing starts before scope is understood.

## 2. Reconnaissance

The purpose of reconnaissance is to understand the attack surface, not simply to generate large lists.

Typical flow:

```text
Domain
  ↓
Subdomains
  ↓
DNS
  ↓
Live HTTP services
  ↓
Technologies
  ↓
URLs and endpoints
  ↓
JavaScript / APIs / parameters
  ↓
Interesting application surfaces
```

Automated results must be manually validated.

## 3. Application mapping

For each interesting application, identify:

- authentication points
- roles and privilege levels
- user-controlled identifiers
- state-changing actions
- file upload/download features
- URL-fetching features
- APIs
- hidden or undocumented endpoints
- client-side security decisions
- trust boundaries

## 4. Hypothesis-driven testing

Do not start with payloads. Start with a question.

Examples:

- Does the server verify ownership of this object?
- Is authorization enforced server-side?
- Can this URL parameter make the backend contact another host?
- Can an unprivileged user call this API operation?
- Does changing this identifier expose another user's data?

Then design the smallest test that can confirm or reject the hypothesis.

## 5. Validation

A valid finding should be:

- reproducible
- clearly scoped
- minimally invasive
- supported by evidence
- separated from assumptions

## 6. Evidence

Useful evidence may include:

- sanitized HTTP requests and responses
- screenshots
- timestamps
- exact reproduction steps
- affected endpoint
- expected vs actual behaviour

Never publish secrets, session material or third-party personal data.

## 7. Reporting

A good report should contain:

1. Title
2. Summary
3. Affected asset
4. Preconditions
5. Steps to reproduce
6. Actual result
7. Expected result
8. Security impact
9. Evidence
10. Suggested remediation when appropriate

## 8. Learning loop

After each lab or report:

```text
What did I expect?
What actually happened?
Why?
What signal did I initially miss?
How could I detect this faster next time?
```
