
---
title: Azure AI
weight: 900
aliases:
  - /documentation/examples/azure-ai-search/
  - /documentation/tutorials/azure-ai-search/
  - /documentation/integrations/azure-ai/ 
---

# Using Azure AI with Qdrant 

Azure AI provides advanced AI capabilities including natural language processing and computer vision.

## Installation

You can install the required package using the following pip command:

```bash
pip install azure-ai-client
```

## Code Example

Below is an example of how to obtain embeddings using Azure AI's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential

# Initialize Azure Text Analytics client
credential = AzureKeyCredential("your_azure_key")
endpoint = "https://your_endpoint.cognitiveservices.azure.com/"
client = TextAnalyticsClient(endpoint=endpoint, credential=credential)

# Generate embeddings using Azure AI
text = "Azure AI offers powerful NLP capabilities."
response = client.extract_key_phrases([text])
embeddings = [float(ord(c)) for c in ''.join(response[0].key_phrases)]

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="AzureNLP",
    points=Batch(
        ids=[1],
        vectors=[embeddings],
    )
)

```

This example demonstrates how to integrate Azure AI's embeddings into Qdrant.
