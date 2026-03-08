---

name: graph_schema_migration_diff
title: Graph Schema Migration Diff (v1 → v2)
description: Analyze differences between two knowledge graph schemas and generate migration plans and scripts for upgrading graph data structures.
category: graph-modeling
tags:

* knowledge-graph
* schema-migration
* graph-evolution
* rdf
* owl
* neo4j
* cypher
* developer-tools
  version: 0.1.0
  author: community
  license: MIT

---

# Graph Schema Migration Diff (v1 → v2)

## Purpose

This skill assists developers in **analyzing differences between two versions of a knowledge graph schema** and generating a migration strategy.

It helps with:

* identifying schema changes
* detecting added or removed entities
* identifying property changes
* detecting relationship changes
* generating migration scripts

The goal is to **safely evolve graph schemas without breaking existing data**.

---

# When To Use This Skill

Use this skill when:

* upgrading a knowledge graph schema
* migrating from **schema v1 → schema v2**
* refactoring graph models
* renaming nodes or relationships
* adding or removing properties
* introducing new graph constraints

Example prompts:

* "Generate a migration plan between these graph schemas."
* "Detect changes between schema versions."
* "Create Cypher migration scripts."
* "Compare two RDF ontology versions."

---

# Inputs

The skill accepts two schema definitions:

* **Schema Version 1**
* **Schema Version 2**

Schemas may be expressed as:

* RDF/OWL ontology files
* property graph models
* Cypher schema definitions
* JSON schema representations
* entity/property lists

Example input:

### Schema v1

```
Entities:
Student
Course

Relationships:
(Student)-[:ENROLLED_IN]->(Course)

Properties:
Student
- student_id
- name
```

### Schema v2

```
Entities:
Student
Course
Department

Relationships:
(Student)-[:ENROLLED_IN]->(Course)
(Course)-[:BELONGS_TO]->(Department)

Properties:
Student
- student_id
- full_name
```

---

# Schema Diff Detection

The skill detects several categories of changes.

---

## 1. New Entities

Example:

```
+ Department
```

---

## 2. Removed Entities

Example:

```
- Instructor
```

---

## 3. Property Changes

Example:

```
Student.name → Student.full_name
```

Detected as:

* property rename
* property addition
* property removal

---

## 4. Relationship Changes

Example:

```
+ (Course)-[:BELONGS_TO]->(Department)
```

---

## 5. Constraint Changes

Example:

```
Student.student_id UNIQUE
```

---

# Migration Plan Output

The skill produces a structured migration plan.

Example:

```
Migration Plan
--------------

1. Add Node Label
Department

2. Add Relationship
(Course)-[:BELONGS_TO]->(Department)

3. Rename Property
Student.name → Student.full_name
```

---

# Neo4j Migration Script Example

Example Cypher migration:

```
MATCH (s:Student)
WHERE s.name IS NOT NULL
SET s.full_name = s.name
REMOVE s.name
```

Add new node type:

```
CREATE CONSTRAINT department_id_unique
FOR (d:Department)
REQUIRE d.department_id IS UNIQUE;
```

---

# RDF / OWL Migration Example

Example RDF change:

```
:Student :name → :fullName
```

Migration strategy:

* add new property
* copy values
* deprecate old property

Example:

```
:s1 :fullName "Alice" .
:s1 :name "Alice" .
```

---

# Developer Implementation Notes

When implementing schema diff tools programmatically, prefer **Python libraries suitable for graph analysis and schema comparison**.

Recommended libraries:

### Graph Processing

* networkx

### RDF / OWL Tools

* rdflib
* owlready2

### Data Comparison

* deepdiff
* dictdiffer

### Neo4j Integration

* neo4j
* py2neo

---

# Example Python Schema Diff

```
from deepdiff import DeepDiff

schema_v1 = {
    "Student": ["student_id", "name"],
    "Course": ["course_id"]
}

schema_v2 = {
    "Student": ["student_id", "full_name"],
    "Course": ["course_id"],
    "Department": ["department_id"]
}

diff = DeepDiff(schema_v1, schema_v2)

print(diff)
```

---

# Migration Script Generator Example

```
def generate_property_rename(node, old_prop, new_prop):

    cypher = f"""
MATCH (n:{node})
WHERE n.{old_prop} IS NOT NULL
SET n.{new_prop} = n.{old_prop}
REMOVE n.{old_prop}
"""

    return cypher

print(generate_property_rename("Student","name","full_name"))
```

---

# Skill Behavior

When executing this skill:

1. parse schema v1
2. parse schema v2
3. detect structural differences
4. classify schema changes
5. generate migration plan
6. produce migration scripts

Outputs should include:

* schema diff report
* migration plan
* database migration scripts

---

# Output Format

Example migration report:

```
Schema Migration Diff
---------------------

Entities Added
+ Department

Properties Changed
Student.name → Student.full_name

Relationships Added
(Course)-[:BELONGS_TO]->(Department)

Migration Complexity: Medium
```

---

# Best Practices

When evolving graph schemas:

* maintain backward compatibility when possible
* deprecate fields before removing them
* perform migrations in stages
* test migrations on staging data
* keep schema version history

---

# Limitations

Automated schema diffs may not detect:

* semantic meaning changes
* complex relationship redesigns
* domain-level schema decisions

Developers should review migration plans carefully.

---

# Future Extensions

Potential improvements:

* automated migration execution
* graph refactoring tools
* schema version registry
* visual schema diff tools
* rollback migration generation

---
