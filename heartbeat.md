---
metadata: {"openclaw":{"emoji":"💓","category":"maintenance"}}
---

# ORDnet Heartbeat Routine

Periodic maintenance checks for your ORDnet Web3 presence.

## Purpose

This heartbeat routine monitors your ORDnet resources and alerts you to issues requiring attention.

## Recommended Frequency

| Activity Level | Check Interval | Use Case |
|----------------|----------------|----------|
| **Active** | Every 4 hours | Frequently updating content, managing multiple domains |
| **Normal** | Every 8 hours | Standard maintenance, occasional updates |
| **Quiet** | Every 24 hours | Static content, minimal changes |
| **Minimal** | Every 48 hours | Archive pages, rarely accessed content |

## Checks to Perform

### 1. Wallet Balance Check
```
Action: Check BSV balance at app.ordnet.io
Threshold: Alert if balance < 0.0001 BSV (~$0.005)
Why: Ensures you can make inscriptions when needed
```

### 2. Service Health Check
```
Action: GET https://names.ordnet.io/health
Expected: { "ok": true, "uptime": >0 }
Alert if: ok !== true or request fails
```

### 3. Domain Status Check (via ai.ordnet.io)
```
Action: Verify each .web3 domain resolves

# Test HTML content
GET https://ai.ordnet.io/{domain}.web3

# Test raw content (recommended method)
GET https://ai.ordnet.io/raw/{domain}.web3

# Alternative raw methods
GET https://ai.ordnet.io/{domain}.web3-raw
GET https://ai.ordnet.io/{domain}.web3?raw=1

Expected: Returns content (status 200)
Alert if: Returns error or empty response
```

### 4. Inscription Verification (via ai.ordnet.io)
```
Action: Verify recent inscriptions are accessible

# HTML content
GET https://ai.ordnet.io/{txid}

# Raw content (recommended)
GET https://ai.ordnet.io/raw/{txid}

# Alternative raw methods
GET https://ai.ordnet.io/{txid}-raw
GET https://ai.ordnet.io/{txid}?raw=1

Expected: Returns inscribed content (status 200)
Alert if: Content not found or corrupted
```

### 5. WHOIS Lookup Check
```
Action: Verify domain registration info

GET https://ai.ordnet.io/whois/{domain}.web3

Expected: Returns domain info (status 200)
Alert if: Domain not found or API error
```

## AI Agent Access Endpoints

Use these endpoints for programmatic checks:

| Check Type | Endpoint | Notes |
|------------|----------|-------|
| HTML by TXID | `ai.ordnet.io/{txid}` | |
| HTML by Domain | `ai.ordnet.io/{domain}.web3` | |
| Raw (recommended) | `ai.ordnet.io/raw/{identifier}` | ✅ Best method |
| Raw (suffix) | `ai.ordnet.io/{identifier}-raw` | |
| Raw (query) | `ai.ordnet.io/{identifier}?raw=1` | |
| WHOIS | `ai.ordnet.io/whois/{domain}.web3` | Domain info |
| Health | `names.ordnet.io/health` | Service status |

**Example verification script:**
```javascript
// Check inscription - HTML content
const htmlResponse = await fetch('https://ai.ordnet.io/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff');
if (!htmlResponse.ok) console.error('HTML content not accessible');

// Check inscription - Raw content (recommended method)
const rawResponse = await fetch('https://ai.ordnet.io/raw/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff');
if (!rawResponse.ok) console.error('Raw content not accessible');

// Check domain resolution
const domainResponse = await fetch('https://ai.ordnet.io/example.web3');
if (!domainResponse.ok) console.error('Domain not resolving');

// Check WHOIS
const whoisResponse = await fetch('https://ai.ordnet.io/whois/example.web3');
if (!whoisResponse.ok) console.error('WHOIS lookup failed');

// Check service health
const healthResponse = await fetch('https://names.ordnet.io/health');
const health = await healthResponse.json();
if (!health.ok) console.error('Service unhealthy');
```

## Sample Notification Messages

### Low Balance Alert
```
⚠️ ORDnet Wallet Balance Low

Your BSV balance is {balance} BSV (~${usd_value}).
This may not be enough for new inscriptions.

Action needed: Fund your wallet at https://swap.ordnet.io
```

### Service Outage Alert
```
🔴 ORDnet Service Issue Detected

The ORDnet health check failed at {timestamp}.
Service: {service_name}
Status: {error_message}

Monitor: https://names.ordnet.io/health
```

### Domain Issue Alert
```
⚠️ Domain Resolution Issue

Your domain {domain}.web3 is not resolving correctly.

Tested endpoints:
- HTML: https://ai.ordnet.io/{domain}.web3
- Raw: https://ai.ordnet.io/raw/{domain}.web3
- WHOIS: https://ai.ordnet.io/whois/{domain}.web3

Possible causes:
- TXID not yet confirmed (wait 2-5 minutes)
- Domain-TXID connection lost
```

### All Clear Message
```
✅ ORDnet Health Check Passed

All systems operational at {timestamp}.

📊 Status:
- Wallet balance: {balance} BSV ✓
- Service health: Online ✓
- Domains checked: {domain_count} ✓
- Inscriptions verified: {inscription_count} ✓
```

## State Tracking

Maintain this state between heartbeat runs:

```json
{
  "last_check": "2025-01-15T10:30:00Z",
  "check_interval_hours": 8,
  "wallet_address": "1YourBsvAddressHere",
  "domains": [
    {
      "name": "example.web3",
      "txid": "abc123...",
      "endpoints": {
        "html": "https://ai.ordnet.io/example.web3",
        "raw": "https://ai.ordnet.io/raw/example.web3",
        "whois": "https://ai.ordnet.io/whois/example.web3"
      },
      "status": "ok"
    }
  ],
  "consecutive_failures": 0
}
```

## Quick Reference

```
┌─────────────────────────────────────────────────────────┐
│  Heartbeat Endpoints                                    │
├─────────────────────────────────────────────────────────┤
│  Health:      GET https://names.ordnet.io/health        │
│  HTML:        GET https://ai.ordnet.io/{id}             │
│  Raw (best):  GET https://ai.ordnet.io/raw/{id}         │
│  Raw (suffix):GET https://ai.ordnet.io/{id}-raw         │
│  Raw (query): GET https://ai.ordnet.io/{id}?raw=1       │
│  WHOIS:       GET https://ai.ordnet.io/whois/{domain}   │
├─────────────────────────────────────────────────────────┤
│  Note: Use ai.ordnet.io for AI agent checks             │
│        browser.ordnet.io is for human viewing only      │
└─────────────────────────────────────────────────────────┘
```

---

*Keeping your Web3 presence healthy and accessible.*
