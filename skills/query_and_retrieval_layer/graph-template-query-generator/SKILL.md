---
name: graph-template-query-generator
description: Generate reusable Cypher or SPARQL query templates for common graph database operations such as finding nodes, relationships, paths, and aggregations.
metadata:
  {"openclaw":{"emoji":"📄","homepage":"https://clawhub.com"}}
---

# Template Query Generator

Generate reusable graph query templates for common graph database operations.

This skill produces parameterized query templates that developers can quickly adapt to query graph databases without writing queries from scratch.

It supports template generation for common tasks such as:

- node lookup
- relationship traversal
- path discovery
- aggregations
- filtering
- graph exploration

Templates can be generated for graph query languages such as Cypher and SPARQL.

---

# When To Use This Skill

Use this skill when a user wants to:

- generate common graph queries
- create reusable query templates
- quickly scaffold Cypher or SPARQL queries
- explore graph data structures
- build starter queries for applications

Example requests:

- “Generate a query template for finding relationships.”
- “Create a Cypher template to search nodes by property.”
- “Generate a SPARQL query template for retrieving entities.”
- “Create a reusable graph query.”

---

# What This Skill Produces

The skill generates parameterized templates for:

- node queries
- relationship queries
- path queries
- aggregation queries
- filtering queries

Templates typically include **query parameters** to allow easy reuse.

---

# Node Lookup Template

Cypher template:

```text
MATCH (n:Label {property:$value})
RETURN n
```

Example usage:
```text
MATCH (p:Person {name:$name})
RETURN p
```

---

SPARQL equivalent:
```text
SELECT ?entity
WHERE {
?entity :property ?value .
}
```

---

# Relationship Query Template

Cypher template:
```text
MATCH (a:LabelA)-[:RELATIONSHIP]->(b:LabelB)
RETURN a,b
```

Example:

```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN p,c
```

---

# Path Discovery Template

Cypher template:
```text
MATCH path = (a)-[*1..$depth]-(b)
RETURN path
LIMIT $limit
```

This template is useful for exploring graph connections.

---

SPARQL path query:
```text
SELECT ?a ?b
WHERE {
?a :relationship+ ?b .
}
```

---

# Aggregation Query Template

Cypher example:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN c.name, COUNT(p) AS employee_count
ORDER BY employee_count DESC
```

---

SPARQL equivalent:
```text
SELECT ?company (COUNT(?person) AS ?count)
WHERE {
?person :worksAt ?company .
}
GROUP BY ?company
```

---

# Parameterized Query Template

Example:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company {name:$company})
RETURN p
LIMIT $limit
```

Parameters:

company = "Acme"

limit = 50


This allows developers to reuse the query in applications.

---

# Template Generation Strategy

When generating query templates:

1. Identify the query goal
   - node lookup
   - relationship discovery
   - path exploration
   - aggregation

2. Select the appropriate graph pattern.

3. Insert parameter placeholders.

4. Generate the query syntax for the target language.

---

# Output Formats

The skill may return:

### Query Template

Reusable Cypher or SPARQL query.

### Parameter List

Variables required to execute the query.

### Query Explanation

Description of what the template does.

---

# Example Developer Workflow

Developer request:

Generate a template to find employees in a company.

Generated template:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company {name:$company})
RETURN p
```

---

# Implementation Notes

The template generator may internally use:

- graph schema awareness
- query pattern libraries
- parameterization logic
- reusable query blueprints

It may also integrate with query generation tools to automatically adapt templates to specific graph schemas.

---

# Best Practices

When designing query templates:

- use clear parameter names
- include result limits
- avoid unbounded traversal
- design templates that work across datasets

---

# Summary

This skill generates reusable graph query templates for common database operations.

It helps developers quickly scaffold Cypher or SPARQL queries, improving productivity and reducing query-writing effort.