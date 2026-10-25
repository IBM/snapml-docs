snapml.preprocessing.TargetEncoder
==================================

.. py:class:: snapml.preprocessing.TargetEncoder(categories='auto', target_type='auto', smooth='auto', cv=5, shuffle=True, random_state=None)

   Target encoding for categorical features.

   Each category is encoded based on a shrunk estimate of the average target value for observations belonging to that category. The encoding is computed with cross-validation on the training set to prevent target leakage and overfitting.

   Parameters
   ----------
   categories : 'auto' or list of array-like, default='auto'
       Categories (unique values) per feature:

       * ``'auto'`` : Determine categories automatically from the training data.
       * ``list`` : ``categories[i]`` holds the categories expected of the ``i``-th column.

   target_type : {'auto', 'continuous', 'binary', 'multiclass'}, default='auto'
       Type of target. If 'auto', type is inferred from ``y``.

   smooth : 'auto' or float >= 0.0, default='auto'
       The amount of mixing of the category target average and the overall target average. A higher value leads to more regularisation towards the global mean.

   cv : int, default=5
       Determines the number of cross-validation folds used to encode the training data during :meth:`fit_transform`.

   shuffle : bool, default=True
       Whether to shuffle the data before splitting it into folds during :meth:`fit_transform`.

   random_state : int, RandomState instance or None, default=None
       Controls the pseudo-random generator used to shuffle the data.

   Attributes
   ----------
   categories_ : list of arrays
       The categories of each feature determined during fitting.

   encodings_ : list of ndarray
       Encodings learned for each feature category.

   target_mean_ : float
       The overall mean of the target.

   n_features_in_ : int
       Number of features seen during :meth:`fit`.

   feature_names_in_ : ndarray of shape (n_features_in_)
       Names of features seen during :meth:`fit`. Defined only when ``X`` has feature names that are all strings.

   See Also
   --------
   :class:`snapml.preprocessing.OrdinalEncoder` : Encode categorical features as an integer array.
   :class:`snapml.preprocessing.OneHotEncoder` : Encode categorical features as a one-hot numeric array.

   Examples
   --------
   >>> import numpy as np
   >>> from snapml.preprocessing import TargetEncoder
   >>> X = np.array([['dog'], ['cat'], ['dog'], ['dog'], ['cat']])
   >>> y = np.array([1, 0, 1, 0, 0])
   >>> enc = TargetEncoder(smooth='auto', cv=2, random_state=42)
   >>> enc.fit(X, y)
   TargetEncoder(cv=2, random_state=42)
   >>> Xt = enc.transform(np.array([['dog'], ['cat']]))
   >>> Xt
   array([[0.61538462],
          [0.11538462]])

   Methods
   -------

   .. py:method:: fit(X, y)

      Fit the TargetEncoder to ``X`` and ``y``.

      :param X: The data to determine the categories of each feature.
      :type X: array-like of shape ``(n_samples, n_features)``
      :param y: The target data.
      :type y: array-like of shape ``(n_samples)``
      :returns: **self** -- Fitted encoder.
      :rtype: object

   .. py:method:: fit_transform(X, y)

      Fit to data, then transform it using cross-validation.

      :param X: The data to encode.
      :type X: array-like of shape ``(n_samples, n_features)``
      :param y: Target data.
      :type y: array-like of shape ``(n_samples)``
      :returns: **Xt** -- Transformed input.
      :rtype: ndarray of shape ``(n_samples, n_features)``

   .. py:method:: get_params(deep=True)

      Get parameters for this estimator.

      :param deep: If True, will return the parameters for this estimator and contained subobjects.
      :type deep: bool, default=True
      :returns: **params** -- Parameter names mapped to their values.
      :rtype: dict

   .. py:method:: set_params(**params)

      Set the parameters of this estimator.

      :returns: **self** -- Estimator instance.
      :rtype: object

   .. py:method:: transform(X)

      Transform ``X`` using target encoding.

      :param X: The data to encode.
      :type X: array-like of shape ``(n_samples, n_features)``
      :returns: **Xt** -- Transformed input.
      :rtype: ndarray of shape ``(n_samples, n_features)``
