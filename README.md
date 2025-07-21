# MySecretary - AI Virtual Receptionist

MySecretary is a comprehensive SaaS application that provides AI-powered virtual receptionist services for independent contractors. Built with Next.js 14, it offers both Starter and Pro plans with automated call handling, transcript generation, and intelligent responses.

## Features

### 🚀 Core Features

- **AI Virtual Receptionist**: Automated call answering with contractor's business name
- **Call Transcription**: Automatic speech-to-text for all incoming calls
- **AI Response Generation**: Intelligent responses using OpenAI's GPT models
- **Call Logging**: Comprehensive call history and analytics
- **Client Management**: Track customer information and call history

### 📋 Service Plans

#### Starter Plan (Basic Receptionist)

- AI answers with contractor's business name
- Basic call logging to database
- Simple conversation recording
- Call transcript generation

#### Pro Plan (Full AI Secretary)

- Everything in Starter Plan
- AI-generated follow-up summaries
- Email/SMS notifications to contractors
- Advanced call analytics
- Calendar integration for appointment booking

## Tech Stack

### Frontend

- **Next.js 14** with App Router
- **TypeScript** for type safety
- **Tailwind CSS** for styling
- **shadcn/ui** for UI components
- **NextAuth.js** for authentication

### Backend

- **tRPC** for type-safe API routes
- **Prisma ORM** for database management
- **PostgreSQL** database (local dev with Prisma)
- **Supabase** for production database

### External Services

- **Twilio** for call handling and forwarding
- **OpenAI** for AI response generation
- **Google OAuth** for user authentication

## Setup Instructions

### Prerequisites

- Node.js 18+ installed
- npm or yarn package manager

### 1. Clone and Install

```bash
git clone <repository-url>
cd my-secretary
npm install
```

### 2. Environment Variables

Update the `.env` file with your actual credentials:

```env
# Database (already configured for local development)
DATABASE_URL="prisma+postgres://localhost:51213/..."

# NextAuth.js
NEXTAUTH_URL="http://localhost:3000"

# Google OAuth
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"

# Twilio
TWILIO_ACCOUNT_SID="your-twilio-account-sid"
TWILIO_AUTH_TOKEN="your-twilio-auth-token"
TWILIO_PHONE_NUMBER="your-twilio-phone-number"

# OpenAI
OPENAI_API_KEY="your-openai-api-key"
```

### 3. Database Setup

```bash
# Start the local Prisma database
npx prisma dev

# In another terminal, push the schema
npx prisma db push

# Generate Prisma client
npx prisma generate
```

### 4. Run Development Server

```bash
npm run dev
```

Visit `http://localhost:3000` to see the application.

## API Routes

### Authentication

- `POST /api/auth/[...nextauth]` - NextAuth.js authentication

### tRPC Routes

- `GET/POST /api/trpc/[trpc]` - tRPC API endpoint

### Twilio Webhook

- `POST /api/twilio/webhook` - Twilio webhook for call processing

## Database Schema

### Core Models

- **User**: NextAuth.js user accounts
- **Contractor**: Business information and settings
- **Client**: Customer contact information
- **CallLog**: Call records with transcripts and AI responses

### Relationships

- Users can have multiple Contractors
- Contractors can have multiple Clients and CallLogs
- Clients can have multiple CallLogs

## Development Workflow

### Adding New Features

1. Update Prisma schema in `prisma/schema.prisma`
2. Run `npx prisma db push` to update database
3. Add tRPC routes in `src/server/api/routers/`
4. Create UI components in `src/components/`
5. Add pages in `src/app/`

### Testing Twilio Integration

1. Set up Twilio webhook URL: `https://your-domain.com/api/twilio/webhook`
2. Configure call forwarding to your Twilio number
3. Test with real phone calls

## Deployment

### Production Environment Variables

- Set up production database (Supabase recommended)
- Configure production OAuth app
- Set up production Twilio webhook URL
- Deploy to Vercel or similar platform

### Database Migration

```bash
npx prisma migrate deploy
```

## Project Structure

```
my-secretary/
├── src/
│   ├── app/              # Next.js 14 app router
│   │   ├── api/          # API routes
│   │   │   ├── auth/     # NextAuth.js
│   │   │   ├── trpc/     # tRPC endpoint
│   │   │   └── twilio/   # Twilio webhook
│   │   └── page.tsx      # Main dashboard
│   ├── components/       # React components
│   │   ├── ui/          # shadcn/ui components
│   │   ├── dashboard.tsx # Main dashboard
│   │   └── contractor-form.tsx
│   ├── lib/             # Utility functions
│   │   ├── auth.ts      # NextAuth config
│   │   ├── prisma.ts    # Database client
│   │   └── trpc.ts      # tRPC client
│   └── server/          # Server-side code
│       └── api/         # tRPC routers
├── prisma/
│   └── schema.prisma    # Database schema
├── .env                 # Environment variables
└── package.json
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests and linting
5. Submit a pull request

## License

This project is licensed under the MIT License.
