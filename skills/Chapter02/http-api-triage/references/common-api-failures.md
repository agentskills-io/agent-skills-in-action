# Common Network & Protocol Failures (SOP-NET-01)

This reference document outlines common non-HTTP failures encountered when interacting with internal and external APIs. Use this to diagnose connection drops, timeouts, and security blocks.

## 1. Connectivity & DNS Issues
These errors occur before the request even reaches the server application.

### DNS Resolution Failure (`NXDOMAIN` / `ENOTFOUND`)
* **Symptom:** Logs show "Host not found," "getaddrinfo EAI_AGAIN," or "Name resolution failed."
* **Likely Root Causes:**
    1.  **Typo:** The URL is misspelled (e.g., `api.acme.interal` instead of `.internal`).
    2.  **VPN/Intranet:** The agent is running outside the corporate VPN and cannot resolve private domains.
    3.  **Dangling DNS:** The service was decommissioned, but the CNAME record remains.
* **Recommended Fix:** Verify the hostname spelling. Check if the environment (Staging vs. Prod) requires a VPN connection.

### Connection Refused (`ECONNREFUSED`)
* **Symptom:** TCP handshake fails immediately.
* **Likely Root Causes:**
    1.  **Service Down:** The process is not running on the target server.
