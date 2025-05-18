   # Part 2: Chapter 8 and Chapter 9

## Summary
Chapters 8 and 9 delve into two foundational challenges in knowledge graph construction. Chapter 8 covers **instance matching**, the task of identifying when different graph nodes refer to the same real-world entity. It explains why brute-force comparisons are infeasible at scale and surveys blocking techniques—such as sorted neighborhood and canopies—that reduce candidate pairs before applying probabilistic (Fellegi–Sunter) or machine-learning scorers[^1]. Chapter 9 introduces **statistical relational learning (SRL)**, which overcomes the i.i.d. assumption of traditional ML by encoding relational dependencies with weighted logical formulas. Two prominent SRL frameworks—**Markov Logic Networks (MLNs)** and **Probabilistic Soft Logic (PSL)**—are described, along with their inference and learning strategies, and their use in cleaning and enriching noisy KG extractions[^2].

---

## Summary of Key Points

Successful knowledge‐graph construction depends on robust instance matching to merge all mentions of the same real‐world entity—despite syntactic variations and missing context—by first using scalable blocking techniques (block purging, sorted neighborhood, canopies) to reduce the O(n²) candidate space to near‐linear size. Instance matching then leverages learned similarity functions that compare contextual attributes (e.g., co-authorship links, shared properties) and graph-based features to distinguish truly identical entities from look-alikes. Once candidates are selected, two-stage scoring pipelines (probabilistic Fellegi–Sunter or supervised ML classifiers with a “possible matches” tier) balance precision and recall. Finally, statistical relational learning frameworks such as Markov Logic Networks (MLNs) and Probabilistic Soft Logic (PSL) integrate first‐order logic with probability to capture rich relational dependencies and perform joint inference over noisy, incomplete knowledge graphs. In MLNs, each logical formula is assigned a weight and “grounded” into a Markov network, so that higher-weight rules exert stronger influence during approximate inference (e.g., Gibbs sampling), enabling collective reasoning about entities and relations even when data are sparse or uncertain.  

---

[^1]: Fellegi, I. P., & Sunter, A. B. (1969). A theory for record linkage. *Journal of the American Statistical Association*.  
[^2]: Richardson, M., & Domingos, P. (2006). Markov logic networks: combining probabilistic graphical models with first-order logic. *Machine Learning*.  
[^3]: Bach, S. H., Broecheler, M., Huang, B., & Getoor, L. (2017). Hinge-loss Markov random fields and probabilistic soft logic. *Journal of Machine Learning Research*.  
