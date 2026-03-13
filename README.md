[README-2.md](https://github.com/user-attachments/files/25976819/README-2.md)
# LedgerOS — Small Business Accounting Platform

> Production-ready accounting software for SMBs — invoicing, payroll, tax prep, cash flow, and reporting in a single, self-contained app.

![LedgerOS Dashboard](https://img.shields.io/badge/status-live-22c984?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![HTML](https://img.shields.io/badge/built%20with-HTML%20%2F%20CSS%20%2F%20JS-1a56db?style=flat-square)
![Netlify](https://img.shields.io/badge/deploy-Netlify-00C7B7?style=flat-square&logo=netlify)

---

## What is LedgerOS?

LedgerOS is a fully functional, client-side accounting dashboard built for small and medium-sized businesses. It ships as a single HTML file with zero dependencies, zero build steps, and zero backend required to get started — yet it's architected to plug into a production Node.js + PostgreSQL backend when you're ready to scale.

**Key design goals:**
- Everything a small business owner needs on one screen
- Professional, distraction-free UI (not generic SaaS boilerplate)
- Zero install — open the file, it works
- Netlify-ready out of the box

---

## Live Demo

> Deploy your own in under 60 seconds — see [Deployment](#deployment) below.

---

## Features

### 📊 Dashboard
- Real-time KPI strip — Revenue, Outstanding, Expenses, Net Profit
- Monthly Revenue vs Expenses bar chart (12-month view)
- Expense category donut chart
- Recent invoices table with inline status and actions
- Smart alerts panel — overdue invoices, tax deadlines, payroll confirmations
- Quick action shortcuts for common tasks

### 🧾 Invoicing
- Create invoices with dynamic line items (add / remove rows, live total calculation)
- Configurable tax rate per invoice
- Status lifecycle: Draft → Sent → Paid / Overdue
- One-click "Mark as Paid" and delete
- Full print-ready invoice preview modal
- Aging analysis across All / Paid / Pending / Overdue / Draft tabs
- CSV export hook

### 👥 Client Management
- Client cards with contact info, industry tag, and total billed
- One-click invoice creation per client
- Add clients with full detail form (company, contact, email, phone, address, industry, payment terms)

### 💳 Expense Tracking
- Log expenses with date, description, category, vendor, and amount
- Tax deductibility flag per expense
- Receipt upload zone (UI-ready for backend file storage)
- Month-to-date stats — total spend, deductible amount, receipts captured
- Categorised breakdown: Software, Office, Travel, Marketing, Payroll, Utilities, Other

### 💼 Payroll
- Employee roster with role, monthly salary, and initials avatar
- Per-period summary — Gross Pay, Tax Withheld, Net Pay
- Tax obligation breakdown — Federal Income, Social Security, Medicare, State
- One-click "Run Payroll" with async confirmation flow
- Pay stub generation per employee
- Add employee form with tax filing status

### 🏛️ Tax Center
- Taxable income estimator (revenue minus deductible expenses)
- Estimated tax owed with effective rate
- Payments already made tracker
- Deduction tracker with progress bars per category
- Filing deadline countdown — Q1, Q2, Form 1099, Annual Return
- Q1 due-date warning alert

### 📈 Reports
- 9 report types: Profit & Loss, Balance Sheet, Cash Flow Statement, Invoice Summary, Expense Report, Client Revenue, Payroll Report, Tax Summary, Year-over-Year
- Preview + Export (PDF / CSV) per report
- Custom date range selector

### 💰 Cash Flow
- 30-day inflow / outflow bar chart
- Month-to-date Cash In, Cash Out, Net Flow, Available Balance KPIs
- Upcoming inflows table with invoice references and due dates
- Upcoming outflows table (payroll, rent, subscriptions)

### 🖥️ Tech Stack Guide (built into the app)
- Full recommended backend architecture for production deployment
- Technology recommendations across 6 categories with rationale
- ASCII architecture diagram showing all system layers

### ⚙️ Settings
- Company profile (name, EIN, address, contact)
- Invoice defaults (payment terms, currency, notes)
- Tax configuration (rate, business type, state)
- Notification toggles with live state
- Data export and danger zone

---

## Screenshots

```
┌─────────────────────────────────────────────────────────┐
│  LedgerOS  │  Dashboard                    🔔  + New    │
├────────────┼────────────────────────────────────────────┤
│ Dashboard  │  ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│ Invoices   │  │ Revenue  │ │Outstandng│ │ Expenses │  │
│ Clients    │  │ $84,250  │ │ $18,400  │ │ $31,200  │  │
│ Expenses   │  └──────────┘ └──────────┘ └──────────┘  │
│ ────────── │                                            │
│ Payroll    │  Revenue vs Expenses ████████████████      │
│ Tax Center │                                            │
│ Reports    │  Recent Invoices                           │
│ Cash Flow  │  INV-0024  Acme Corp    $8,500  ● Paid    │
│ ────────── │  INV-0023  TechStart    $4,200  ● Paid    │
│ Tech Stack │  INV-0022  Global Rtl  $12,000  ● Pending │
│ Settings   │                                            │
└────────────┴────────────────────────────────────────────┘
```

---

## Tech Stack

### Current (Zero-dependency frontend)

| Layer | Technology |
|---|---|
| UI | Vanilla HTML5 + CSS3 + JavaScript (ES6+) |
| Fonts | Syne (display) · Instrument Sans (body) · IBM Plex Mono (numbers) |
| Charts | Pure CSS bar charts, SVG donut charts |
| State | In-memory JS object (`D`) |
| Hosting | Any static host — Netlify, Vercel, GitHub Pages, S3 |

### Recommended Production Backend

| Layer | Choice | Why |
|---|---|---|
| **Runtime** | Node.js 20 LTS | Huge ecosystem, fast I/O, perfect for fintech webhooks |
| **Language** | TypeScript | Catches currency/amount bugs at compile time |
| **Framework** | Fastify | 2× faster than Express, built-in schema validation |
| **ORM** | Prisma | Type-safe queries, migrations as code |
| **Database** | PostgreSQL (Supabase / AWS RDS) | ACID transactions — essential for double-entry bookkeeping |
| **Cache / Queues** | Redis + BullMQ | Async payroll processing, scheduled invoice reminders |
| **Auth** | Clerk + Row-Level Security | Multi-tenant — each business sees only their own data |
| **Payments** | Stripe | Invoice payment links, ACH, subscriptions |
| **Bank Sync** | Plaid | Auto-import and reconcile transactions |
| **Email** | Resend | Transactional invoice delivery and tax reminders |
| **Frontend** | Next.js 14 (App Router) | Server rendering, Vercel deploy, edge performance |
| **Monitoring** | Sentry + PostHog + Datadog | Error tracking, product analytics, infrastructure |
| **CI/CD** | GitHub Actions | Test, build, and deploy on every merge |
| **Hosting** | Railway / Fly.io + Vercel | Zero-config containers + edge frontend |

### Full Architecture

```
Browser (Next.js)
      │  HTTPS / REST + WebSocket
      ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  API Server  │◄──►│  Auth (Clerk)│    │  BullMQ Jobs │
│  Node.js +   │    │  + RLS       │    │  (Redis)     │
│  TypeScript  │    └──────────────┘    │  · Payroll   │
│  + Prisma    │                        │  · Reminders │
└──────┬───────┘                        │  · Tax calc  │
       │                                └──────────────┘
       ▼
┌──────────────────────────────────────────────────────┐
│              PostgreSQL (Supabase)                   │
│  invoices · clients · expenses · payroll · taxes    │
│  ← Row-Level Security enforces multi-tenancy →      │
└──────────────────────────────────────────────────────┘
       │                    │                  │
       ▼                    ▼                  ▼
┌──────────┐       ┌──────────────┐    ┌──────────────┐
│  Stripe  │       │  Plaid API   │    │  S3 / R2     │
│ Payments │       │  Bank Sync   │    │  Receipts    │
└──────────┘       └──────────────┘    └──────────────┘

Monitoring: Sentry · Datadog · PostHog · GitHub Actions CI
```

---

## Project Structure

```
ledgeros/
├── index.html          # Entire application (UI + logic)
├── 404.html            # Branded 404 page
├── netlify.toml        # Netlify config — headers, caching, redirects
├── _redirects          # Netlify SPA routing fallback
├── robots.txt          # SEO crawl rules
├── site.webmanifest    # PWA manifest (installable on mobile)
└── README.md           # This file
```

---

## Deployment

### Option 1 — Netlify Drag & Drop (60 seconds)

1. Go to **[app.netlify.com/drop](https://app.netlify.com/drop)**
2. Drag the `ledgeros` folder onto the page
3. Your site is live at a `*.netlify.app` URL instantly

### Option 2 — Netlify CLI

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy from the project folder
cd ledgeros
netlify deploy --prod --dir .
```

### Option 3 — GitHub + Netlify (auto-deploy on push)

1. Push this repo to GitHub
2. Go to [app.netlify.com](https://app.netlify.com) → **Add new site → Import from Git**
3. Select your repo
4. Set **Publish directory** to `.` (root)
5. Click **Deploy site**

Every push to `main` will trigger a new deploy automatically.

### Option 4 — Vercel

```bash
npm install -g vercel
cd ledgeros
vercel --prod
```

### Option 5 — GitHub Pages

1. Push to a repo named `ledgeros`
2. Go to **Settings → Pages → Source: Deploy from branch → main / root**
3. Live at `https://yourusername.github.io/ledgeros`

### Custom Domain

In Netlify: **Site settings → Domain management → Add custom domain**
SSL is provisioned automatically via Let's Encrypt.

---

## Getting Started (Local Development)

No build tools required.

```bash
# Clone the repo
git clone https://github.com/yourusername/ledgeros.git
cd ledgeros

# Open directly in browser
open index.html

# Or serve locally with any static server
npx serve .
# → Available at http://localhost:3000
```

---

## Roadmap

The following features are planned for the production backend version:

- [ ] User authentication with multi-company support
- [ ] PostgreSQL persistence (invoices, expenses, clients, employees)
- [ ] Stripe integration — pay invoices via link (card + ACH)
- [ ] Plaid bank sync — auto-import and categorise transactions
- [ ] PDF invoice generation (Puppeteer / React-PDF)
- [ ] Email delivery via Resend — invoices, receipts, reminders
- [ ] Automated overdue invoice reminders (BullMQ scheduled jobs)
- [ ] Recurring invoices
- [ ] Multi-currency support
- [ ] Accountant / bookkeeper access role
- [ ] QuickBooks and Xero export
- [ ] Mobile app (React Native or PWA)
- [ ] AI-powered expense categorisation

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

```bash
# Fork the repo, then:
git checkout -b feature/your-feature-name
# Make your changes to index.html
git commit -m "feat: describe your change"
git push origin feature/your-feature-name
# Open a pull request
```

**Coding conventions:**
- Keep all logic in `index.html` until a proper frontend framework is introduced
- Use the existing CSS variable system (`--ink`, `--blue`, `--green`, etc.) for any new UI
- Match the existing font stack — Syne for headings, Instrument Sans for body, IBM Plex Mono for numbers
- Toast notifications for all user-facing feedback (`toast('message', 'ok' | 'err' | 'inf')`)

---

## License

MIT — free to use, modify, and distribute. Attribution appreciated but not required.

---

## Author

Built with [Claude](https://claude.ai) · Designed for real small business owners · Deployed in seconds on Netlify

---

*LedgerOS is a frontend prototype. For production use with real financial data, connect the recommended backend stack and ensure compliance with your local financial data regulations (SOC 2, GDPR, PCI-DSS as applicable).*
