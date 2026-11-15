# Professional Quality Standard for Security Research

**Version:** 1.0 (2026-11-15)  
**Scope:** Public learning notes, authorized labs, methodology, and sanitized reports. This document is a self-imposed quality standard, **not an official grading rubric** or a claim about any individual's evaluation preferences.

## The goal

The objective is not to collect as many subdomains, scan results, or payloads as possible. A strong result should withstand three independent reviews:

1. **Offensive-security review:** What security boundary could be violated? What is the smallest authorized test that could prove or reject the hypothesis? What real effect would follow?
2. **Vulnerability triage and attack-surface review:** Is the asset genuinely within scope? Is the issue actionable, reproducible, and distinct from a purely functional error? What should the owner fix?
3. **Scientific-method review:** Is the hypothesis falsifiable? Are the conditions, controls, data, and tool versions documented? What conclusions are supported, and what remains unknown?

These are **review perspectives**, not attributed quotes from professors or security researchers.

## 1. Evidence levels

| Level | Classification | Supported conclusion |
|---|---|---|
| E0 | OSINT discovery | A hostname, URL, or product reference appeared in a public source |
| E1 | DNS observation | A particular resolver returned a DNS answer/status at a known time |
| E2 | Protocol observation | A specific HTTP/TLS/service response was observed |
| E3 | Hypothesis designed | A falsifiable security question and its controls are defined |
| E4 | Anomaly reproduced | An unexpected behavior was reproduced under documented conditions |
| E5 | Security issue validated | An actual security control violation and its impact were demonstrated safely |

**Do not skip from E0/E2 to E5.** A missing header, a redirect loop, an HTTP 404/500, a certificate warning, or a pattern in a scanner output is not necessarily a vulnerability.

## 2. Reconnaissance quality

For every dataset, capture:
- Authorized scope and rules (with date and version).
- Query/sample universe, tool, version, exact options, time, and original input.
- Counts of raw records versus normalized unique hostnames.
- Source attribution and biases; historical sources and Certificate Transparency may overrepresent generated or stale names.
- Evidence needed to distinguish a discovered hostname from an accessible service or application.
- Data quality, false positives, coverage gaps, and explicit limitations.

**Do not assume** that naming patterns prove PTR records, NSEC3, wildcard DNS, host availability, or third-party ownership. These need separate evidence.

## 3. Hypothesis and controls

Before running an authorized test, write:
- The precise security question and expected control.
- The principal, role, object, operation, and trust boundary involved.
- A **positive control** for expected allowed behavior and a **negative control** for expected denied behavior.
- A baseline and the minimum change needed to isolate the tested condition.
- Relevant permissions, group inheritance, environment, application version, and resource ownership.
- What observation would refute the hypothesis; what would confirm a violation.
- The minimum number of requests needed, in line with the program rules.

**Compare effects, not just HTTP status codes.** A 200 response does not prove a restricted action succeeded; a 404 does not always mean a resource does not exist.

Use the [experiment record template](../reports/templates/experiment-record.md).

## 4. Negative results matter

Correct: "For the operations and roles tested, the expected authorization rules were enforced."

Incorrect: "The application is secure."

An inconclusive case is also a legitimate result when the setup, permissions, or observable effects cannot distinguish a failure from expected behavior. Record what prevented a stronger conclusion.

## 5. Reporting quality

A potential finding should be:
- Within the exact authorized scope and disclosure rules.
- Supported by minimal reproduction steps and sanitized evidence.
- Clear about preconditions, expected versus actual behavior, and the affected security property.
- Explicit about **demonstrated impact**, root-cause hypothesis, and practical remediation.
- Separated from functional defects, speculative risk, and unactionable informational observations.
- Assigned severity only when impact and exploitability support it; never invent a CVSS score.

Use a lab note or experiment record for observations and negative outcomes. A vulnerability report is reserved for validated security issues. **Private or undisclosed bugs must not be published here** without explicit permission.

## 6. Tool-use principle

Every tool needs a purpose: *Which question does it answer? What can it miss? What can it falsely flag?* Document where automated discovery ended and human validation began.

For high-impact or noisy techniques, use intentionally vulnerable local labs unless the external program clearly authorizes that specific method. Being able to run a tool is not evidence that using it on a production target is appropriate.

## 7. Learning record

For each exercise, distinguish:
- **Memorize:** definitions, formats, protocol semantics, and conditions required by the technique.
- **Understand:** why a control succeeds or fails, alternative explanations, and limitations.
- **Apply:** how to build and execute a permitted test, interpret the response, and report it.

Record commands only when they serve the question and are safe to publish. Maintain clear links between a claim, a tool result, a date, and a reproducible method.

## 8. Final quality check

- [ ] Scope and permitted technique verified for the date and asset.
- [ ] The claim is no stronger than its evidence level.
- [ ] Hypothesis is falsifiable and has meaningful controls.
- [ ] Environment, relevant versions, and input data are recorded.
- [ ] Positive/negative outcomes and alternative causes are addressed.
- [ ] Impact is demonstrated or explicitly left unconfirmed.
- [ ] Limitations and false positives are documented.
- [ ] Report is usable by a technical reviewer and does not disclose secrets.
- [ ] Documentation could be defended orally without relying on a scanner screenshot.

**Quality target:** a small number of well-controlled, reproducible experiments is better than a large inventory of unverified findings.
