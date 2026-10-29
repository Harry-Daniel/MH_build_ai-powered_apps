# AI-Powered Apps

A full-stack TypeScript monorepo with two AI features:

- **Chatbot**: a customer-support assistant for "WonderWorld", a fictional theme park, powered by OpenAI (`gpt-4o-mini`) with conversation memory.
- **Review summarizer**: generates and caches AI summaries of product reviews, using a local model through Ollama (`tinyllama`).

🎥 **[Watch the demo](https://drive.google.com/file/d/1aHd_DA9qHIHqiXdsIOy0DL01YsE4E_SA/view)**

## Tech stack

| Layer   | Tools                                                                      |
| ------- | -------------------------------------------------------------------------- |
| Runtime | [Bun](https://bun.com) workspaces                                          |
| Server  | Express 5, Prisma (MySQL), Zod, OpenAI SDK, Ollama, Hugging Face Inference |
| Client  | React 19, Vite, Tailwind CSS, TanStack Query, React Hook Form, shadcn/ui   |

## Project structure

```
packages/
├── server/   # Express API: controllers → services → repositories, LLM client, prompts
└── client/   # React UI: chat and review components
```

## Prerequisites

- [Bun](https://bun.com)
- A MySQL database
- An [OpenAI API key](https://platform.openai.com/api-keys)
- [Ollama](https://ollama.com) running locally, with the model pulled: `ollama pull tinyllama`
- Optional: a [Hugging Face token](https://huggingface.co/settings/tokens)

## Setup

```bash
bun install

cp packages/server/.env.example packages/server/.env
# Fill in OPENAI_API_KEY, DATABASE_URL (e.g. mysql://user:password@localhost:3306/db) and optionally HF_TOKEN

cd packages/server
bunx prisma migrate dev
cd ../..
```

## Running

```bash
bun run dev
```

This starts the server on `http://localhost:3000` and the Vite client (which proxies `/api` to the server) in one terminal.

## API

| Method | Endpoint                              | Description                         |
| ------ | ------------------------------------- | ----------------------------------- |
| POST   | `/api/chat`                           | Send a message to the chatbot       |
| GET    | `/api/products/:id/reviews`           | Get a product's reviews and summary |
| POST   | `/api/products/:id/reviews/summarize` | Generate a review summary           |
