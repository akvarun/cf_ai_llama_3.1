# cf_ai_llama_3.1 — LLM Chat Application (Cloudflare Workers AI)

A simple, ready-to-deploy chat application powered by **Cloudflare Workers AI**. This project is based on the **LLM Chat Application Template** and is deployed with streaming responses via **Server-Sent Events (SSE)**.

**Live Demo:** https://llm-chat-app-template.akvarunx.workers.dev/

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/akvarun/cf_ai_llama_3.1)

---

## Optional Assignment Checklist (Cloudflare AI App)

This repository is intended to satisfy the optional Cloudflare AI app assignment requirements:

- **LLM:** Cloudflare **Workers AI** (Llama-family model)
- **Workflow / Coordination:** **Cloudflare Workers** (API + streaming coordination)
- **User Input:** Web **chat** UI
- **Memory / State:** Chat history maintained on the client (browser session)

> If you want stronger server-side memory/state for the assignment, you can extend this project with **Durable Objects** / **D1** / **KV**. (See **Optional Enhancements** below.)

References:
- Cloudflare Workers AI: https://developers.cloudflare.com/workers-ai/
- Workers AI models: https://developers.cloudflare.com/workers-ai/models/
- Cloudflare Agents (optional extension): https://developers.cloudflare.com/agents/
- Agents examples: https://agents.cloudflare.com/

---

## Demo

This template demonstrates how to build an AI-powered chat interface using Cloudflare Workers AI with streaming responses. It features:

- Real-time streaming of AI responses using Server-Sent Events (SSE)
- Easy customization of models and system prompts
- Support for AI Gateway integration
- Clean, responsive UI that works on mobile and desktop

**Deployed Demo Link:** https://llm-chat-app-template.akvarunx.workers.dev/

## Features

- Simple and responsive chat interface
- Server-Sent Events (SSE) for streaming responses
- Powered by Cloudflare Workers AI LLMs
- Built with TypeScript and Cloudflare Workers
- Mobile-friendly design
- Maintains chat history on the client
- Built-in observability logging

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or newer)
- [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install-and-update/)
- A Cloudflare account with Workers AI access

### Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/akvarun/cf_ai_llama_3.1.git
   cd cf_ai_llama_3.1
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Generate Worker type definitions (if the script exists in your package.json):

   ```bash
   npm run cf-typegen
   ```

## Development

Start a local development server:

```bash
npm run dev
# or
npx wrangler dev
```

This will start a local server (commonly) at: http://localhost:8787

**Note:** Using Workers AI accesses your Cloudflare account even during local development, which can incur usage charges.

## Deployment

Deploy to Cloudflare Workers:

```bash
npm run deploy
# or
npx wrangler deploy
```

**Deployed link:** https://llm-chat-app-template.akvarunx.workers.dev/

## Monitor

View real-time logs associated with any deployed Worker:

```bash
npx wrangler tail
```

## Project Structure

```
/
├── public/             # Static assets
│   ├── index.html      # Chat UI HTML
│   └── chat.js         # Chat UI frontend script
├── src/
│   ├── index.ts        # Main Worker entry point
│   └── types.ts        # TypeScript type definitions
├── test/               # Test files (if present)
├── wrangler.jsonc      # Cloudflare Worker configuration
├── tsconfig.json       # TypeScript configuration
└── README.md           # This documentation
```

## How It Works

### Backend

The backend is built with Cloudflare Workers and uses the Workers AI platform to generate responses. The main components are:

- **API Endpoint (/api/chat):** Accepts POST requests with chat messages and streams responses
- **Streaming:** Uses Server-Sent Events (SSE) for real-time streaming of AI responses
- **Workers AI Binding:** Connects to Cloudflare's AI service via the Workers AI binding

### Frontend

The frontend is a simple HTML/CSS/JavaScript application that:

- Presents a chat interface
- Sends user messages to the API
- Processes streaming responses in real-time
- Maintains chat history on the client side

## Customization

### Changing the Model

To use a different AI model, update the `MODEL_ID` constant in `src/index.ts`.

**Available models:**
https://developers.cloudflare.com/workers-ai/models/

### Using AI Gateway

The template includes commented code for AI Gateway integration, which provides additional capabilities like rate limiting, caching, and analytics.

To enable AI Gateway:

1. Create an AI Gateway in the Cloudflare dashboard:
   https://dash.cloudflare.com/?to=/:account/ai/ai-gateway

2. Uncomment the gateway configuration in `src/index.ts`

3. Replace `YOUR_GATEWAY_ID` with your actual AI Gateway ID

4. Configure other gateway options as needed:
   - `skipCache`: Set to `true` to bypass gateway caching
   - `cacheTtl`: Set the cache time-to-live in seconds

**Learn more:**
https://developers.cloudflare.com/ai-gateway/

### Modifying the System Prompt

Update the `SYSTEM_PROMPT` constant in `src/index.ts`.

### Styling

The UI styling is contained in the `<style>` section of `public/index.html`. Modify the CSS variables at the top to change the color scheme quickly.

## Optional Enhancements (Recommended for the Assignment)

If you want to strengthen "Memory / State" beyond client-side chat history:

- **Durable Objects:** Per-user/per-session memory store (best for chat agents)
- **D1:** Persist chat transcripts and user profiles in SQL
- **KV:** Lightweight key-value memory for preferences

These are simple add-ons and make the "memory/state" requirement very explicit.
