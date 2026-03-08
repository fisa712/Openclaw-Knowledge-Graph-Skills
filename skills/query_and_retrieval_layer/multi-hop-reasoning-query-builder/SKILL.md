---
name: multi-hop-reasoning-query-builder
description: Generate graph queries that perform multi-hop traversal and reasoning across relationships in graph databases and knowledge graphs.
metadata:
  {"openclaw":{"emoji":"🔗","homepage":"https://clawhub.com"}}
---

# Multi-hop Reasoning Query Builder

Construct graph queries that explore indirect relationships through multiple hops in a graph.

This skill helps developers generate queries that traverse several relationships to discover hidden connections and complex patterns within graph datasets.

Multi-hop reasoning is commonly used in:

- knowledge graph exploration
- recommendation systems
- fraud detection
- supply chain analysis
- social network analysis

The skill produces queries that traverse multiple edges to identify connections between entities.

---

# When To Use This Skill

Use this skill when a user wants to:

- build multi-hop graph queries
- explore indirect relationships
- perform reasoning across graph paths
- discover connections through several relationships
- construct path traversal queries

Example requests:

- “Find friends of friends of Alice.”
- “Find suppliers connected to a company within three hops.”
- “Discover customers linked through purchase chains.”
- “Find entities connected to a node within multiple relationships.”

---

# What This Skill Produces

The skill generates graph queries capable of:

- multi-hop traversal
- path discovery
- indirect relationship detection
- graph reasoning queries
- variable-length path exploration

Outputs may include:

- Cypher traversal queries
- SPARQL property path queries
- graph path exploration queries

---

# Example Multi-hop Query

Natural language request:

Find friends of friends of Alice.

Generated Cypher query:
```text
MATCH (a:Person {name:"Alice"})-[:FRIEND_OF*2]->(friend)
RETURN friend
```

This query finds people who are two friendship relationships away from Alice.

---

# Variable Hop Query

Query that finds connections within a range of hops:
```text
MATCH (a:Person {name:"Alice"})-[:FRIEND_OF*1..3]->(person)
RETURN person
```

This returns all people connected to Alice within one to three hops.

---

# Path Discovery Query

Cypher example:
```text
MATCH path = (a:Person {name:"Alice"})-[*1..4]-(connected)
RETURN path
LIMIT 50
```

This query returns relationship paths connecting Alice to other nodes.

---

# SPARQL Property Path Example

Equivalent SPARQL query:
```text
SELECT ?person
WHERE {
:Alice :friendOf+ ?person .
}
```

The `+` operator represents traversal across one or more relationships.

---

# Supply Chain Reasoning Example

Natural language request:

Find suppliers connected to CompanyA within three relationships.

Generated query:
```text
MATCH (c:Company {name:"CompanyA"})-[:SUPPLIES_TO*1..3]->(supplier)
RETURN supplier
```

This identifies indirect suppliers within a supply chain network.

---

# Fraud Detection Example

Multi-hop queries can detect suspicious relationship clusters.

Example:
```text
MATCH (a:Account)-[:TRANSFER*1..4]->(b:Account)
WHERE a.id <> b.id
RETURN a,b
```

This query finds transaction paths that may indicate fraud rings.

---

# Reasoning Strategy

When building multi-hop queries:

1. **Identify the starting node**

Determine the entity where traversal begins.

2. **Identify relationship types**

Detect which relationships are relevant to the reasoning process.

3. **Determine hop depth**

Define the number of traversal steps required.

4. **Construct traversal pattern**

Generate variable-length relationship paths.

5. **Return nodes or paths**

Return either the connected nodes or the full traversal paths.

---

# Output Formats

The skill may generate:

### Traversal Query

Executable Cypher or SPARQL query.

### Path Query

Queries that return relationship paths.

### Parameterized Query

Reusable templates.

Example:
```text
MATCH (start:Entity {id:$id})-[*1..$depth]-(target)
RETURN target
```

---

# Implementation Notes

The reasoning query builder may internally perform:

- graph traversal pattern generation
- relationship inference
- path search optimization
- schema-aware query construction

It can integrate with other query skills such as:

- Natural Language → Query Translator
- Query Optimization Assistant
- Template Query Generator

---

# Best Practices

When building multi-hop queries:

- limit traversal depth to prevent expensive queries
- restrict relationship types when possible
- use result limits to avoid large responses
- start traversal from specific nodes

Example:
```text
MATCH (a:Person {name:"Alice"})-[:FRIEND_OF*1..2]-(friend)
RETURN friend
LIMIT 25
```

---

# Summary

This skill generates multi-hop graph queries that traverse multiple relationships to uncover indirect connections and hidden patterns in graph datasets.

It enables developers to perform advanced graph reasoning using Cypher or SPARQL.