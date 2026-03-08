---
name: api-ingestion-connectors
description: Connect to external APIs and ingest data into graph-ready structures for ETL pipelines and knowledge graph construction.
metadata:
  {"openclaw":{"emoji":"🌐","homepage":"https://clawhub.com"}}
---

# API Ingestion Connectors

Connect external APIs to graph ingestion pipelines.

This skill retrieves data from APIs and prepares it for transformation into **graph-ready formats** such as nodes, relationships, and triples.

It enables automated ingestion of structured or semi-structured data from:

- REST APIs
- GraphQL APIs
- web services
- SaaS platforms
- public data APIs

The retrieved data can then be processed by downstream transformation skills such as:

- JSON → Triples Converter
- CSV → Graph Loader Generator
- Text → Entity / Relation Extractor

---

# When To Use This Skill

Use this skill when a user wants to:

- ingest data from an **API**
- integrate **external services into a data pipeline**
- pull data periodically from web services
- transform API responses into **graph datasets**
- connect APIs to **knowledge graph ingestion workflows**

Example requests:

- “Ingest data from this REST API.”
- “Build a pipeline that pulls data from an API and converts it into triples.”
- “Fetch data from this endpoint and load it into a graph database.”
- “Create an ingestion connector for a public API.”

---

# What This Skill Produces

The skill generates **API ingestion configurations** and **data connectors** that can be used inside ETL pipelines.

The configuration typically includes:

1. **API Endpoint**
2. **Authentication Method**
3. **Request Parameters**
4. **Response Format**
5. **Transformation Strategy**

---

# Example API Configuration

Example REST API connector:
connector:
```text
type: rest_api
endpoint: https://api.example.com/products
method: GET
response_format: json
```

---

# Example GraphQL Connector
connector:

type: graphql

endpoint: https://api.example.com/graphql

query:
```json
{
    products {
        id
        name
        manufacturer
    }
}
```

---

# Example Pipeline Integration

Example ingestion pipeline using an API source:

pipeline:

extract:

type: api

endpoint: https://api.example.com/users

transform:
- convert_json_to_triples
- normalize_entities

load:

target: graph_database

---

# Example Data Flow

Step 1 — Fetch data

GET https://api.example.com/users

Step 2 — API response

```json
{
    "users": [
        {"id":1,"name":"Alice","company":"Acme"}
    ]
}
```

Step 3 — Transformation

Entities:
```text
Alice → Person
Acme → Organization
```

Relationships:
```text
Alice WORKS_AT Acme
```

Step 4 — Graph Output
```text
:Alice :worksAt :Acme .
```

---

# Supported Authentication Methods

API connectors may support:

- API keys
- bearer tokens
- OAuth
- basic authentication

Example:
```text
auth:
type: bearer
token: ${API_TOKEN}
```

---

# Pagination Handling

Many APIs return paginated responses. The connector may support automatic pagination.

Example:

```text
pagination:
type: page
parameter: page
start: 1
```

---

# Output Formats

The ingested data can be passed to downstream skills as:

- JSON datasets
- CSV files
- graph triples
- node/edge structures

---

# Implementation Notes

The connector may internally:

- perform HTTP requests
- handle authentication
- process pagination
- parse API responses
- convert results into structured datasets

These outputs can then feed ETL pipelines and knowledge graph ingestion processes.

---

# Best Practices

When ingesting data from APIs:

- respect API rate limits
- implement retry logic
- validate response schemas
- normalize repeated entities
- cache results when possible

---

# Summary

This skill creates connectors that ingest data from **external APIs** and feed it into **graph ingestion pipelines**.

It enables:

- automated API data ingestion
- integration of external services
- real-time knowledge graph updates
- scalable data pipeline architectures