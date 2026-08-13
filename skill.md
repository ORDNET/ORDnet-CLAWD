---
metadata: {"openclaw":{"emoji":"🌐","category":"web3","homepage":"https://clawdbot.ordnet.io","api_base":"https://app.ordnet.io"}}
user-invocable: true
---

# ORDnet Web3 Hosting Skill

Inscribe HTML content permanently on the Bitcoin SV blockchain and register .web3 domains.

## Overview

ORDnet provides decentralized, permanent web hosting through blockchain inscription. Content inscribed on the blockchain cannot be taken down, censored, or removed.

**Key Benefits:**
- Permanent storage (content exists as long as the blockchain exists)
- Censorship-resistant
- No recurring hosting fees
- One-time cost (typically less than $0.01)
- Human-readable .web3 domains
- Direct AI access via ai.ordnet.io

## Services

| Service | URL | Purpose |
|---------|-----|---------|
| ORD/app | https://app.ordnet.io | Create wallet, inscribe content |
| ORD/domains | https://domains.ordnet.io | Register .web3 domains |
| ORD/browser | https://browser.ordnet.io | View .web3 sites (for humans) |
| AI Endpoint | https://ai.ordnet.io | Direct content access (for AI agents) |
| Health API | https://names.ordnet.io/health | Check service status |

## Content Access: Humans vs AI Agents

| Audience | Endpoint | Format |
|----------|----------|--------|
| **Humans** | browser.ordnet.io | Full browser UI |
| **AI Agents** | ai.ordnet.io/{identifier} | HTML content |
| **AI Agents** | ai.ordnet.io/raw/{identifier} | Raw content (recommended) |

### AI Content Access (ai.ordnet.io)

AI agents should use `ai.ordnet.io` for direct content access:

```
# HTML content (with minimal wrapper)
https://ai.ordnet.io/{txid}
https://ai.ordnet.io/{domain}.web3

# Raw content - Method 1: Dedicated /raw/ endpoint (RECOMMENDED)
https://ai.ordnet.io/raw/{txid}
https://ai.ordnet.io/raw/{domain}.web3

# Raw content - Method 2: Suffix -raw
https://ai.ordnet.io/{txid}-raw
https://ai.ordnet.io/{domain}.web3-raw

# Raw content - Method 3: Query parameter ?raw=1
https://ai.ordnet.io/{txid}?raw=1
https://ai.ordnet.io/{domain}.web3?raw=1

# WHOIS lookup (domain info)
https://ai.ordnet.io/whois/{domain}.web3
```

**Examples:**
```
# HTML content
https://ai.ordnet.io/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff
https://ai.ordnet.io/example.web3

# Raw content (recommended: /raw/ endpoint)
https://ai.ordnet.io/raw/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff
https://ai.ordnet.io/raw/example.web3

# Raw content (suffix method)
https://ai.ordnet.io/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff-raw
https://ai.ordnet.io/example.web3-raw

# Raw content (query parameter)
https://ai.ordnet.io/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff?raw=1

# WHOIS lookup
https://ai.ordnet.io/whois/example.web3
```

**Raw Content Methods Summary:**
| Method | Example | Notes |
|--------|---------|-------|
| `/raw/{id}` | `ai.ordnet.io/raw/example.web3` | ✅ Recommended |
| `{id}-raw` | `ai.ordnet.io/example.web3-raw` | Suffix method |
| `{id}?raw=1` | `ai.ordnet.io/example.web3?raw=1` | Query parameter |

## Step-by-Step Guide

### Step 1: Create Account
Navigate to https://app.ordnet.io and create a new account. This generates a BSV wallet for you.

**What you'll receive:**
- BSV wallet address (starts with `1`)
- Dashboard access
- Inscription tools

### Step 2: Fund Your Wallet
Your wallet needs BSV to pay for inscriptions. Options:

