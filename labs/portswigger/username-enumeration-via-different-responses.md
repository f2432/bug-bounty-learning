# Username enumeration via different responses

**Platform:** PortSwigger Web Security Academy  
**Area:** Authentication  
**Status:** Completed  
**Date:** 2026-10-02

## Objective

Understand how an authentication mechanism can disclose whether a username exists by returning observably different responses for valid and invalid usernames.

## Vulnerability

The application provides different feedback depending on whether the submitted username exists. Even when the login fails in both cases, the difference in the server response can act as an oracle for username enumeration.

Once a valid username is identified, the attack surface is reduced from guessing both username and password to testing passwords for a known account.

## Methodology

1. Capture a normal login request.
2. Identify the parameters used for username and password.
3. Keep the password fixed and vary the username.
4. Compare the HTTP responses.
5. Look for a stable difference such as response text, status code, response length or another observable property.
6. Identify a username that produces the distinct response.
7. Use the confirmed username in the next authentication test.
8. Validate the result in the lab environment.

## What to observe

The important point is not simply that authentication fails. The relevant signal is that the application reacts differently depending on whether the username exists.

This behaviour creates an information disclosure issue in the authentication workflow.

## Security impact

Username enumeration can help an attacker:

- identify valid accounts;
- improve password guessing efficiency;
- focus credential-stuffing attempts;
- discover privileged or interesting account names;
- combine account discovery with other authentication weaknesses.

## Mitigation

Authentication responses should be consistent for invalid usernames and invalid passwords.

Applications should avoid observable differences in:

- error messages;
- HTTP status codes;
- response size;
- response timing, where practical;
- other metadata that reveals whether an account exists.

Rate limiting, monitoring and multi-factor authentication provide additional protection but do not replace consistent authentication responses.

## Lesson learned

A failed login response can still leak useful information.

When testing authentication, compare responses carefully instead of looking only at whether the login succeeded or failed.

## Ethics

This exercise was performed in the PortSwigger Web Security Academy training environment.
