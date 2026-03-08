---
name: kg_schema_from_text
title: Knowledge Graph Ontology & Schema Generation from Text
description: Generate a structured knowledge graph ontology or schema from unstructured or semi-structured text sources.
category: graph-modeling
tags:
  - knowledge-graph
  - ontology
  - schema
  - rdf
  - owl
  - graph-modeling
  - entity-extraction
  - developer-tools
version: 0.1.0
author: community
license: MIT
---

# Knowledge Graph Ontology / Schema Generation from Text

## Purpose

This skill helps developers **automatically derive a knowledge graph ontology or schema from natural language descriptions, documentation, datasets, or domain text**.

It converts textual descriptions into structured graph models including:

- Entities / Node Types
- Relationships / Edge Types
- Properties / Attributes
- Constraints
- Domain ontology definitions

This is primarily designed for **knowledge graph developers designing initial schemas from domain documentation**.

---

# When To Use This Skill

Use this skill when:

- A developer provides **domain documentation**
- A developer wants to **bootstrap a knowledge graph schema**
- A developer wants to convert **requirements → ontology**
- A developer needs a **first version of RDF/OWL or property graph schema**

Example prompts:

- "Generate a knowledge graph schema from this domain description."
- "Extract ontology entities and relationships from this text."
- "Create an RDF ontology from this documentation."
- "Design a Neo4j schema based on this business domain."

---

# Inputs

The skill expects one or more of the following:

- Natural language domain descriptions
- Technical documentation
- Example records
- JSON/CSV structures
- API response schemas
- Requirements specifications

Example input:

A university system contains students, professors, courses and departments.

Students enroll in courses.

Professors teach courses.

Departments manage professors and courses.


---

# Expected Output

The skill should generate:

1. **Entity Types**
2. **Relationship Types**
3. **Properties**
4. **Constraints**
5. **Graph Schema Representation**

Outputs may include:

- Property Graph Schema
- RDF Triples
- OWL Ontology
- JSON Schema representation

Example output structure:

Entities:

- Student

- Professor

- Course

- Department

Relationships:

Student -> ENROLLED_IN -> Course

Professor -> TEACHES -> Course

Department -> MANAGES -> Course

Department -> EMPLOYS -> Professor

Properties:

Student:

- student_id

- name

- email

Course:

- course_id

- title

- credits


---

# Developer Implementation Notes

When code generation or automation is required, prefer **Python implementations** using common knowledge graph and NLP libraries.

Recommended libraries:

### NLP / Extraction

- spaCy
- transformers
- nltk

### Knowledge Graph Construction

- networkx
- rdflib
- pyvis
- owlready2

### Schema Generation

- pydantic
- dataclasses
- jsonschema

### Visualization

- pyvis
- graphviz

---

# Example Python Workflow

Below is a minimal reference implementation showing how extracted entities and relations can be converted into a graph.

```python
import networkx as nx

entities = ["Student", "Professor", "Course", "Department"]

relationships = [
    ("Student", "ENROLLED_IN", "Course"),
    ("Professor", "TEACHES", "Course"),
    ("Department", "MANAGES", "Course"),
]

G = nx.MultiDiGraph()

for entity in entities:
    G.add_node(entity, type="entity")

for src, rel, dst in relationships:
    G.add_edge(src, dst, relation=rel)

print(G.nodes())
print(G.edges(data=True))
```
Example RDF generation:

```python
from rdflib import Graph, Namespace, RDF

g = Graph()
ex = Namespace("http://example.org/")

g.add((ex.Student, RDF.type, ex.Entity))
g.add((ex.Student, ex.ENROLLED_IN, ex.Course))

print(g.serialize(format="turtle"))
```

## Skill Behavior Guidelines

When executing this skill:

1. Identify core entities
2. Identify relationships
3. Extract properties
4. Infer graph structure
5. Suggest ontology extensions
6. Output machine-readable schema

Always:

* prefer clear graph structures

* avoid ambiguous relationships

* normalize entity naming

* follow knowledge graph modeling best practices

##### Best Practices

Recommended modeling principles:

* Use clear entity naming

* Avoid duplicate relationships

* Use domain-driven design

* Separate schema vs instance data

* Maintain consistent relationship direction

