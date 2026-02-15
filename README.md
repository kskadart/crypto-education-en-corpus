---
language:
  - en
license: mit
tags:
  - crypto
  - cryptocurrency
  - blockchain
  - education
  - rag
  - retrieval-augmented-generation
size_categories:
  - 1K<n<10K
task_categories:
  - text-retrieval
  - question-answering
---

# Crypto Education Corpus (EN)

A curated educational corpus about cryptocurrency and blockchain technology, designed for building and evaluating RAG (Retrieval-Augmented Generation) systems.

## Dataset Description

- **Total documents:** 3,487
- **Total words:** ~3.6M
- **Language:** English
- **Domain:** Cryptocurrency & blockchain education

### Source Distribution

| Source | Documents | Share |
|--------|----------|-------|
| iqwiki.com | 2,379 | 68.2% |
| academy.binance.com | 581 | 16.7% |
| kraken.com | 183 | 5.2% |
| coinbase.com | 125 | 3.6% |
| gemini.com | 94 | 2.7% |
| ethereum.org | 74 | 2.1% |
| investopedia.com | 51 | 1.5% |

### Word Count Statistics

| Metric | Value |
|--------|-------|
| Mean | 1,021 |
| Median | 888 |
| Min | 100 |
| Max | 7,259 |

## Schema

| Column | Type | Description |
|--------|------|-------------|
| `url` | string | Source URL of the document |
| `title` | string | Document title |
| `markdown` | string | Full text content in Markdown format |
| `word_count` | int | Number of words in the document |
| `depth` | int | Crawl depth (0 = seed page) |
| `source` | string | Source domain name |
| `related_topics` | list[string] | Related topic names extracted from internal wiki links (iqwiki.com docs only; 59% of docs have topics) |

## Data Collection

The corpus was built from multiple sources:

1. **Web scraping** (Round 1 & 2) — Educational pages from [Investopedia](https://www.investopedia.com/cryptocurrency-4427699), [Coinbase Learn](https://www.coinbase.com/learn), [Kraken Learn](https://www.kraken.com/learn), [Ethereum.org](https://ethereum.org/en/developers/docs/), [Gemini Cryptopedia](https://www.gemini.com/cryptopedia), and others, scraped using [Crawl4AI](https://github.com/unclecode/crawl4ai) with BFS deep crawl strategy
2. **HuggingFace datasets** — Filtered educational splits from [`distilled-ai/web3-oriented-pretraining-data`](https://huggingface.co/datasets/distilled-ai/web3-oriented-pretraining-data) (Binance Academy articles, IQ Wiki encyclopedia)

### Quality Filters Applied

- Minimum 100 words per document
- Boilerplate detection (cookie/privacy/newsletter heavy pages removed)
- URL-based deduplication (normalized: lowercase, stripped fragments/query params)
- English language only
- Listing/category pages removed (link-heavy pages with <50 words of actual content)
- Raw bytecode/assembly pages removed
- Markup cleanup: wiki-style internal links, citation markers, markdown links, and bare URLs stripped from text
- Related topics metadata extracted from wiki links before cleanup

## Usage

```python
from datasets import load_dataset

ds = load_dataset("kskada/crypto-education-en-corpus")
df = ds["train"].to_pandas()

print(f"Documents: {len(df)}")
print(f"Sources: {df['source'].nunique()}")
```

## Related Datasets

- **Golden evaluation set:** [`kskada/crypto-education-en-golden-set`](https://huggingface.co/datasets/kskada/crypto-education-en-golden-set) — 497 Q&A pairs for RAG evaluation

## Citation

If you use this dataset, please reference:

```
@dataset{konovalov2026crypto_corpus,
  title={Crypto Education Corpus (EN)},
  author={Konovalov, Kirill},
  year={2026},
  publisher={HuggingFace},
  url={https://huggingface.co/datasets/kskada/crypto-education-en-corpus}
}
```

## License

MIT
