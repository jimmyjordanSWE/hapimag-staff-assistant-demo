# Data Sources Strategy

## Short answer

Yes, we can build a strong RAG demo without Hapimag internal data.

The best approach is a **hybrid corpus**:

1. Synthetic hospitality SOP/policy docs (primary RAG corpus)
2. Open hospitality/travel QA datasets (evaluation and robustness)
3. Public official references (compliance/security grounding)

## Recommended dataset mix

### 1) Core RAG corpus (recommended first)

- Create synthetic but realistic resort docs:
  - booking rules
  - cancellation/refund policy
  - check-in/out exception playbooks
  - front desk escalation SOPs
- Keep all examples fictional and non-identifying.
- This is the safest and most interview-effective path.

### 2) Open hospitality/travel QA data (for eval and scenario coverage)

- Bitext hospitality LLM dataset (25k rows, CDLA-Sharing 1.0)
  - https://huggingface.co/datasets/bitext/Bitext-hospitality-llm-chatbot-training-dataset
- Bitext travel LLM dataset (CDLA-Sharing 1.0)
  - https://huggingface.co/datasets/bitext/Bitext-travel-llm-chatbot-training-dataset

Use these mostly for:
- test prompts,
- intent coverage,
- adversarial/safety scenario generation.

### 3) Structured hotel demand data (optional analytics sidecar)

- Hotel Booking Demand dataset (open access article + supplied data)
  - https://www.sciencedirect.com/science/article/pii/S2352340918315191
- Useful for analytics demos (cancellations/seasonality), not SOP RAG text itself.

### 4) Public Swiss tourism stats (context layer)

- Swiss BFS PX-Web hotel arrivals/overnight stays table
  - https://www.pxweb-r.bfs.admin.ch/pxweb/en/px-x-1003020000_102/-/px-x-1003020000_102.px/

Use this for:
- dashboard context,
- interview narrative about demand trends.

## Licensing and usage notes

- Track license per source in a simple `DATA_SOURCES.md` table.
- Keep third-party text in a separate folder from synthetic docs.
- For CDLA/ODbL-like share-alike sources, keep attribution in repo docs.
- Do not mix unclear-license scraped content into the core demo corpus.

## Proposed folder split

```text
data/
  synthetic_resort_policies/      # primary RAG corpus
  external_open_datasets/         # eval/scenario data only
  references/                     # official PDFs/links + metadata
```

## Decision

For this project, we should treat synthetic resort policy docs as source-of-truth and use open datasets only to improve test coverage and realism.

