Isolation Forest
================

Isolation Forest
----------------

.. py:class:: snapml.IsolationForest(n_estimators=100, max_samples='auto', max_features=1.0, contamination='auto', n_jobs=1, random_state=None, compress_trees=False)

   This class implements an isolation forest for unsupervised anomaly detection
   using the IBM Snap ML library. The model isolates observations by randomly
   selecting a feature and a split value; anomalies require fewer splits to be
   isolated and therefore receive lower scores.

   For all scoring methods, lower values indicate more anomalous samples (see
   ``score_samples``, ``decision_function`` and ``predict``).

   .. note::

      Only dense ``numpy.ndarray`` input is supported.

   :param n_estimators: The number of trees in the forest. Must be at least 1.
   :type n_estimators: int, default=100
   :param max_samples: The number of samples drawn from X to train each tree.

      - If "auto", then ``max_samples = min(256, n_samples)``.
      - If int, it must be greater than 0. Then draw ``max_samples`` samples
        (capped at ``n_samples``).
      - If float, it must be in the range (0.0, 1.0]. Then draw
        ``int(max_samples * n_samples)`` samples, with a minimum of 1.
   :type max_samples: "auto", int or float, default="auto"
   :param max_features: The number of features drawn from X to train each tree.

      - If int, it must be greater than 0. Then draw ``max_features`` features
        (capped at ``n_features``).
      - If float, it must be in the range (0.0, 1.0]. Then draw
        ``int(max_features * n_features)`` features, with a minimum of 1.
        A float greater than 1.0 raises a ``ValueError``.
   :type max_features: int or float, default=1.0
   :param contamination: The expected proportion of outliers in the training data.
      It is used to define the threshold on the scores of the samples.

      - If "auto", ``offset`` is fixed at -0.5, so samples with a raw score below -0.5
        are predicted as outliers.
      - If float, it must be in the range (0, 0.5]. ``offset`` is set to the
        ``100 * contamination``-th percentile of the raw training scores returned by
        ``score_samples(X)`` (lower scores are more anomalous). For example,
        ``contamination=0.1`` sets ``offset`` to the 10th percentile, so that
        approximately 10% of the training samples have a negative
        ``decision_function`` value and are predicted as outliers (-1).
   :type contamination: "auto" or float, default="auto"
   :param n_jobs: The number of threads used to run fit and predict in parallel.
      Must be -1 or an integer of at least 1. If -1, all available CPU cores are used.
   :type n_jobs: int, default=1
   :param random_state: If integer (at least 0), random_state is the seed used by the
      random number generator. If None, a random seed is generated using ``np.random``.
   :type random_state: int or None, default=None
   :param compress_trees: Compress trees after training for fast inference.
   :type compress_trees: bool, default=False

   **Attributes**

   .. py:attribute:: offset
      :type: float

      Offset used to define the decision function from the raw scores:
      ``decision_function(X) = score_samples(X) - offset``.

   .. py:attribute:: max_samples_res
      :type: int

      The actual number of samples used to train each tree.

   .. py:attribute:: max_features_res
      :type: int

      The actual number of features used to train each tree. It is set by ``fit`` and is
      not available on a model restored with ``import_model``.

   .. py:method:: fit(X, y=None, sample_weight=None)

      Fit the model on X.

      :param X: Training data. It must be a 2-D ``numpy.ndarray`` with at least one row
         and one column, and is converted to ``float32`` internally. Other input types,
         such as lists or pandas DataFrames, raise a ``TypeError``.
      :type X: dense matrix (ndarray), shape=(n_samples, n_features)
      :param y: Ignored. Not used, present for API consistency.
      :param sample_weight: Ignored. Not used, present for API consistency.
      :returns: self
      :rtype: object

   .. py:method:: score_samples(X)

      Compute the raw anomaly score of each sample in X.

      :param X: Input data. It must be a 2-D ``numpy.ndarray``. Other input types raise
         a ``TypeError``.
      :type X: dense matrix (ndarray), shape=(n_samples, n_features)
      :returns: Raw anomaly scores, between -1 and 0. The lower the score (the closer
         to -1), the more anomalous the sample.
      :rtype: array-like, shape=(n_samples,)

   .. py:method:: decision_function(X)

      Compute the shifted anomaly score of each sample in X, i.e.
      ``score_samples(X) - offset``.

      :param X: Input data. It must be a 2-D ``numpy.ndarray``. Other input types raise
         a ``TypeError``.
      :type X: dense matrix (ndarray), shape=(n_samples, n_features)
      :returns: Positive values indicate inliers, negative values indicate outliers.
      :rtype: array-like, shape=(n_samples,)

   .. py:method:: predict(X)

      Predict whether each sample in X is an inlier or an outlier.

      :param X: Input data. It must be a 2-D ``numpy.ndarray``. Other input types raise
         a ``TypeError``.
      :type X: dense matrix (ndarray), shape=(n_samples, n_features)
      :returns: +1 for inliers, -1 for outliers.
      :rtype: array-like of int, shape=(n_samples,)

   .. py:method:: export_model(output_file, output_type='pmml')

      Export a fitted IsolationForest model to a file.

      Writes the model structure to ``output_file`` in the requested format.
      A companion ``<output_file>.snapml_meta.json`` file is also written alongside it,
      storing runtime hyperparameters that are not captured by the PMML schema. Both
      files are needed to import the model again with ``import_model``.

      .. note::

         Within Python, a fitted model can also be saved with ``pickle`` (or copied with
         ``copy``). The native model is stored inside the pickled object, so no companion
         file is needed. The inference cache is rebuilt when the object is loaded. If the
         cache cannot be rebuilt, a ``UserWarning`` is issued and the model runs without
         the cache optimization.

      :param output_file: Output filename.
      :type output_file: str
      :param output_type: Output file type. Currently only ``'pmml'`` is supported.
      :type output_type: {'pmml'}

   .. py:method:: import_model(input_file, input_type='pmml')

      Import a pre-trained IsolationForest model from a file.

      Loads the model structure from ``input_file`` and rebuilds the inference
      cache. A companion ``<input_file>.snapml_meta.json`` file must be present in the
      same location to restore runtime hyperparameters not embedded in the PMML schema;
      a ``FileNotFoundError`` is raised if it is missing. To restore a model saved with
      ``pickle`` instead, see the note under ``export_model``.
      Any cache held by a previous ``fit()`` or ``import_model()`` call is released
      before the new model is loaded.

      :param input_file: Input filename.
      :type input_file: str
      :param input_type: Input file type. Currently only ``'pmml'`` is supported.
      :type input_type: {'pmml'}
      :returns: self
      :rtype: object

   .. py:method:: get_params(deep=True)

      Get parameters for this estimator.

      :param deep: If True, will return the parameters for this estimator and
         contained subobjects that are estimators.
      :type deep: bool, default=True
      :returns: Parameter names mapped to their values.
      :rtype: dict

   .. py:method:: set_params(**params)

      Set the parameters of this estimator.

      :param params: Estimator parameters.
      :type params: dict
      :returns: self
      :rtype: estimator instance
