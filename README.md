# Hybrid AI Search Application

An advanced AI-powered research and search application that combines the strengths of multiple LLMs, search providers, and cutting-edge RAG (Retrieval Augmented Generation) techniques. Built with a hybrid approach using Next.js, Vercel AI SDK, and Python/LangChain backend services.

## Features

### Core Search Capabilities
- **Multi-provider Search**: Choose between SearXNG, Exa.ai, or Tavily
- **AI-enhanced Results**: LLM processing of search results for summarization and insights
- **Document Processing**: Upload and analyze documents within your research
- **Citation Management**: Automatically extract and validate sources

### AI Integration
- **Multiple LLM Support**: 
  - OpenAI (GPT-4o)
  - Anthropic (Claude 3)
  - Google (Gemini)
- **Model Switching**: Change models on-the-fly in the chat interface
- **Streaming Responses**: Real-time streaming for better UX
- **Context Retention**: Conversation memory for meaningful exchanges

### User Management
- **User Profiles**: Customizable preferences and settings
- **Chat History**: Persistent storage of all research sessions
- **Document Storage**: Save and organize research documents
- **Subscription Plans**: Tiered access using Razorpay payment integration

## Tech Stack

### Frontend
- **Next.js 14+** with App Router
- **Tailwind CSS** + shadcn/ui components
- **Vercel AI SDK** for streaming UI
- **Zustand** for state management

### Backend & Infrastructure
- **Next.js API Routes** for core functionality
- **Python FastAPI** service for complex processing
- **Supabase** for database, auth, and storage
  - PostgreSQL with pgvector for vector search
- **Upstash Redis** for caching and rate limiting
- **Razorpay** for subscription management

### AI & Search
- **LangChain** for document processing and advanced agents
- **SearXNG/Exa.ai/Tavily** for web search capabilities
- **OpenAI Embeddings** for vector search

## Architecture

The application uses a hybrid architecture that leverages:

1. **Next.js and Vercel AI SDK** for the user-facing application and real-time AI interactions
2. **Python/LangChain services** for complex document processing, agent behaviors, and research workflows
3. **Supabase** as the core data layer for users, chats, and vector embeddings
4. **Redis** for performance optimization and caching

## Subscription Model

The app offers multiple subscription tiers through Razorpay:

- **Free**: Limited searches and basic AI features
- **Basic**: More searches and document uploads
- **Pro**: All LLM models and advanced research features
- **Enterprise**: Custom limits and dedicated support

Subscription management handles:
- Recurring billing
- Plan upgrades/downgrades
- Usage tracking and quotas

## Environment Setup

The application requires the following environment variables:

```env
# Core Infrastructure
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_key

# Redis
UPSTASH_REDIS_REST_URL=your_redis_url
UPSTASH_REDIS_REST_TOKEN=your_redis_token

# LLM APIs
OPENAI_API_KEY=your_openai_key
ANTHROPIC_API_KEY=your_anthropic_key
GEMINI_API_KEY=your_gemini_key

# Search Providers
SEARXNG_INSTANCE_URL=your_searxng_url
EXA_API_KEY=your_exa_key
TAVILY_API_KEY=your_tavily_key

# Default Search Provider (options: "searxng", "exa", "tavily")
NEXT_PUBLIC_DEFAULT_SEARCH=tavily

# Razorpay
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
RAZORPAY_WEBHOOK_SECRET=your_webhook_secret
```

## Getting Started

### Prerequisites
- Node.js 18+
- Python 3.9+
- pnpm (recommended)
- Poetry (for Python dependencies)
- Docker (optional, for local development)

### Installation

1. Clone the repository
```bash
git clone https://github.com/smartduke/hybrid-search-app.git
cd hybrid-search-app
```

2. Install dependencies
```bash
# Install frontend dependencies
pnpm install

# Install Python dependencies (for local development)
cd python-services
poetry install
cd ..
```

3. Set up environment variables
```bash
cp .env.example .env.local
# Edit .env.local with your API keys and configuration
```

4. Set up Supabase
- Create a Supabase project
- Run the database migrations in `supabase/migrations`
- Configure authentication providers

5. Start the development servers
```bash
# Start the Next.js app
pnpm dev

# In another terminal, start the Python service
cd python-services
poetry run uvicorn app.main:app --reload
```

6. Visit http://localhost:3000 to see the application

## Deployment

### Deploying to Vercel
1. Push your code to GitHub
2. Create a new project in Vercel
3. Link your repository
4. Set up environment variables
5. Deploy!

### Deploying Python Services
1. Deploy to Railway.app or Fly.io
2. Set environment variables
3. Update the API endpoint in your Next.js app

## Project Structure

```
/
├── app/                    # Next.js App Router
│   ├── api/                # API routes
│   │   ├── auth/           # Auth endpoints
│   │   ├── chat/           # Chat endpoints
│   │   ├── search/         # Search endpoints
│   │   ├── subscription/   # Razorpay integration
│   │   └── vector/         # Vector operations
│   ├── (auth)/             # Auth pages
│   ├── chat/               # Chat interface
│   ├── search/             # Search interface
│   ├── pricing/            # Subscription plans
│   └── profile/            # User profile management
├── components/             # React components
├── lib/                    # Shared utilities
│   ├── supabase/           # Supabase client
│   ├── redis/              # Upstash Redis client
│   ├── razorpay/           # Razorpay utilities
│   └── ai/                 # AI utilities
├── python-services/        # Python backend
│   ├── app/                # FastAPI app
│   ├── processors/         # Document processors
│   └── agents/             # Research agents
├── public/                 # Static assets
└── supabase/               # Supabase configuration
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
