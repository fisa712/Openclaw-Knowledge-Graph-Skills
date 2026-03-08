---
name: etl-pipeline-generator
description: Generate automated ETL pipelines for transforming and loading data into graph databases or knowledge graphs.
metadata:
  {"openclaw":{"emoji":"⚙️","homepage":"https://clawhub.com"}}
---

# ETL Pipeline Generator

Design automated pipelines for **Extract–Transform–Load (ETL)** workflows.

This skill generates structured ETL pipelines that move raw data from various sources into **graph-ready datasets** or **knowledge graph storage systems**.

It orchestrates data ingestion, transformation, and loading steps so that messy input data becomes structured graph data.

---

# When To Use This Skill

Use this skill when a user wants to:

- Build an **ETL pipeline**
- Automate **data ingestion workflows**
- Transform datasets before loading them into a **graph database**
- Connect multiple transformation steps together
- Create **repeatable data pipelines**

Example requests:

- “Generate an ETL pipeline for my dataset.”
- “Build a workflow that ingests CSV and outputs triples.”
- “Create a pipeline for loading JSON API data into a knowledge graph.”
- “Automate data transformation and graph ingestion.”

---

# What This Skill Produces

The skill generates a **multi-step pipeline** consisting of three stages.

### 1. Extract

Retrieve raw data from external sources.

Possible sources:

- CSV files
- JSON files
- APIs
- databases
- text documents
- logs
- streaming sources

Example extract step:
```text
source: api

endpoint: https://api.example.com/products

format: json
```


---

### 2. Transform

Convert raw data into graph-ready structures.

Transformation examples:

- CSV → nodes and edges
- JSON → RDF triples
- text → entity relationships
- normalization of entities
- schema mapping

Example transformation:

transform:

* normalize_entities

* generate_relationships

* map_schema


---

### 3. Load

Load transformed data into the target graph system.

Possible targets:

- graph databases
- RDF triple stores
- property graph engines
- knowledge graph platforms

Example load step:

load:
```
target: neo4j
method: bulk_import
```

---

# Example Pipeline

Example pipeline specification:

pipeline:

`name: customer_graph_ingestion`

extract:
```text
type: csv
source: customers.csv
```

transform:
- detect_entities
- generate_relationships
- convert_to_triples

load:
```text
target: graph_database
format: property_graph
```
---

# Example Generated Workflow

Step 1 — Extract

Read CSV file containing customer data.

Step 2 — Transform

Convert rows into entities such as Customer, Product, and Order.

Step 3 — Relationship Generation

Customer → PURCHASED → Product

Step 4 — Load

Insert nodes and relationships into the graph database.

---

# Output Formats

The pipeline can be generated in multiple formats.

### YAML Pipeline

extract:
```text
source: customers.csv
format: csv
```

transform:

```text
detect_entities

create_nodes

create_relationships
```

load:
```text
target: neo4j
```

---

### DAG Representation

Extract → Transform → Normalize → Generate Triples → Load

---

### Script-Based Pipeline

Example pseudocode:
```python
extract_data()
transform_entities()
generate_relationships()
load_graph()
```

---

# Implementation Notes

The pipeline generator may integrate with:

- CSV ingestion tools
- JSON processing pipelines
- graph ETL frameworks
- streaming data processors
- knowledge graph loaders

It can orchestrate transformations using previously defined skills such as:

- CSV → Graph Loader Generator
- JSON → Triples Converter
- Text → Entity / Relation Extractor

---

# Best Practices

When designing ETL pipelines:

- Ensure **data validation** before loading.
- Normalize entities to avoid duplicates.
- Maintain **consistent identifiers**.
- Log pipeline steps for observability.
- Make pipelines **repeatable and idempotent**.

---

# Summary

This skill generates automated **Extract–Transform–Load pipelines** that convert raw datasets into structured graph data.

It enables:

- scalable ingestion workflows
- automated knowledge graph construction
- repeatable data transformation pipelines