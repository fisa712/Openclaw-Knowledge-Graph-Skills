---
name: json-triples-converter
description: Convert JSON documents into RDF triples or graph-ready subject–predicate–object statements for knowledge graphs and semantic databases.
metadata:
  {"openclaw":{"emoji":"🔗","homepage":"https://clawhub.com"}}
---

# JSON → Triples Converter

Transform JSON documents into **RDF triples** or **graph-ready structures**.

This skill converts hierarchical JSON data into **subject–predicate–object triples**, enabling the data to be ingested into **knowledge graphs, semantic web systems, and graph databases**.

The generated triples can be exported in formats such as:

- RDF Turtle
- N-Triples
- JSON-LD
- Graph JSON

Use this skill whenever structured **JSON needs to be transformed into graph or semantic data formats**.

---

# When To Use This Skill

Use this skill when a user wants to:

- Convert **JSON data into RDF triples**
- Transform **JSON APIs into knowledge graphs**
- Extract **semantic relationships from JSON structures**
- Convert **nested JSON into subject–predicate–object statements**
- Generate **JSON-LD or RDF from JSON documents**
- Prepare JSON for **graph database ingestion**

Example requests:

- “Convert this JSON to RDF triples.”
- “Turn this API JSON response into a knowledge graph.”
- “Generate semantic triples from this JSON dataset.”
- “Create a JSON-LD representation from this JSON.”

---

# What This Skill Produces

The skill generates:

### 1. RDF Triples

Triples follow the structure:
```
Subject → Predicate → Object
```
Example:
```
:Alice :worksAt :Acme .
:Alice :age 30 .
```

---

### 2. JSON-LD

Example transformation:

Input JSON
```json
{
    "person": {
        "name": "Alice",
        "age": 30,
        "company": "Acme"
    }
}
```

Converted JSON-LD

```json
{
    "@context": {
        "name": "http://schema.org/name",
        "age": "http://schema.org/age",
        "worksAt": "http://schema.org/worksFor"
    },
    "@type": "Person",
    "name": "Alice",
    "age": 30,
    "worksAt": "Acme"
}
```

---

### 3. Graph Representation

Nodes:
```
(:Person {name:"Alice"})
(:Company {name:"Acme"})
```

Edges:
```
(:Person)-[:WORKS_AT]->(:Company)
```

---

# Transformation Strategy

When converting JSON to triples:

1. **Identify Entities**

   Detect objects that represent real-world entities such as:

   - people
   - organizations
   - products
   - locations

2. **Generate Subjects**

   Create unique identifiers for each entity.

3. **Map Keys to Predicates**

   JSON keys become predicates in triples.

Example:

`"name": "Alice"`

becomes

`:entity :name "Alice"`


4. **Handle Nested Objects**

Nested JSON structures become **relationships between entities**.

Example:
```json
{
    "employee": {
        "name": "Alice",
        "company": {
            "name": "Acme"
        }
    }
}
```

Triples:
```
:Alice :worksAt :Acme .
:Acme rdf:type :Company .
```

5. **Normalize Repeated Entities**

Ensure shared entities are not duplicated.

---

# Output Formats

This skill can generate triples in multiple formats.

### Turtle
```
@prefix ex: http://example.org/.
ex:Alice ex:worksAt ex:Acme .
ex:Alice ex:age 30 .
```

---

### N-Triples
http://example.org/Alice    http://example.org/worksAt    http://example.org/Acme .

---

### Graph JSON
```json
{
    "nodes": [
        {"id": "Alice", "type": "Person"},
        {"id": "Acme", "type": "Company"}
    ],
    "edges": [
        {"from": "Alice", "to": "Acme", "type": "WORKS_AT"}
    ]
}
```

---

# Implementation Notes

The skill may internally:

- Parse JSON structures
- Traverse nested objects
- Generate subject identifiers
- Map keys to predicates
- Produce RDF triples or JSON-LD

Possible tooling used:

- JSON parsers
- RDF generators
- schema.org mappings
- graph ETL utilities

If the user provides a JSON dataset, analyze the structure and automatically generate the **most appropriate triple representation**.

---

# Best Practices

When generating triples:

- Use consistent **URI namespaces**
- Avoid duplicate nodes for the same entity
- Normalize repeated objects into shared nodes
- Use standard vocabularies when possible (e.g., schema.org)

---

# Summary

This skill converts **JSON data into RDF triples and graph-ready formats**, enabling JSON datasets to be used in:

- knowledge graphs
- semantic web applications
- graph databases
- linked data systems

Use it whenever JSON needs to be transformed into **subject–predicate–object graph structures**.