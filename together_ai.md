
---
title: Together AI
weight: 900
aliases:
  - /documentation/examples/together-ai-search/
  - /documentation/tutorials/together-ai-search/
  - /documentation/integrations/together-ai/ 
---

# Using Together AI with Qdrant 

Together AI focuses on collaborative AI embeddings that enhance multi-user search scenarios when integrated with Qdrant.

## Installation

You can install the required package using the following pip command:

```bash
pip install togetherai
```

## Code Example

Below is an example of how to obtain embeddings using Together AI's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from togetherai import TogetherAI

# Initialize Together AI model
model = TogetherAI("togetherai-collab")

# Generate embeddings for collaborative content
text = "Together AI enhances collaborative content search."
embeddings = model.embed(text)

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="CollaborativeContent",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate Together AI's embeddings into Qdrant.
