---
name: nl-to-graph-query-translator
description: Translate natural language questions into Cypher or SPARQL queries for graph databases and knowledge graphs.
metadata:
  {"openclaw":{"emoji":"🔍","homepage":"https://clawhub.com"}}
---

# Natural Language → Cypher / SPARQL Translator

Convert natural language questions into executable graph queries.

This skill translates human-readable requests into graph query languages such as Cypher or SPARQL, allowing developers to interact with graph databases using natural language instead of writing complex query syntax.

It improves developer productivity by simplifying graph query construction and enabling quick data exploration.

---

# When To Use This Skill

Use this skill when a user wants to:

- Convert natural language questions into graph queries
- Generate Cypher queries for property graph databases
- Generate SPARQL queries for RDF triple stores
- Explore graph datasets using plain English
- Quickly prototype graph queries

Example requests:

- “Find employees who work at Acme.”
- “Show all companies located in California.”
- “List people connected to Alice within two hops.”
- “Find products purchased by customers in London.”

---

# What This Skill Produces

The skill generates executable graph queries in supported query languages.

Possible outputs:

- Cypher queries
- SPARQL queries
- query explanations
- query parameter templates

---

# Example Translation

Natural language:

Find employees who work at Acme.

Cypher query:

```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company {name:"Acme"})
RETURN p
```

---

Natural language:

List companies located in California.


SPARQL query:

```text
SELECT ?company
WHERE {
?company rdf:type :Company .
?company :locatedIn :California .
}
```

---

# Multi-Hop Query Example

Natural language:

Find people connected to Alice within two relationships.

Cypher query:

```text
MATCH (a:Person {name:"Alice"})-[*1..2]-(connected)
RETURN connected
```

---

# Query Translation Strategy

When translating natural language into graph queries:

1. **Identify Entities**

   Detect entity names such as people, organizations, or locations.

2. **Identify Relationships**

   Extract relationship verbs such as:

   - works at
   - located in
   - purchased
   - founded

3. **Determine Query Type**

   Determine whether the request is asking for:

   - nodes
   - relationships
   - counts
   - paths
   - aggregations

4. **Construct Query Pattern**

   Build graph patterns representing entity relationships.

5. **Generate Query Syntax**

   Convert the graph pattern into the appropriate query language.

---

# Supported Query Languages

### Cypher

Used in property graph databases.

Example:
```text
MATCH (p:Person)-[:PURCHASED]->(product:Product)
RETURN p, product
```

---

### SPARQL

Used in RDF knowledge graphs.

Example:
```text
SELECT ?person ?product
WHERE {
?person :purchased ?product .
}
```

---

# Output Formats

The skill may generate several outputs:

### Graph Query

Executable Cypher or SPARQL query.

### Query Explanation

Human-readable explanation of what the query does.

Example:

This query finds all people connected to Alice through the WORKS_AT relationship.


### Query Template

Parameterized queries.

Example:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company {name:$company})
RETURN p
```

---

# Implementation Notes

The translator may internally perform:

- entity recognition
- intent detection
- graph schema awareness
- query pattern generation

It may also integrate with schema metadata to produce more accurate queries.

---

# Best Practices

When generating graph queries:

- use schema labels consistently
- avoid overly broad relationship patterns
- prefer parameterized queries
- include limits for large datasets

Example:

MATCH (p:Person)
RETURN p
LIMIT 50

---

# Summary

This skill translates natural language questions into graph queries.

It enables developers to interact with graph databases using plain English while automatically generating Cypher or SPARQL syntax.