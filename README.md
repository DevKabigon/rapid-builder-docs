<div align="center">

# 🚀 Rapid Builder

**From Idea to Deployed SaaS in 60 Seconds**

[![Next.js](https://img.shields.io/badge/Next.js-16.1.1-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19.2.3-61DAFB?style=for-the-badge&logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-3178C6?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org/)
[![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase)](https://supabase.com/)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel)](https://vercel.com/)

> Build the foundation with Rapid Builder, add the details with Cursor

[Features](#-features) • [Quick Start](#-quick-start) • [How It Works](#-how-it-works) • [Documentation](#-documentation) • [Contributing](#-contributing)

</div>

---

## ✨ Overview

**Rapid Builder** is an intelligent SaaS platform that automates your entire project setup and deployment workflow. Instead of spending hours configuring repositories, databases, authentication, and deployment pipelines, Rapid Builder handles all the infrastructure setup automatically. With one click, you get a fully configured GitHub repository, Supabase project with optimized database, Resend email audiences, and Vercel deployment—ready to code immediately.

### 🎯 Why Rapid Builder?

- ⚡ **60-Second Deployment** - From template selection to live SaaS in under a minute
- 🔧 **Zero Manual Configuration** - Automatic setup of GitHub, Supabase, Vercel, and Resend
- 🎨 **Professional Templates** - Production-ready templates with best practices built-in
- 🔒 **Enterprise-Grade Security** - AES-256-GCM encrypted token storage and secure defaults
- 📊 **Real-Time Progress Tracking** - Watch your project come to life with live updates via Server-Sent Events
- 🎭 **Customizable Presets** - shadcn/ui presets with theme, font, and icon library customization
- 🔄 **Idempotent Operations** - Resume from failures, never lose progress
- 🚀 **Built for Vibe Coding** - Perfect companion for Cursor AI and modern development workflows
- 🛡️ **Error Recovery** - Intelligent error handling with detailed logging and recovery paths

---

## 🎨 Features

### 🔥 Core Capabilities

#### 🚀 Automated Infrastructure Setup

- **One-Click GitHub Repository Creation** - Automatically creates your repository from template, configures files, and sets up initial commit
- **Intelligent Supabase Project Creation** - Fully automated Supabase project setup with:
  - Automatic database initialization
  - Optimized database configurations
  - Security policies and RLS (Row Level Security) setup
  - Environment variables pre-configured
  - Organization management support
- **Instant Vercel Deployment** - Creates Vercel project and optionally deploys automatically with:
  - Environment variables automatically injected
  - Production-ready configurations
  - Custom domain support (Pro plans)
- **Resend Email Integration** - Automatically creates email audiences and API keys for transactional emails
- **Smart Environment Variable Management** - Pre-populates `.env.example` with actual credentials from created services

#### 📊 Real-Time Monitoring & Progress Tracking

- **Live Progress Updates** - Server-Sent Events (SSE) for real-time progress tracking without polling
- **Detailed Job Timeline** - Visual timeline showing each step of the creation process
- **Step-by-Step Status** - Track individual steps: repository creation, Supabase setup, Vercel deployment
- **Error Logging** - Comprehensive error messages with context for easy debugging
- **Progress Indicators** - Dynamic progress bars that adjust based on enabled services

#### 🔒 Security & Token Management

- **AES-256-GCM Encryption** - All API tokens encrypted at rest using industry-standard encryption
- **Secure Token Storage** - Tokens stored in Supabase with automatic expiration for session tokens
- **OAuth Integration** - Secure GitHub OAuth flow for repository access
- **Token Verification** - Automatic validation of all API tokens before use
- **Organization-Based Access** - Secure Supabase organization management

#### 🎨 Template System & Customization

- **Professional Template Library** - Curated collection of production-ready Next.js templates
- **Template Presets** - Pre-configured shadcn/ui presets with:
  - Multiple component libraries (Radix UI, Base UI)
  - Style variants (Vega, Lyra)
  - 17+ theme colors
  - 4+ icon libraries (Lucide, Tabler Icons, Hugeicons, Phosphor)
  - Custom fonts (Inter, Noto Sans, Nunito Sans, Figtree)
- **Brand Customization** - Configure project name and brand settings during creation
- **Template Preview** - View template details, features, and documentation before selection

#### 🔄 Reliability & Error Handling

- **Idempotent Operations** - Safe to retry; operations resume from last completed step
- **Async Job Processing** - Background job processing with status tracking
- **Failure Recovery** - Detailed error messages and recovery suggestions
- **Job State Management** - Persistent job state with step completion tracking
- **Step Result Storage** - Intermediate results stored for seamless step transitions

### 📦 Template Library

- **AI Chatbot Template** - OpenAI/Anthropic integration with streaming chat UI, conversation history, and Supabase backend
- **Landing Page + Waitlist** - Beautiful, responsive landing pages with email collection via Resend
- **SaaS Starter** - Complete SaaS boilerplate with authentication, payments, dashboard, and user management
- _More templates coming soon..._

### 🎯 Use Cases

- **Rapid Prototyping** - Validate ideas quickly with fully functional infrastructure
- **MVP Development** - Launch MVPs in minutes instead of days
- **Side Projects** - Start personal projects without infrastructure setup overhead
- **Client Projects** - Speed up client onboarding with instant project scaffolding
- **Educational Projects** - Learn modern SaaS stack with working examples
- **Hackathons** - Get a head start with production-ready templates

---

## 🔄 How It Works

Rapid Builder orchestrates the entire project creation workflow automatically:

### Step 1: Template Selection & Configuration

1. Choose from professionally crafted templates
2. Configure project name and brand settings
3. Select UI presets (theme, fonts, icon libraries)
4. Choose which services to enable (Supabase, Vercel, Resend)

### Step 2: Service Provisioning (Parallel Where Possible)

1. **Supabase Project Creation** (if enabled)

   - Creates Supabase project in your organization
   - Initializes database with optimized configurations
   - Sets up security policies
   - Generates API keys and connection strings

2. **Resend Audience Creation** (if enabled)

   - Creates email audience
   - Generates API key for transactional emails

3. **GitHub Repository Creation**

   - Creates repository from template
   - Injects environment variables (from Supabase/Resend)
   - Configures `.env.example` with actual values
   - Pushes initial commit

4. **Vercel Project Creation** (if enabled)
   - Creates Vercel project linked to GitHub repo
   - Configures environment variables
   - Optionally triggers initial deployment

### Step 3: Real-Time Monitoring

- Watch progress updates via Server-Sent Events
- See detailed status for each step
- Get notified of completion or errors
- Access all created resources (repo URLs, deployment links, API keys)

### Step 4: Ready to Code

- Clone your new repository
- Environment variables pre-configured
- All services connected and ready
- Start building features immediately!

---

## 🛠️ Tech Stack

### Frontend

- **Next.js 16.1.1** with App Router

  - Server Components for optimal performance
  - Built-in API routes for serverless functions
  - File-based routing for intuitive structure
  - Automatic code splitting and optimization

- **React 19.2.3** - Latest React with improved performance and concurrent features
- **TypeScript 5.0** - Full type safety across the entire codebase
- **Tailwind CSS 4** - Utility-first CSS with JIT compilation
- **shadcn/ui** - Accessible, customizable component library built on Radix UI primitives

### Backend & Infrastructure

- **Supabase** - Open-source Firebase alternative providing:

  - PostgreSQL database with real-time subscriptions
  - Built-in authentication (email, OAuth, magic links)
  - Row Level Security (RLS) for data protection
  - Storage buckets for file uploads
  - Auto-generated REST APIs

- **Vercel** - Serverless deployment platform with:

  - Automatic HTTPS and CDN
  - Edge functions for global performance
  - Preview deployments for every push
  - Analytics and monitoring

- **GitHub API** - Repository management and template repository creation
- **Resend API** - Transactional email service with React email support

### Architecture & Patterns

- **Job-Based Architecture** - Async job processing with persistent state
- **Server-Sent Events (SSE)** - Real-time progress updates without WebSocket overhead
- **Idempotent Operations** - Safe retries and failure recovery
- **Step Orchestration** - Coordinated multi-step workflows with dependency management

### Security

- **AES-256-GCM Encryption** - Industry-standard encryption for sensitive data
- **PBKDF2 Key Derivation** - Secure key derivation from master encryption key
- **Token Expiration** - Time-limited session tokens for enhanced security
- **OAuth 2.0** - Secure GitHub authentication flow

### Development Tools

- **ESLint** - Code quality and consistency
- **TypeScript** - Compile-time error detection
- **pnpm** - Efficient package management with shared dependencies
- **Supabase CLI** - Database migrations and local development

---

## 📁 Project Structure

```
rapid-builder/
├── app/                          # Next.js App Router
│   ├── api/                      # API routes (serverless functions)
│   │   ├── auth/                # Authentication & OAuth callbacks
│   │   ├── github/              # GitHub token management & verification
│   │   ├── projects/            # Project creation & job management
│   │   │   ├── create/         # Project initialization
│   │   │   ├── create-job/     # Job creation endpoint
│   │   │   ├── start/          # Start async job processing
│   │   │   └── [jobId]/        # Job-specific endpoints
│   │   │       └── stream/     # SSE stream for real-time updates
│   │   ├── supabase/            # Supabase token & organization management
│   │   ├── templates/           # Template fetching & management
│   │   ├── vercel/              # Vercel token & deployment management
│   │   └── resend/              # Resend token management
│   ├── auth/                    # Authentication pages
│   │   ├── login/              # GitHub OAuth login
│   │   └── callback/           # OAuth callback handler
│   ├── dashboard/               # Protected dashboard pages
│   │   ├── create/             # Project creation wizard
│   │   ├── jobs/               # Job listing & detail pages
│   │   ├── projects/           # Completed projects management
│   │   ├── templates/          # Template browser
│   │   └── settings/           # User settings & integrations
│   ├── templates/               # Public template browsing
│   └── pricing/                 # Pricing page
├── components/                   # React components
│   ├── auth/                   # Authentication UI components
│   ├── dashboard/              # Dashboard-specific components
│   │   ├── progress-tracker/   # Real-time progress tracking UI
│   │   ├── job-timeline.tsx    # Visual job execution timeline
│   │   ├── preset-config-form/ # UI preset configuration
│   │   └── integration-status/ # Service integration status
│   ├── marketing/              # Landing page components
│   ├── templates/              # Template preview components
│   └── ui/                     # Reusable shadcn/ui components
├── lib/                         # Core business logic
│   ├── jobs/                   # Job orchestration & processing
│   │   ├── project-creator.ts  # Main project creation orchestrator
│   │   ├── job-state.ts        # Job state management
│   │   ├── logger.ts           # Structured logging
│   │   ├── steps/              # Individual step implementations
│   │   │   ├── github-step.ts  # GitHub repo creation
│   │   │   ├── supabase-step.ts # Supabase project setup
│   │   │   ├── vercel-step.ts  # Vercel deployment
│   │   │   └── resend-step.ts  # Resend audience creation
│   │   └── types.ts            # Type definitions
│   ├── github/                 # GitHub API client
│   ├── supabase/               # Supabase client utilities
│   ├── supabase-management/    # Supabase Management API client
│   ├── vercel/                 # Vercel API client
│   ├── resend/                 # Resend API client
│   ├── templates/              # Template parsing & configuration
│   │   ├── preset-config.ts    # Preset configuration management
│   │   ├── readme-parser.ts    # Template README parsing
│   │   └── theme-utils.ts      # Theme & styling utilities
│   └── encryption.ts           # AES-256-GCM encryption utilities
├── supabase/                    # Database schema & migrations
│   └── migrations/             # SQL migration files
├── types/                       # TypeScript type definitions
│   └── supabase.ts             # Auto-generated Supabase types
└── docs/                        # Documentation
    ├── template-creation-guide.md
    ├── template-examples/      # Example template READMEs
    └── ...
```

### Key Architecture Decisions

- **Separation of Concerns** - Clear separation between UI, API routes, and business logic
- **Modular Step System** - Each integration (GitHub, Supabase, Vercel) is a separate, testable step
- **State Management** - Centralized job state with persistent storage for reliability
- **Type Safety** - Full TypeScript coverage with auto-generated Supabase types
- **Error Handling** - Comprehensive error handling at each layer with detailed logging

---

## 🔐 Environment Variables

| Variable                        | Description                        | Required | Notes                                               |
| ------------------------------- | ---------------------------------- | -------- | --------------------------------------------------- |
| `NEXT_PUBLIC_SUPABASE_URL`      | Your Supabase project URL          | ✅       | Get from Supabase project settings                  |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous/public key      | ✅       | Safe to expose in client code                       |
| `SUPABASE_SERVICE_ROLE_KEY`     | Supabase service role key (secret) | ✅       | **Keep secret!** Has admin access                   |
| `GITHUB_CLIENT_ID`              | GitHub OAuth App Client ID         | ✅       | Create at https://github.com/settings/developers    |
| `GITHUB_CLIENT_SECRET`          | GitHub OAuth App Client Secret     | ✅       | **Keep secret!** Store securely                     |
| `GITHUB_OAUTH_CALLBACK_URL`     | GitHub OAuth callback URL          | ✅       | Usually `http://localhost:3000/auth/callback` (dev) |
| `VERCEL_TOKEN`                  | Vercel API token                   | ⚠️       | Optional if Vercel deployment is disabled           |
| `ENCRYPTION_KEY`                | 32-byte encryption key (base64)    | ✅       | Generate with: `openssl rand -base64 32`            |
| `NEXT_PUBLIC_APP_URL`           | Your application URL               | ✅       | `http://localhost:3000` (dev) or production URL     |
| `RESEND_API_KEY`                | Resend API key (optional)          | ⚠️       | Only needed if Resend email integration is enabled  |

### Generating Encryption Key

```bash
# Generate a secure 32-byte encryption key
openssl rand -base64 32

# Copy the output and add to .env.local
ENCRYPTION_KEY=<generated-key>
```

### Getting API Tokens

1. **GitHub OAuth**

   - Go to https://github.com/settings/developers
   - Create new OAuth App
   - Set Authorization callback URL to your app URL + `/auth/callback`

2. **Supabase**

   - Use your project's anon key and service role key from project settings
   - For project creation, use Management API token from https://supabase.com/dashboard/account/tokens

3. **Vercel**

   - Generate token at https://vercel.com/account/tokens
   - Token has full access, keep it secure

4. **Resend** (optional)
   - Get API key from https://resend.com/api-keys
   - Only needed if using email features

---

## 🌟 What Makes Rapid Builder Unique?

### Traditional Approach vs Rapid Builder

**Traditional SaaS Setup (2-4 hours):**

1. Create GitHub repository manually
2. Set up Next.js project from scratch
3. Configure Supabase project, database, auth
4. Set up environment variables manually
5. Configure Vercel deployment
6. Set up email service (Resend/SendGrid)
7. Connect all services together
8. Test everything works
9. Debug configuration issues

**With Rapid Builder (60 seconds):**

1. Choose template → Configure presets → Click "Create"
2. ✅ Everything is done automatically

### Key Advantages

- **Time Savings** - Reduce setup time from hours to seconds
- **Zero Configuration Errors** - Eliminates manual configuration mistakes
- **Best Practices Built-In** - All templates follow security and performance best practices
- **Consistent Setup** - Every project starts with the same high-quality foundation
- **Instant Productivity** - Start coding features immediately, not infrastructure
- **Production-Ready** - Templates are production-ready, not just demos

### Perfect For

- **Solo Developers** - Launch side projects without DevOps overhead
- **Startups** - Rapid MVP development and iteration
- **Agencies** - Consistent project scaffolding for client work
- **Educational** - Learn modern SaaS architecture with working examples
- **Hackathons** - Get a competitive edge with instant setup
- **Teams** - Standardize project initialization across the team

---

## 📚 Documentation

### Getting Started

- [Template Creation Guide](./docs/template-creation-guide.md) - Learn how to create and contribute templates
- [Template Examples](./docs/template-examples/) - Example template READMEs and structures

### Development Guides

- [Testing Project Creation](./docs/testing-project-creation.md) - Comprehensive testing guide
- [Manual Setup Steps](./docs/manual-setup-steps.md) - Manual configuration guide (if needed)
- [Template Preset Guide](./docs/template-preset-guide.md) - Understanding preset configurations

### Template Development

- [Template README Guide](./docs/template-readme-review.md) - Writing effective template READMEs
- [Template Environment Variables](./docs/template-environment-variables-guide.md) - Managing env vars in templates
- [Template Local Setup](./docs/template-local-setup.md) - Local template development workflow

---

## 🧪 Development

### Available Scripts

```bash
# Development
pnpm dev                    # Start development server on http://localhost:3000

# Production
pnpm build                  # Build for production
pnpm start                  # Start production server

# Code Quality
pnpm lint                   # Run ESLint

# Templates
pnpm seed:templates         # Seed template database with default templates
pnpm update:template-repo   # Update template repository from GitHub

# Supabase
pnpm supabase:gen-types     # Generate TypeScript types from Supabase schema
pnpm supabase:gen-types:local # Generate types from local Supabase instance
```

### Database Migrations

Migrations are located in `supabase/migrations/`. The schema includes:

- **project_jobs** - Tracks project creation jobs with status, progress, and results
- **projects** - Stores completed project information
- **templates** - Template metadata and configuration
- **user_tokens** - Encrypted API tokens (GitHub, Vercel, Supabase, Resend)
- **subscriptions** - User subscription management

To apply migrations:

```bash
# Using Supabase CLI (recommended)
supabase db push

# Or manually via Supabase Dashboard SQL Editor
# Copy and paste each migration file in order
```

### Development Workflow

1. **Local Development**

   ```bash
   # Clone and install
   git clone <repo-url>
   cd rapid-builder
   pnpm install

   # Set up environment variables (see .env.example)
   cp .env.example .env.local

   # Run migrations
   supabase db push

   # Start dev server
   pnpm dev
   ```

2. **Testing Project Creation**

   - Use the testing guide in `docs/testing-project-creation.md`
   - Test with a separate GitHub/Supabase/Vercel account to avoid conflicts
   - Check job status in `/dashboard/jobs`

3. **Adding New Templates**

   - Follow the template creation guide
   - Add template to database via `pnpm seed:templates` or manually
   - Test template creation end-to-end

4. **Debugging Jobs**
   - Check job logs in the database (`project_jobs.status_message`)
   - Review step results in `project_jobs.step_results`
   - Check browser console for client-side errors
   - Review server logs for API errors

### Project Creation Flow

Understanding how projects are created helps with debugging and extending:

1. **Job Creation** (`/api/projects/create-job`)

   - Validates user authentication
   - Creates job record with "pending" status
   - Returns job ID

2. **Job Start** (`/api/projects/start`)

   - Validates all required tokens/services
   - Starts async `createProjectAsync()` function
   - Returns immediately (doesn't wait for completion)

3. **Project Creation** (`lib/jobs/project-creator.ts`)

   - Orchestrates all steps in sequence
   - Updates job status and progress
   - Stores intermediate results
   - Handles errors and retries

4. **Real-Time Updates** (`/api/projects/[jobId]/stream`)
   - SSE endpoint for live progress
   - Polls database every second
   - Sends updates to client
   - Closes when job completes/fails

### Environment Setup Tips

- **Encryption Key**: Generate a secure 32-byte key: `openssl rand -base64 32`
- **GitHub OAuth**: Create OAuth app at https://github.com/settings/developers
- **Supabase**: Use Management API token (not project API key) for project creation
- **Vercel**: Generate token at https://vercel.com/account/tokens
- **Local Testing**: Use Supabase CLI for local database development

---

## ❓ Frequently Asked Questions

### How long does project creation take?

Typically 30-60 seconds depending on which services are enabled:

- GitHub repository: ~5-10 seconds
- Supabase project: ~15-20 seconds
- Resend audience: ~5 seconds
- Vercel deployment: ~20-30 seconds

### What if a step fails?

Rapid Builder uses idempotent operations, so you can safely retry. The system will:

- Resume from the last completed step
- Skip already completed steps
- Only retry failed operations

### Are my API tokens secure?

Yes! All tokens are encrypted using AES-256-GCM encryption before storage. Tokens are:

- Encrypted at rest in the database
- Only decrypted when needed for API calls
- Never exposed to the client-side code
- Session tokens expire after 5 minutes

### Can I use my own Supabase/Vercel accounts?

Absolutely! Rapid Builder uses your own accounts and credentials. You're in full control of all created resources.

### What happens to projects created by Rapid Builder?

All projects are created in your accounts:

- GitHub repositories are in your GitHub account
- Supabase projects are in your Supabase organization
- Vercel projects are in your Vercel team

You own and manage everything. Rapid Builder just automates the setup.

### Can I customize templates after creation?

Yes! Templates are starting points. After creation, the repository is yours to modify however you want. You can:

- Add/remove features
- Change styling
- Update dependencies
- Deploy to different platforms

### Do I need to pay for Rapid Builder?

Rapid Builder itself may have subscription plans, but you'll need accounts for:

- GitHub (free for public repos)
- Supabase (free tier available)
- Vercel (free tier available)

Check the [Pricing](/pricing) page for current plans.

### Can I contribute templates?

Yes! We welcome community-contributed templates. See the [Template Creation Guide](./docs/template-creation-guide.md) for details.

---

## 🤝 Contributing

We welcome contributions! Whether it's fixing bugs, adding features, improving documentation, or contributing templates, your help makes Rapid Builder better for everyone.

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Make your changes** following our coding standards
4. **Test your changes** thoroughly
5. **Commit with clear messages** (`git commit -m 'Add amazing feature'`)
6. **Push to your fork** (`git push origin feature/amazing-feature`)
7. **Open a Pull Request** with a detailed description

### Areas Where We Need Help

- 🎨 **New Templates** - Create production-ready templates for different use cases
- 🐛 **Bug Fixes** - Help us squash bugs and improve reliability
- 📚 **Documentation** - Improve guides, add examples, clarify instructions
- ✨ **Features** - Propose and implement new features
- 🎯 **Testing** - Add tests, improve test coverage
- 🌐 **Internationalization** - Translate the interface to other languages

### Development Guidelines

- **Code Style**: Follow the existing code style and use ESLint
- **TypeScript**: Maintain full type safety
- **Commits**: Write clear, descriptive commit messages
- **Tests**: Add tests for new features and bug fixes
- **Documentation**: Update README and docs for user-facing changes
- **PRs**: Include context about what changed and why

### Template Contributions

We especially welcome template contributions! A great template should:

- Be production-ready (not just a demo)
- Follow best practices (security, performance, accessibility)
- Include comprehensive documentation
- Use modern tech stack (Next.js, React, TypeScript)
- Be well-tested and documented

See the [Template Creation Guide](./docs/template-creation-guide.md) for detailed instructions.

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

Rapid Builder is built with amazing open-source tools and services:

- **[Next.js](https://nextjs.org)** - The React framework that powers Rapid Builder
- **[Supabase](https://supabase.com)** - Open-source Firebase alternative for backend services
- **[Vercel](https://vercel.com)** - The deployment platform that makes everything fast
- **[shadcn/ui](https://ui.shadcn.com)** - Beautiful, accessible component library
- **[React](https://react.dev)** - The UI library we love
- **[TypeScript](https://www.typescriptlang.org)** - Type-safe JavaScript
- **[Tailwind CSS](https://tailwindcss.com)** - Utility-first CSS framework
- **Built for the [Vibe Coding](https://vibecoding.com) community** - Empowering developers to ship faster

Special thanks to the open-source community and all contributors who make projects like this possible.

---

## 📖 Documentation & Repository Strategy

### Why We Keep Code Private

Rapid Builder is a commercial SaaS product, so the main source code repository remains **private** to protect intellectual property and business logic. However, we believe in transparency and want developers to understand what Rapid Builder offers.

### Public Documentation Repository

We maintain a **public documentation repository** that contains:

- ✅ Complete README with features, architecture, and guides
- ✅ All documentation files from the `docs/` directory
- ✅ Template examples and guides
- ✅ Setup instructions and best practices

**Public Repository**: `rapid-builder-docs` (or your chosen name)

### Benefits of This Approach

1. **Transparency** - Developers can see exactly what Rapid Builder offers
2. **Security** - Business logic and proprietary code remain protected
3. **Documentation** - Comprehensive guides are publicly accessible
4. **Community** - Users can contribute to documentation improvements

### Syncing Documentation

To keep the public documentation repository up-to-date:

```bash
# Automatic sync (recommended)
pnpm sync:docs

# Or manual sync (Mac/Linux)
bash scripts/sync-docs.sh ../rapid-builder-docs

# Windows PowerShell
.\scripts\sync-docs.ps1 ..\rapid-builder-docs
```

The sync script copies:

- `README.md` → Public repo root
- `docs/` folder → Public repo `docs/`

### Alternative: Documentation Website

You can also host documentation as a static website using:

- **Vercel** - Deploy Next.js documentation site
- **GitHub Pages** - Free static hosting
- **Netlify** - Documentation-focused hosting
- **Documentation generators** - Docusaurus, GitBook, etc.

---

## 📞 Support

- 🐛 [Report a Bug](https://github.com/gyorutan/rapid-builder/issues)
- 💡 [Request a Feature](https://github.com/gyorutan/rapid-builder/issues)
- 📧 Email: support@rapidbuilder.com

---

<div align="center">

**Made with ❤️ for developers who want to ship fast**

[⬆ Back to Top](#-rapid-builder)

</div>
