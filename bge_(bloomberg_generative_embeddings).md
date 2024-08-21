
---
title: BGE (Bloomberg Generative Embeddings)
weight: 900
aliases:
  - /documentation/examples/bge-(bloomberg-generative-embeddings)-search/
  - /documentation/tutorials/bge-(bloomberg-generative-embeddings)-search/
  - /documentation/integrations/bge-(bloomberg-generative-embeddings)/ 
---

# Using BGE (Bloomberg Generative Embeddings) with Qdrant 

BGE provides advanced financial text embeddings that are particularly useful for integrating with Qdrant in the finance sector.

## Installation

You can install the required package using the following pip command:

```bash
pip install bge
```

## Code Example

Below is an example of how to obtain embeddings using BGE (Bloomberg Generative Embeddings)'s API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from bge_client import BGEModel

# Initialize the BGE model
model = BGEModel(api_key="your_api_key")

# Specify the model variant, e.g., "bge-small", "bge-medium", etc.
model_name = "bge-small"

# Generate embeddings for financial text
text = "The stock market showed significant volatility in the past quarter."
embeddings = model.embed(text, model_name=model_name)

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="FinancialData",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate BGE (Bloomberg Generative Embeddings)'s embeddings into Qdrant.
