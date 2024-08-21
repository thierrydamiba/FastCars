
---
title: Ollama
weight: 900
aliases:
  - /documentation/examples/ollama-search/
  - /documentation/tutorials/ollama-search/
  - /documentation/integrations/ollama/ 
---

# Using Ollama with Qdrant 

Ollama provides specialized embeddings for niche applications, making it a valuable addition to Qdrant’s vector search capabilities.

## Installation

You can install the required package using the following pip command:

```bash
pip install ollama
```

## Code Example

Below is an example of how to obtain embeddings using Ollama's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from ollama import Ollama

# Initialize Ollama model
model = Ollama("ollama-unique")

# Generate embeddings for niche applications
text = "Ollama excels in niche applications with specific embeddings."
embeddings = model.embed(text)

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="NicheApplications",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate Ollama's embeddings into Qdrant.
