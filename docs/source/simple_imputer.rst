snapml.preprocessing.SimpleImputer
==================================

.. py:class:: snapml.preprocessing.SimpleImputer(*, missing_values=numpy.nan, strategy='mean', fill_value=None, copy=True, add_indicator=False, keep_empty_features=False)

   Univariate imputer for completing missing values with simple strategies.

   Replace missing values using a provided fill value or using statistical measures (mean, median or most frequent) along each column in which the missing values are located.

   Parameters
   ----------
   missing_values : int, float, str, np.nan, None or pandas.NA, default=np.nan
       The placeholder for the missing values. All occurrences of ``missing_values`` will be imputed.

   strategy : str, default='mean'
       The imputation strategy:

       * ``'mean'`` : Replace missing values using the mean along each column. Can only be used with numeric data.
       * ``'median'`` : Replace missing values using the median along each column. Can only be used with numeric data.
       * ``'most_frequent'`` : Replace missing using the most frequent value along each column. Can be used with strings or numeric data.
       * ``'constant'`` : Replace missing values with ``fill_value``. Can be used with strings or numeric data.

   fill_value : str or numerical value, default=None
       When ``strategy='constant'``, ``fill_value`` is used to replace all occurrences of ``missing_values``. If None, ``fill_value`` will be 0 when imputing numerical data and "missing_value" for strings or object data types.

   copy : bool, default=True
       If True, a copy of ``X`` will be created. If False, imputation will be done in-place whenever possible.

   add_indicator : bool, default=False
       If True, a ``MissingIndicator`` transform will stack indicators onto the output of the imputer's transform.

   keep_empty_features : bool, default=False
       If True, features that consist of only missing values in the training data will be kept and filled with 0 for 'mean', 'median', 'most_frequent', or with ``fill_value`` for 'constant'.

   Attributes
   ----------
   statistics_ : array of shape (n_features)
       The imputation fill value for each feature.

   n_features_in_ : int
       Number of features seen during :meth:`fit`.

   feature_names_in_ : ndarray of shape (n_features_in_)
       Names of features seen during :meth:`fit`. Defined only when ``X`` has feature names that are all strings.

   See Also
   --------
   :class:`snapml.preprocessing.Normalizer` : Normalize samples individually to unit norm.

   Examples
   --------
   >>> import numpy as np
   >>> from snapml.preprocessing import SimpleImputer
   >>> imp = SimpleImputer(missing_values=np.nan, strategy='mean')
   >>> X = [[1, 2], [np.nan, 3], [7, 6]]
   >>> imp.fit(X)
   SimpleImputer()
   >>> X_test = [[np.nan, 2], [6, np.nan], [7, 6]]
   >>> imp.transform(X_test)
   array([[4.        , 2.        ],
          [6.        , 3.66666667],
          [7.        , 6.        ]])

   Methods
   -------

   .. py:method:: fit(X, y=None)

      Fit the imputer on ``X``.

      :param X: Input data, where ``n_samples`` is the number of samples and ``n_features`` is the number of features.
      :type X: {array-like, sparse matrix} of shape ``(n_samples, n_features)``
      :param y: Ignored.
      :type y: None
      :returns: **self** -- Fitted imputer.
      :rtype: object

   .. py:method:: fit_transform(X, y=None)

      Fit to data, then transform it.

      :param X: Input data of shape ``(n_samples, n_features)``.
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

   .. py:method:: get_params(deep=True)

      Get parameters for this estimator.

      :param deep: If True, will return the parameters for this estimator and contained subobjects.
      :type deep: bool, default=True
      :returns: **params** -- Parameter names mapped to their values.
      :rtype: dict

   .. py:method:: inverse_transform(X)

      Convert the data back to the original representation.

      :param X: The transformed data matrix.
      :type X: {array-like, sparse matrix} of shape ``(n_samples, n_features)``
      :returns: **X_tr** -- Inverted original data.
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

      Impute all missing values in ``X``.

      :param X: The input data to complete.
      :type X: {array-like, sparse matrix} of shape ``(n_samples, n_features)``
      :returns: **Xt** -- Imputed data.
      :rtype: {ndarray, sparse matrix}
