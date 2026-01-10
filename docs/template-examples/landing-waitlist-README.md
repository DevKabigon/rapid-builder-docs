# Landing Page + Waitlist Template

A beautiful landing page template perfect for Product Hunt launches. Includes email collection with Resend integration, simple dashboard, and GitHub repository creation.

## 🚀 Features

- **Product Hunt Ready** - Optimized for launch day
- **Email Collection** - Resend integration for waitlist management
- **Simple Dashboard** - Basic admin interface
- **Modern Design** - Clean, professional UI
- **Mobile Responsive** - Works perfectly on all devices
- **SEO Optimized** - Built-in SEO best practices

## 🛠️ Tech Stack

- **Next.js** 16.1.1 - React framework
- **React** 19.2.3 - UI library
- **TypeScript** 5.0.0 - Type safety
- **Tailwind CSS** 4.0 - Styling
- **Resend** - Email service

## 📋 Prerequisites

Before you start, make sure you have:

- [ ] Node.js 18+ installed
- [ ] A Resend account (for email collection)
- [ ] GitHub account (for repository creation)

## 🏃 Getting Started

### 1. Install Dependencies

```bash
npm install
# or
pnpm install
# or
yarn install
```

### 2. Set Up Environment Variables

Copy `.env.example` to `.env.local` and fill in your values:

```bash
cp .env.example .env.local
```

Required environment variables:

```env
RESEND_API_KEY=your_resend_api_key_here
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### 3. Run Development Server

```bash
npm run dev
# or
pnpm dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) to see your landing page.

## 📧 Email Collection Setup

This template uses [Resend](https://resend.com) for email collection:

1. Sign up for a Resend account
2. Create an API key
3. Add it to your `.env.local` file
4. Configure your domain (optional, for production)

## 🚢 Deployment

### Deploy to Vercel

1. Push your code to GitHub
2. Import your repository in Vercel
3. Add environment variables
4. Deploy!

The template is optimized for Vercel deployment and will work out of the box.

## 📁 Project Structure

```
landing-waitlist/
├── app/
│   ├── layout.tsx          # Root layout
│   ├── page.tsx            # Landing page
│   ├── dashboard/          # Admin dashboard
│   └── api/                # API routes
│       └── waitlist/       # Waitlist API
├── components/             # React components
├── lib/                    # Utilities
└── public/                 # Static assets
```

## 🎨 Customization

### Colors

Edit `tailwind.config.ts` to customize your color scheme:

```typescript
theme: {
  extend: {
    colors: {
      primary: '#your-color',
    },
  },
}
```

### Content

Edit `app/page.tsx` to customize your landing page content.

## 📝 License

MIT License - feel free to use this template for your projects!

## 🤝 Support

If you have questions or need help, please open an issue on GitHub.

---

Built with ❤️ using Rapid Builder
