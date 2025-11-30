# Screen Recorder Pro - SaaS Platform

A professional screen recording web application with Stripe payment integration for €2.99 one-time purchase.

## Overview

This project converts the original Electron screen recorder into a web-based SaaS business with:
- User authentication and authorization
- Stripe payment integration (€2.99 one-time payment)
- License management
- Modern web-based screen recording

## Features

- **High-Quality Screen Recording**: Record your screen in 1080p quality
- **Browser-Based**: No downloads required, works directly in the browser
- **One-Time Payment**: €2.99 for lifetime access via Stripe
- **User Authentication**: Secure login and registration system
- **Payment Verification**: Automatic license activation after payment
- **Modern UI**: Built with React, Next.js, and Tailwind CSS

## Technology Stack

### Backend
- **Node.js** + **Express**: RESTful API server
- **PostgreSQL**: User and payment data storage
- **Stripe**: Payment processing
- **JWT**: Authentication tokens
- **bcrypt**: Password hashing

### Frontend
- **Next.js 14**: React framework with App Router
- **React 18**: UI components
- **Tailwind CSS**: Styling
- **Stripe.js**: Payment integration
- **Axios**: API requests

## Project Structure

```
screenrecording/
├── backend/                 # Backend API server
│   ├── config/             # Database configuration
│   ├── controllers/        # Business logic
│   ├── middleware/         # Authentication middleware
│   ├── models/             # Database schema
│   ├── routes/             # API routes
│   ├── .env.example        # Environment variables template
│   ├── package.json        # Backend dependencies
│   └── server.js           # Express server entry point
│
├── frontend/               # Next.js frontend
│   ├── src/
│   │   ├── app/           # Next.js App Router pages
│   │   ├── components/    # React components
│   │   ├── lib/           # Utilities and API client
│   │   └── styles/        # CSS styles
│   ├── .env.local.example # Frontend environment variables
│   ├── next.config.js     # Next.js configuration
│   └── package.json       # Frontend dependencies
│
├── [Electron files]        # Original Electron app (legacy)
└── README.md              # This file
```

## Setup Instructions

### Prerequisites

