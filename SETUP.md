# Dev Arsenal - Setup Guide

> **LavaPunk Hackathon 2026 Submission**  
> A blockchain-integrated IDE with AI-assisted development capabilities

This guide provides comprehensive setup instructions for developers, judges, and contributors who want to run Dev Arsenal locally or deploy it to production.

---

## 📋 Prerequisites

Before setting up Dev Arsenal, ensure the following tools are installed:

- **Node.js** 18.0 or higher ([Download](https://nodejs.org/))
- **npm** or **pnpm** (pnpm recommended for faster installations)
- **Git** for version control
- **Modern web browser** (Chrome, Firefox, Safari, or Edge)
- **Ethereum wallet** (optional, for blockchain features)

### Recommended System Requirements

- **RAM:** 4GB minimum, 8GB recommended
- **Storage:** 500MB free space for dependencies
- **OS:** Windows 10+, macOS 10.15+, or Linux (Ubuntu 20.04+)

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/mrbrightsides/devarsenal.git
cd devarsenal
```

### 2. Install Dependencies

Using npm:
```bash
npm install
```

Using pnpm (recommended):
```bash
pnpm install
```

### 3. Configure Environment Variables

Create a `.env.local` file in the root directory:

```bash
cp .env.example .env.local
```

Edit `.env.local` and add the required API keys (see Configuration section below).

### 4. Run Development Server

```bash
npm run dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in the browser to access Dev Arsenal.

---

## ⚙️ Environment Configuration

Dev Arsenal requires several API keys and configuration values. Create a `.env.local` file with the following variables:

### Essential Configuration

```env
# OpenAI API (Required for AI Cannon, Quality Shield, Bug Hunter)
OPENAI_API_KEY=sk-proj-xxxxxxxxxxxxxxxxxxxxx

# Base Blockchain Configuration (Required for Proof-of-Build)
NEXT_PUBLIC_ALCHEMY_API_KEY=your_alchemy_api_key_here
NEXT_PUBLIC_BASE_RPC_URL=https://base-mainnet.g.alchemy.com/v2/your_key
NEXT_PUBLIC_BASE_CHAIN_ID=8453

# IPFS/Pinata Configuration (Required for Code Vault)
NEXT_PUBLIC_PINATA_API_KEY=your_pinata_api_key
NEXT_PUBLIC_PINATA_SECRET_KEY=your_pinata_secret_key
NEXT_PUBLIC_PINATA_JWT=your_pinata_jwt_token

# Judge0 CE API (Optional - for code execution)
JUDGE0_API_URL=https://judge0-ce.p.rapidapi.com
JUDGE0_API_KEY=your_rapidapi_key

# Error Monitoring (Optional but recommended)
NEXT_PUBLIC_SENTRY_DSN=your_sentry_dsn
SENTRY_AUTH_TOKEN=your_sentry_auth_token
```

### API Keys Setup Instructions

#### OpenAI API Key
1. Visit [platform.openai.com](https://platform.openai.com/)
2. Create an account or sign in
3. Navigate to API Keys section
4. Generate a new secret key
5. Copy the key to `OPENAI_API_KEY` in `.env.local`

#### Alchemy API Key (Base Network)
1. Visit [alchemy.com](https://www.alchemy.com/)
2. Create a free account
3. Create a new app and select "Base" network
4. Copy the API key to `NEXT_PUBLIC_ALCHEMY_API_KEY`
5. Use the provided RPC URL for `NEXT_PUBLIC_BASE_RPC_URL`

#### Pinata IPFS Credentials
1. Visit [pinata.cloud](https://pinata.cloud/)
2. Sign up for a free account
3. Go to API Keys section
4. Create a new API key with admin permissions
5. Copy API Key, API Secret, and JWT to respective variables

#### Judge0 CE API (Optional)
1. Visit [RapidAPI Judge0](https://rapidapi.com/judge0-official/api/judge0-ce)
2. Subscribe to the free tier
3. Copy the API key to `JUDGE0_API_KEY`

**Self-Hosted Option:** Deploy Judge0 CE on a private server using [Docker](https://github.com/judge0/judge0) for unlimited executions.

#### Sentry Error Monitoring (Optional)
1. Visit [sentry.io](https://sentry.io/)
2. Create a new project
3. Copy the DSN to `NEXT_PUBLIC_SENTRY_DSN`
4. Generate an auth token for source maps

---

## 🏗️ Build and Deployment

### Local Production Build

Test the production build locally:

```bash
npm run build
npm start
```

The production server will start on port 3000.

### Deploy to Vercel (Recommended)

Dev Arsenal is optimized for Vercel deployment:

1. **Install Vercel CLI:**
   ```bash
   npm install -g vercel
   ```

2. **Login to Vercel:**
   ```bash
   vercel login
   ```

3. **Deploy:**
   ```bash
   vercel
   ```

4. **Add Environment Variables:**
   - Go to Vercel Dashboard → Project Settings → Environment Variables
   - Add all variables from `.env.local`
   - Deploy again to apply changes

### Deploy to Other Platforms

Dev Arsenal can also be deployed to:
- **Netlify:** Use `npm run build` and deploy the `.next` folder
- **Railway:** Connect GitHub repo and add environment variables
- **AWS Amplify:** Configure build settings with Next.js preset
- **Docker:** Use the provided Dockerfile (see Docker section below)

---

## 🐳 Docker Deployment

Build and run Dev Arsenal using Docker:

```bash
# Build the image
docker build -t devarsenal .

# Run the container
docker run -p 3000:3000 --env-file .env.local devarsenal
```

Using Docker Compose:

```bash
docker-compose up -d
```

---

## 🧪 Testing

### Run Development Tests

```bash
npm run test
```

### Run Build Verification

Ensure all TypeScript types are correct:

```bash
npm run type-check
```

### Lint Code

Check code quality:

```bash
npm run lint
```

---

## 🔧 Troubleshooting

### Common Issues and Solutions

#### 1. Monaco Editor SSR Errors

**Issue:** `ReferenceError: window is not defined` or `document is not defined`

**Solution:** Monaco Editor is already configured with `'use client'` directive and dynamic imports. If errors persist, clear `.next` cache:

```bash
rm -rf .next
npm run dev
```

#### 2. API Rate Limits

**Issue:** OpenAI or Judge0 returns 429 Too Many Requests

**Solution:** 
- Implement request throttling on the client side
- Upgrade to paid tier for higher limits
- Use self-hosted Judge0 for unlimited code executions

#### 3. Blockchain Connection Failures

**Issue:** Unable to connect to Base network

**Solution:**
- Verify `NEXT_PUBLIC_BASE_RPC_URL` is correct
- Check Alchemy API key validity
- Ensure wallet extension (MetaMask) is installed
- Switch wallet network to Base mainnet (Chain ID: 8453)

#### 4. IPFS Upload Failures

**Issue:** Pinata upload returns 401 or 403 errors

**Solution:**
- Verify all three Pinata credentials (API Key, Secret, JWT)
- Check API key permissions (must have pinning rights)
- Ensure JWT token hasn't expired

#### 5. Module Not Found Errors

**Issue:** `Cannot find module '@/components/...'`

**Solution:**
```bash
rm -rf node_modules package-lock.json
npm install
```

#### 6. Build Errors in Production

**Issue:** Build fails with TypeScript errors

**Solution:**
```bash
npm run type-check
```
Fix all type errors before building. Dev Arsenal uses strict TypeScript mode.

---

## 📂 Project Structure

```
devarsenal/
├── src/
│   ├── app/                  # Next.js app router
│   │   ├── api/              # API routes
│   │   │   ├── ai-battle/
│   │   │   ├── analyze-error/
│   │   │   ├── compile/
│   │   │   ├── ipfs-upload/
│   │   │   ├── optimize-code/
│   │   │   ├── proof-of-build/
│   │   │   └── quality-scan/
│   │   ├── layout.tsx        # Root layout
│   │   └── page.tsx          # Main application page
│   ├── components/           # React components
│   │   ├── ui/               # shadcn/ui components
│   │   ├── ai-cannon.tsx
│   │   ├── code-editor.tsx
│   │   ├── syntax-showdown.tsx
│   │   └── ...
│   ├── hooks/                # Custom React hooks
│   ├── lib/                  # Utility functions
│   └── utils/                # Helper utilities
├── public/                   # Static assets
├── .env.local                # Environment variables (not in repo)
├── .env.example              # Example environment file
├── next.config.js            # Next.js configuration
├── package.json              # Dependencies
├── tsconfig.json             # TypeScript configuration
└── tailwind.config.ts        # Tailwind CSS configuration
```

---

## 🛠️ Development Workflow

### Adding New Features

1. Create feature branch:
   ```bash
   git checkout -b feature/new-weapon
   ```

2. Develop and test locally:
   ```bash
   npm run dev
   ```

3. Type-check and lint:
   ```bash
   npm run type-check
   npm run lint
   ```

4. Commit changes:
   ```bash
   git add .
   git commit -m "feat: add new weapon functionality"
   ```

5. Push and create pull request:
   ```bash
   git push origin feature/new-weapon
   ```

### Code Style Guidelines

- Use TypeScript strict mode
- Follow Airbnb React/TypeScript style guide
- Use Tailwind CSS for styling (no custom CSS files)
- Component names use PascalCase
- Utility functions use camelCase
- Constants use UPPER_SNAKE_CASE

---

## 🔒 Security Considerations

### API Key Management

- **Never commit** `.env.local` to version control
- Use Vercel environment variables for production
- Rotate API keys regularly
- Implement rate limiting on API routes
- Use server-side API routes for sensitive operations

### Blockchain Security

- Validate all wallet addresses
- Use ethers.js for safe contract interactions
- Implement transaction confirmation dialogs
- Never store private keys in code or environment variables

---

## 📊 Performance Optimization

Dev Arsenal is optimized for performance:

- **Monaco Editor:** Lazy-loaded with dynamic imports
- **Code splitting:** Automatic with Next.js App Router
- **Image optimization:** Next.js Image component
- **API caching:** Implemented on frequently-used endpoints
- **Bundle size:** Monitored with `@next/bundle-analyzer`

---

## 🌐 Browser Compatibility

Dev Arsenal supports:

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

**Note:** Monaco Editor requires modern JavaScript features. IE11 is not supported.

---

## 📞 Support & Contact

For setup issues, questions, or feedback:

- **GitHub Issues:** [github.com/mrbrightsides/devarsenal/issues](https://github.com/mrbrightsides/devarsenal/issues)
- **Email:** support@elpeef.com
- **Telegram:** [@khudriakhmad](https://t.me/khudriakhmad)
- **Discord:** @khudri_61362

---

## 🏆 LavaPunk Hackathon 2026

This project is a submission for the **LavaPunk Hackathon 2026**, showcasing:

- Blockchain integration with Base network
- AI-assisted development tools
- Real-time collaborative coding
- Decentralized code storage (IPFS)
- Multi-language IDE capabilities

Built with ❤️ by the Dev Arsenal team.

---

## 📄 License

This project is open source. See LICENSE file for details.

---

## 🙏 Acknowledgments

Special thanks to:
- Monaco Editor by Microsoft
- shadcn/ui component library
- OpenAI for GPT API
- Alchemy for blockchain infrastructure
- Pinata for IPFS hosting
- Judge0 for code execution engine

---

**Last Updated:** January 2026  
**Version:** 1.0.0  
**Hackathon:** LavaPunk 2026
