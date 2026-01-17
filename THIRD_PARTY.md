# Third-Party Integrations & APIs

## Dev Arsenal - External Service Documentation

**Last Updated:** January 2026  
**Project:** Dev Arsenal - AI-Powered Blockchain IDE  
**Event:** LavaPunk Hackathon 2026

---

## Overview

Dev Arsenal integrates multiple third-party services and APIs to deliver a comprehensive development experience. This document outlines all external dependencies, their purposes, configuration requirements, and usage limits.

---

## Core Integrations

### 1. **Monaco Editor** (Microsoft)

**Purpose:** Primary code editor component  
**Version:** Latest (via CDN)  
**License:** MIT License  
**Website:** https://microsoft.github.io/monaco-editor/

**Features Used:**
- Multi-language syntax highlighting (JavaScript, Python, Solidity, Rust)
- IntelliSense and auto-completion
- Error diagnostics and linting
- Theme customization (VS Dark adaptation)
- Diff editor for Syntax Showdown

**Implementation:**
```typescript
// Loaded via Monaco React wrapper
import Editor from '@monaco-editor/react';
```

**Configuration:** No API key required  
**Rate Limits:** None (client-side library)

---

### 2. **OpenAI API** (GPT-4)

**Purpose:** AI-powered code analysis, optimization, and generation  
**Used In:** AI Cannon, Quality Shield, Bug Hunter  
**Website:** https://openai.com/api

**Endpoints Used:**
- `/v1/chat/completions` - Code analysis and suggestions
- Model: `gpt-4` or `gpt-3.5-turbo`

**Features:**
- Code optimization recommendations
- Bug detection and fixing
- Code quality scoring
- Security vulnerability analysis
- Performance improvement suggestions

**Required Configuration:**
```env
OPENAI_API_KEY=your_api_key_here
```

**Rate Limits:**
- Free Tier: 3 requests/minute
- Paid Tier: 3,500 requests/minute (GPT-4)
- Token limits apply per request

**Cost Estimation:**
- GPT-4: ~$0.03-0.06 per analysis (depending on code length)
- GPT-3.5-Turbo: ~$0.002 per analysis

**API Documentation:** https://platform.openai.com/docs

---

### 3. **Ethers.js** (Ethereum Library)

**Purpose:** Blockchain interaction for Base network  
**Version:** ^6.x  
**License:** MIT License  
**Website:** https://docs.ethers.org

**Used In:** Proof-of-Build module

**Features:**
- Wallet connection (MetaMask, WalletConnect)
- Smart contract interaction
- Transaction signing and broadcasting
- Event listening for on-chain verification

**Implementation:**
```typescript
import { ethers } from 'ethers';
```

**Network Configuration:**
- **Chain:** Base Mainnet
- **Chain ID:** 8453
- **RPC:** https://mainnet.base.org
- **Explorer:** https://basescan.org

**No API Key Required** (uses public RPC endpoints)

---

### 4. **IPFS / Pinata**

**Purpose:** Decentralized storage for code snapshots  
**Used In:** Code Vault, Proof-of-Build  
**Website:** https://pinata.cloud

**Features:**
- Permanent code storage
- Content addressing (CID generation)
- Distributed file retrieval
- Proof-of-existence for builds

**Required Configuration:**
```env
PINATA_API_KEY=your_pinata_api_key
PINATA_SECRET_API_KEY=your_pinata_secret
```

**API Endpoints:**
- `/pinning/pinJSONToIPFS` - Store code snapshots
- `/pinning/pinFileToIPFS` - Store build artifacts

**Rate Limits:**
- Free Tier: 1GB storage, 100 requests/month
- Paid Tier: Unlimited requests, scalable storage

**Pricing:**
- Starter: Free (1GB)
- Pro: $20/month (100GB)

**API Documentation:** https://docs.pinata.cloud

---

### 5. **Judge0 CE** (Code Execution Engine)

**Purpose:** Multi-language code compilation and execution  
**Used In:** Syntax Showdown (execution battles)  
**Website:** https://judge0.com

**Supported Languages:**
- JavaScript (Node.js)
- Python 3
- Rust
- Solidity (via Remix Compiler API)

**API Endpoints:**
- `/submissions` - Submit code for execution
- `/submissions/:token` - Get execution results

**Required Configuration:**
```env
JUDGE0_API_KEY=your_judge0_api_key
JUDGE0_ENDPOINT=https://judge0-ce.p.rapidapi.com
```

**Rate Limits (RapidAPI):**
- Free Tier: 50 requests/day
- Basic: 2,500 requests/month ($10)
- Pro: 10,000 requests/month ($30)

**Features:**
- Sandboxed execution environment
- Time and memory limit enforcement
- Compilation error reporting
- Output capture (stdout, stderr)

**API Documentation:** https://ce.judge0.com

---

### 6. **Remix Compiler API** (Solidity)

**Purpose:** Solidity smart contract compilation  
**Used In:** Arsenal HQ (Solidity language support)  
**Website:** https://remix.ethereum.org

**Features:**
- Solidity version management
- Contract compilation
- ABI generation
- Bytecode output

**Implementation:**
```typescript
// Loaded via CDN
import { compile } from '@remix-project/remix-solidity';
```

**Configuration:** No API key required (open-source)  
**Rate Limits:** None (client-side library)

---

## Analytics & Monitoring

### 7. **Vercel Analytics**

**Purpose:** App performance and usage tracking  
**Website:** https://vercel.com/analytics

**Metrics Tracked:**
- Page views and user sessions
- Core Web Vitals (LCP, FID, CLS)
- User geography and device info
- Feature usage statistics

