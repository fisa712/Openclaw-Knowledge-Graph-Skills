---

name: graph_schema_validation
title: Graph Schema Validation
description: Validate knowledge graph schemas and data against defined ontology, RDF/OWL, or property graph schema constraints.
category: graph-modeling
tags:

* knowledge-graph
* schema-validation
* rdf
* owl
* property-graph
* neo4j
* data-validation
* shacl
* developer-tools
  version: 0.1.0
  author: community
  license: MIT

---

# Graph Schema Validation

## Purpose

This skill helps developers **validate knowledge graph schemas and graph data against defined constraints**.

It ensures that a graph structure conforms to:

* Ontology definitions
* RDF / OWL schema rules
* Property graph modeling constraints
* Relationship consistency
* Node property requirements

The skill is designed to **detect modeling errors early in graph development**.

---

# When To Use This Skill

Use this skill when:

* Validating graph data before ingestion
* Testing knowledge graph schema correctness
* Enforcing ontology constraints
* Checking graph consistency
* Verifying RDF or OWL compliance
* Validating Neo4j property graph models

Example prompts:

* "Validate this RDF graph against the ontology."
* "Check if this Neo4j graph violates schema constraints."
* "Verify node properties and relationships."
* "Validate graph data using SHACL."

---

# Inputs

The skill can accept:

* RDF datasets
* OWL ontologies
* Property graph schemas
* Cypher graph structures
* Graph data files
* Graph database exports
* JSON-LD or Turtle datasets

Example RDF input:

```
:Alice rdf:type :Student
:Alice :enrolledIn :CS101
:CS101 rdf:type :Course
```

Example property graph structure:

```
(Student {student_id:"S001"})-[:ENROLLED_IN]->(Course {course_id:"CS101"})
```

---

# Validation Checks

The skill performs multiple types of validation.

## 1. Schema Conformance

Checks whether graph entities conform to defined schema types.

Examples:

* Node labels must match schema classes
* Relationships must match allowed relationships
* Property types must be valid

---

## 2. Property Validation

Checks for:

* missing required properties
* invalid data types
* inconsistent property names

Example:

```
Student must have:
- student_id
- name
```

Invalid example:

```
(Student {name:"Alice"})   # missing student_id
```

---

## 3. Relationship Validation

Ensures relationships follow schema rules.

Example rule:

```
(Student)-[:ENROLLED_IN]->(Course)
```

Invalid example:

```
(Course)-[:ENROLLED_IN]->(Student)
```

---

## 4. Cardinality Constraints

Checks for rules such as:

```
Student must enroll in at least 1 Course
Professor may teach multiple Courses
```

---

## 5. Graph Integrity Checks

Detects issues such as:

* orphan nodes
* broken references
* duplicate identifiers
* inconsistent relationships

---

# RDF / OWL Validation Using SHACL

For semantic graphs, the skill can generate or validate **SHACL shapes**.

Example SHACL constraint:

```
:StudentShape
  a sh:NodeShape ;
  sh:targetClass :Student ;
  sh:property [
      sh:path :student_id ;
      sh:datatype xsd:string ;
      sh:minCount 1 ;
  ] .
```

---

# Developer Implementation Notes

When implementing validation logic programmatically, prefer **Python libraries designed for graph validation and semantic constraints**.

Recommended libraries:

### RDF / OWL Validation

* rdflib
* pyshacl
* owlready2

### Property Graph Validation

* neo4j
* py2neo
* networkx

### Data Validation

* pydantic
* jsonschema

### Graph Analysis

* networkx

---

# Example RDF Validation with PySHACL

```python
from pyshacl import validate
from rdflib import Graph

data_graph = Graph().parse("data.ttl", format="turtle")
shapes_graph = Graph().parse("shapes.ttl", format="turtle")

conforms, results_graph, results_text = validate(
    data_graph,
    shacl_graph=shapes_graph,
)

print(conforms)
print(results_text)
```

---

# Example Property Graph Validation (NetworkX)

```python
import networkx as nx

G = nx.MultiDiGraph()

G.add_node("S001", label="Student", name="Alice")
G.add_node("CS101", label="Course")

G.add_edge("S001", "CS101", relation="ENROLLED_IN")

for node, data in G.nodes(data=True):
    if data.get("label") == "Student":
        if "student_id" not in data:
            print("Invalid Student node:", node)
```

---

# Example Neo4j Constraint Validation

Example Cypher constraint checks:

```
CREATE CONSTRAINT student_id_unique IF NOT EXISTS
FOR (s:Student)
REQUIRE s.student_id IS UNIQUE;
```

Check for missing properties:

```
MATCH (s:Student)
WHERE s.student_id IS NULL
RETURN s
```

---

# Skill Behavior

When executing this skill:

1. Identify schema definitions
2. Identify graph structure
3. Compare graph data against schema
4. detect violations
5. produce validation report
6. suggest corrections

The skill should return:

* validation status
* detected violations
* suggested fixes

---

# Output Format

The validation report should include:

```
Validation Summary
------------------

Nodes Checked: 240
Relationships Checked: 512

Violations:

1. Missing Property
Node: Student(S004)
Missing: student_id

2. Invalid Relationship
(Course)-[:ENROLLED_IN]->(Student)

3. Duplicate Identifier
student_id = S002
```

---

# Best Practices

Developers should:

* validate graphs before production deployment
* enforce constraints at the database level
* maintain consistent property naming
* define validation rules early in schema design

---

# Limitations

Automated validation cannot fully detect:

* domain semantic errors
* poorly modeled relationships
* incorrect business rules

Developers should review validation results carefully.

---

# Future Extensions

Potential improvements:

* automated SHACL generation
* graph schema diff validation
* ontology consistency reasoning
* Neo4j schema audit tools
* graph integrity dashboards

---
