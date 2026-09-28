# EvidenceDesk

A document question-answering service that answers only from its sources, cites them, and says "I don't know" when the evidence isn't there.

```
HTTP → FastAPI → service → PostgreSQL + pgvector → hybrid retrieval (BM25 + semantic) → LLM → cited answer
```

I'm building it in public over eight weeks to take an LLM application from a script to a tested, evaluated and deployed service.

## What it will do
- **Ingest** a corpus of documents into typed `Document` / `Chunk` records stored in PostgreSQL.
- **Retrieve** with BM25, semantic search (pgvector) and hybrid rank fusion, plus optional reranking.
- **Answer** through a `/ask` endpoint with citations, and refuse questions the sources can't support.
- **Act** through a tool-calling agent (`search_documents`, `get_document`, `list_sources`) with guardrails: step limits, allowlists and timeouts.
- **Measure** itself: a gold query set with Recall@k / MRR, answer faithfulness, refusal accuracy and agent trajectory checks, gated in CI.
- **Run anywhere** with Docker Compose, GitHub Actions and an AWS deployment.

## Progress
- [ ] Week 1: Python foundations, domain models, first FastAPI endpoints
- [ ] Week 2: PostgreSQL, SQLAlchemy, repository layer, tests
- [ ] Week 3: LLM mechanics, metrics, first cited answer
- [ ] Week 4: BM25, embeddings, pgvector
- [ ] Week 5: Hybrid retrieval, reranking, evaluation harness
- [ ] Week 6: Docker, logging, CI with an evaluation gate
- [ ] Week 7: Tool-calling agent and agent evaluation
- [ ] Week 8: AWS deployment and hardening → `v1.0.0`

## Layout
```
evidence_desk/   application package
tests/           pytest suite
corpus/          sample documents for local runs
notes/adr/       architecture decision records
```

## Setup
```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
pytest
```
