
---
title: Clarifai
weight: 900
aliases:
  - /documentation/examples/clarifai-search/
  - /documentation/tutorials/clarifai-search/
  - /documentation/integrations/clarifai/ 
---

# Using Clarifai Embeddings with Qdrant 

Clarifai is a leading provider of visual embeddings, which are particularly strong in image and video analysis. Clarifai offers an API that allows you to create embeddings for various media types, which can be integrated into Qdrant for efficient vector search and retrieval. You can install the Clarifai Python client with pip:

```bash
pip install clarifai-client
```

Below is an example of how to obtain embeddings for an image using Clarifai's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from clarifai.rest import ClarifaiApp

# Initialize Clarifai client
clarifai_app = ClarifaiApp(api_key="<< your_api_key >>")

# Choose the model for embeddings
model = clarifai_app.public_models.general_embedding_model

# Upload and get embeddings for an image
image_path = "./path/to/the/image.jpg"
response = model.predict_by_filename(image_path)

# Extract the embedding from the response
embedding = response['outputs'][0]['data']['embeddings'][0]['vector']

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient()

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="MyCollection",
    points=Batch(
        ids=[1],
        vectors=[embedding],
    )
)
```

This example demonstrates how to integrate Clarifai's visual embeddings into Qdrant. You can use similar steps for text or video embeddings by selecting the appropriate model and input method.