- Node.js 18+ and npm
- PostgreSQL 14+
- Stripe account (get API keys from https://dashboard.stripe.com)

### 1. Database Setup

Create a PostgreSQL database:

```bash
createdb screenrecorder
```

Initialize the database schema:

```bash
psql -d screenrecorder -f backend/models/init.sql
```

### 2. Backend Setup

Navigate to the backend directory:

```bash
cd backend
```

Install dependencies:

```bash
npm install
```

Create `.env` file from template:

```bash
cp .env.example .env
```

Edit `.env` and add your configuration:

```env
PORT=3001
NODE_ENV=development

DATABASE_URL=postgresql://username:password@localhost:5432/screenrecorder

JWT_SECRET=your-super-secret-jwt-key-generate-a-random-string

STRIPE_SECRET_KEY=sk_test_your_stripe_secret_key
STRIPE_PUBLISHABLE_KEY=pk_test_your_stripe_publishable_key
STRIPE_WEBHOOK_SECRET=whsec_your_webhook_secret

FRONTEND_URL=http://localhost:3000

PRODUCT_PRICE_EUR=2.99
```

Start the backend server:

```bash
npm run dev
```

The API will be available at `http://localhost:3001`

### 3. Frontend Setup

Navigate to the frontend directory:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Create `.env.local` file:

```bash
cp .env.local.example .env.local
```

Edit `.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_your_stripe_publishable_key
```

Start the development server:

```bash
npm run dev
```

The app will be available at `http://localhost:3000`

### 4. Stripe Setup

1. **Create a Stripe account** at https://stripe.com
2. **Get your API keys** from Dashboard → Developers → API keys
3. **Set up webhook** for payment confirmation:
   - Go to Dashboard → Developers → Webhooks
   - Click "Add endpoint"
   - URL: `https://your-domain.com/api/payment/webhook`
   - Events to listen: `checkout.session.completed`, `payment_intent.succeeded`
   - Copy the webhook signing secret to `.env`

4. **Test with Stripe CLI** (optional for local development):

```bash
# Install Stripe CLI
npm install -g stripe

# Forward webhooks to local server
stripe listen --forward-to localhost:3001/api/payment/webhook

# Use test card: 4242 4242 4242 4242
```

## Deployment

### Backend Deployment (Railway/Render)

1. **Push code to GitHub**

2. **Deploy to Railway**:
   - Connect GitHub repository
   - Add PostgreSQL database
   - Set environment variables
   - Deploy

3. **Set up Stripe webhook** with production URL

### Frontend Deployment (Vercel)

1. **Deploy to Vercel**:

```bash
cd frontend
npm run build
vercel --prod
```

2. **Set environment variables** in Vercel dashboard:
   - `NEXT_PUBLIC_API_URL`: Your backend URL
   - `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY`: Stripe live key

### Environment Variables Checklist

#### Backend (.env)
- [ ] `DATABASE_URL` - PostgreSQL connection string
- [ ] `JWT_SECRET` - Random secure string
- [ ] `STRIPE_SECRET_KEY` - Stripe secret key (live mode)
- [ ] `STRIPE_WEBHOOK_SECRET` - Webhook signing secret
- [ ] `FRONTEND_URL` - Your frontend domain

#### Frontend (.env.local)
- [ ] `NEXT_PUBLIC_API_URL` - Backend API URL
- [ ] `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` - Stripe publishable key

## Testing

### Test Payment Flow

1. Register a new account
2. Login to dashboard
3. Click "Purchase for €2.99"
4. Use Stripe test card: `4242 4242 4242 4242`
5. Complete payment
6. Verify license is activated
7. Access screen recorder

### Test Screen Recording

1. Navigate to `/recorder`
2. Click "Start Recording"
3. Allow screen capture permission
4. Select screen/window to record
5. Record for a few seconds
6. Click "Stop Recording"
7. Download the video file

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/verify` - Verify JWT token

### Payment
- `POST /api/payment/create-checkout-session` - Create Stripe checkout
- `POST /api/payment/webhook` - Stripe webhook handler
- `GET /api/payment/verify-access` - Check license status

### User
- `GET /api/user/profile` - Get user profile
- `POST /api/user/recording-session` - Track recording analytics

## Security Considerations

- **HTTPS Only**: Always use HTTPS in production
- **Environment Variables**: Never commit `.env` files
- **Password Hashing**: bcrypt with salt rounds
- **JWT Expiration**: Tokens expire after 7 days
- **Rate Limiting**: API rate limiting enabled
- **CORS**: Configured for frontend domain only
- **SQL Injection**: Parameterized queries used
- **XSS Protection**: React auto-escapes output

## Troubleshooting

### Database Connection Error
- Check PostgreSQL is running
- Verify DATABASE_URL is correct
- Ensure database exists and schema is initialized

### Stripe Payment Not Working
- Verify API keys are correct (test vs live)
- Check webhook is configured properly
- Test with Stripe CLI locally

### Recording Not Starting
- Check browser permissions for screen capture
- Ensure HTTPS is used (required for MediaRecorder API)
- Test in Chrome/Edge (best compatibility)

## Business & Legal

### Required Pages
- [ ] Privacy Policy
- [ ] Terms of Service
- [ ] Refund Policy
- [ ] Contact Page

### Payment Processing
- Stripe handles PCI compliance
- One-time payment model
- Lifetime access after purchase

### Analytics (Optional)
- Track recording sessions
- Monitor user registrations
- Payment conversion rates

## Support & Maintenance

### Monitoring
- Database backups (daily recommended)
- Error logging (Sentry integration recommended)
- Uptime monitoring

### Updates
- Keep dependencies updated
- Monitor Stripe API changes
- Security patches

## License

MIT License - Feel free to modify for your needs

---

## Original Electron App (Legacy)

The original Electron desktop application files are still in the root directory for reference. To use the legacy version:

```bash
npm install
npm start
```

**Built with Next.js, Express, PostgreSQL, and Stripe**
# screenrecorder
