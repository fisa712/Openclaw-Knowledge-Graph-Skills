---
name: mapping-dsl-builder
description: Generate declarative mapping rules that transform structured data sources into graph triples or nodes using a domain-specific mapping language similar to R2RML.
metadata:
  {"openclaw":{"emoji":"🗺️","homepage":"https://clawhub.com"}}
---

# Mapping DSL Builder (R2RML-style)

Create declarative mapping rules that convert structured data sources into **graph triples or graph entities**.

This skill generates mappings using a **domain-specific language (DSL)** that defines how data fields from structured sources such as databases, CSV files, or APIs should be transformed into **nodes, relationships, and triples** for graph databases or knowledge graphs.

The mapping language functions similarly to **R2RML**, which is used for defining relational-to-RDF mappings.

---

# When To Use This Skill

Use this skill when a user wants to:

- Define mappings between **structured datasets and graph models**
- Create **declarative transformation rules**
- Convert **relational schemas into RDF triples**
- Build **graph ingestion mapping specifications**
- Generate reusable **data-to-graph mapping configurations**

Example requests:

- “Create mapping rules for converting this database schema into RDF.”
- “Generate an R2RML-style mapping for this dataset.”
- “Define how CSV columns map to graph nodes and relationships.”
- “Build a mapping configuration for graph ingestion.”

---

# What This Skill Produces

The skill generates **mapping definitions** that specify how source data should be transformed.

Mappings include:

1. **Source Definition**
2. **Entity Mapping**
3. **Property Mapping**
4. **Relationship Mapping**

---

# Example Input Schema

Relational table:

### Employee
```text
id
name
company_id
```
### Company
```text
id
name
location
```

---

# Generated Mapping DSL

Example mapping specification:

```text
mapping EmployeeMapping
source: table(Employee)

subject:
type: Person
id: Employee.id


properties:
name -> Employee.name

relationships:
WORKS_AT -> Company.id
```

---

# Example Triple Output

```text
:employee_1 rdf:type :Person .
:employee_1 :name "Alice" .
:employee_1 :worksAt :company_5 .
```

---

# CSV Mapping Example

CSV:
```text
person_id,name,company
1,Alice,Acme
```

Mapping DSL:
```text
mapping PersonCSV
source: csv("people.csv")
```
subject:
```text
type: Person
id: person_id
```
properties:
```text
name -> name
```
relationships:
```text
WORKS_AT -> company
```


---

# JSON Mapping Example

JSON input:
```json
{
    "name": "Alice",
    "company": "Acme"
}
```


Mapping DSL:

```text
mapping PersonJSON
source: json
```

subject:
```text
type: Person
id: name
```

properties:
```text
name -> name
```

relationships:
```text
WORKS_AT -> company
```


---

# Transformation Strategy

When generating mapping rules:

1. **Identify Data Source**

   Detect whether the input is:

   - relational database
   - CSV dataset
   - JSON document
   - API response

2. **Define Subjects**

   Determine which fields uniquely identify entities.

3. **Map Properties**

   Convert source attributes into node properties.

4. **Define Relationships**

   Map foreign keys or references into graph relationships.

5. **Generate DSL Specification**

   Produce a declarative mapping that can be executed by ETL pipelines.

---

# Output Formats

The generated mapping may be represented in several formats.

### Mapping DSL

```text
mapping Person
source: csv("people.csv")
```

subject:
```text
type: Person
id: person_id
```

properties:
```text
name -> name
age -> age
```

---

### RDF Mapping
```text
rr:TriplesMap
rr:logicalTable "Employee"
rr:subjectMap rr:template "http://example.com/person/{id}"
```

---

### YAML Mapping

source:
```text
type: csv
file: people.csv
```

entity:
```text
type: Person
id: person_id
```

properties:
```text
name: name
```

---

# Implementation Notes

The mapping builder may support:

- relational databases
- CSV ingestion
- JSON transformation
- API data mapping

It can integrate with ETL systems that execute mapping rules to produce **graph triples or property graph structures**.

---

# Best Practices

When designing mappings:

- Use stable identifiers for entity subjects.
- Normalize repeated entities.
- Avoid ambiguous relationships.
- Keep mappings reusable across pipelines.

---

# Summary

This skill generates **declarative mapping specifications** that describe how structured data should be transformed into **graph entities, relationships, and triples**.

It enables:

- relational-to-graph conversion
- CSV-to-graph mappings
- JSON-to-graph mappings
- reusable transformation configurations