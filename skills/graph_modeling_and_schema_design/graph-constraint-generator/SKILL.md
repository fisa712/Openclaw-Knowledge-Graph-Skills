---

name: graph_constraint_generator
title: Knowledge Graph Constraint Generator
description: Generate structural, semantic, and property constraints for knowledge graph schemas including RDF/OWL ontologies and property graph models.
category: graph-modeling
tags:

* knowledge-graph
* schema-constraints
* rdf
* owl
* neo4j
* shacl
* data-integrity
* graph-modeling
* developer-tools
  version: 0.1.0
  author: community
  license: MIT

---

# Knowledge Graph Constraint Generator

## Purpose

This skill assists developers in **automatically generating constraints for knowledge graph schemas** to enforce data integrity and consistent graph structure.

It produces constraint definitions suitable for:

* RDF / OWL semantic graphs
* SHACL validation rules
* Neo4j property graph constraints
* Graph schema enforcement policies

The goal is to ensure that **graph data remains consistent, valid, and aligned with the intended schema design**.

---

# When To Use This Skill

Use this skill when:

* Designing constraints for a new graph schema
* Enforcing graph integrity rules
* Generating validation rules for RDF graphs
* Creating Neo4j database constraints
* Defining property requirements
* Designing graph data governance policies

Example prompts:

* "Generate constraints for this knowledge graph schema."
* "Create Neo4j constraints for these node types."
* "Produce SHACL rules for this RDF ontology."
* "Define property requirements for graph entities."

---

# Inputs

The skill may receive:

* Graph schema definitions
* Ontology structures
* Property graph models
* RDF/OWL ontology files
* Node and relationship definitions
* Entity property lists
* Data integrity requirements

Example schema input:

```
Entities:
Student
Course
Professor

Relationships:
(Student)-[:ENROLLED_IN]->(Course)
(Professor)-[:TEACHES]->(Course)

Properties:
Student:
  student_id
  name
Course:
  course_id
  title
```

---

# Types of Constraints Generated

The skill generates multiple categories of constraints.

---

## 1. Unique Constraints

Ensure that certain properties uniquely identify nodes.

Example:

```
Student.student_id must be unique
Course.course_id must be unique
```

Example Neo4j constraint:

```
CREATE CONSTRAINT student_id_unique
FOR (s:Student)
REQUIRE s.student_id IS UNIQUE;
```

---

## 2. Required Property Constraints

Define mandatory properties.

Example:

```
Student must contain:
- student_id
- name
```

Invalid example:

```
(Student {name:"Alice"})
```

---

## 3. Relationship Constraints

Define allowed graph connections.

Example rule:

```
(Student)-[:ENROLLED_IN]->(Course)
```

Invalid structure:

```
(Course)-[:ENROLLED_IN]->(Student)
```

---

## 4. Cardinality Constraints

Define how many relationships are allowed.

Examples:

```
Student must enroll in at least one Course
Professor may teach multiple Courses
Course must be taught by at least one Professor
```

---

## 5. Domain and Range Constraints (RDF/OWL)

Define semantic constraints for relationships.

Example:

```
writes
  domain: Researcher
  range: Paper
```

Example RDF:

```
:writes rdfs:domain :Researcher
:writes rdfs:range :Paper
```

---

## 6. Data Type Constraints

Ensure property values match expected data types.

Example:

```
student_id → string
credits → integer
publicationYear → integer
```

---

# SHACL Constraint Generation Example

Example generated SHACL rule:

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

When generating constraints programmatically, prefer **Python libraries commonly used for graph modeling and validation**.

Recommended libraries:

### RDF / OWL Constraint Tools

* rdflib
* pyshacl
* owlready2

### Property Graph Tools

* neo4j
* py2neo
* networkx

### Data Validation

* pydantic
* jsonschema

---

# Example Python Constraint Generator

Example constraint generation for a property graph schema.

```python
schema = {
    "Student": ["student_id", "name"],
    "Course": ["course_id", "title"]
}

constraints = []

for node, props in schema.items():
    unique_property = props[0]

    cypher = f"""
CREATE CONSTRAINT {node.lower()}_{unique_property}_unique
FOR (n:{node})
REQUIRE n.{unique_property} IS UNIQUE
"""

    constraints.append(cypher)

for c in constraints:
    print(c)
```

---

# Example SHACL Shape Generator

```python
from rdflib import Graph, Namespace

EX = Namespace("http://example.org/")

g = Graph()

shape = """
:StudentShape
  a sh:NodeShape ;
  sh:targetClass :Student ;
  sh:property [
      sh:path :student_id ;
      sh:minCount 1 ;
  ] .
"""

print(shape)
```

---

# Skill Behavior

When executing this skill:

1. Analyze schema entities
2. Identify key properties
3. Generate unique constraints
4. Generate required property constraints
5. Generate relationship constraints
6. Suggest cardinality rules
7. Produce constraint definitions

The skill should output:

* constraint list
* database constraint scripts
* semantic validation rules

---

# Output Format

Example constraint report:

```
Generated Constraints
---------------------

Unique Constraints
Student.student_id
Course.course_id

Required Properties
Student.name
Course.title

Relationship Constraints
(Student)-[:ENROLLED_IN]->(Course)

Cardinality Constraints
Student → ENROLLED_IN → Course (min:1)
```

---

# Best Practices

When designing graph constraints:

* define unique identifiers early
* avoid overly restrictive constraints
* maintain clear domain/range rules
* validate graph data frequently
* combine database and semantic constraints

---

# Limitations

Constraint generation is based on **schema interpretation** and may require developer refinement.

Some domain rules may not be inferable automatically.

---

# Future Extensions

Potential improvements:

* automated constraint discovery from datasets
* constraint conflict detection
* graph rule engine generation
* dynamic schema enforcement tools
* constraint visualization

---
