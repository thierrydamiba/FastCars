
---
title: Instruct
weight: 900
aliases:
  - /documentation/examples/instruct-search/
  - /documentation/tutorials/instruct-search/
  - /documentation/integrations/instruct/ 
---

# Using Instruct with Qdrant 

Instruct is a specialized provider offering detailed embeddings for instructional content, which can be effectively used with Qdrant.

## Installation

You can install the required package using the following pip command:

```bash
pip install instruct
```

## Code Example

Below is an example of how to obtain embeddings using Instruct's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from instruct import Instruct

# Initialize Instruct model
model = Instruct("instruct-base")

# Generate embeddings for instructional content
text = "Instruct provides detailed embeddings for learning content."
embeddings = model.embed(text)

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="LearningContent",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate Instruct's embeddings into Qdrant.
