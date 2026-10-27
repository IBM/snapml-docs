snapml.preprocessing.Normalizer
===============================

.. py:class:: snapml.preprocessing.Normalizer(norm='l2', *, copy=True)

   Normalize samples individually to unit norm.

   Each sample (i.e. each row of the data matrix) with at least one non zero component is rescaled independently of other samples so that its norm (l1, l2, or max) equals one.

   This transformer is useful for text classification or clustering, where vector length reflects document length rather than informational content.

   Parameters
   ----------
   norm : {'l1', 'l2', 'max'}, default='l2'
       The norm to use to normalize each non zero sample:

       * ``'l1'`` : Sum of absolute values equals 1.
       * ``'l2'`` : Sum of squares equals 1 (Euclidean norm).
       * ``'max'`` : Maximum absolute value equals 1.

   copy : bool, default=True
       Set to False to perform inplace row normalization and avoid a copy (if the input is already a numpy array or scipy.sparse CSR matrix).

   Attributes
   ----------
   n_features_in_ : int
       Number of features seen during :meth:`fit`.

   feature_names_in_ : ndarray of shape (n_features_in_)
       Names of features seen during :meth:`fit`. Defined only when ``X`` has feature names that are all strings.

   See Also
   --------
   :class:`snapml.preprocessing.KBinsDiscretizer` : Bin continuous data into intervals.

   Notes
   -----
   Unlike standard scalers (which standardize column-wise across samples), :class:`Normalizer` rescales rows (samples) independently.

   Examples
   --------
   >>> from snapml.preprocessing import Normalizer
   >>> X = [[4, 1, 2, 2],
   ...      [1, 3, 9, 3],
   ...      [5, 7, 5, 1]]
   >>> transformer = Normalizer(norm='l2')
   >>> transformer.transform(X)
   array([[0.8, 0.2, 0.4, 0.4],
          [0.1, 0.3, 0.9, 0.3],
          [0.5, 0.7, 0.5, 0.1]])

   Methods
   -------

   .. py:method:: fit(X, y=None)

      Do nothing and return the estimator unchanged.

      This method is just there to implement the standard scikit-learn transformer API.

      :param X: Training data of shape ``(n_samples, n_features)``.
      :type X: {array-like, sparse matrix}
      :param y: Ignored.
      :type y: None
      :returns: **self** -- Fitted transformer.
      :rtype: object

   .. py:method:: fit_transform(X, y=None)

      Fit to data, then transform it.

      :param X: Input samples of shape ``(n_samples, n_features)``.
      :type X: {array-like, sparse matrix}
      :param y: Target values (default None).
      :type y: None
      :returns: **Xt** -- Transformed array.
      :rtype: {ndarray, sparse matrix}

   .. py:method:: get_feature_names_out(input_features=None)

      Get output feature names for transformation.

      :param input_features: Input features. If None, feature names seen during :meth:`fit` are used.
      :type input_features: array-like of str or None, default=None
      :returns: **feature_names_out** -- Transformed feature names.
      :rtype: ndarray of str objects

   .. py:method:: get_metadata_routing()

      Get metadata routing of this object.

      :returns: **routing** -- A ``MetadataRequest`` encapsulating routing information.
      :rtype: MetadataRequest

   .. py:method:: get_params(deep=True)

      Get parameters for this estimator.

      :param deep: If True, will return the parameters for this estimator and contained subobjects.
      :type deep: bool, default=True
      :returns: **params** -- Parameter names mapped to their values.
      :rtype: dict

   .. py:method:: set_num_threads(n=4)

      Set the number of OMP threads used by the C++ backend.

      :param n: Number of threads. Must be a non-negative integer.
      :type n: int, default=4
      :returns: **self** -- Estimator instance.
      :rtype: object

   .. py:method:: set_output(*, transform=None)

      Set output container.

      :param transform: Configure output of ``transform`` and ``fit_transform``.
      :type transform: {"default", "pandas", "polars"}, default=None
      :returns: **self** -- Estimator instance.
      :rtype: object

   .. py:method:: set_params(**params)

      Set the parameters of this estimator.

      :returns: **self** -- Estimator instance.
      :rtype: object

   .. py:method:: transform(X, copy=None)

      Scale each non-zero row of ``X`` to unit norm.

      :param X: The data to normalize, row by row.
      :type X: {array-like, sparse matrix} of shape ``(n_samples, n_features)``
      :param copy: Copy the input X or not.
      :type copy: bool, default=None
      :returns: **Xt** -- Transformed array.
      :rtype: {ndarray, sparse matrix}
