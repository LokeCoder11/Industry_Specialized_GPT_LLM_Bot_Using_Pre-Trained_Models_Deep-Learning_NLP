# Industry_Specialized_GPT_LLM_Bot_Using_Pre-Trained_Models_Deep-Learning_NLP
Industry_Specialized_GPT_LLM_Bot creation using  Pre-Trained_Models and NLP Deep Learning

# Banking KYC GPT — Industry‑Specialized LLM Chatbot

I built an AI chatbot specialized for Banking, focused on India’s Know Your Customer (KYC) rules and customer queries. The bot is trained and grounded on the Reserve Bank of India’s “FAQs on Master Direction on KYC” to give clear, accurate, and up‑to‑date guidance to typical customer questions.

> Primary reference: Reserve Bank of India — FAQs on Master Direction on KYC (June 9, 2025)

## What I set out to build

- A practical, domain‑aware chatbot that answers common KYC questions customers ask banks in India.
- A Colab‑friendly workflow that runs smoothly on a T4 GPU with modest resources.
- A simple, polished user experience suitable for demos and classroom or internal training use.

## What the chatbot can do

- Explain KYC basics: when KYC is required, who needs it, and why it matters.
- List accepted documents: OVDs, deemed OVDs for address, PAN/Form 60, and edge cases like name change.
- Clarify onboarding modes: in‑person, e‑KYC, V‑CIP, and non‑face‑to‑face options.
- Handle practical scenarios: opening accounts with a different current address, small accounts without OVDs, periodic re‑KYC, risk categorization, and inoperative account reactivation.
- Provide compliance‑aligned answers by referencing the RBI KYC FAQ content in natural language.

## Why RBI KYC FAQs

- Authoritative: Official guidance used across Indian banks for KYC.
- Customer‑centric: FAQ format aligns with real user queries and branch operations.
- Updated: The June 9, 2025 update reflects current practices, including e‑KYC and V‑CIP.

## Scope and guardrails

- I focus on KYC in the Indian banking context. I do not provide legal advice.
- Where policy depends on a bank’s internal procedures, I indicate that customers should confirm with their bank.
- For sensitive or unclear cases, I prompt users toward official channels or detailed documentation.

## How I structured the project

- Data curation: Extracted and organized relevant Q&A from the RBI KYC FAQ, preserving definitions and conditions (e.g., thresholds like ₹50,000, periodicity for re‑KYC by risk segment).
- Model selection: Compact, instruction‑tuned LLM suitable for Colab GPU for fast, reliable responses.
- Prompting and grounding: Concise prompts with retrieved snippets from the RBI FAQ to keep answers faithful and minimize hallucination.
- Evaluation: Tested with realistic customer scenarios (opening new accounts, address changes, joint accounts, re‑KYC reminders, V‑CIP questions, inoperative accounts).

## Example user journeys

- “Do I need to redo KYC if I open another account at the same bank?”
- “My Aadhaar has an old address. Can I still open an account where I currently live?”
- “What documents are acceptable as proof of address if my OVD has a different address?”
- “How often do I need to update KYC? What if I’m low risk?”
- “What is V‑CIP and do I need to do any special gestures for liveness?”
- “Can I use my KYC Identifier to open an account at another bank branch?”
- “What happens if I don’t update KYC even after reminders?”

## What’s included in this repo

- LLMBotProject.ipynb
- LLMBotProject.ipynb - Colab.html
- LLMBotProject.ipynb - Colab_files(Folder)
- Project Summary.doc
- FAQs on Master Direction on KYC.pdf
- chatbot workflow.jpg
- WorkingChatbotScreenshot.png
- faiss_index.index
- requirements.txt
- README.md

## Quality, safety, and ethics

- I follow the RBI’s definitions and recommended practices to reduce ambiguity.
- I avoid storing or requesting personal data.
- I include clear disclaimers and direct users to the bank or official sources for case‑specific guidance.

## Limitations

- I do not replace a bank’s official KYC process or legal advice.
- Certain operational details vary across banks (e.g., exact branch procedures). I point users to confirm with their bank where necessary.
- Regulations evolve. I aim to reflect the RBI KYC FAQ as of June 9, 2025 and will update as guidance changes.

## Planned improvements

- Expand coverage to additional RBI consumer protection FAQs relevant to KYC and onboarding.
- Provide multilingual support for broader accessibility.
- Add structured retrieval for specific clauses (e.g., paragraph references) to improve traceability.

## How to use this project

1. Open the Colab notebook in GPU mode.
2. Start the chat interface and test with real‑world KYC questions.

## Retrieval-Augmented Generation (RAG) Overview
This project uses a retrieval + generator pipeline to answer domain questions accurately and transparently.

