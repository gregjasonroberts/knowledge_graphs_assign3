# Part 1: Week 6 Knowledge Graphs Textbook Readings Summary

Structured querying in knowledge graphs relies heavily on SPARQL, the W3C-standardized RDF query language designed to express graph patterns as sets of triple templates. Variables prefixed with “?” bind to subjects, predicates, or objects, and shared variables across multiple patterns naturally result in join operations. SPARQL 1.1 extends basic pattern matching with SQL-style features such as aggregates, subqueries, optional patterns, and negation, enabling complex queries (e.g., grouping, ordering) that go beyond simple triple matching. Its formal semantics and bottom-up evaluation model allow systems to leverage decades of relational query optimization research, even though RDF data often resists straightforward tabular representation.[^1]

## Key Summary Points

- **Triple-Table Layout**  
  Stores every RDF triple in one large table (subject, predicate, object) with extensive indexing; while this generality simplifies ingestion, complex queries incur many self-joins and can suffer severe I/O bottlenecks.

- **Property-Table Layout**  
  Co-locates a subject’s common properties in wide tables, reducing joins for multi-predicate lookups but requiring careful schema design or adaptive clustering to avoid sparse columns.

- **Horizontal (Vertical Partitioning) Layout**  
  Splits data into one two-column table per predicate, sorted by subject; this vertical partitioning simplifies table creation and reduces union clauses yet demands merge-joins across many narrow tables.[^2]

- **Property-Graph & Hypergraph Databases**  
  - **Neo4j (Property-Graph Model)** attaches arbitrary key–value properties to nodes and relationships and exposes them via the Cypher DSL (`MATCH`, `WHERE`, `RETURN`), abstracting explicit join syntax and emphasizing pattern matching.[^3]  
  - **Hypergraph Databases** generalize edges to hyperedges that can connect any number of vertices—often represented as nested hypernodes—making it easier to model higher-order relations without decomposing them into multiple binary triples.[^4]

---

[^1]: W3C. (2013). SPARQL 1.1 Query Language. https://www.w3.org/TR/sparql11-query/   
[^2]: Kim, H.-J., & Park, J.-S. (2020). Evaluating Performance of Vertical Partitioned RDF Stores. *Data & Knowledge Engineering*.  
[^3]: https://neo4j.com/blog/knowledge-graph/what-is-knowledge-graph/ 
[^4]: Bretto, A. (2013). *Hypergraph Theory: An Introduction*. Springer.  



