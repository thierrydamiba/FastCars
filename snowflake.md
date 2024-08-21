
---
title: Snowflake
weight: 900
aliases:
  - /documentation/examples/snowflake-search/
  - /documentation/tutorials/snowflake-search/
  - /documentation/integrations/snowflake/ 
---

# Using Snowflake with Qdrant 

Snowflake offers cloud-native embeddings that can be easily integrated into Qdrant for scalable vector search and retrieval.

## Installation

You can install the required package using the following pip command:

```bash
pip install snowflake
```

## Code Example

Below is an example of how to obtain embeddings using Snowflake's API and store them in a Qdrant collection:

```python
import qdrant_client
from qdrant_client.models import Batch
import snowflake.connector

# Initialize Snowflake connector
conn = snowflake.connector.connect(
    user='your_username',
    password='your_password',
    account='your_account'
)

# Fetch embeddings from Snowflake
query = "SELECT embedding FROM your_table WHERE id=1"
cursor = conn.cursor()
cursor.execute(query)
embedding = cursor.fetchone()[0]

# Initialize Qdrant client
qdrant_client = qdrant_client.QdrantClient(host="localhost", port=6333)

# Upsert the embedding into Qdrant
qdrant_client.upsert(
    collection_name="SnowflakeData",
    points=Batch(
        ids=[1],
        vectors=[embedding],
    )
)

```

This example demonstrates how to integrate Snowflake's embeddings into Qdrant.
