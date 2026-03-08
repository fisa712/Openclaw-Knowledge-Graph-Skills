---
name: graph-path-reasoning-analyzer
description: Analyze paths between entities in a graph to explain relationships, discover indirect connections, and provide reasoning over graph traversal patterns.
metadata:
  {"openclaw":{"emoji":"🧭","homepage":"https://clawhub.com"}}
---

# Path Reasoning Analyzer

Analyze graph traversal paths to understand how entities are connected.

This skill examines graph paths between nodes and explains the sequence of relationships that link them.  
It helps developers and analysts understand *why* two entities are related by exploring intermediate nodes and relationships.

Path reasoning is useful for:

- explainable knowledge graphs
- relationship discovery
- graph analytics
- fraud investigation
- recommendation systems

The analyzer reveals the logical connection chain between entities.

---

# When To Use This Skill

Use this skill when a user wants to:

- explain why two entities are connected
- analyze graph traversal paths
- identify intermediate relationships between nodes
- discover reasoning chains in knowledge graphs
- inspect multi-step connections

Example requests:

- “Explain how Alice is connected to CompanyX.”
- “Show the path between two entities.”
- “Find the relationship chain linking two nodes.”
- “Analyze how two accounts are connected.”

---

# What This Skill Produces

The analyzer generates:

- relationship paths between entities
- reasoning chains
- intermediate nodes
- path explanations
- graph traversal queries

Outputs typically include both **query results and explanations**.

---

# Example Path Reasoning

Graph relationships:

```text
Alice WORKS_AT Acme
Acme PARTNER_OF BetaCorp
BetaCorp LOCATED_IN California
```

Reasoning chain:
```text
Alice → WORKS_AT → Acme
Acme → PARTNER_OF → BetaCorp
BetaCorp → LOCATED_IN → California
```

Explanation:

Alice is indirectly connected to California through her company’s business partner.


---

# Path Discovery Query

Cypher example:
```text
MATCH path = (a:Person {name:"Alice"})-[*1..4]-(target)
RETURN path
LIMIT 10
```

This query retrieves possible reasoning paths from Alice to other nodes.

---

# Targeted Path Reasoning

Finding the path between two specific nodes:

```text
MATCH path = shortestPath(
(a:Person {name:"Alice"})-[*]-(b:Company {name:"BetaCorp"})
)
RETURN path
```

This reveals the shortest reasoning path between the entities.

---

# SPARQL Property Path Example

Equivalent SPARQL query:
```text
SELECT ?intermediate
WHERE {
:Alice (:worksAt|:partnerOf|:locatedIn)+ ?intermediate .
}
```

The `+` operator explores multi-step relationships.

---

# Fraud Investigation Example

Graph:
```text
AccountA TRANSFERRED_TO AccountB
AccountB TRANSFERRED_TO AccountC
AccountC OWNS CompanyX
```

Reasoning result:
```text
AccountA → AccountB → AccountC → CompanyX
```

Explanation:
```text
AccountA is indirectly connected to CompanyX through a chain of transfers.
```

This helps detect suspicious transaction networks.

---

# Path Reasoning Strategy

When analyzing paths:

1. **Identify source node**

Determine the starting entity.

2. **Identify target node**

Define the entity being investigated.

3. **Explore relationship paths**

Traverse graph relationships.

4. **Limit traversal depth**

Prevent overly complex path searches.

5. **Explain reasoning chain**

Describe the relationships linking the nodes.

---

# Output Formats

The analyzer may generate:

### Graph Path

List of nodes and relationships forming the path.

### Path Explanation

Human-readable explanation of the reasoning chain.

### Path Query

Executable Cypher or SPARQL query used to discover the path.

---

# Implementation Notes

The path reasoning analyzer may internally use:

- graph traversal algorithms
- shortest-path search
- relationship filtering
- path ranking

It can integrate with other reasoning tools such as:

- multi-hop query builders
- rule engines
- anomaly detection systems

---

# Best Practices

When analyzing graph paths:

- limit traversal depth to avoid expensive queries
- filter relationship types for relevant reasoning
- prioritize shortest paths when possible
- return explanations alongside path results

Example:
```text
MATCH path = shortestPath((a)-[*..5]-(b))
RETURN path
```

---

# Summary

This skill analyzes graph traversal paths to explain how entities are connected through sequences of relationships.

It enables explainable reasoning in graph systems by revealing the relationship chains linking nodes.