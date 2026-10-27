snapml.preprocessing.OrdinalEncoder
===================================

.. py:class:: snapml.preprocessing.OrdinalEncoder(*, categories='auto', dtype=numpy.float64, handle_unknown='error', unknown_value=None, encoded_missing_value=numpy.nan, min_frequency=None, max_categories=None)

   Encode categorical features as an integer array.

   The input to this transformer should be an array-like of integers or strings, denoting the values taken on by categorical (discrete) features. The features are converted to ordinal integers. This results in a single column of integers (0 to n_categories - 1) per feature.

   Parameters
   ----------
   categories : 'auto' or list of array-like, default='auto'
       Categories (unique values) per feature:

       * ``'auto'`` : Determine categories automatically from the training data.
       * ``list`` : ``categories[i]`` holds the categories expected of the ``i``-th column. The passed categories should not mix strings and numeric values, and should be sorted in case of numeric values.

   dtype : number type, default=np.float64
       Desired dtype of output.

   handle_unknown : {'error', 'use_encoded_value'}, default='error'
       When set to ``'error'``, an error will be raised in case an unknown categorical feature is present during transform. When set to ``'use_encoded_value'``, the encoded value of unknown categories will be set to the value given for the parameter ``unknown_value``.

   unknown_value : int or np.nan, default=None
       The value used to encode unknown categories. Required if ``handle_unknown='use_encoded_value'``.

   encoded_missing_value : int or np.nan, default=np.nan
       Encoded value of missing categories.

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

   n_features_in_ : int
       Number of features seen during :meth:`fit`.

   feature_names_in_ : ndarray of shape (n_features_in_)
       Names of features seen during :meth:`fit`. Defined only when ``X`` has feature names that are all strings.

   See Also
   --------
   :class:`snapml.preprocessing.OneHotEncoder` : Performs a one-hot encoding of categorical features.
   :class:`snapml.preprocessing.LabelEncoder` : Encodes target labels with value between 0 and n_classes-1.
   :class:`snapml.preprocessing.TargetEncoder` : Encodes categorical features using target values.

   Examples
   --------
   >>> from snapml.preprocessing import OrdinalEncoder
   >>> enc = OrdinalEncoder()
   >>> X = [['Male', 1], ['Female', 3], ['Female', 2]]
   >>> enc.fit(X)
   OrdinalEncoder()
   >>> enc.categories_
   [array(['Female', 'Male'], dtype=object), array([1, 2, 3], dtype=object)]
   >>> enc.transform([['Female', 3], ['Male', 1]])
   array([[0., 2.],
          [1., 0.]])
   >>> enc.inverse_transform([[1, 0], [0, 1]])
   array([['Male', 1],
          ['Female', 2]], dtype=object)

   Methods
   -------

   .. py:method:: fit(X, y=None)

      Fit the OrdinalEncoder to ``X``.

      :param X: The data to determine the categories of each feature.
      :type X: array-like of shape ``(n_samples, n_features)``
      :param y: Ignored. This parameter exists only for compatibility.
      :type y: None
      :returns: **self** -- Fitted encoder.
      :rtype: object

   .. py:method:: fit_transform(X, y=None)

      Fit to data, then transform it.

      :param X: The data to encode.
      :type X: array-like of shape ``(n_samples, n_features)``
      :param y: Target values (default None).
      :type y: None
      :returns: **Xt** -- Transformed input.
      :rtype: ndarray of shape ``(n_samples, n_features)``

   .. py:method:: get_feature_names_out(input_features=None)

      Get output feature names for transformation.

      :param input_features: Input features. If None, feature names seen during :meth:`fit` are used.
      :type input_features: array-like of str or None, default=None
      :returns: **feature_names_out** -- Transformed feature names.
      :rtype: ndarray of str objects

   .. py:method:: get_params(deep=True)

      Get parameters for this estimator.

      :param deep: If True, will return the parameters for this estimator and contained subobjects.
      :type deep: bool, default=True
      :returns: **params** -- Parameter names mapped to their values.
      :rtype: dict

   .. py:method:: inverse_transform(X)

      Convert the data back to the original representation.

      :param X: The transformed data matrix.
      :type X: array-like of shape ``(n_samples, n_features)``
      :returns: **X_tr** -- Inverted original categories.
      :rtype: ndarray of shape ``(n_samples, n_features)``

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

      Transform ``X`` to ordinal integers.

      :param X: The data to encode.
      :type X: array-like of shape ``(n_samples, n_features)``
      :returns: **Xt** -- Transformed input.
      :rtype: ndarray of shape ``(n_samples, n_features)``
