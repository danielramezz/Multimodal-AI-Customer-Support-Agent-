# Multimodal AI Customer-Support Agent for Shopify Stores

An automated support agent that answers customers from your own documents, **reads photos**, **listens to voice notes**, **remembers the conversation**, and **looks up live order status** — all over Telegram.

Built end-to-end in **n8n**.

> ⚠️ This repository is a **case study / portfolio piece**. It shows the architecture and results, not the runnable workflow file. Not licensed for reuse — see [License](#license).

---

## What it does

A customer messages the store's Telegram bot. Whatever they send — typed text, a photo of a product or receipt, or a voice note — the agent understands it, finds the answer in the store's knowledge base or live order system, and replies in seconds. No human needed for routine questions.

**Example interactions it handles:**
- *"What's your return policy?"* → answered from the store's uploaded policy docs
- *Sends a photo of a damaged item* → the agent reads the image, identifies the product, and responds
- *Leaves a voice note asking about shipping* → transcribed and answered
- *"Where's my order 1001?"* → live status, fulfillment, and tracking pulled straight from Shopify

---

## Key features

- **RAG knowledge base** — ingests the store's own files (PDF, Excel, CSV, text, even scanned images via OCR) from a Google Drive folder, so answers are grounded in real policies, never made up.
- **Vision** — customers can send a picture; a vision model describes it and transcribes any visible text (order numbers, model/serial numbers, error messages) to search against.
- **Voice notes** — voice messages are transcribed and answered like any other question.
- **Per-customer memory** — the agent remembers the conversation, so follow-ups like *"and what about returning that?"* keep context. Customers never see each other's history.
- **Live Shopify order lookup** — a dedicated tool queries the Shopify Admin API by order number for real-time status.
- **Typing indicator** — the bot shows "typing…" the moment a message arrives, so it feels responsive.
- **Automatic version control** — when a knowledge-base file is updated, its old content is cleanly replaced, so answers never go stale.

---

## Architecture

The system has two halves that share one vector store.

**1. Ingestion pipeline** — watches a Google Drive folder, routes each new file by type to the right extractor, chunks and embeds the content, and stores it in Postgres + pgvector with source metadata and delete-before-insert version control.

**2. Conversational agent** — a Telegram bot routes each message by type (text / photo / voice), normalizes it into a query, and hands it to an AI agent that chooses between two tools: the knowledge base and live order lookup. Memory persists per customer.

<!-- Add your screenshots here. Keep node panels closed so no settings/secrets are visible. -->

## Workflow Overview
<img width="2184" height="1145" alt="▶️ RAG 3 0 - n8n - Google Chrome 6_30_2026 5_24_34 PM(1)" src="https://github.com/user-attachments/assets/32db8706-9f0c-4ec9-86a0-ab0cc2be7960" />
)

## Customer Agent
<img width="1591" height="1128" alt="▶️ RAG 3 0 - n8n - Google Chrome 6_30_2026 5_30_13 PM(1)" src="https://github.com/user-attachments/assets/d2a63fa6-9baa-43c9-b39f-37ad63b82027" />


---

## Small Test

<!-- Drop a short screen recording or GIF here, or link to a Loom / YouTube demo. -->

📹 
<img width="2424" height="1198" alt="Telegram Web - Google Chrome 6_30_2026 5_32_22 PM(1)" src="https://github.com/user-attachments/assets/2cb9bf51-dfd9-471a-8714-f533bff3cdb7" />


---

## Tech stack

| Layer | Tool |
|---|---|
| Orchestration | n8n |
| Vector store | PostgreSQL + pgvector |
| Embeddings & reasoning | OpenAI |
| Vision | GPT-4o |
| Speech-to-text | Whisper |
| Messaging | Telegram |
| Commerce | Shopify Admin API |

---

## Why it's useful for a store

- Deflects routine support tickets 24/7
- Answers only from the store's real docs — no hallucinated policies
- Meets customers where they already are (Telegram) and in whatever format they send
- Turns "where's my order?" — the #1 support question — into an instant self-serve answer

---

## License

All rights reserved. This repository is published to demonstrate the architecture and outcomes of a custom build. The workflow itself is not included and is not licensed for copying, reuse, or redistribution.

---

## Let's work together

I build custom AI automations for e-commerce and SMBs — agents, RAG systems, and workflow automation that actually ship.

**Want something like this for your store? Let's talk.**

- 💼 LinkedIn: **[Daniel Ramez](www.linkedin.com/in/daniel-ramez-mounir-4b64aa3b0)**
- 📧 Email: your@email.com
