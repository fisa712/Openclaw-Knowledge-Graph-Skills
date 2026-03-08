---
name: graph-query-debugging-tool
description: Diagnose errors in Cypher or SPARQL queries and suggest fixes for syntax issues, schema mismatches, and incorrect graph traversal patterns.
metadata:
  {"openclaw":{"emoji":"🛠️","homepage":"https://clawhub.com"}}
---

# Query Debugging Tool

Analyze graph queries, identify errors, and suggest fixes.

This skill helps developers debug graph database queries by detecting syntax errors, schema mismatches, incorrect relationship patterns, and logical mistakes.

It explains why a query fails or returns incorrect results and provides corrected query versions.

---

# When To Use This Skill

Use this skill when a user wants to:

- debug Cypher queries
- debug SPARQL queries
- understand query errors
- fix incorrect graph traversal patterns
- diagnose why a query returns no results
- correct query syntax

Example requests:

- “Why is this Cypher query failing?”
- “Fix this SPARQL query.”
- “Debug this graph query.”
- “Explain what is wrong with this query.”

---

# What This Skill Produces

The debugging tool provides:

- error diagnosis
- corrected query versions
- explanations of the issue
- debugging steps
- schema mismatch detection

---

# Syntax Error Example

Broken Cypher query:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company
RETURN p
```

Issue:

Missing closing parenthesis.

Fixed query:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN p
```

---

# Schema Mismatch Example

Query:
```text
MATCH (p:Employee)-[:WORKS_AT]->(c:Company)
RETURN p
```

Problem:

The label Employee may not exist in the graph schema.

Possible correction:
```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN p
```

---

# Relationship Error Example

Broken query:
```text
MATCH (p:Person)-[:WORK_AT]->(c:Company)
RETURN p
```

Issue:

Relationship type WORK_AT may be incorrect.

Correct query:

```text
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN p
```

---

# Query Returning No Results

Example query:
```text
MATCH (p:Person {name:"Alice"})-[:WORKS_AT]->(c:Company {name:"Google"})
RETURN p
```

Possible issues:

- Alice does not work at Google.
- Company name may differ in the dataset.
- Relationship type may be different.

Suggested debugging approach:
```text
MATCH (p:Person {name:"Alice"})-[r]->(c)
RETURN r,c
```

This reveals the actual relationships connected to Alice.

---

# SPARQL Debugging Example

Broken SPARQL query:
```text
SELECT ?person
WHERE {
?person rdf:type :Person
?person :worksAt :Acme .
}
```

Issue:

Missing period between triple statements.

Fixed query:
```text
SELECT ?person
WHERE {
?person rdf:type :Person .
?person :worksAt :Acme .
}
```

---

# Debugging Strategy

When analyzing a query:

1. **Check Syntax**

Ensure parentheses, brackets, and clauses are valid.

2. **Validate Schema Elements**

Confirm that node labels, properties, and relationships exist.

3. **Verify Relationship Patterns**

Ensure traversal directions and types are correct.

4. **Check Query Logic**

Determine whether the query structure matches the intended request.

5. **Test Intermediate Steps**

Break complex queries into smaller parts to locate the issue.

---

# Output Formats

The skill may provide:

### Error Explanation

Human-readable explanation of the issue.

### Corrected Query

A fixed version of the query.

### Debugging Suggestions

Step-by-step instructions to isolate the problem.

---

# Example Debugging Workflow

Original query:
```text
MATCH (p:Person)-[:PURCHASED]->(product)
WHERE product.price > 100
RETURN p
```

Potential issue:

The property 'price' may not exist on the Product node.

Suggested debugging query:

```text
MATCH (product:Product)
RETURN product
LIMIT 10
```

This allows inspection of actual node properties.

---

# Implementation Notes

The debugging tool may internally perform:

- syntax validation
- schema awareness checks
- relationship validation
- logical query analysis
- step-by-step query breakdown

---

# Best Practices

When debugging graph queries:

- test query components separately
- inspect node labels and properties
- verify relationship types
- limit result sets while debugging
- simplify queries before expanding them

---

# Summary

This skill helps developers diagnose and fix issues in graph queries.

It detects syntax errors, schema mismatches, and logical mistakes, while providing corrected query versions and debugging guidance.