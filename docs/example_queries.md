# SapientIAGraph – Example Cypher Queries

This document contains example Cypher queries for exploring and analyzing the SapientIAGraph in a Neo4j database.

## 1. List all degree programs

```cypher
MATCH (d:DegreeProgram)
RETURN d.name, d.code
ORDER BY d.name
```

## 2. Retrieve all curricula for a given degree program

```cypher
MATCH (d:DegreeProgram {name: "Economia aziendale"})-[:HAS_CURRICULUM]->(c:Curriculum)
RETURN c.name
```


## 3. Count the number of curricula per degree program

```cypher
MATCH (d:DegreeProgram)-[:HAS_CURRICULUM]->(c:Curriculum)
RETURN d.name AS DegreeProgram, COUNT(c) AS NumCurricula
ORDER BY NumCurricula DESC
```


## 4. Retrieve all modules belonging to a specific SSD

```cypher
MATCH (m:Module)
WHERE m.ssd = "INF/01"
RETURN m.title, m.code
```

## 5. Display the full structure of a degree program

```cypher
MATCH (d:DegreeProgram {name: "Data Science"})-[:HAS_CURRICULUM]->(c:Curriculum)-[:INCLUDES_MODULE]->(m:Module)-[:TAUGHT_BY]->(i:Instructor)
RETURN d.name, c.name, m.title, i.name
ORDER BY c.name, m.title
```

## 6. Count the number of degree programs per subject area

```cypher
MATCH (d:DegreeProgram)-[:BELONGS_TO]->(s:SubjectArea)
RETURN s.name AS SubjectArea, COUNT(d) AS NumPrograms
ORDER BY NumPrograms DESC
```

## 7. Identify modules that contain other modules

```cypher
MATCH (m1:Module)-[:CONTAINS_MODULE]->(m2:Module)
RETURN m2.title AS ParentModule, COLLECT(m2.title) AS Submodules
```

## 8. Find degree programs that share at least one module

```cypher
MATCH (d1:DegreeProgram)-[:HAS_CURRICULUM]->(:Curriculum)-[:INCLUDES_MODULE]->(m:Module)<-[:INCLUDES_MODULE]-(:Curriculum)<-[:HAS_CURRICULUM]-(d2:DegreeProgram)
WHERE d1 <> d2
RETURN d1.name, d2.name, COUNT(DISTINCT m) AS SharedModules
ORDER BY SharedModules DESC
```
