snapml.preprocessing.LabelEncoder
=================================

.. py:class:: snapml.preprocessing.LabelEncoder()

   Encode target labels with value between 0 and n_classes-1.

   It can be used to normalize labels (such as string target labels in classification) to integer values.

   Parameters
   ----------
   This transformer accepts no initialization parameters.

   Attributes
   ----------
   classes_ : ndarray of shape (n_classes)
       Holds the label for each class seen during :meth:`fit`.

   See Also
   --------
   :class:`snapml.preprocessing.OrdinalEncoder` : Encode categorical features using an ordinal integer scheme.
   :class:`snapml.preprocessing.OneHotEncoder` : Encode categorical features using a one-hot scheme.

   Examples
   --------
   >>> from snapml.preprocessing import LabelEncoder
   >>> le = LabelEncoder()
   >>> le.fit(["paris", "paris", "tokyo", "amsterdam"])
   LabelEncoder()
   >>> list(le.classes_)
   ['amsterdam', 'paris', 'tokyo']
   >>> le.transform(["tokyo", "tokyo", "paris"])
   array([2, 2, 1])
   >>> list(le.inverse_transform([2, 2, 1]))
   ['tokyo', 'tokyo', 'paris']

   Methods
   -------

   .. py:method:: fit(y)

      Fit label encoder to target labels ``y``.

      :param y: Target values.
      :type y: array-like of shape ``(n_samples)``
      :returns: **self** -- Fitted encoder.
      :rtype: object

   .. py:method:: fit_transform(y)

      Fit label encoder and return encoded labels.

      :param y: Target values.
      :type y: array-like of shape ``(n_samples)``
      :returns: **y_enc** -- Encoded labels.
      :rtype: ndarray of shape ``(n_samples)``

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

   .. py:method:: inverse_transform(y)

      Transform labels back to original encoding.

      :param y: Target values.
      :type y: array-like of shape ``(n_samples)``
      :returns: **y_orig** -- Original labels.
      :rtype: ndarray of shape ``(n_samples)``

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

   .. py:method:: transform(y)

      Transform labels to normalized encoding.

      :param y: Target values.
      :type y: array-like of shape ``(n_samples)``
      :returns: **y_enc** -- Encoded labels.
      :rtype: ndarray of shape ``(n_samples)``
