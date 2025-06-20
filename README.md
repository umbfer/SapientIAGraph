# SapientIAGraph

**SapientIAGraph** is an open knowledge graph describing the structure of all degree programs offered by Sapienza University of Rome.  
It is released as part of the paper:  
_"SapientIAGraph: An Open Knowledge Graph of University Degree Programs at Sapienza"_.

- 309 degree programs  
- 10,000+ teaching modules  
- Semantic metadata on instructors, curricula, and disciplinary sectors  
- Released under [CC-BY 4.0](LICENSE)  
- Usable in Neo4j and CSV formats  

## Getting Started (Neo4J)

1. Clone the repository:

```bash
git clone https://github.com/umbfer/SapientIAGraph.git
cd SapientIAGraph
```

2. Restore the Neo4j dump:

Make sure your Neo4j instance is **stopped** before restoring the database.

```bash
neo4j stop
neo4j-admin restore --from=data/SapientIAGraph_neo4j.dump --database=siag.db --force
neo4j start
```

If you're using Neo4j Desktop, place the dump in the `import` folder of your project and use the "Restore from Dump" option in the interface.

3. Set the active database in `neo4j.conf` (if needed):

```bash
dbms.default_database=siag.db
```

4. Open Neo4j Browser at [http://localhost:7474](http://localhost:7474) and start exploring.

5. Try the example queries in [`docs/example_queries.md`](docs/example_queries.md)


## CSV Files Data Format

The graph is represented using two CSV files:

### `SapientIAGraph_nodes.csv`
This file lists all the nodes in the graph. Each row contains the following fields:

- `id`: Unique identifier of the node.
- `label`: Type of the node (e.g., Module, Instructor).
- `language`: Language of instruction (if applicable).
- `name`: Short name of the node.
- `semester`: Semester of offering (if applicable)..
- `ssd`: Scientific Disciplinary Sector code (if applicable)..
- `title`: Title of the module .
- `type`: Degree type (if applicable)..
- `year`: Academic year (if applicable)..

### `SapientIAGraph_edges.csv`
This file lists all edges between nodes. Each row contains:

- `label`: Type of relationship (e.g., TAUGHT_BY, INCLUDES_MODULE).
- `source`: ID of the source node.
- `target`: ID of the target node.


## Project Structure

```
SapientIAGraph/
├── data/
│   ├── SapientIAGraph_nodes.csv
│   ├── SapientIAGraph_edges.csv
│   ├── SapientIAGraph_neo4j.dump
├── docs/
│   ├── schema.png
│   └── example_queries.md
├── README.md
├── LICENSE

```


## License

Distributed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
