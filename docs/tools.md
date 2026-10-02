# Tools

This file records what each tool is for. Installation commands are intentionally kept separate from methodology.

## Browser

### Firefox
Used for normal interaction with web applications and integration with Burp Suite.

### Browser DevTools
Useful for inspecting:
- requests
- responses
- JavaScript
- storage
- cookies
- frontend behaviour

## HTTP

### curl
Manual HTTP client for reproducing and validating requests.

### Burp Suite
Primary tool for manual web testing.

Initial modules:
- Proxy
- HTTP history
- Repeater
- Decoder
- Comparer

Later:
- Intruder
- Logger

## Reconnaissance

### subfinder
Passive subdomain enumeration.

### dnsx
DNS resolution and validation.

### httpx
HTTP/HTTPS probing and service metadata.

### Nuclei
Template-based detection. Results must be validated manually.

### ffuf
Content and parameter discovery.

## Data processing

### jq
JSON processing from the command line.

### Python 3
Automation, parsing and small custom tools.

### Go
Required by several ProjectDiscovery and security tools.

## Rule

A tool result is evidence to investigate, not automatically a vulnerability.
