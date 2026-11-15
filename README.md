# Bug Bounty Learning

Practical learning journey in Web Security, Bug Bounty Hunting and offensive security.

This repository documents a progressive, hands-on learning path focused on understanding web applications, identifying security weaknesses, validating findings in authorized environments and writing clear vulnerability reports.

## Environment

Primary system: Debian GNU/Linux

Main tools:
- Firefox
- Burp Suite
- curl
- Git
- Python 3
- Go
- subfinder
- dnsx
- httpx
- Nuclei
- ffuf
- jq

## Learning approach

The project follows this workflow:

```text
Scope
  ↓
Reconnaissance
  ↓
Attack surface mapping
  ↓
Hypothesis
  ↓
Manual testing
  ↓
Validation
  ↓
Evidence
  ↓
Report
```

The focus is not on collecting payloads or running tools blindly. The goal is to understand how applications work, why a vulnerability exists, how to validate it and how to communicate the impact.

## Repository structure

```text
docs/               Learning notes, roadmap and methodology
labs/               Controlled laboratory exercises
  portswigger/      PortSwigger Web Security Academy labs
  local/            Local intentionally vulnerable applications
recon/              Generic reconnaissance notes, templates and scripts
reports/            Report templates and sanitized examples
scripts/            Small reusable utilities
writeups/           Public writeups for labs and disclosed findings
```

## Responsible use

Only test systems where explicit authorization exists.

Do not commit:
- credentials
- session cookies
- API tokens
- private keys
- raw evidence containing third-party data
- private program targets
- undisclosed vulnerability details

Real bug bounty investigations should be kept outside this public repository until disclosure is permitted.

## Roadmap

See [docs/roadmap.md](docs/roadmap.md).

## Methodology and quality standard

See [docs/methodology.md](docs/methodology.md) and the [Professional Quality Standard](docs/professional-quality-standard.md). Each authorized lab or test should produce a [reproducible experiment record](reports/templates/experiment-record.md), including positive/negative controls, expected/actual outcomes, and limits of the conclusion. A vulnerability report is reserved for a validated issue, not an unexplained scanner result.

## Current status

Foundations underway: HTTP and Burp basics are recorded, and the first PortSwigger authentication lab is documented. Next focus: cookies/sessions, recon data quality, and controlled authorization testing. Progress is tracked in [docs/roadmap.md](docs/roadmap.md).
