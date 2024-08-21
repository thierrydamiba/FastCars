
---
title: MixedBread
weight: 900
aliases:
  - /documentation/examples/mixedbread-search/
  - /documentation/tutorials/mixedbread-search/
  - /documentation/integrations/mixedbread/ 
---

# Using MixedBread with Qdrant 

MixedBread is a unique provider offering embeddings across multiple domains. Their models are versatile for various search tasks when integrated with Qdrant.

## Installation

You can install the required package using the following pip command:

```bash
pip install mixedbread
```

## Code Example

Below is an example of how to obtain embeddings using MixedBread's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from mixedbread import MixedBreadModel

# Initialize MixedBread model
model = MixedBreadModel("mixedbread-variant")

# Generate embeddings
text = "MixedBread provides versatile embeddings for various domains."
embeddings = model.embed(text)

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="VersatileEmbeddings",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate MixedBread's embeddings into Qdrant.
