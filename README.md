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
---

# Crypto Education EN Corpus

A curated English-language corpus of crypto and blockchain educational content, scraped from public sources and converted to clean Markdown. Designed for use in RAG (Retrieval-Augmented Generation) pipelines.

## Stats

- **66 pages**
- **95,286 words**
- **Sources**: Ethereum.org, Coinbase Learn, Binance Academy, Investopedia

## Format

Single JSON file (`corpus.json`) with structure:

```json
{
  "pages": [
    {
      "url": "https://...",
      "title": "Page Title",
      "markdown": "Clean markdown content...",
      "word_count": 1234,
      "depth": 0
    }
  ],
  "metadata": {
    "total_pages": 66,
    "total_words": 95286
  }
}
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
