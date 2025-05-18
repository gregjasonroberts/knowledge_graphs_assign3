
# Assignment3 Knowledge Graphs & Investment Analysis README

## Part 1: Structured Querying in Knowledge Graphs  
Structured querying relies on SPARQL, the W3C-standardized RDF query language, which expresses graph patterns as sets of triple templates. SPARQL 1.1 adds SQL-style features (aggregates, subqueries, OPTIONAL, MINUS) on top of basic pattern matching, and its formal bottom-up evaluation leverages decades of relational-query optimization research—even though RDF often resists tabular representation.

**Physical Storage Layouts**  
- **Triple-Table**: All triples in a single (subject, predicate, object) table. Simple to ingest but many self-joins can cause I/O bottlenecks.  
- **Property-Table**: Wide tables co-locate common properties of each subject, reducing joins for multi-predicate lookups but requiring careful schema design.  
- **Horizontal (Vertical Partitioning)**: One two-column table per predicate, sorted by subject. Simplifies table creation and reduces UNIONs at the cost of many merge-joins.

**NoSQL & Alternative Stores**  
- **Apache Cassandra**: Distributed wide-column store with tunable consistency and high-throughput writes/reads.  
- **Apache HBase**: Versioned, sparse tables on HDFS with real-time random access and seamless Hadoop integration.

**Property-Graph & Hypergraph Models**  
- **Neo4j (Property-Graph)**: Nodes and relationships carry arbitrary key-value pairs, queried via the Cypher DSL (`MATCH`, `WHERE`, `RETURN`).  
- **Hypergraph Databases**: Generalize edges into hyperedges that can connect any number of vertices, modeling higher-order relations without decomposing them into multiple binary triples.

---

## Part 2: Instance Matching & Statistical Relational Learning  
Accurate knowledge graphs require **instance matching** to merge nodes representing the same real-world entity—despite syntactic variations, missing context, and domain-specific ambiguity.  

1. **Scalable Blocking**  
   - **Block Purging**, **Sorted Neighborhood**, and **Canopies** reduce the O(n²) comparison space to near-linear scale by grouping or clustering roughly similar entities.  
2. **Two-Stage Scoring Pipelines**  
   - After blocking, candidate pairs are scored by probabilistic models (Fellegi–Sunter) or supervised classifiers, allowing precision–recall trade-offs and a “possible matches” tier for manual review.  
3. **Statistical Relational Learning (SRL)**  
   - **Markov Logic Networks (MLNs)** assign weights to first-order logic formulas, grounding them into a Markov network for approximate inference (Gibbs sampling, belief propagation).  
   - **Probabilistic Soft Logic (PSL)** “softens” logic into hinge-loss MRFs with continuous truth values, enabling convex MAP inference and high scalability.  
4. **Applications**  
   - Joint inference over noisy, incomplete extractions—inferring missing links, cleaning errors, and classifying entities in a unified probabilistic framework.

---

## Part 3: Fundamental Analysis of Investments  
**Fundamental analysis** measures a security’s intrinsic value by examining financial statements (revenue, assets, liabilities) and macroeconomic indicators (GDP, interest rates).

**Benefits**  
- Focuses on underlying value drivers (earnings growth, cash flow, competitive moats).  
- Provides a long-term framework less influenced by short-term market noise.

**Limitations**  
- Relies on forecasts and intrinsic-value estimates that vary across analysts.  
- Qualitative factors (management quality, brand strength) are subjective and hard to quantify.

**Term Project Applications**  
1. Create **Company** nodes linked to **FinancialMetric** nodes (P/E ratios, debt-to-equity) extracted from EDGAR filings.  
2. Query for companies trading below intrinsic value via a RAG-based recommendation engine.  
3. Map how changes in fundamentals propagate across peer-group and industry relationships.

---

## Part 4: Technical Analysis of Investments  
**Technical analysis** studies past market data—price and volume—to forecast future price movements.

**Benefits**  
- Signals short-term entry and exit opportunities.  
- Applies across asset classes and timeframes.  
- Provides rule-based indicators (moving averages, RSI, MACD) to reduce emotional bias.

**Limitations**  
- Based solely on historical data; may fail during unforeseen market shifts.  
- Prone to false signals (“whipsaws”) in sideways markets.  
- Interpretation can vary; reliable use requires backtesting.  
- Critiqued as self-fulfilling and challenged by the Efficient Market Hypothesis.

**Term Project Applications**  
1. Model **Price** nodes (timestamped close, high, low, volume) linked to **Company** nodes.  
2. Generate **Indicator** nodes (MovingAverage, RSI, MACD) linked to Price and Company.  
3. Query graph patterns (e.g., moving-average crossovers) to flag trade signals.  
4. Feed technical signals into the RAG engine alongside fundamental metrics.

---

## Part 5: Sentiment Analysis of Investments  
**Sentiment analysis** uses NLP and text mining to quantify positive, negative, or neutral opinions in text about companies, markets, or products.

**Benefits**  
- Captures real-time investor mood faster than traditional indicators.  
- Leverages unstructured data (news, social media) as an alternative data source.  
- Enhances predictive models when combined with quantitative metrics.

**Limitations**  
- Data sparsity for individual stocks can yield unreliable signals.  
- Noise and false positives from information overload and writing-style variation.  
- Financial language nuances require specialized lexicons (e.g., Loughran-McDonald).  
- Models need continuous retraining to adapt to evolving language and market contexts.

**Term Project Applications**  
1. Create **NewsArticle** and **SocialMediaPost** nodes with sentiment polarity and confidence attributes.  
2. Link sentiment nodes to **Company** nodes to track opinion shifts over time.  
3. Aggregate sentiment time series as RAG-engine features for queries like “Which companies saw sentiment improve after earnings calls?”  
4. Combine sentiment indicators with fundamental and technical metrics to build hybrid trading signals.
