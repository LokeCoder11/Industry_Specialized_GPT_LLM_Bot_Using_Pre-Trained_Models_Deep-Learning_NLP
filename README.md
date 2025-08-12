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
- Project Summary.doc
- FAQs on Master Direction on KYC.pdf
- LLMBotProject.ipynb - Colab.html
- chatbot workflow.jpg
- WorkingChatbotScreenshot.png
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

## Acknowledgements

- Acknowledgements: Thanks to the Reserve Bank of India for the publicly available KYC FAQ resource and to the open‑source community behind the LLM tooling that makes small‑GPU experimentation possible.

## Disclaimer

This project is for educational and prototyping purposes. For official guidance, customers should rely on their bank’s communications and the RBI’s latest publications.

## Author

Lokesh Todi
