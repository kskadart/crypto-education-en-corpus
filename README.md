---
license: apache-2.0
language:
  - en
tags:
  - crypto
  - blockchain
  - education
  - rag
size_categories:
  - n<1K
dataset_info:
  splits:
    - name: train
      num_examples: 52
    - name: validation
      num_examples: 6
    - name: test
      num_examples: 8
---

# Crypto Education EN Corpus

A curated English-language corpus of crypto and blockchain educational content, scraped from public sources and converted to clean Markdown. Designed for use in RAG (Retrieval-Augmented Generation) pipelines.

## Stats

- **66 pages** (train: 52, validation: 6, test: 8)
- **95,286 words**
- **Sources**: Ethereum.org, Coinbase Learn, Binance Academy, Investopedia

## Format

JSONL files split into `train.jsonl`, `validation.jsonl`, and `test.jsonl` (80/10/10). Each line is one page:

```json
{"url": "https://...", "title": "Page Title", "markdown": "Clean markdown content...", "word_count": 1234, "depth": 0}
```

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `url` | string | Source page URL |
| `title` | string | Page title |
| `markdown` | string | Clean Markdown content |
| `word_count` | int | Number of words in the page |
| `depth` | int | Crawl depth (0 = seed page) |

## Collection

Scraped using [simple-web-scraper](https://github.com/kskadart/web-scraper) with Crawl4AI. Content was filtered with a pruning threshold of 0.4 and a minimum of 30 words per page.
