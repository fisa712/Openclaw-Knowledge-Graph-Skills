---

name: tigergraph_connector
description: Connect to a TigerGraph database to query, load, and manage knowledge graph data using TigerGraph's REST APIs and GSQL query language.
category: integrations
tags:

* knowledge-graph
* tigergraph
* graph-database
* gsql
* graph-analytics
* integration
  version: 1.0.0
  author: kg-dev-skills

---

# TigerGraph Connector

## Purpose

This skill enables interaction with a **TigerGraph graph database** for storing, querying, and analyzing knowledge graph data.

TigerGraph is a **high-performance distributed graph database** designed for large-scale graph analytics and real-time graph processing.

This skill allows developers to:

* connect to a TigerGraph instance
* execute **GSQL queries**
* load nodes and edges into the graph
* retrieve graph structures and analytics results
* integrate TigerGraph into knowledge graph workflows

---

## When To Use This Skill

Use this skill when:

* interacting with a **TigerGraph-based knowledge graph**
* executing **GSQL queries**
* loading graph data into TigerGraph
* retrieving nodes, edges, or analytics results
* running graph algorithms provided by TigerGraph

Example triggers:

* "Run this GSQL query"
* "Insert vertices into TigerGraph"
* "Create edges between nodes"
* "Fetch connected nodes"
* "Analyze relationships in the graph"

---

## Connection Configuration

The skill requires connection information for a TigerGraph server.

Example configuration:

```json
{
  "host": "http://localhost",
  "restpp_port": 9000,
  "graph_name": "MyGraph",
  "api_token": "YOUR_API_TOKEN"
}
```

Authentication typically uses:

* API tokens
* username/password credentials

---

## Core Capabilities

### Execute GSQL Queries

Example query:

```gsql
RUN QUERY getNeighbors("Alice")
```

Example query definition:

```gsql
CREATE QUERY getNeighbors(VERTEX<Person> person) FOR GRAPH MyGraph {
  Start = {person};
  Result = SELECT t
           FROM Start:s -(KNOWS:e)-> Person:t;
  PRINT Result;
}
```

---

### Insert Vertices

Example REST request payload:

```json
{
  "vertices": {
    "Person": {
      "Alice": {
        "name": "Alice",
        "age": 30
      }
    }
  }
}
```

---

### Insert Edges

Example payload:

```json
{
  "edges": {
    "Person": {
      "Alice": {
        "KNOWS": {
          "Person": {
            "Bob": {}
          }
        }
      }
    }
  }
}
```

---

### Retrieve Graph Data

Example request:

```
GET /graph/MyGraph/vertices/Person
```

This retrieves all vertices of a specified type.

---

### Run Graph Analytics

TigerGraph supports advanced graph algorithms such as:

* PageRank
* community detection
* shortest path
* centrality analysis

Example:

```
RUN QUERY pagerank()
```

---

## Inputs

Expected inputs include:

* GSQL queries
* vertex or edge data
* graph name
* authentication credentials

Example input:

```json
{
  "query": "RUN QUERY getNeighbors(\"Alice\")"
}
```

---

## Output

Query results returned from TigerGraph.

Example output:

```json
{
  "results": [
    {
      "person": "Bob"
    },
    {
      "person": "Charlie"
    }
  ]
}
```

Results may include:

* vertices
* edges
* analytics outputs
* query statistics

---

## Procedure

1. Connect to the TigerGraph server.
2. Authenticate using API token or credentials.
3. Select the target graph.
4. Accept GSQL queries or graph operations.
5. Execute the request through REST++ APIs or GSQL engine.
6. Retrieve and format results.

---

## Developer Notes

TigerGraph is optimized for:

* large-scale graphs
* distributed processing
* graph analytics workloads

Typical workflow:

1. define graph schema
2. load data into vertices and edges
3. run queries or algorithms
4. analyze results

For large datasets:

* batch data loading is recommended
* use built-in graph algorithms where possible
* monitor query performance

---

## Expected Benefits

Using this skill enables:

* integration with TigerGraph systems
* high-performance graph analytics
* scalable knowledge graph processing
* advanced graph algorithm execution
