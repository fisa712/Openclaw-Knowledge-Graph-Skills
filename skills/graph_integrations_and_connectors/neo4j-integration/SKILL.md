---

name: neo4j_integration
description: Connect to a Neo4j graph database, execute Cypher queries, and perform graph operations from within the knowledge graph development workflow.
category: integrations
tags:

* knowledge-graph
* neo4j
* graph-database
* cypher
* integration
* graph-query
  version: 1.0.0
  author: kg-dev-skills

---

# Neo4j Integration

## Purpose

This skill enables interaction with a **Neo4j graph database** for storing, querying, and managing knowledge graph data.

It allows developers to:

* connect to a Neo4j instance
* execute Cypher queries
* insert nodes and relationships
* retrieve graph structures
* update or delete graph data

Neo4j uses the **property graph model**, where data is represented as nodes, relationships, and properties.

---

## When To Use This Skill

Use this skill when:

* working with a **Neo4j-backed knowledge graph**
* executing **Cypher queries**
* importing graph data into Neo4j
* retrieving nodes or relationships
* updating graph structures
* debugging graph queries

Example triggers:

* "Run this Cypher query"
* "Insert these nodes into Neo4j"
* "Create relationships in the graph"
* "Fetch nodes connected to X"
* "Update node properties"

---

## Connection Configuration

The skill requires connection credentials for a Neo4j instance.

Example configuration:

```json
{
  "uri": "bolt://localhost:7687",
  "username": "neo4j",
  "password": "password"
}
```

Supported protocols:

* `bolt`
* `neo4j`
* `neo4j+s`
* `neo4j+ssc`

---

## Core Capabilities

### Execute Cypher Queries

Run Cypher queries to interact with graph data.

Example query:

```cypher
MATCH (n:Person)
RETURN n
LIMIT 10
```

---

### Create Nodes

Example:

```cypher
CREATE (p:Person {name: "Alice", age: 30})
```

---

### Create Relationships

Example:

```cypher
MATCH (a:Person {name: "Alice"}), (b:Person {name: "Bob"})
CREATE (a)-[:KNOWS]->(b)
```

---

### Retrieve Graph Data

Example:

```cypher
MATCH (a)-[r]->(b)
RETURN a, r, b
```

---

### Update Node Properties

Example:

```cypher
MATCH (p:Person {name: "Alice"})
SET p.age = 31
```

---

### Delete Nodes or Relationships

Example:

```cypher
MATCH (p:Person {name: "Alice"})
DELETE p
```

---

## Inputs

Expected inputs may include:

* Cypher queries
* node data
* relationship definitions
* connection credentials

Example input:

```json
{
  "query": "MATCH (n) RETURN n LIMIT 5"
}
```

---

## Output

Results returned from Neo4j queries.

Example:

```json
{
  "records": [
    {"name": "Alice"},
    {"name": "Bob"}
  ]
}
```

Results may include:

* nodes
* relationships
* query statistics

---

## Procedure

1. Establish connection to the Neo4j database.
2. Validate connection credentials.
3. Accept Cypher queries or graph operations.
4. Execute queries using the Neo4j driver.
5. Retrieve results from the database.
6. Format output for downstream use.

---

## Developer Notes

Neo4j drivers available for:

* Python
* JavaScript
* Java
* Go

Typical workflow:

1. ingest data
2. build graph schema
3. run queries
4. analyze results

Best practices:

* use indexes for frequent queries
* avoid large cartesian products
* batch large data imports

---

## Expected Benefits

Using this skill enables:

* direct interaction with Neo4j databases
* efficient graph querying with Cypher
* easy graph data management
* integration with graph-based applications

---

## Related Skills

* RDF Triple Store Integration
* TigerGraph Connector
* JanusGraph Connector
* GraphQL Graph Mapping
