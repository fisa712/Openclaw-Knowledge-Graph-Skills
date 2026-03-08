---

name: causal_chain_analyzer
description: Analyze and trace cause-effect chains in a knowledge graph to identify root causes and downstream impacts.
category: reasoning
tags:

* knowledge-graph
* reasoning
* causal-analysis
* graph-analysis
* dependency-tracing
  version: 1.0.0
  author: kg-dev-skills

---

# Causal Chain Analyzer

## Purpose

This skill identifies and analyzes **cause-and-effect chains** within a knowledge graph.

It helps determine:

* What **caused** a particular event or outcome
* What **consequences** result from a given cause
* How effects propagate across multiple nodes

This is useful for understanding **complex system behaviors, failures, dependencies, and event propagation**.

---

## When To Use This Skill

Use this skill when:

* A user wants to **identify the root cause** of an event
* Analyzing **impact propagation** in a system
* Tracing **decision or event chains**
* Investigating **failures or cascading dependencies**
* Understanding **how one event led to another**

Example triggers:

* "What caused this event?"
* "Trace the cause of this failure"
* "Show the causal chain leading to X"
* "What are the downstream effects of Y?"
* "Explain how A led to B"

---

## Supported Relation Types

This skill operates on relations representing **causal or dependency relationships**, such as:

* `causes`
* `leads_to`
* `results_in`
* `triggers`
* `depends_on`
* `influences`
* `contributes_to`

These relationships should represent **directional influence** from cause → effect.

---

## Inputs

Expected inputs include:

* A target node (event or entity)
* Relation types representing causality
* Optional traversal depth

Example input:

```json
{
  "target": "System_Outage",
  "relation": "causes"
}
```

---

## Output

The skill returns a **causal chain or graph of influence** showing upstream causes and/or downstream effects.

Example output:

```json
{
  "causal_chain": [
    ["Database_Overload", "API_Failure"],
    ["API_Failure", "Authentication_Service_Down"],
    ["Authentication_Service_Down", "System_Outage"]
  ]
}
```

Optionally, results may include:

* chain depth
* root cause nodes
* terminal effects

---

## Procedure

1. Identify the **target node**.
2. Select the **causal relationship type**.
3. Traverse the graph following the relation direction.
4. Collect nodes that form **cause → effect chains**.
5. Identify:

   * root causes (nodes with no incoming causal edges)
   * downstream consequences
6. Return ordered causal paths.

Traversal methods may include:

* Depth First Search (DFS)
* Breadth First Search (BFS)
* path-based traversal with cycle detection

---

## Example

Graph:

```
Power_Surge → Server_Shutdown
Server_Shutdown → API_Failure
API_Failure → User_Login_Error
```

Query:

```
What caused User_Login_Error?
```

Output causal chain:

```
Power_Surge → Server_Shutdown → API_Failure → User_Login_Error
```

---

## Developer Notes

Key considerations:

* Detect and prevent infinite loops in cyclic graphs
* Allow configurable traversal depth
* Support both **forward analysis (effects)** and **backward analysis (causes)**
* Rank causes based on proximity or edge weights when available

Optional enhancements:

* probabilistic causality scoring
* temporal filtering
* confidence weighting

---

## Expected Benefits

Using this skill enables:

* root cause analysis
* impact tracing
* better debugging of system graphs
* improved explainability of graph-based reasoning

---

## Related Skills

* Transitive Closure Generator
* Path Reasoning Analyzer
* Dependency Graph Builder
* Graph Impact Analyzer
