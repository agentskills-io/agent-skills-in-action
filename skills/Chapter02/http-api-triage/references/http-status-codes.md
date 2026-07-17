# Acme Corp HTTP Status Code Guide

Use this mapping to diagnose API responses.

## Client Errors (4xx)
* **400 Bad Request:**
    * *Meaning:* The JSON payload is malformed or missing required fields.
    * *Action:* Validate `input_schema` against the request body. Check for trailing commas.
* **401 Unauthorized:**
    * *Meaning:* Authentication token is missing or invalid.
    * *Action:* Check if the `Authorization: Bearer` header is present. Check token expiration.
* **403 Forbidden:**
    * *Meaning:* Token is valid, but permissions are lacking (Scope Error).
    * *Action:* Compare user scopes (e.g., `read:reports`) against required endpoint scopes.
* **404 Not Found:**
    * *Meaning:* Resource ID is wrong OR the URL path is typoed.
    * *Action:* Verify the UUID format. Check for double slashes `//` in the URL.
* **429 Too Many Requests:**
    * *Meaning:* Rate limit exceeded.
    * *Action:* Check the `Retry-After` header. Do NOT retry immediately.

## Server Errors (5xx)
* **500 Internal Server Error:**
    * *Meaning:* Unhandled exception in backend code.
    * *Action:* Escalation required. Capture the `X-Request-ID` and search Splunk logs.
* **502/503/504 Gateway Errors:**
    * *Meaning:* Upstream service is down or timing out.
    * *Action:* Check the "System Status Page." Suggest exponential backoff.