**Via an exchange:**
1. Buy BSV at an exchange that lists it — MEXC (https://www.mexc.com), Gate (https://www.gate.io) or KuCoin (https://www.kucoin.com)
2. Withdraw to your BSV wallet address
3. Small amounts go a long way: an inscription costs well under a cent

**Exchange Method (for larger amounts):**
- MEXC: https://www.mexc.com
- Gate.io: https://www.gate.io
- KuCoin: https://www.kucoin.com

**Cost Guide:**
| Content Size | Estimated Cost |
|--------------|----------------|
| Simple HTML (<1KB) | < $0.001 |
| Standard page (5KB) | ~$0.005 |
| Rich content (50KB) | ~$0.05 |
| Large app (500KB) | ~$0.50 |

### Step 3: Create Your Content
Create your HTML content. Example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Web3 Page</title>
    <style>
        body { 
            font-family: sans-serif; 
            text-align: center; 
            padding: 50px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            min-height: 100vh;
        }
        h1 { font-size: 3rem; margin-bottom: 20px; }
        p { font-size: 1.2rem; opacity: 0.9; }
    </style>
</head>
<body>
    <h1>🌐 Hello Web3!</h1>
    <p>This page is permanently stored on the blockchain.</p>
    <p>Created by [Agent Name] on [Date]</p>
</body>
</html>
```

### Step 4: Inscribe to Blockchain
1. Go to https://app.ordnet.io
2. Select "Inscribe" or "Upload HTML"
3. Paste or upload your content
4. Confirm the transaction
5. **Save the TXID** (64-character hex string)

**Example TXID:** `11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff`

### Step 5: Register .web3 Domain
1. Go to https://domains.ordnet.io
2. Connect your wallet
3. Search for available domain
4. Register the domain

**Domain Pricing:**
| Length | Price | Example |
|--------|-------|---------|
| 1-5 chars | $5 (premium) | `ai.web3` |
| 6-9 chars | $1 | `myagent.web3` |
| 10+ chars | Free | `myfirstpage.web3` |

### Step 6: Connect Domain to Content
1. In domain settings, add your TXID as the target
2. The domain now points to your inscribed content

### Step 7: View Your Creation

**For Humans:**
Visit https://browser.ordnet.io and enter your .web3 domain or TXID.

**For AI Agents:**
```
# HTML content
https://ai.ordnet.io/{your-domain}.web3
https://ai.ordnet.io/{your-txid}

# Raw content (recommended)
https://ai.ordnet.io/raw/{your-domain}.web3
https://ai.ordnet.io/raw/{your-txid}

# Raw content (alternatives)
https://ai.ordnet.io/{your-txid}-raw
https://ai.ordnet.io/{your-txid}?raw=1
```

## Verify Your Setup

After completing the steps, verify everything works:

**Check wallet balance:**
```
Visit https://app.ordnet.io and check your dashboard
Balance should show > 0 BSV
```

**Test inscription (AI agents):**
```
# HTML content
GET https://ai.ordnet.io/{YOUR_TXID}

# Raw content (recommended)
GET https://ai.ordnet.io/raw/{YOUR_TXID}

# Raw content (alternatives)
GET https://ai.ordnet.io/{YOUR_TXID}-raw
GET https://ai.ordnet.io/{YOUR_TXID}?raw=1

Example (working):
https://ai.ordnet.io/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff
https://ai.ordnet.io/raw/11e344e6c424d0dfb00b9190e5cdde17d7ff1e9661d9a99f08365c9b64bdf0ff
```

**Check domain WHOIS:**
```
GET https://ai.ordnet.io/whois/{domain}.web3

Example:
https://ai.ordnet.io/whois/example.web3
```

**Check service health:**
```
GET https://names.ordnet.io/health

Expected response:
{
  "ok": true,
  "domains": <number>,
  "reserved": <number>,
  "uptime": <seconds>
}
```

## Example Workflow

```
Agent Task: Create a Web3 presence for "TechBot"

1. Created account at app.ordnet.io
   → Wallet: 1ABC...XYZ
   
2. Funded from an exchange
   → Withdrew 0.001 BSV to the wallet
   
3. Created HTML landing page
   → Professional design with bot info
   
4. Inscribed content
   → TXID: abc123...def456
   
5. Registered techbot.web3
   → Cost: Free (10+ chars)
   
6. Connected TXID to domain
   → techbot.web3 → abc123...def456
   
7. Verified access:
   → Humans: https://browser.ordnet.io/techbot.web3
   → AI (HTML): https://ai.ordnet.io/techbot.web3 ✅
   → AI (Raw): https://ai.ordnet.io/raw/techbot.web3 ✅
   → WHOIS: https://ai.ordnet.io/whois/techbot.web3 ✅
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Insufficient balance | Fund wallet from an exchange (MEXC, Gate, KuCoin) |
| Domain taken | Try alternative name or longer variant |
| TXID not showing | Wait 1-2 minutes for blockchain confirmation |
| Page not loading | Verify TXID is correctly linked to domain |
| Swap failed | Check minimum amounts (varies by coin) |

## Security Notes

⚠️ **Important:**
- Keep your wallet seed phrase secure - never share it
- Inscriptions are permanent and cannot be edited or deleted
- Content is public and visible to everyone
- Domain ownership is tied to your wallet

## API Reference

**Health Check:**
```
GET https://names.ordnet.io/health
Returns: { ok, domains, reserved, flagged, uptime }
```

**WHOIS Lookup:**
```
GET https://ai.ordnet.io/whois/{domain}.web3
Returns: { available, content_url, registration_url, ... }
```

**Content Retrieval (for AI agents):**
```
# HTML content
GET https://ai.ordnet.io/{txid}
GET https://ai.ordnet.io/{domain}.web3

# Raw content (dedicated endpoint - recommended)
GET https://ai.ordnet.io/raw/{txid}
GET https://ai.ordnet.io/raw/{domain}.web3

# Raw content (suffix method)
GET https://ai.ordnet.io/{txid}-raw
GET https://ai.ordnet.io/{domain}.web3-raw

# Raw content (query parameter)
GET https://ai.ordnet.io/{txid}?raw=1
GET https://ai.ordnet.io/{domain}.web3?raw=1
```

**Content Retrieval (for humans):**
```
Browser: https://browser.ordnet.io/{domain}.web3
Browser: https://browser.ordnet.io/{txid}
```

## Installation

```bash
mkdir -p ~/.openclaw/skills/ordnet
curl -s https://clawdbot.ordnet.io/skill.md > ~/.openclaw/skills/ordnet/SKILL.md
curl -s https://clawdbot.ordnet.io/heartbeat.md > ~/.openclaw/skills/ordnet/HEARTBEAT.md
curl -s https://clawdbot.ordnet.io/skill.json > ~/.openclaw/skills/ordnet/package.json
```

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────┐
│  ORDnet Quick Reference for AI Agents                   │
├─────────────────────────────────────────────────────────┤
│  📝 Create/Inscribe:  https://app.ordnet.io             │
│  💱 Get BSV:          exchange (MEXC / Gate / KuCoin)   │
│  🌐 Register Domain:  https://domains.ordnet.io         │
│  👤 Human Browser:    https://browser.ordnet.io         │
│  ❤️ Health Check:     https://names.ordnet.io/health    │
├─────────────────────────────────────────────────────────┤
│  🤖 AI Access:                                          │
│    • HTML:    ai.ordnet.io/{identifier}                 │
│    • Raw:     ai.ordnet.io/raw/{identifier}  (best)     │
│    • Raw:     ai.ordnet.io/{identifier}-raw             │
│    • Raw:     ai.ordnet.io/{identifier}?raw=1           │
│    • WHOIS:   ai.ordnet.io/whois/{domain}.web3          │
└─────────────────────────────────────────────────────────┘
```

## Support

- Website: https://ordnet.io
- Tutorial: https://hello.ordnet.io
- AI Skill: https://clawdbot.ordnet.io
- Twitter: https://x.com/ORDNETio
- Telegram: https://t.me/ORDNET.io

---

*Your content is permanently stored on the blockchain. No one can take it down, censor it, or remove it. Welcome to true digital ownership.*
