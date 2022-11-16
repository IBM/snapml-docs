Graph-Based Feature Extraction
==============================

The GraphFeaturePreprocessor is a scikit-learn compatible preprocessing library that enables feature extraction from graph-structured data.  
The library includes features for creating, updating, and transforming graph-structured data. 
The basic input and output data representation used by the library is an edge list with edge features.
As an example, in a financial transaction graph, the graph nodes represent accounts and the graph edges represent transactions.
The date of the transactions as well as the amount transferred between the accounts may be given as edge features.
However, the GraphFeaturePreprocessor can generate a much richer set of edge features by analyzing the graph.   
For instance, the GraphFeaturePreprocessor can extract the number of cycles each transaction is a part of in the graph.
Such additional features can significantly increase the predictive power of machine learning models in many practical settings. 

.. image:: graph-feature-extraction.png
  :width: 800
  :align: center
  :alt: Graph feature extraction 

.. autofunction:: snapml.GraphFeaturePreprocessor
