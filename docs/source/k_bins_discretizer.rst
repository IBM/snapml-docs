snapml.preprocessing.KBinsDiscretizer
=====================================

.. py:class:: snapml.preprocessing.KBinsDiscretizer(n_bins=5, *, encode='onehot', strategy='quantile', dtype=None, subsample=200000, random_state=None)

   Bin continuous data into intervals.

   Discretization (otherwise known as quantization or binning) provides a way to partition continuous features into discrete values. Certain datasets with continuous features may benefit from discretization when preparing data for linear models or decision trees.

   Parameters
   ----------
   n_bins : int or array-like of shape (n_features), default=5
       The number of bins to produce. Raises ``ValueError`` if ``n_bins < 2``.

   encode : {'onehot', 'onehot-dense', 'ordinal'}, default='onehot'
       Method used to encode the transformed result:

       * ``'onehot'`` : Encode the transformed result with one-hot encoding and return a sparse matrix.
       * ``'onehot-dense'`` : Encode the transformed result with one-hot encoding and return a dense array.
       * ``'ordinal'`` : Return the bin identifier encoded as an integer value.

   strategy : {'uniform', 'quantile', 'kmeans'}, default='quantile'
       Strategy used to define the widths of the bins:

       * ``'uniform'`` : All bins in each feature have identical widths.
       * ``'quantile'`` : All bins in each feature have the same number of points.
       * ``'kmeans'`` : Values in each bin have the same nearest center of a 1D k-means cluster.

   dtype : {np.float32, np.float64}, default=None
       The desired dtype for output. If None, output dtype is ``np.float64``.

   subsample : int or None, default=200000
       Maximum number of samples, used to fit the model for computational efficiency.

   random_state : int, RandomState instance or None, default=None
       Determines random number generation for subsampling and k-means initialization.

   Attributes
   ----------
   bin_edges_ : ndarray of ndarray of shape (n_features)
       The edges of each bin. Contain arrays of shape ``(n_bins + 1)``.

   n_bins_ : ndarray of shape (n_features), dtype=np.int_
       Number of bins for each feature.

   n_features_in_ : int
       Number of features seen during :meth:`fit`.

   feature_names_in_ : ndarray of shape (n_features_in_)
       Names of features seen during :meth:`fit`. Defined only when ``X`` has feature names that are all strings.

   See Also
   --------
   :class:`snapml.preprocessing.OneHotEncoder` : Encode categorical features as a one-hot numeric array.
   :class:`snapml.preprocessing.OrdinalEncoder` : Encode categorical features as an integer array.

   Examples
   --------
   >>> from snapml.preprocessing import KBinsDiscretizer
   >>> import numpy as np
   >>> X = [[-2, 1.5], [-1, -0.5], [0, 0.5], [1, -1.5]]
   >>> est = KBinsDiscretizer(
   ...     n_bins=3, encode='ordinal', strategy='uniform'
   ... )
   >>> est.fit(X)
   KBinsDiscretizer(encode='ordinal', n_bins=3, strategy='uniform')
   >>> Xt = est.transform(X)
   >>> Xt
   array([[0., 2.],
          [1., 1.],
          [2., 2.],
          [2., 0.]])
   >>> est.bin_edges_[0]
   array([-2., -1.,  0.,  1.])
   >>> est.inverse_transform(Xt)
   array([[-1.5,  1.],
          [-0.5,  0.],
          [ 0.5,  1.],
          [ 0.5, -1.]])

   .. note::

      ``inverse_transform()`` converts each bin index back to the midpoint of its bin edges. It does not recover the exact original values because discretization loses information.

   Methods
   -------

   .. py:method:: fit(X, y=None)

      Fit the estimator on data ``X``.

      :param X: Training data of shape ``(n_samples, n_features)``.
      :type X: array-like
      :param y: Ignored. This parameter exists only for compatibility.
      :type y: None
      :returns: **self** -- Fitted estimator.
      :rtype: object

   .. py:method:: fit_transform(X, y=None)

      Fit to data, then transform it.

      :param X: Input samples of shape ``(n_samples, n_features)``.
      :type X: array-like
      :param y: Target values (default None).
      :type y: array-like, optional
      :returns: **Xt** -- Transformed array.
      :rtype: {ndarray, sparse matrix}

   .. py:method:: get_feature_names_out(input_features=None)

      Get output feature names for transformation.

      :param input_features: Input features. If None, feature names seen during :meth:`fit` are used.
      :type input_features: array-like of str or None, default=None
      :returns: **feature_names_out** -- Transformed feature names.
      :rtype: ndarray of str objects

   .. py:method:: get_params(deep=True)

      Get parameters for this estimator.

      :param deep: If True, will return the parameters for this estimator and contained subobjects that are estimators.
      :type deep: bool, default=True
      :returns: **params** -- Parameter names mapped to their values.
      :rtype: dict

   .. py:method:: inverse_transform(Xt)

      Transform discretized data back to original feature space.

      :param Xt: Transformed data in the binned space.
      :type Xt: array-like of shape ``(n_samples, n_features)``
      :returns: **Xinv** -- Data with values corresponding to bin centers.
      :rtype: ndarray

   .. py:method:: set_num_threads(n=4)

      Set the number of OMP threads used by the C++ backend.

      :param n: Number of threads. Must be a non-negative integer.
      :type n: int, default=4
      :returns: **self** -- Estimator instance.
      :rtype: object

   .. py:method:: set_params(**params)

      Set the parameters of this estimator.

      :returns: **self** -- Estimator instance.
      :rtype: object

   .. py:method:: transform(X)

      Discretize the data ``X``.

      :param X: Data to be discretized of shape ``(n_samples, n_features)``.
      :type X: array-like
      :returns: **Xt** -- Discretized data in the binned space.
      :rtype: {ndarray, sparse matrix}
