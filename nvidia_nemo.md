
---
title: NVIDIA NeMo
weight: 900
aliases:
  - /documentation/examples/nvidia-nemo-search/
  - /documentation/tutorials/nvidia-nemo-search/
  - /documentation/integrations/nvidia-nemo/ 
---

# Using NVIDIA NeMo with Qdrant 

NVIDIA NeMo offers powerful models for generating embeddings from large datasets, optimized for performance with Qdrant.

## Installation

You can install the required package using the following pip command:

```bash
pip install nemo
```

## Code Example

Below is an example of how to obtain embeddings using NVIDIA NeMo's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from nemo.collections.nlp.models import BERTLMModel

# Initialize NVIDIA NeMo model
model = BERTLMModel.from_pretrained("nemo_bert")

# Generate embeddings for large datasets
text = "NVIDIA NeMo powers large-scale NLP applications."
embeddings = model.forward([text])[0]

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="LargeScaleNLP",
    points=Batch(
        ids=[1],
        vectors=[embeddings.detach().numpy().tolist()],
    )
)

```

This example demonstrates how to integrate NVIDIA NeMo's embeddings into Qdrant.