**Configuration:** Auto-enabled on Vercel deployment  
**Privacy:** GDPR compliant, no cookies

---

### 8. **Sentry** (Error Tracking)

**Purpose:** Runtime error monitoring and debugging  
**Website:** https://sentry.io

**Features:**
- Real-time error notifications
- Stack trace analysis
- User context and breadcrumbs
- Performance monitoring

**Required Configuration:**
```env
NEXT_PUBLIC_SENTRY_DSN=your_sentry_dsn
```

**Rate Limits:**
- Developer: 5K errors/month (Free)
- Team: 50K errors/month ($26/month)

---

## Optional Integrations

### 9. **GitHub API** (Code Import/Export)

**Purpose:** Import repos, export snippets  
**Used In:** Arsenal Supply  
**Website:** https://docs.github.com/rest

**Endpoints:**
- `/repos/:owner/:repo/contents` - Fetch file contents
- `/gists` - Create code snippets

**Required Configuration:**
```env
GITHUB_TOKEN=your_github_personal_access_token
```

**Rate Limits:**
- Authenticated: 5,000 requests/hour
- Unauthenticated: 60 requests/hour

---

### 10. **Discord Webhook** (Notifications)

**Purpose:** Real-time notifications for leaderboard updates  
**Used In:** Performance Colosseum  
**Website:** https://discord.com/developers

**Configuration:**
```env
DISCORD_WEBHOOK_URL=your_webhook_url
```

**Rate Limits:** 30 requests/minute per webhook  
**No API Key Required**

---

## Security & Compliance

### API Key Management

**All API keys are stored securely:**
- Environment variables (`.env.local`)
- Never committed to version control
- Server-side only (Next.js API routes)

**Recommended .env.local structure:**
```env
# OpenAI
OPENAI_API_KEY=sk-...

# IPFS/Pinata
PINATA_API_KEY=...
PINATA_SECRET_API_KEY=...

# Code Execution
JUDGE0_API_KEY=...
JUDGE0_ENDPOINT=...

# GitHub (optional)
GITHUB_TOKEN=ghp_...

# Monitoring
NEXT_PUBLIC_SENTRY_DSN=...

# Discord (optional)
DISCORD_WEBHOOK_URL=...
```

### CORS & Security Headers

All third-party API calls are proxied through Next.js API routes (`/api/*`) to:
- Hide API keys from client
- Implement rate limiting
- Add request validation
- Enable CORS policies

---

## Cost Estimation (Monthly)

**Minimum (MVP):**
- OpenAI (GPT-3.5): ~$10/month (moderate usage)
- Pinata Free: $0
- Judge0 Basic: $10/month
- Vercel Hobby: $0
- **Total: ~$20/month**

**Recommended (Production):**
- OpenAI (GPT-4): ~$50-100/month
- Pinata Pro: $20/month
- Judge0 Pro: $30/month
- Vercel Pro: $20/month
- Sentry Team: $26/month
- **Total: ~$146-196/month**

**Enterprise Scale:**
- OpenAI Enterprise: Custom pricing
- Pinata Enterprise: Custom pricing
- Self-hosted Judge0: Infrastructure costs
- Vercel Enterprise: $150+/month
- **Total: $500-1000+/month**

---

## Fallback Strategies

### When APIs Fail:

1. **OpenAI Timeout/Error:**
   - Display cached suggestions
   - Offer manual code review checklist
   - Queue request for retry

2. **IPFS Upload Failure:**
   - Store code in browser localStorage
   - Retry upload automatically
   - Provide download option

3. **Judge0 Unavailable:**
   - Disable execution battles temporarily
   - Show syntax-only comparison
   - Alert user of service disruption

4. **Blockchain RPC Error:**
   - Switch to backup RPC endpoint
   - Use alternative Base RPC providers
   - Cache transaction data locally

---

## Compliance & Licensing

### Open Source Components:
- Monaco Editor: MIT License
- Ethers.js: MIT License
- React: MIT License
- Next.js: MIT License

### Commercial APIs:
- OpenAI: Terms of Service apply
- Pinata: Subscription agreement
- Judge0: RapidAPI marketplace terms

### Data Privacy:
- **No user code is stored** without explicit consent
- All IPFS uploads are user-initiated
- API logs are anonymized
- GDPR compliant data handling

---

## Support & Resources

### Contact Information:
- **Email:** support@elpeef.com
- **Telegram:** https://t.me/khudriakhmad
- **Discord:** @khudri_61362
- **GitHub:** https://github.com/mrbrightsides/devarsenal

### External Documentation:
- [OpenAI API Docs](https://platform.openai.com/docs)
- [Ethers.js Docs](https://docs.ethers.org)
- [Judge0 API Reference](https://ce.judge0.com)
- [Pinata API Guide](https://docs.pinata.cloud)
- [Monaco Editor API](https://microsoft.github.io/monaco-editor/api)

### Troubleshooting:
- Check API key validity in `.env.local`
- Verify rate limit status on provider dashboards
- Review Next.js API route logs (`/api/*`)
- Test endpoints using Postman/Insomnia

---

## Changelog

**January 2026:**
- Initial third-party integration documentation
- Added LavaPunk Hackathon 2026 reference
- Configured Base blockchain integration
- Implemented OpenAI GPT-4 for code analysis

---

**Built for LavaPunk Hackathon 2026**  
Dev Arsenal - Where AI Meets Blockchain Development

**Repository:** https://github.com/mrbrightsides/devarsenal  
**License:** MIT (for open-source components)
