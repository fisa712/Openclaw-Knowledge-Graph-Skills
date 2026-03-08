---
name: csv-graph-loader-generator
description: Generate graph database loaders and triple mappings from CSV datasets. Converts tabular CSV data into graph-ready nodes, edges, and triples for graph databases or knowledge graphs.
metadata:
  {"openclaw":{"emoji":"📥","homepage":"https://clawhub.com"}}
---

# CSV → Graph Loader Generator

Convert CSV datasets into graph-ready structures.

This skill helps transform **tabular CSV data** into **graph database ingestion formats** such as nodes, edges, or triples.  
It generates mappings and loader scripts that make it easy to import CSV datasets into graph systems like **Neo4j, RDF triple stores, property graphs, or knowledge graphs**.

Use this skill whenever a user wants to **convert structured tabular data into graph structures**.

---

# When To Use This Skill

Use this skill when the user asks to:

- Convert **CSV datasets into a graph structure**
- Generate **nodes and relationships from tabular data**
- Create **graph import scripts**
- Prepare **CSV data for graph databases**
- Build **triples or property graphs from tables**
- Generate **ETL loaders for CSV graph ingestion**

Example requests:

- “Turn this CSV into a graph schema.”
- “Generate nodes and relationships from a CSV dataset.”
- “Create a Neo4j import script from CSV.”
- “Convert this table into RDF triples.”

---

# What This Skill Produces

The skill can generate:

1. **Graph Schema**
   - Node types
   - Relationship types
   - Property definitions

2. **Mapping Definitions**
   - Column → node property mappings
   - Column → relationship mappings
   - Entity identifiers

3. **Loader Scripts**
   Examples include:

- Neo4j `LOAD CSV`
- RDF triple generation
- Graph ETL scripts
- JSON-LD conversion

4. **Triple Format**

Example transformation:

```CSV
person_id,name,company

1,Alice,Acme

2,Bob,Acme
```
**Graph representation**

Nodes:
```
(:Person {id:1,name:"Alice"})

(:Person {id:2,name:"Bob"})

(:Company {name:"Acme"})
```
Edges:
```
(:Person)-[:WORKS_AT]->(:Company)
```

---

# Transformation Strategy

When converting CSV to a graph structure:

1. **Detect Entities**
   Identify columns that represent entities (people, organizations, locations).

2. **Determine Node Types**
   Create node labels from entity categories.

3. **Create Relationships**
   Map relational columns to graph edges.

4. **Assign Properties**
   Map remaining columns as node properties.

5. **Generate Import Script**
   Produce loader instructions for the target graph engine.

---

# Output Formats

The generated output may include:

### Neo4j Loader
```
LOAD CSV WITH HEADERS FROM 'file:///data.csv' AS row

MERGE (p:Person {id: row.person_id})

SET p.name = row.name

MERGE (c:Company {name: row.company})

MERGE (p)-[:WORKS_AT]->(c);
```

### RDF Triples

:Alice rdf:type :Person .

:Alice :worksAt :Acme .

:Acme rdf:type :Company .

### Graph JSON
```json
{
    "nodes":[
        {"id":"Alice","type":"Person"},
        {"id":"Acme","type":"Company"}
    ],
    "edges":[
        {"from":"Alice","to":"Acme","type":"WORKS_AT"}
    ]
}
```


---

# Implementation Notes

The skill may:

- Parse CSV headers
- Infer entity columns
- Generate node and relationship definitions
- Produce graph ingestion scripts

Possible tools used internally:

- CSV parsers
- Graph schema generators
- RDF mappers
- ETL pipelines

If the user provides a CSV dataset, analyze the schema and automatically produce the **best graph mapping**.

---

# Best Practices

When generating graph loaders:

- Prefer **stable identifiers** for node keys.
- Avoid duplicating nodes when relationships repeat.
- Normalize repeated entities into shared nodes.
- Clearly define relationship directions.

---

# Summary

This skill transforms **tabular CSV datasets into graph-ready structures** by generating:

- node schemas
- relationship mappings
- loader scripts
- graph triples

Use it whenever structured CSV data must be **ingested into a graph database or knowledge graph**.