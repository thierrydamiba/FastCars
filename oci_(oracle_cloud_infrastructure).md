
---
title: OCI (Oracle Cloud Infrastructure)
weight: 900
aliases:
  - /documentation/examples/oci-(oracle-cloud-infrastructure)-search/
  - /documentation/tutorials/oci-(oracle-cloud-infrastructure)-search/
  - /documentation/integrations/oci-(oracle-cloud-infrastructure)/ 
---

# Using OCI (Oracle Cloud Infrastructure) with Qdrant 

OCI provides robust cloud-based embeddings for various media types. Their integration into Qdrant allows for efficient vector search.

## Installation

You can install the required package using the following pip command:

```bash
pip install oci
```

## Code Example

Below is an example of how to obtain embeddings using OCI (Oracle Cloud Infrastructure)'s API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
import oci

# Initialize OCI client
config = oci.config.from_file()
ai_client = oci.ai_language.AIServiceLanguageClient(config)

# Generate embeddings using OCI's AI service
text = "OCI provides cloud-based AI services."
response = ai_client.batch_detect_language_entities(text)
embeddings = response.data[0].entities[0].embedding

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="CloudAI",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate OCI (Oracle Cloud Infrastructure)'s embeddings into Qdrant.
