snapml.preprocessing.OneHotEncoder
===================================

.. py:class:: snapml.preprocessing.OneHotEncoder(*, categories='auto', drop=None, sparse_output=True, dtype=numpy.float64, handle_unknown='error', min_frequency=None, max_categories=None)

   Encode categorical features as a one-hot numeric array.

   The input to this transformer should be an array-like of integers or strings, denoting the values taken on by categorical (discrete) features. The features are encoded using a one-hot (also known as 'one-of-K' or 'dummy') encoding scheme. This creates a binary column for each category and returns a sparse matrix or dense array.

   Parameters
   ----------
   categories : 'auto' or list of array-like, default='auto'
       Categories (unique values) per feature:

       * ``'auto'`` : Determine categories automatically from the training data.
       * ``list`` : ``categories[i]`` holds the categories expected of the ``i``-th column. The passed categories should not mix strings and numeric values within a single feature, and should be sorted in case of numeric values.

   drop : {'first', 'if_binary'} or array-like of shape (n_features,), default=None
       Specifies a methodology to use to drop one of the categories per feature. This is useful in situations where perfectly collinear features cause problems:

       * ``None`` : retain all features (the default).
       * ``'first'`` : drop the first category in each feature. If only one category is present, the feature will be dropped entirely.
       * ``'if_binary'`` : drop the first category in each feature with two categories. Features with 1 or more than 2 categories are left intact.
       * ``array-like`` : ``drop[i]`` is the category in feature ``X[:, i]`` that should be dropped.

   sparse_output : bool, default=True
       Will return sparse CSR matrix if set to ``True`` else will return an array.

   dtype : number type, default=np.float64
       Desired dtype of output.

   handle_unknown : {'error', 'ignore', 'infrequent_if_exist'}, default='error'
       Whether to raise an error or ignore if an unknown categorical feature is present during transform:

       * ``'error'`` : Raise an error if an unknown category is present during transform.
       * ``'ignore'`` : When an unknown category is encountered during transform, the resulting one-hot encoded columns for this feature will be all zeros.
       * ``'infrequent_if_exist'`` : Map unknown categories to infrequent category, if an infrequent category exists.

   min_frequency : int or float, default=None
       Specifies the minimum frequency below which a category will be considered infrequent:

       * If ``int``, categories with smaller cardinality will be considered infrequent.
       * If ``float``, categories with a smaller cardinality than ``min_frequency * n_samples`` will be considered infrequent.

   max_categories : int, default=None
       Specifies an upper limit to the number of output features for each input feature. It considers the most frequent categories first.

   Attributes
   ----------
   categories_ : list of arrays
       The categories of each feature determined during fitting (in order of the features in ``X`` and corresponding with the output of :meth:`transform`).

   drop_idx_ : array of shape (n_features,)
       ``drop_idx_[i]`` is the index in ``categories_[i]`` of the category to be dropped for each feature. ``None`` if all categories are kept.

   infrequent_categories_ : list of ndarray
       Defined only if infrequent categories are enabled.

   n_features_in_ : int
       Number of features seen during :meth:`fit`.

   feature_names_in_ : ndarray of shape (n_features_in_,)
       Names of features seen during :meth:`fit`. Defined only when ``X`` has feature names that are all strings.

   See Also
   --------
   :class:`snapml.preprocessing.OrdinalEncoder` : Encode categorical features as an integer array.
   :class:`snapml.preprocessing.TargetEncoder` : Encode categorical features using target encoding.

   Examples
   --------
   >>> from snapml.preprocessing import OneHotEncoder
   >>> enc = OneHotEncoder(handle_unknown='ignore', sparse_output=False)
   >>> X = [['Male', 1], ['Female', 3], ['Female', 2]]
   >>> enc.fit(X)
   OneHotEncoder(handle_unknown='ignore', sparse_output=False)
   >>> enc.categories_
   [array(['Female', 'Male'], dtype=object), array([1, 2, 3], dtype=object)]
   >>> enc.transform([['Female', 1], ['Male', 4]])
   array([[1., 0., 1., 0., 0.],
          [0., 1., 0., 0., 0.]])
   >>> enc.inverse_transform([[0, 1, 1, 0, 0], [0, 0, 0, 1, 0]])
   array([['Male', 1],
          [None, 2]], dtype=object)

   Methods
   -------

   .. py:method:: fit(X, y=None)

      Fit OneHotEncoder to ``X``.

      :param X: The data to determine the categories of each feature.
      :type X: array-like of shape ``(n_samples, n_features)``
      :param y: Ignored. This parameter exists only for compatibility.
      :type y: None
      :returns: **self** -- Fitted encoder.
      :rtype: object

   .. py:method:: fit_transform(X, y=None)

      Fit OneHotEncoder to ``X``, then transform ``X``.

      :param X: The data to encode.
      :type X: array-like of shape ``(n_samples, n_features)``
      :param y: Target values (default None).
      :type y: None
      :returns: **Xt** -- Transformed input.
      :rtype: {ndarray, sparse matrix}

   .. py:method:: get_feature_names_out(input_features=None)

      Get output feature names for transformation.

      :param input_features: String names for input features.
      :type input_features: array-like of str, default=None
      :returns: **feature_names_out** -- Transformed feature names.
      :rtype: ndarray of str objects

   .. py:method:: get_params(deep=True)

      Get parameters for this estimator.

      :param deep: If True, will return the parameters for this estimator and contained subobjects.
      :type deep: bool, default=True
      :returns: **params** -- Parameter names mapped to their values.
      :rtype: dict

   .. py:method:: inverse_transform(X)

      Convert the data back to the original categories.

      :param X: The transformed data matrix.
      :type X: {array-like, sparse matrix} of shape ``(n_samples, n_encoded_features)``
      :returns: **X_tr** -- Inverted original categories.
      :rtype: ndarray of shape ``(n_samples, n_features)``

   .. py:method:: set_params(**params)

      Set the parameters of this estimator.

      :returns: **self** -- Estimator instance.
      :rtype: object

   .. py:method:: transform(X)

      Transform ``X`` using one-hot encoding.

      :param X: The data to encode.
      :type X: array-like of shape ``(n_samples, n_features)``
      :returns: **Xt** -- Transformed input.
      :rtype: {ndarray, sparse matrix}
