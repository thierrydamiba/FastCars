
---
title: Clip
weight: 900
aliases:
  - /documentation/examples/clip-search/
  - /documentation/tutorials/clip-search/
  - /documentation/integrations/clip/ 
---

# Using Clip with Qdrant 

Clip provides advanced AI capabilities including natural language processing and computer vision.

## Installation

You can install the required package using the following pip command:

```bash
pip install clip-client
```

## Code Example

Below is an example of how to obtain embeddings using Clip's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
from transformers import CLIPProcessor, CLIPModel
from PIL import Image

# Load the CLIP model and processor
model = CLIPModel.from_pretrained("openai/clip-vit-base-patch32")
processor = CLIPProcessor.from_pretrained("openai/clip-vit-base-patch32")

# Load and process the image
image = Image.open("path/to/image.jpg")
inputs = processor(images=image, return_tensors="pt")

# Generate embeddings
with torch.no_grad():
    embeddings = model.get_image_features(**inputs).numpy().tolist()

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="ImageEmbeddings",
    points=Batch(
        ids=[1],
        vectors=embeddings,
    )
)

```

This example demonstrates how to integrate Clip's embeddings into Qdrant.