- Retriever:
  - Scrape the RBI FAQ content from the provided RBI FAQ link only.
  - Create dense embeddings with a sentence-transformer model.
  - Index embeddings using FAISS for fast similarity search.

- Generator:
  - Use Hugging Face Transformers flan-t5-small to generate answers grounded in retrieved RBI FAQ passages.

- Flow:
  1. User question
  2. Embed with sentence-transformer
  3. FAISS similarity search over RBI FAQ chunks
  4. Concatenate top-k contexts
  5. flan-t5-small generates the final answer conditioned on retrieved context

## Data Source Policy
- Only use the RBI FAQ content from the single RBI FAQ link specified in this repository/documentation.
- Do not use external sources for retrieval or training beyond the approved RBI FAQ link.

## Environment and Dependencies
- Python 3.9 or later recommended
- Core libraries:
  - transformers
  - sentence-transformers
  - faiss-cpu
  - gradio
  - datasets
  - requests, beautifulsoup4
  - accelerate, peft, bitsandbytes (for efficient fine-tuning)

## RBI FAQ Scraping (Strict Source Use)
- Input: the single approved RBI FAQ URL provided in this project.
- Expected output: cleaned question-answer pairs (Q/A) normalized for whitespace and boilerplate removal, stored with fields: id, question, answer, url.
- Note: Adjust parsing selectors to match the exact RBI FAQ page structure.

## Embedding and Indexing
- Embedding model: sentence-transformers (e.g., all-MiniLM-L6-v2 or similar compact model).
- Chunking: split RBI FAQ answers into manageable chunks (e.g., 200–500 tokens with overlap) and store metadata (faq_id, question, url).
- Index: build a FAISS index (e.g., inner product or HNSW) for similarity search.
- Persistence: save the FAISS index and metadata for reproducible retrieval.

## Answer Generator
- Model: google/flan-t5-small (Hugging Face Transformers).
- Prompting guidelines:
  - Use only the provided RBI FAQ context.
  - Cite RBI FAQ and avoid speculation.
  - Keep answers concise and factual.
- Decoding: beam search or nucleus sampling with a conservative max token budget.

## Gradio Web UI in Colab
- An interactive Gradio chat UI embedded in Google Colab is provided for demos.
- Features:
  - Input box for user questions
  - Display of top-k retrieved snippets for transparency
  - Generated answer with clear source attribution
  - Optional toggle to show the model prompt
- Launch with public share enabled for easy review and testing.

## Example Interaction
- Ask: “What is X according to the RBI FAQ?”
- Pipeline:
  1. Embed the question
  2. Retrieve top-3 context chunks from FAISS
  3. Format the prompt with retrieved context
  4. Generate answer with flan-t5-small
  5. Present answer and sources in the UI

## Fine-Tuning
- Objective: optionally fine-tune flan-t5-small on RBI FAQ Q/A pairs to improve domain tone and format while staying grounded in context.
- Data format:
  - Input: “Context: \nQuestion: \nAnswer:”
  - Target: the official RBI answer text (lightly cleaned if necessary)
- Training:
  - Epochs: up to 25
  - Learning rate: 5e-5 to 1e-4
  - Batch size: fit to GPU memory; use gradient accumulation as needed
  - Early stopping on evaluation loss to reduce overfitting
  - Optional PEFT/LoRA for parameter-efficient fine-tuning
- Important: keep retrieval enabled even after fine-tuning to ensure answers remain grounded.

## Evaluation
- Intrinsic:
  - Retrieval quality: recall@k on held-out questions
  - Generation quality: exact match or ROUGE-L against official RBI answers
- Extrinsic:
  - Human review to confirm that responses are strictly supported by the retrieved RBI FAQ context

## Reproducibility
- Fix random seeds across embedding, indexing, and generation.
- Persist artifacts:
  - Scraped RBI FAQ dataset (JSONL)
  - Embedding model name and version
  - FAISS index and metadata
  - flan-t5-small revision or fine-tuned checkpoint tag

## Security and Compliance
- Source restriction: only the provided RBI FAQ link is permitted for scraping, retrieval, and (optional) fine-tuning.
- Citation: each answer must indicate it is derived from the RBI FAQ context shown in the UI.
- No personal data processing; all content is public RBI FAQ text.

## Summary
- Scrape the RBI FAQ from the approved link
- Build sentence-transformer embeddings and FAISS index
- Load flan-t5-small as the answer generator
- Provide a Gradio chat interface with context transparency
- Run fine-tuning (up to 25 epochs) and evaluate

## Acknowledgements

- Acknowledgements: Thanks to the Reserve Bank of India for the publicly available KYC FAQ resource and to the open‑source community behind the LLM tooling that makes small‑GPU experimentation possible.

## Disclaimer

This project is for educational and prototyping purposes. For official guidance, customers should rely on their bank’s communications and the RBI’s latest publications.

## Author

Lokesh Todi
