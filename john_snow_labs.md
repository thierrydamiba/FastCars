
---
title: John Snow Labs
weight: 900
aliases:
  - /documentation/examples/john-snow-labs-search/
  - /documentation/tutorials/john-snow-labs-search/
  - /documentation/integrations/john-snow-labs/ 
---

# Using John Snow Labs with Qdrant 

John Snow Labs is a leading provider of NLP solutions, particularly in the healthcare domain. They offer pre-trained models that can generate embeddings for medical text data.

## Installation

You can install the required package using the following pip command:

```bash
pip install johnsnowlabs
```

## Code Example

Below is an example of how to obtain embeddings using John Snow Labs's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from johnsnowlabs import nlp

# Load the pre-trained model, for example, a named entity recognition (NER) model
model = nlp.load_model("ner_jsl")

# Sample text to generate embeddings
text = "John Snow Labs provides state-of-the-art healthcare NLP solutions."

# Generate embeddings for the text
document = nlp.DocumentAssembler().setInput(text)
embeddings = model.transform(document).collectEmbeddings()

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embeddings into Qdrant
qdrant_client.upsert(
    collection_name="HealthcareNLP",
    points=Batch(
        ids=[1],  # This would be your unique ID for the data point
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate John Snow Labs's embeddings into Qdrant.
