---
name: text-entity-relation-extractor
description: Extract entities and relationships from unstructured text and convert them into graph-ready structures such as triples, nodes, and edges.
metadata:
  {"openclaw":{"emoji":"🧠","homepage":"https://clawhub.com"}}
---

# Text → Entity / Relation Extractor

Extract structured knowledge from unstructured text.

This skill analyzes natural language text and identifies **entities and relationships** that can be converted into **knowledge graph structures** such as nodes, edges, or semantic triples.

It is useful for transforming documents, articles, transcripts, or raw text into **graph-ready data** suitable for knowledge graphs, semantic systems, or graph databases.

---

# When To Use This Skill

Use this skill when a user wants to:

- Extract **entities from text**
- Identify **relationships between entities**
- Convert natural language text into **knowledge graphs**
- Generate **triples from text**
- Build **graph datasets from documents**
- Perform **information extraction from unstructured content**

Example requests:

- “Extract entities from this article.”
- “Build a knowledge graph from this text.”
- “Identify relationships between people and companies in this paragraph.”
- “Convert this document into graph triples.”

---

# What This Skill Produces

The skill extracts structured information in three layers.

### 1. Entities

Entities are real-world objects mentioned in text.

Common entity types include:

- Person
- Organization
- Location
- Product
- Event
- Technology

Example:

Text:
```text
Alice works at Acme Corporation in London.
```

Extracted entities:
```text
Alice → Person
Acme Corporation → Organization
London → Location
```

---

### 2. Relationships

Relationships describe how entities are connected.

Example:
```text
Alice works at Acme Corporation
```

Extracted relationship:
```text
Alice → WORKS_AT → Acme Corporation
```


---

### 3. Triples

The final output is structured as **subject–predicate–object triples**.

Example:

```text
Alice WORKS_AT Acme_Corporation
Acme_Corporation LOCATED_IN London
```

These triples can be used directly in **knowledge graphs or graph databases**.

---

# Example Transformation

Input text:
```text
Elon Musk founded SpaceX in 2002.
SpaceX is headquartered in California.
```

Extracted entities:
```text
Elon Musk → Person
SpaceX → Organization
California → Location
2002 → Date
```

Extracted relationships:
```text
Elon Musk FOUNDED SpaceX
SpaceX HEADQUARTERED_IN California
```

Triples:
```text
Elon_Musk FOUNDED SpaceX
SpaceX HEADQUARTERED_IN California
```

---

# Output Formats

The extracted knowledge can be exported in multiple formats.

### RDF Triples
```text
:Elon_Musk :founded :SpaceX .
:SpaceX :headquarteredIn :California .
```

---

### Graph JSON
```json
{
    "nodes": [
        {"id":"Elon Musk","type":"Person"},
        {"id":"SpaceX","type":"Organization"},
        {"id":"California","type":"Location"}
    ],
    "edges":[
        {"from":"Elon Musk","to":"SpaceX","type":"FOUNDED"},
        {"from":"SpaceX","to":"California","type":"HEADQUARTERED_IN"}
    ]
}
```

---

### Tabular Output

| Entity 1 | Relationship | Entity 2 |
|--------|-------------|--------|
| Elon Musk | FOUNDED | SpaceX |
| SpaceX | HEADQUARTERED_IN | California |

---

# Extraction Strategy

When processing text:

1. **Named Entity Recognition (NER)**  
   Identify entities such as people, organizations, locations, and products.

2. **Relationship Detection**  
   Detect verbs or phrases that indicate relationships between entities.

3. **Entity Normalization**  
   Standardize entity names and remove duplicates.

4. **Triple Generation**  
   Convert extracted information into structured triples.

5. **Graph Construction**  
   Represent entities as nodes and relationships as edges.

---

# Implementation Notes

The skill may internally use:

- Named Entity Recognition (NER)
- Relation extraction models
- Dependency parsing
- Pattern-based extraction
- Semantic parsing

These techniques enable converting **unstructured text into structured knowledge graphs**.

---

# Best Practices

When extracting entities and relationships:

- Normalize repeated entities.
- Use consistent naming conventions.
- Prefer meaningful relationship labels.
- Avoid creating duplicate nodes.
- Validate relationships before adding them to the graph.

---

# Summary

This skill converts **unstructured natural language text into structured knowledge** by extracting:

- entities
- relationships
- graph triples

The resulting data can be used to build **knowledge graphs, semantic search systems, and graph databases**.