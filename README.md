# QuickInvoice

Production-ready invoice management SaaS for freelancers and small businesses.

![QuickInvoice](https://img.shields.io/badge/QuickInvoice-v1.0.0-6C63FF)

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Next.js 14 (App Router), TypeScript, Tailwind CSS v3 |
| State | TanStack Query v5, React Hook Form + Zod |
| UI | Framer Motion, Lucide React, next-themes, sonner |
| PDF | @react-pdf/renderer (multi-page) |
| Backend | Node.js, Express, TypeScript |
| Database | Supabase (Postgres + Auth + Storage) |
| Email | Resend SDK |

## Project Structure

```
quickinvoice/
├── apps/
│   ├── web/          # Next.js 14 frontend
│   │   ├── app/      # App Router pages
│   │   ├── components/  # UI, layout, invoice, dashboard, pdf
│   │   ├── hooks/    # TanStack Query hooks
│   │   ├── lib/      # API client, Supabase, utilities
│   │   └── types/    # Shared TypeScript types
│   └── api/          # Express backend
│       └── src/
│           ├── controllers/
│           ├── middleware/
│           ├── routes/
│           ├── schemas/
│           ├── services/
│           └── lib/
└── supabase/
    └── migrations/   # SQL migration files
```

## Getting Started

### Prerequisites

- Node.js 18+
- npm 9+
- A [Supabase](https://supabase.com) project
- A [Resend](https://resend.com) account (for email)

### 1. Clone and Install

```bash
# Install root dependencies
npm install

# Install web dependencies
cd apps/web && npm install && cd ../..

# Install API dependencies
cd apps/api && npm install && cd ../..
```

### 2. Set Up Supabase

1. Create a new project at [supabase.com](https://supabase.com)
2. Go to **SQL Editor** and run the migration file:
   ```
   supabase/migrations/001_initial.sql
   ```
3. Copy your project URL and keys from **Settings > API**

### 3. Configure Environment Variables

**Frontend** (`apps/web/.env.local`):
```env
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
NEXT_PUBLIC_API_URL=http://localhost:3001/api
```

**Backend** (`apps/api/.env`):
```env
SUPABASE_URL=your-supabase-url
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
RESEND_API_KEY=your-resend-api-key
PORT=3001
FRONTEND_URL=http://localhost:3000
STORAGE_BUCKET=invoices
```

### 4. Run Development Servers

```bash
# Start both frontend and backend simultaneously
npm run dev

# Or start individually:
npm run dev:web   # Next.js on http://localhost:3000
npm run dev:api   # Express on http://localhost:3001
```

### 5. Open the App

Visit [http://localhost:3000](http://localhost:3000) and create an account.

## Features

### Authentication
- Email + password registration/login
- Magic link authentication
- JWT-based API authentication

### Dashboard
- Revenue overview with trend indicators
- Monthly revenue chart (last 6 months)
- Recent invoices table
- Quick action buttons

### Invoice Management
- Create invoices with live PDF preview
- Drag-and-drop line items reordering
- Auto-calculated totals (subtotal, tax, discount)
- Multi-page PDF generation (A4 format)
- Send invoices via email with PDF attachment
- Status tracking (Draft → Sent → Viewed → Paid)
- Invoice filtering, searching, and sorting
- Auto-generated invoice numbers

### Client Management
- Client cards with invoice summary stats
- Side drawer for add/edit
- Client detail with full invoice history

### Settings
- Business profile (name, email, address, logo)
- Invoice defaults (currency, payment terms, prefix)
- Notification preferences
- Logo upload to Supabase Storage

### Design System
- Custom violet-based color palette
- Dark mode support (system/manual toggle)
- Inter font family
- Responsive layout with collapsible sidebar
- Framer Motion micro-animations
- Sonner toast notifications

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login |
| POST | `/api/auth/magic-link` | Send magic link |
| GET | `/api/auth/me` | Get current user |
| GET | `/api/invoices` | List invoices (filterable) |
| POST | `/api/invoices` | Create invoice |
| GET | `/api/invoices/:id` | Get invoice detail |
| PUT | `/api/invoices/:id` | Update invoice |
| DELETE | `/api/invoices/:id` | Delete invoice |
| PATCH | `/api/invoices/:id/status` | Update status |
| POST | `/api/invoices/:id/send` | Send via email |
| POST | `/api/invoices/:id/generate-pdf` | Generate PDF |
| GET | `/api/invoices/next-number` | Get next number |
| GET | `/api/clients` | List clients |
| POST | `/api/clients` | Create client |
| GET | `/api/clients/:id` | Client detail |
| PUT | `/api/clients/:id` | Update client |
| DELETE | `/api/clients/:id` | Delete client |
| GET | `/api/settings` | Get profile |
| PUT | `/api/settings` | Update profile |
| POST | `/api/settings/logo` | Upload logo |
| GET | `/api/dashboard/stats` | Dashboard stats |
| GET | `/api/dashboard/revenue` | Revenue chart data |

## License

MIT
