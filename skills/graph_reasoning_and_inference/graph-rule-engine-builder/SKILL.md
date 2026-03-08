---
name: graph-rule-engine-builder
description: Generate rule-based reasoning engines that infer new relationships and facts from existing graph data using declarative logic rules.
metadata:
  {"openclaw":{"emoji":"🧩","homepage":"https://clawhub.com"}}
---

# Rule Engine Builder

Create rule-based reasoning systems for graph databases and knowledge graphs.

This skill helps developers define rules that derive new knowledge from existing graph data.  
Rules allow the graph to infer relationships and properties that are not explicitly stored.

Rule-based reasoning is commonly used in:

- knowledge graphs
- semantic web systems
- fraud detection
- recommendation engines
- compliance and policy systems

The rule engine applies logical rules to graph data and generates new inferred facts.

---

# When To Use This Skill

Use this skill when a user wants to:

- define reasoning rules for a knowledge graph
- derive new relationships automatically
- create inference logic over graph data
- implement rule-based reasoning systems
- build semantic rule engines

Example requests:

- “Create rules to infer manager relationships.”
- “Generate reasoning rules for my knowledge graph.”
- “Build a rule engine for graph inference.”
- “Infer new relationships using logic rules.”

---

# What This Skill Produces

The rule engine builder generates:

- rule definitions
- inference rules
- derived relationship patterns
- rule execution logic
- inferred graph triples

Rules are typically expressed in a **logical IF–THEN format**.

---

# Basic Rule Example

Rule definition:
```text
IF
(a:Person)-[:WORKS_AT]->(c:Company)
AND
(b:Person)-[:WORKS_AT]->(c:Company)

THEN
(a)-[:COLLEAGUE_OF]->(b)
```

This rule infers colleague relationships between people working at the same company.

---

# Hierarchy Rule Example

Graph data:

Alice REPORTS_TO Bob

Bob REPORTS_TO Carol


Inference rule:
```text
IF
(a)-[:REPORTS_TO]->(b)
AND
(b)-[:REPORTS_TO]->(c)

THEN
(a)-[:REPORTS_TO]->(c)
```

This rule derives indirect reporting relationships.

---

# Fraud Detection Rule Example

Rule:
```text
IF
(a:Account)-[:TRANSFERRED]->(b:Account)
AND
(b)-[:TRANSFERRED]->(c:Account)
AND
(c)-[:TRANSFERRED]->(a)

THEN
flag FraudRing(a,b,c)
```

This rule identifies circular transfer patterns.

---

# Semantic Reasoning Rule

Example semantic rule:
```text
IF
(person)-[:BORN_IN]->(city)
AND
(city)-[:LOCATED_IN]->(country)

THEN
(person)-[:BORN_IN_COUNTRY]->(country)
```

This rule derives new geographic knowledge.

---

# Rule Definition Structure

Rules typically include:

1. **Conditions (IF)**

Patterns that must exist in the graph.

2. **Inference (THEN)**

New relationships or facts that should be added.

3. **Optional Constraints**

Filters such as property conditions.

---

# Rule Execution Workflow

Step 1 — Scan graph for rule patterns
```text
MATCH (a)-[:WORKS_AT]->(c)<-[:WORKS_AT]-(b)
```

Step 2 — Identify rule matches

Step 3 — Generate inferred relationship

```text
MERGE (a)-[:COLLEAGUE_OF]->(b)
```

---

# Output Formats

The skill may generate rules in several formats.

### Rule DSL

rule colleague_inference

IF person1 WORKS_AT company

AND person2 WORKS_AT company

THEN person1 COLLEAGUE_OF person2

---

### Cypher Rule Execution
```text
MATCH (a:Person)-[:WORKS_AT]->(c)<-[:WORKS_AT]-(b:Person)
MERGE (a)-[:COLLEAGUE_OF]->(b)
```

---

### RDF Rule Representation
```text
?person1 :worksAt ?company .
?person2 :worksAt ?company .
⇒
?person1 :colleagueOf ?person2 .
```

---

# Implementation Notes

The rule engine builder may internally support:

- logical rule parsing
- graph pattern matching
- rule execution scheduling
- inference materialization

Rules may run:

- periodically
- on data updates
- during graph ingestion

---

# Best Practices

When designing graph reasoning rules:

- avoid circular rules that create infinite inference loops
- ensure rules produce deterministic outcomes
- use clear relationship names
- validate inferred data before materializing it

---

# Summary

This skill enables rule-based reasoning for knowledge graphs by generating inference rules that derive new facts and relationships from existing graph data.

It allows graph systems to produce knowledge beyond what is explicitly stored.