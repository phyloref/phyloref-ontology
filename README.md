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

The Tetrapoda.owl example (same procedure: load into Protege, run reasoner, switch to DL Query tab) defines phyloreferences for 3 different definitions of Tetrapoda. (Note that for the DL query to return the phyloreference classes, the "Equivalent Classes" option needs to be checked.)

* It also demonstrates use of an apomorphy-based phyloreferences:

  ```TU and has_Ancestor some (has_Progenitor some ('has part' some 'manual digit'))```