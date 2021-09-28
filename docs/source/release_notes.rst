Release Notes
##################

The latest stable version of Snap ML is available at https://pypi.org/project/snapml/.

Snap ML v1.7.7 (July 21, 2021)
==============================

* Added support for A100 GPUs
* Fixed unit-tests that were failing on POWER systems when using multiple GPUs


Snap ML v1.7.6 (June 18, 2021)
==============================

* Relaxed numpy dependency to be >= 1.18.5


Snap ML v1.7.5 (June 17, 2021)
==============================

* Relaxed numpy dependency to be >= 1.19.0
* Added support for reading ONNX files generated on Z systems


Snap ML v1.7.4 (June 11, 2021)
==============================

* New and improved inference engine for tree-based ensembles
* Removed predict_proba from DecisionTreeRegressor and RandomForestRegressor
* Relaxed numpy dependency to be >= 1.19.2


Snap ML v1.7.3 (May 26, 2021)
==============================

* Pinned numpy dependency to 1.19.2


Snap ML v1.7.2 (May 26, 2021)
==============================

* Simplified the pre-trained model import API for Boosting Machines
* Fixed support for string labels at training/inference time
* Stop the train routine if the input dataset is empty by raising a ValueError
* Fixed issues related to the Windows build
* Fixed bug in single-record inference when fit_intercept=True (linear models)
* Unified code inference path for tree ensembles
* Added exception handling for OpenMP code


Snap ML v1.7.1 (May 17, 2021)
==============================

* Added multi-class classification support (Decision Trees and Random Forests)
* Fixed issue related to class weights and Logistic Regression
* Fixed issue with pickled boosting machine models


Snap ML v1.7.0 (February 22, 2021)
==================================

* Added Windows, MacOS, Linux/x86, Linux/PPC support
* Accelerated inference engine for tree ensembles
* Added support for importing pre-trained tree ensembles from PMML, XGBoost, LightGBM and ONNX
* Added a new ML algorithm: heterogeneous boosting machine model (for more details: https://proceedings.neurips.cc/paper/2020/file/7fd3b80fb1884e2927df46a7139bb8bf-Paper.pdf)
* Integrated Snap ML into Lale
* Added non-linear kernel support for linear models
* Added predict_proba to LogisticRegression in the multi-class case
* Added support for arbitrary class labels support for linear models
* Added feature importance for tree-based models
* Added support for cross_entropy loss for boosting machines
* Various bug fixes

Version 1.7.0 included already all the following Machine Learning models and solvers:

* Linear Regression: multi-threaded CPU, GPU, multi-GPU
* Logistic Regression: multi-threaded CPU, GPU, multi-GPU
* Support Vector Machine: multi-threaded CPU, GPU, multi-GPU
* Decision Tree: multi-threaded CPU, GPU
* Random Forest: multi-threaded CPU, GPU, multi-GPU
* Boosting Machine: multi-threaded CPU, GPU

