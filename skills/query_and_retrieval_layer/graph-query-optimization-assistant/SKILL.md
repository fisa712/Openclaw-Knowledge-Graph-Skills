---
name: graph-query-optimization-assistant
description: Analyze graph queries and suggest optimizations to improve performance, reduce execution time, and ensure efficient traversal in graph databases.
metadata:
  {"openclaw":{"emoji":"⚡","homepage":"https://clawhub.com"}}
---

# Query Optimization Assistant

Analyze graph queries and recommend performance optimizations.

This skill helps developers improve the performance of graph database queries by identifying inefficiencies and suggesting optimized query patterns.

It evaluates queries written in languages such as Cypher or SPARQL and provides recommendations that reduce query cost, improve traversal efficiency, and minimize unnecessary graph scans.

---

# When To Use This Skill

Use this skill when a user wants to:

- optimize graph queries
- improve query performance
- reduce query execution time
- analyze inefficient query patterns
- tune Cypher or SPARQL queries
- debug slow graph queries

Example requests:

- “Optimize this Cypher query.”
- “Why is this SPARQL query slow?”
- “Suggest improvements for this graph query.”
- “Help me tune this Neo4j query.”

---

# What This Skill Produces

The skill analyzes queries and produces:

- optimized query versions
- performance recommendations
- indexing suggestions
- traversal improvements
- query execution explanations

---

# Example Query Analysis

Input query:

```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
WHERE c.name = "Acme"
RETURN p
```

Potential issue:

The query may scan all Person nodes before filtering.

Optimized version:
```text
MATCH (c:Company {name:"Acme"})<-[:WORKS_AT]-(p:Person)
RETURN p
```

Why it is faster:

The query begins with a selective node lookup instead of scanning all Person nodes.


---

# Index Optimization Example

Original query:

MATCH (c:Company)
WHERE c.name = "Acme"
RETURN c

Recommended improvement:

Create an index on Company.name

Example index:
```text
CREATE INDEX company_name_index
FOR (c:Company)
ON (c.name)
```

This significantly reduces lookup time.

---

# Relationship Traversal Optimization

Inefficient traversal:
```text
MATCH (p:Person)-[*]->(c:Company)
RETURN p,c
```

Issue:

Unbounded relationship traversal may cause expensive graph exploration.

Optimized query:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN p,c
```

This restricts traversal to the relevant relationship type.

---

# SPARQL Optimization Example

Original SPARQL query:

```text
SELECT ?person
WHERE {
?person rdf:type :Person .
?person :worksAt :Acme .
}
```

Possible improvement:

Use selective patterns and avoid unnecessary triple patterns when possible.

Optimized query:
```text
SELECT ?person
WHERE {
?person :worksAt :Acme .
}
```

If schema guarantees workers are persons, the additional triple may be redundant.

---

# Optimization Strategy

When optimizing graph queries:

1. **Identify selective entry points**

Start queries from nodes with unique identifiers or indexed properties.

2. **Reduce graph scans**

Avoid scanning large node sets when specific labels or properties can be used.

3. **Limit traversal depth**

Avoid unlimited relationship traversal patterns.

4. **Use indexes**

Recommend indexes for frequently queried properties.

5. **Simplify patterns**

Remove unnecessary query clauses.

---

# Output Formats

The skill may return:

### Optimized Query

Improved query syntax.

### Optimization Suggestions

Bullet list of improvements.

Example:

- Start traversal from indexed node
- Limit traversal depth
- Add property index

### Performance Explanation

Explanation of why the optimized query is faster.

---

# Implementation Notes

The optimization assistant may internally perform:

- query pattern analysis
- traversal cost estimation
- index usage detection
- query plan reasoning

It may also compare queries against known optimization best practices used in graph database engines.

---

# Best Practices

When writing graph queries:

- start from selective nodes
- use indexed properties
- avoid unnecessary wildcard traversals
- limit result sets using `LIMIT`
- restrict traversal depth when possible

Example:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN p
LIMIT 50
```

---

# Summary

This skill improves the performance of graph database queries by analyzing query structure and suggesting optimized query patterns.

It helps developers write faster and more efficient Cypher and SPARQL queries for large graph datasets.