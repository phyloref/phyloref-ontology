Phyloreferencing using OWL Ontologies and Reasoning
===================================================

This repository contains a phyloreferencing ontology and examples of phylogenies encoded in OWL using OWL-DL reasoning to match phyloreferences to nodes in the phylogeny.

This is entirely experimental at this point. (Re)use at your own risk. If you do, please give credit, for the time being by citing this repository.

To try out the example, load Campanulaceae.owl into Protege. Then run the reasoner, switch to the DL Query tab, and type (or paste) something like the following into the DL query field (also be sure to check "Individuals" as one of the entities returned by the query):

* The node in the phylogeny that instantiates a phyloreference:

  ```has_Descendant value Campanula_latifolia and excludes_lineage_to value Lobelia```

* The clade defined by a phyloreference:

  ```has_Ancestor some (has_Descendant value Campanula_latifolia and excludes_lineage_to value Lobelia)```

* The tip nodes included by a phyloreference:

  ```TU and has_Ancestor some (has_Descendant value Campanula_latifolia and excludes_lineage_to value Lobelia)```

This series of patterns in essence corresponds to branch-based [phylogenetic clade definitions] [1], i.e., definitions using exclusion. We can use these to build phyloreferences corresponding to node-based clade definitions (i.e., definitions using a most recent common ancestor), by using the parent of the nodes that include one but exclude the other lineage(s).

* For example, for the most recent common ancestor of the Campanula_latifolia and Lobelia, we define the parent of the two nodes has one as descendent and excludes the other:

  ```
has_Child some (has_Descendant value Campanula_latifolia and excludes_lineage_to value Lobelia)
and
has_Child some (has_Descendant value Lobelia and excludes_lineage_to value Campanula_latifolia)
  ```

* We can make this shorter by defining a phyloreference for each of the two components, which we name here Campanula!Lobelia and Lobelia!Campanula:

  ```has_Child some Campanula!Lobelia and has_Child some Lobelia!Campanula```

* We can use the same pattern variations as above to obtain the whole clade or the tip nodes included by this phyloreference. For example:

  ```has_Ancestor some (has_Child some Campanula!Lobelia and has_Child some Lobelia!Campanula)```

The Tetrapoda.owl example (same procedure: load into Protege, run reasoner, switch to DL Query tab) defines phyloreferences for 3 different definitions of Tetrapoda. (Note that for the DL query to return the phyloreference classes, the "Equivalent Classes" option needs to be checked.)

* It also demonstrates use of an apomorphy-based phyloreferences:

  ```TU and has_Ancestor some (has_Progenitor some ('has part' some 'manual digit'))```

[1]: http://dx.doi.org/10.1080/106351591007453 (P. C. Sereno, “The logical basis of phylogenetic taxonomy.,” Systematic Biology, vol. 54, no. 4, pp. 595–619, Aug. 2005.)
