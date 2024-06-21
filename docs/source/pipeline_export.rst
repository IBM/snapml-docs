Preprocessing Pipeline Export
==============================

Snap ML now has the capability to export scikit-learn prepreprocessing pipelines to a JSON format.
This format is then consuamble by `IBM Z Accelerated for NVIDIA Triton Inference Sever™ <https://github.com/IBM/ibmz-accelerated-for-nvidia-triton-inference-server>`_.

The export function handles pipelines for numerical and categorical features separately (see example below). 

For numerical features, we currently support the following preprocessing steps and hyper-parameters:

.. code-block:: python

    sklearn.preprocessing.Normalizer()

    sklearn.preprocessing.KBinsDiscretizer(
        encode="ordinal"
    )

    sklearn.preprocessing.FunctionTransformer(
        func=np.log1p
    )

And for categorical features, we currently support the following preprocessing steps and hyper-parameters:

.. code-block:: python

    sklearn.preprocessing.OneHotEncoder(
        categories="auto", 
        sparse_output=False, 
        handle_unknown="ignore"
    )

An example of using the export function is given below:

.. code-block:: python

    from sklearn.pipeline import Pipeline
    from sklearn.compose import ColumnTransformer
    from snapml import export_preprocessing_pipeline

    num_trsf = Pipeline(
        steps=[
            ('normalizer', Normalizer()), 
            ('discretizer', KBinsDiscretizer(encode="ordinal"))
        ]
    )
    cat_trsf = Pipeline(
        steps=[
            ('onehot', OneHotEncoder(categories='auto', sparse=False)
        )])
    preprocessor = ColumnTransformer(
        transformers=[ 
            ('num', num_trsf, [2,3]), 
            ('cat', cat_trsf, [0,1])
        ], 
        remainder='passthrough'
    )
    pipeline = Pipeline(
        steps=[ 
            ('prep', preprocessor), 
            ('classifier', model)
        ]
    )
    pipeline.fit(X,y)
    
    # export preprocessing pipeline to json format
    export_preprocessing_pipeline(
        pipeline['prep'], 'pipeline.json'
    )

