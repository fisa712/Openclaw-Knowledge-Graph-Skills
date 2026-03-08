---

name: property_graph_schema_designer
title: Property Graph Schema Designer (Neo4j Style)
description: Design property graph schemas for knowledge graph systems using Neo4j-style node labels, relationships, and properties based on domain descriptions or developer requirements.
category: graph-modeling
tags:

* knowledge-graph
* property-graph
* neo4j
* graph-schema
* graph-modeling
* cypher
* developer-tools
  version: 0.1.0
  author: community
  license: MIT

---

# Property Graph Schema Designer (Neo4j Style)

## Purpose

This skill assists developers in **designing property graph schemas** used in systems such as Neo4j and other property graph databases.

It translates domain descriptions or system requirements into a structured schema containing:

* Node labels
* Relationship types
* Node properties
* Relationship properties
* Graph constraints
* Index recommendations

The result is a **developer-friendly graph schema blueprint** that can be implemented in Neo4j or similar databases.

---

# When To Use This Skill

Use this skill when:

* Designing a **property graph data model**
* Creating schemas for **Neo4j-based knowledge graphs**
* Converting **domain documentation into graph structures**
* Modeling **entities and relationships for graph databases**
* Bootstrapping **graph database projects**

Example prompts:

* "Design a Neo4j schema for a university system."
* "Create a property graph model for an e-commerce platform."
* "Generate a graph schema for a social network."
* "Model relationships for a supply chain graph."

---

# Inputs

The skill accepts inputs such as:

* Domain descriptions
* System architecture documentation
* Entity relationship diagrams
* Relational schemas
* JSON or API schemas
* Business rules
* Graph use cases

Example input:

```
A university system contains students, professors, courses, and departments.

Students enroll in courses.
Professors teach courses.
Departments manage professors and courses.
```

---

# Expected Output

The skill produces a **property graph schema specification**.

## Node Labels

```
Student
Professor
Course
Department
```

## Relationships

```
(Student)-[:ENROLLED_IN]->(Course)

(Professor)-[:TEACHES]->(Course)

(Department)-[:MANAGES]->(Course)

(Department)-[:EMPLOYS]->(Professor)
```

## Node Properties

Student:

* student_id
* name
* email
* enrollment_year

Course:

* course_id
* title
* credits

Professor:

* professor_id
* name
* research_area

Department:

* department_id
* name



## Relationship Properties (optional)

```

ENROLLED_IN

* semester
* grade

TEACHES

* semester

```

---

# Example Cypher Schema Draft

Example Cypher statements for implementing the schema:

```

CREATE CONSTRAINT student_id IF NOT EXISTS
FOR (s:Student)
REQUIRE s.student_id IS UNIQUE;

CREATE CONSTRAINT course_id IF NOT EXISTS
FOR (c:Course)
REQUIRE c.course_id IS UNIQUE;

CREATE INDEX professor_name IF NOT EXISTS
FOR (p:Professor)
ON (p.name);

```

Example relationship creation:

```

MATCH (s:Student {student_id: "S001"})
MATCH (c:Course {course_id: "CS101"})
CREATE (s)-[:ENROLLED_IN {semester:"Fall"}]->(c);

```

---

# Developer Implementation Notes

When implementing schema generation or graph manipulation programmatically, prefer **Python libraries commonly used with property graph databases**.

Recommended libraries:

### Graph Database Drivers

- neo4j
- py2neo

### Graph Modeling

- networkx

### Visualization

- pyvis
- graphviz

### Data Processing

- pandas

---

# Example Python Graph Model (NetworkX)

```

import networkx as nx

G = nx.MultiDiGraph()

G.add_node("Student", type="label")
G.add_node("Course", type="label")

G.add_edge("Student", "Course", relationship="ENROLLED_IN")

print(G.nodes())
print(G.edges(data=True))

```

---

# Example Neo4j Connection (Python)

```

from neo4j import GraphDatabase

driver = GraphDatabase.driver("bolt://localhost:7687", auth=("neo4j","password"))

def create_student(tx, student_id, name):
tx.run(
"CREATE (s:Student {student_id:$id, name:$name})",
id=student_id,
name=name
)

with driver.session() as session:
session.write_transaction(create_student, "S001", "Alice")

```

---

# Skill Behavior

When executing this skill:

1. Identify **node entities**
2. Define **node labels**
3. Identify **relationships**
4. Define **relationship types**
5. Determine **node properties**
6. Determine **relationship properties**
7. Suggest **indexes and constraints**
8. Produce **Cypher schema templates**

Outputs should be compatible with:

- Neo4j
- Memgraph
- Amazon Neptune (property graph mode)
- TigerGraph-style modeling concepts

---

# Graph Modeling Guidelines

Recommended best practices:

- Use **clear node labels**
- Use **UPPERCASE relationship types**
- Avoid overly complex node structures
- Prefer **directional relationships**
- Use **indexes for frequently queried properties**
- Normalize entities rather than duplicating data

Example naming conventions:

```

Node labels: PascalCase
Relationships: UPPERCASE
Properties: camelCase

```

---

# Limitations

This skill generates **schema drafts**, not production-ready implementations.

Developers should still:

- validate with domain experts
- refine constraints
- benchmark query patterns
- optimize indexes

---

# Future Extensions

Potential improvements:

- automatic Cypher migration scripts
- query optimization hints
- graph refactoring suggestions
- schema evolution tools
- Neo4j APOC integration
---
```
