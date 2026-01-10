# AI Chatbot Template

Build AI-powered chatbots with OpenAI/Anthropic integration, streaming chat UI, conversation history management, and Supabase backend. Perfect for AI applications.

## 🚀 Features

- **OpenAI/Anthropic Integration** - Support for multiple AI providers
- **Streaming Chat UI** - Real-time message streaming
- **Conversation History** - Persistent chat history with Supabase
- **Supabase Integration** - Auto-configured database
- **Real-time Updates** - Live chat experience
- **TypeScript** - Full type safety
- **Modern UI Components** - Beautiful, accessible components

## 🛠️ Tech Stack

- **Next.js** 16.1.1 - React framework
- **React** 19.2.3 - UI library
- **TypeScript** 5.0.0 - Type safety
- **Supabase** - Backend & database
- **OpenAI SDK** - AI integration
- **Tailwind CSS** 4.0 - Styling

## 📋 Prerequisites

Before you start, make sure you have:

- [ ] Node.js 18+ installed
- [ ] OpenAI API key OR Anthropic API key
- [ ] Supabase account (will be created automatically)
- [ ] GitHub account

## 🏃 Getting Started

### 1. Install Dependencies

```bash
npm install
# or
pnpm install
```

### 2. Set Up Environment Variables

Copy `.env.example` to `.env.local`:

```bash
cp .env.example .env.local
```

Required environment variables:

```env
# OpenAI (or use ANTHROPIC_API_KEY)
OPENAI_API_KEY=your_openai_api_key_here

# Supabase (auto-configured by Rapid Builder)
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### 3. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to start chatting!

## 🤖 AI Provider Setup

### OpenAI

1. Get your API key from [OpenAI Platform](https://platform.openai.com)
2. Add `OPENAI_API_KEY` to `.env.local`

### Anthropic (Alternative)

1. Get your API key from [Anthropic Console](https://console.anthropic.com)
2. Add `ANTHROPIC_API_KEY` to `.env.local`
3. Update the API route to use Anthropic SDK

## 💾 Database Schema

The template includes a Supabase schema for storing conversations:

```sql
-- Conversations table
CREATE TABLE conversations (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id UUID NOT NULL,
  title TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Messages table
CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  conversation_id UUID REFERENCES conversations(id),
  role TEXT NOT NULL, -- 'user' or 'assistant'
  content TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

## 🚢 Deployment

### Deploy to Vercel

1. Push your code to GitHub
2. Import repository in Vercel
3. Add environment variables:
   - `OPENAI_API_KEY`
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
4. Deploy!

## 📁 Project Structure

```
ai-chatbot/
├── app/
│   ├── layout.tsx
│   ├── page.tsx            # Chat interface
│   ├── api/
│   │   └── chat/           # Chat API route
│   └── dashboard/          # Conversation history
├── components/
│   ├── chat/               # Chat components
│   └── ui/                 # UI components
├── lib/
│   ├── openai.ts          # OpenAI client
│   └── supabase.ts        # Supabase client
└── supabase/
    └── migrations/        # Database migrations
```

## 🎨 Customization

### Chat Interface

Edit `components/chat/ChatInterface.tsx` to customize the chat UI.

### AI Model

Change the model in `app/api/chat/route.ts`:

```typescript
const response = await openai.chat.completions.create({
  model: "gpt-4", // Change to your preferred model
  messages: [...],
});
```

## 📝 License

MIT License

---

Built with ❤️ using Rapid Builder
