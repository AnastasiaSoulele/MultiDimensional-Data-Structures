# Multidimensional Data Structures — R-Tree & LSH

A Python implementation of an **R-Tree** and **LSH (Locality Sensitive Hashing)**
for multidimensional spatial indexing and similarity search.
Built as a university Multidimensional Data Structures project.

##  Overview

The project implements two advanced data structures for
multidimensional querying on scientist data scraped from Wikipedia:

- **R-Tree** — spatial indexing using Minimum Bounding Rectangles (MBR)
  for efficient range queries
- **LSH** — probabilistic similarity search using MinHash signatures
  and Jaccard similarity

##  R-Tree Architecture

### Node Operations
| Method | Description |
|--------|-------------|
| `add_entry()` | Inserts entry into correct node, recomputes MBR, triggers split if needed |
| `split()` | Simple node split — O(N) |
| `linear_split()` | Optimized split along best axis — O(N), better MBR quality |
| `compute_mbr()` | Recomputes MBR from scratch (used after splits) |
| `enlarge_rect()` | Computes new MBR from two existing ones |

### R-Tree Operations
| Method | Description |
|--------|-------------|
| `insert()` | Inserts entry into the appropriate leaf node |
| `balance_tree()` | Handles root splits and propagates splits upward recursively |
| `leaf_area()` | Finds optimal insertion area based on MBR overlap |
| `query_rtree()` | Range search comparing query against MBRs |

##  Complexity

| Operation | Average | Worst |
|-----------|---------|-------|
| Search | O(log_M(N)) | O(N) |
| Insert | O(log_M(N)) | O(N) |

> `M` = max_nodes per node. Tuning `max_nodes` and choosing the right
> split method significantly impacts performance and MBR integrity.

##  LSH Pipeline

```
Education text → Shingling → MinHash signatures → Band hashing → Candidate pairs → Jaccard filter
```

| Function | Description |
|----------|-------------|
| `shingle()` | Converts text to k-shingles set |
| `minhash()` | Generates 50-hash MinHash signature |
| `backet_creator()` | Groups signature into bands for LSH bucketing |
| `jaccard()` | Computes Jaccard similarity between shingle sets |
| `lsh()` | Returns pairs above similarity threshold |

##  How to Run

```bash
python menu.py
```

##  Technologies
- Python 3
- Custom R-Tree implementation
- LSH with MinHash & Jaccard similarity
- BeautifulSoup4 (web scraping)

##  Context
University project — Multidimensional Data Structures course.
