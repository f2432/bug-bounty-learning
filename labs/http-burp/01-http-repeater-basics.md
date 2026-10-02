# Session 01 — HTTP and Burp Suite Repeater Basics

Date: 2026-10-02

## Objective

Understand HTTP request/response flow with Burp Suite and use Repeater to modify requests manually.

Environment:

- Debian GNU/Linux
- Burp Suite Community Edition v2026.8
- Burp embedded browser
- HTTP/2 target

## What was practiced

### 1. Proxy and HTTP history

The Burp browser was used to generate requests while Burp recorded them in:

```text
Proxy → HTTP history
```

This made it possible to inspect requests and responses independently from the rendered page.

### 2. Repeater

A request was sent from HTTP history to Repeater and modified manually.

The basic workflow became:

```text
observe request
→ change one element
→ send
→ compare response
→ interpret
```

### 3. Public resource

A public text resource was requested:

```http
GET /robots.txt HTTP/2
Host: <authorized-target>
```

Result:

```http
HTTP/2 200 OK
Content-Type: text/plain
```

Removing the original browser cookies did not prevent access. This showed that the resource was public and did not depend on the existing browser session.

### 4. REST API discovery

A WordPress REST API root was queried:

```http
GET /wp-json/ HTTP/2
Host: <authorized-target>
```

The response returned JSON and exposed API namespaces.

A namespace endpoint was then queried:

```http
GET /wp-json/wp/v2/ HTTP/2
Host: <authorized-target>
```

The response described routes, methods and arguments.

This demonstrated that an API may expose a machine-readable map of its own surface.

### 5. Collections and resources

A collection request:

```http
GET /wp-json/wp/v2/posts HTTP/2
```

returned multiple objects.

A single resource request:

```http
GET /wp-json/wp/v2/posts/<id> HTTP/2
```

returned one object.

Conceptually:

```text
/posts
→ collection

/posts/<id>
→ individual resource
```

### 6. Query parameters and pagination

The parameter:

```http
GET /wp-json/wp/v2/posts?per_page=1 HTTP/2
```

changed the number of objects returned per page.

The response headers exposed pagination metadata such as:

```text
X-WP-Total
X-WP-TotalPages
Link
```

This showed how query parameters influence an API response without changing the underlying collection.

### 7. Authorization boundary

The same resource was compared using different methods.

Public read:

```http
GET /wp-json/wp/v2/posts/<id> HTTP/2
```

Result:

```text
200 OK
```

Unauthenticated write attempt:

```http
POST /wp-json/wp/v2/posts/<id> HTTP/2
```

Result:

```text
401 Unauthorized
rest_cannot_edit
```

This demonstrated an important distinction:

```text
resource exists
≠
every operation on the resource is authorized
```

## Key concepts learned

- HTTP request and response anatomy
- GET and POST
- status codes 200 and 401
- headers
- cookies and session context
- Burp Proxy
- HTTP history
- Burp Repeater
- REST API
- namespace
- route
- method
- collection
- individual resource
- query parameter
- pagination
- authorization

## Security mindset

The session reinforced a useful testing discipline:

```text
Change one thing at a time.
Observe the exact response.
Separate evidence from assumptions.
Do not treat exposed endpoints as vulnerabilities by themselves.
```

## Next step

Move to a controlled training environment and continue with:

- authenticated vs unauthenticated requests
- session handling
- access control
- first PortSwigger Web Security Academy lab
