---

name: ontology_based_inference_helper
description: Infer new knowledge in a graph using ontology rules such as subclass, domain, range, and property inheritance.
category: reasoning
tags:

* knowledge-graph
* reasoning
* ontology
* inference
* semantic-web
* rdf
* owl
  version: 1.0.0
  author: kg-dev-skills

---

# Ontology-Based Inference Helper

## Purpose

This skill derives **implicit knowledge** from a knowledge graph by applying **ontology rules and semantic constraints**.

Ontologies define structured knowledge about:

* classes
* subclasses
* properties
* domains
* ranges
* logical relationships

Using these definitions, the system can infer **new facts that are not explicitly stored in the graph**.

---

## When To Use This Skill

Use this skill when:

* A knowledge graph includes **ontology definitions**
* The user wants to **infer class memberships**
* Relationships should propagate across **class hierarchies**
* Semantic rules should generate **new triples**
* Graph consistency needs to be validated

Example triggers:

* "Infer missing relationships from ontology"
* "Apply ontology reasoning"
* "Expand subclass relationships"
* "Check class inheritance"
* "Generate implied triples"

---

## Supported Ontology Rules

This skill can apply several common ontology inference rules.

### Subclass Inference

If:

```
A subclass_of B
X instance_of A
```

Then infer:

```
X instance_of B
```

---

### Property Domain Inference

If:

```
property P has domain D
X P Y
```

Then infer:

```
X instance_of D
```

---

### Property Range Inference

If:

```
property P has range R
X P Y
```

Then infer:

```
Y instance_of R
```

---

### Property Inheritance

If:

```
P subproperty_of Q
X P Y
```

Then infer:

```
X Q Y
```

---

### Symmetric or Inverse Properties

Example:

```
married_to inverse_of married_to
A married_to B
```

Infer:

```
B married_to A
```

---

## Inputs

Expected inputs include:

* ontology schema
* graph triples
* inference rule types

Example input:

```json
{
  "triples": [
    ["Dog", "subclass_of", "Animal"],
    ["Buddy", "instance_of", "Dog"]
  ]
}
```

---

## Output

The skill returns **new inferred triples** derived from ontology rules.

Example output:

```json
[
  ["Buddy", "instance_of", "Animal"]
]
```

Each inferred statement may include metadata:

```
inferred: true
source: ontology_inference
rule: subclass_propagation
```

---

## Procedure

1. Load ontology definitions.
2. Identify supported inference rules.
3. Scan graph triples for rule triggers.
4. Apply ontology reasoning rules.
5. Generate new inferred triples.
6. Avoid duplicates or contradictions.
7. Mark inferred knowledge appropriately.

---

## Example

Graph input:

```
Car subclass_of Vehicle
Vehicle subclass_of Transport
Tesla_Model3 instance_of Car
```

Inferred knowledge:

```
Tesla_Model3 instance_of Vehicle
Tesla_Model3 instance_of Transport
```

---

## Developer Notes

This skill is compatible with **semantic web standards** such as:

* RDF
* RDFS
* OWL Lite reasoning
* Property graph ontologies

Possible reasoning approaches:

* forward chaining
* rule-based reasoning
* semantic rule engines

Large graphs may require:

* incremental inference
* rule caching
* batch reasoning strategies

---

## Expected Benefits

Using ontology-based inference enables:

* automatic expansion of knowledge graphs
* richer semantic relationships
* improved query results
* stronger graph reasoning capabilities

---

## Related Skills

* Transitive Closure Generator
* Causal Chain Analyzer
* Rule-Based Inference Engine
* Path Reasoning Analyzer
