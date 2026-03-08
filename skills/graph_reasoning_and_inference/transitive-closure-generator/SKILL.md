---
name: transitive_closure_generator
description: Generate inferred relationships using transitive closure over graph relations.
category: reasoning
tags:
  - knowledge-graph
  - reasoning
  - inference
  - graph-analysis
  - transitive-closure
version: 1.0.0
author: kg-dev-skills
---

# Transitive Closure Generator

## Purpose

This skill derives **implicit relationships** in a knowledge graph by applying **transitive closure** over relations that are logically transitive.

Transitive closure allows the system to infer relationships such as:

- If **A → B** and **B → C**, then infer **A → C**
- If **A depends on B** and **B depends on C**, then **A depends on C**
- If **A is ancestor of B** and **B is ancestor of C**, then **A is ancestor of C**

This helps expand the graph with **logically implied connections**.

---

## When To Use This Skill

Use this skill when:

- A graph contains **transitive relationships**
- The user wants to **infer indirect connections**
- Multi-hop relationships need to be **collapsed into direct edges**
- Dependency chains need to be expanded
- Hierarchies need to be computed

Example triggers:

- "Find indirect dependencies"
- "Generate ancestor relationships"
- "Infer hierarchical connections"
- "Compute reachability"
- "Expand all transitive relations"

---

## Supported Relation Types

Typical transitive relations include:

- `ancestor_of`
- `parent_of`
- `depends_on`
- `subclass_of`
- `part_of`
- `located_in`
- `prerequisite_of`

Do **not apply transitive closure** to relations that are not logically transitive (e.g., `friend_of`, `married_to`).

---

## Inputs

The skill expects:

- A graph dataset
- A relation type that is transitive
- Optional depth limits

Example input structure:

```json
{
  "relation": "depends_on",
  "edges": [
    ["ServiceA", "ServiceB"],
    ["ServiceB", "DatabaseC"],
    ["DatabaseC", "StorageD"]
  ]
}
```
## Output
The skill produces inferred edges created via transitive reasoning.

Example output:
```json
[
  ["ServiceA", "DatabaseC"],
  ["ServiceA", "StorageD"],
  ["ServiceB", "StorageD"]
]
```
These inferred edges may optionally be labeled as:
```text
inferred: true
source: transitive_closure
```
### Procedure

1. Identify the relation type to analyze.
2. Verify the relation is transitive.
3. Build a graph traversal structure.

4. For each node:

    - traverse reachable nodes via the relation

5. Record inferred edges for all reachable paths.
6. Avoid duplicating existing edges.
7. Mark newly inferred relationships as derived knowledge.
---
### Example

Input graph:
```text
A → B
B → C
C → D
```
Computed closure:
```text
A → C
A → D
B → D
```
---
### Developer Notes

Recommended algorithms:

* Depth First Search (DFS)
* Breadth First Search (BFS)
* Floyd–Warshall (for dense graphs)
* Warshall's algorithm for transitive closure

For large graphs, ensure:

* cycle detection
* memoization
* duplicate edge avoidance

### Expected Benefits

Using this skill allows:

* automatic inference of hidden relationships
* improved reasoning over graph structures
* stronger graph completeness for queries
* better downstream analytics and path reasoning