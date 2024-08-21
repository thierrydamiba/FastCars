
---
title: GPT4All
weight: 900
aliases:
  - /documentation/examples/gpt4all-search/
  - /documentation/tutorials/gpt4all-search/
  - /documentation/integrations/gpt4all/ 
---

# Using GPT4All with Qdrant 

GPT4All offers a range of large language models that can be fine-tuned for various applications. These embeddings can be integrated with Qdrant for advanced text search.

## Installation

You can install the required package using the following pip command:

```bash
pip install gpt4all
```

## Code Example

Below is an example of how to obtain embeddings using GPT4All's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from gpt4all import GPT4All

# Initialize GPT4All model
model = GPT4All("gpt4all-lora-quantized")

# Generate embeddings for a text
text = "GPT4All enables open-source AI applications."
embeddings = model.embed(text)

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="OpenSourceAI",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate GPT4All's embeddings into Qdrant.
