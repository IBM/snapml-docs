Release Notes
##################

The latest stable version of Snap ML is available at https://pypi.org/project/snapml/.

Snap ML v1.15.6 (Apr. 23, 2024)
=================================

Bug fixes:

- Fix concurrency issue during load testing in TIS.

Snap ML v1.15.5 (Apr. 5, 2024)
=================================

Features:

- Support for importing and exporting multi-class boosting models.

Bug fixes:

- Fix memory layout for `GraphFeaturePreprocessor`.
- `OneHotEncoder`: use `sparse_output` rather than `sparse`.

Snap ML v1.15.4 (Feb. 7, 2024)
=================================

Bug fixes:

- Support gRPC input buffers for pre-processing.

Snap ML v1.15.3 (Jan. 15, 2024)
=================================

Bug fixes:

- Core dump using pre-processed data for prediction.

Snap ML v1.15.2 (Jan. 8, 2024)
=================================

Bug fixes:

- Extended `AnyDataset` public API to get number of examples.

Snap ML v1.15.1 (Dec. 20, 2023)
=================================

Bug fixes:

- Missing symbols in libsnapmlcore.so when using the Snap ML C++ API for preprocessing.

Snap ML v1.15.0 (Dec. 12, 2023)
=================================

New feature:

- Support for accelerated pre-processing at C++ level.

Snap ML v1.14.6 (Apr. 11, 2024)
=================================

Bug fixes:

- Fix issue with feature importances for some estimators.

Snap ML v1.14.5 (Dec. 12, 2023)
=================================

Bug fixes:

- Raise exception when no features can be parsed from PMML file.

Snap ML v1.14.4 (Nov. 29, 2023)
=================================

Bug fixes:

- PMML import: support for scikit-learn models trained in 32-bit precision.

Snap ML v1.14.3 (Nov. 29, 2023)
=================================

Bug fixes:

- `GenericTreeEnsemble` exposes model schema after import.

Snap ML v1.14.2 (Oct. 19, 2023)
=================================

New features:

- New `GenericTreeEnsemble` C++ API.

Bug fixes:

- Fix bug when using `std::vector` input to `snapml::DenseDataset`.
- Fix segfault for `MBITreeEnsemble`.
- Fix hanging for SVM with RBF kernel on IBM Power™ architecture.

Snap ML v1.14.1 (Jul. 23, 2023)
=================================

New features:

- Add Python 3.11 support and drop support for Python 3.7 (EOL).
- Support for quantile loss in `BoostingMachineRegressor`. 
- Updates for Graph Preprocessor.

Bug fixes:

- Ensure thread safety in C++ API.

Packaging:

- In this release we switch to distributing `manylinux_2_28` wheels for all Linux platforms.

Snap ML v1.14.0 (May 3, 2023)
=================================

Bug fixes:

- Fix incorrect predictions with `zdnn_tensors` in certain cases.

Packaging:

- Wheels for `s390x` are now built using `manylinux_2_28`.

Snap ML v1.13.2 (Jan. 15, 2024)
=================================

Bug fixes:

- Fix issue with missing feature importances for decision trees and random forests.

Snap ML v1.13.1 (Oct. 24, 2023)
=================================

Bug fixes:

- Fix hanging for SVM with RBF kernel on IBM Power™ architecture.

Snap ML v1.13.0 (Mar. 23, 2023)
=================================

New features:

- C++ API (e.g., headers + shared library) is now packaged within the Snap ML wheel.
- Compressed tree ensembles now support multi-class classification.

Snap ML v1.12.1 (Mar. 22, 2023)
=================================

Bug fixes:

- Overflow issue for dense datasets.

Snap ML v1.12.0 (Jan. 31, 2023)
=================================

New features:

- Further improved inference engine for tree ensembles on IBM z16™ AI accelerator.
- Support for Poisson regression loss in boosting machines.

Bug fixes:

- :class: `BatchedTreeEnsemble`: handle case when some classes are not present in batch.
- Various documentation improvements.

Snap ML v1.11.1 (Nov. 29, 2022)
=================================

Documentation:

- Updated the documentation of the GraphFeaturePreprocessor class

Snap ML v1.11.0 (Nov. 22, 2022)
=================================

New features:

- Added :class:`GraphFeaturePreprocessor` that enables scalable and real-time feature extraction from graph-structured data.

Snap ML v1.10.2 (Nov. 18, 2022)
=================================

API changes:

- When using the generic import_model function, if the IBM z16™ AI accelerator is detected, we set the number of CPU threads automatically based on the detected number of cores.

Bug fixes:

- Supporting a larger variety of compression types applied to disjoint tree sets within the same ensemble.

Snap ML v1.10.1 (Nov. 3, 2022)
=================================

Bug fixes:

- Fix segfault when scoring certain PMML files.

Snap ML v1.10.0 (Oct. 26, 2022)
=================================

New features:

- Significantly improved inference engine for tree ensembles on IBM z16™ AI accelerator.
- Automatic selection of zdnn_tensors vs. compress_trees based on hardware availability.


Snap ML v1.9.7 (Oct. 25, 2022)
=================================

Bug fixes:

- Raise exception when importing PMML that contains no trees.

Snap ML v1.9.6 (Oct. 20, 2022)
=================================

Packaging changes:

- Make numpy dependency conditional on Python version.


Snap ML v1.9.5 (Oct. 7, 2022)
=================================

Bug fixes:

- Attribute :attr:`used_features_` lists features in the same order that they appear in :attr:`schema_` attribute.


Snap ML v1.9.4 (Sep. 24, 2022)
=================================

New features:

- Populate :attr:`schema_` attribute when importing PPML models via generic import API.
- Python 3.10 support.

Bug fixes:

- Remove NUMA-related warnings when the machine does not have any NUMA nodes configured.
- Fix bug during pre-processing for compressed decision trees.
- Fix various issue with caching and pickling tree ensemble models.

Snap ML v1.9.3 (Sep. 9, 2022)
=================================

Performance improvements:

- Tree ensemble inference now leverages vector instructions on IBM Power™ systems.

Snap ML v1.9.2 (Aug. 31, 2022)
=================================

Bug fixes:
    - Fix issue with binary incompatibility between Linux/MacOS and Windows.
    - BoostingMachine: Fix overflow issue for heterogeneous ensembles on very large data.
    - MultiOutputCalibratedClassifier: support for RBF kernels.
    - BatchedTreeEnsemble: better handling of default SnapRandomForest.
    - BatchedTreeEnsemble: add base_score calculation.
    - BatchedTreeEnsemble: support calling partial_fit after fit.
    - ModelImport: improved error handling.
    - GeneralizedLinearModels: fix issue with RBFSampler transform function on s390x.

API changes:
    - Added generic :func:`import_model` function that can detect the ensemble and type task from the PMML file.
    - Added option :attr:`remap_feature_indices` to score imported models using only the features that are listed in the model file.

Snap ML v1.9.1 (May 31, 2022)
=================================

New features:
    - New export_model method for RandomForest[Classifier/Regressor] and BoostingMachine[Classifier/Regressor].

Bug fixes:
    - Support importing ensembles from PMML that were trained using sample weights.
    - Fix reference counting for PyNone.
    - Improved memory management for inference engine on IBM z16™ AI accelerator.

API changes:
    - Expose import_model method in BoostingMachine[Classifier/Regressor].
    - Expose optimize_trees method in RandomForest[Classifier/Regressor] and BoostingMachine[Classifier/Regressor].

Snap ML v1.9.0 (Apr. 1, 2022)
=================================

New features:

- New matrix-based algorithms for tree-ensemble inference using zDNN library (available for IBM z16™ systems only).

Snap ML v1.8.12 (Oct. 28, 2022)
=================================

Bug fixes:

- BatchedTreeEnsemble: handle case when some classes are not present in batch.

Snap ML v1.8.11 (Oct. 18, 2022)
=================================

Packaging changes:

- Make numpy dependency conditional on Python version.

Snap ML v1.8.10 (Sep. 15, 2022)
=================================

Features:

- Python 3.10 support.

Bug fixes:

- Do not print NUMA warnings on machines where no NUMA nodes are configured.

Packaging notes:

- Linux/x86 wheels are now built with manylinux2014 platform tag (manylinux2010 reached EOL in 2020).
- Runtime numpy dependency is now numpy>=1.21.3 since this is the oldest release that supports Python 3.7, 3.8, 3.9 and 3.10.

Snap ML v1.8.9 (Aug. 11, 2022)
=================================

Bug-fixes:

- Fix overflow issue for heterogeneous BoostingMachines on very large data.
- Support for RBF kernels in MultiOutputCalibratedClassifier. 

Snap ML v1.8.8 (Jul. 20, 2022)
=================================

Bug-fixes:

- Better handling of default SnapRandomForest inside BatchedTreeEnsemble.

Snap ML v1.8.7 (Jun. 20, 2022)
=================================

Bug-fixes:

- Improved classes logic in BatchedTreeEnsemble.

Snap ML v1.8.6 (Jun. 16, 2022)
=================================

Bug-fixes: 

- Add base score computation to BatchedTreeEnsemble.
- Fix issue with binary incompatibility between Linux/MacOS and Windows.

Snap ML v1.8.5 (Apr. 22, 2022)
=================================

Bug-fixes:

- BatchedTreeEnsemble: call to fit is now equivalent to calling partial_fit on first batch.

Snap ML v1.8.4 (Feb. 24, 2022)
=================================

Bug-fixes:

- Fix bug with string labels in BoostingMachine.
- Fix bug with overflow in RBFSampler.
- Fix bug related to compressed ensembles of variable depth.
- Fix bug related to number of features-based optimization in compressed ensemble.

New features:

- ExtraTrees support in inference engine.
- New features for knowledge distillation.

Perf. improvements:

- Training performance improvement for all tree-based models.

Snap ML v1.8.3 (Dec. 10, 2021)
=================================

API changes:

- Added option to enable/disable optimized inference for MultiOutputCalibratedClassifier

Bug-fixes:

- MultiOutputCalibratedClassifier now returns self

Snap ML v1.8.2 (Dec. 7, 2021)
=================================

Bug fixes:

- Fix segfault for cross entropy loss and early stopping
- Fix issue with class weights and BoostingMachineClassifier


Snap ML v1.8.1 (Dec. 2, 2021)
=================================

New Features:

- Support for older machines that do not have AVX2 instructions.
- New MultiOutputCalibratedClassifier estimator.
- SVM: support for squared hinge loss and shrinkage.
- Support np.memmap as input for GLMs.

API Changes:

- Added fit function to BatchedTreeEnsemble classes.

Dependency Changes:

- Compile against numpy==1.19.3, to support numpy>=1.18.5 at runtime.

Bug-fixes:

- Correct class label predictions when importing RF/XGB models.
- Fix issue when deepcopying estimators that were not yet fitted.
- Fix documentation in BoostingMachineClassifier.

Snap ML v1.8.0 (Nov. 11, 2021)
==================================

New Features:

* Python 3.9 support (Python 3.6 is no longer supported).
* Accelerated scoring of random forest models trained in scikit-learn via PMML or ONNX import.
* Faster tree ensemble inference.
* Support for multiclass classification in BoostingMachineClassifier.
* Feature importance for boosting machines.
* New estimators to support batched training of tree ensembles on very large datasets.

API Changes:

* Setter functions are provided for all estimators to change parameters for training and inference.
* Deprecated setting n_jobs at inference time as argument to predict.
* Expose intercept attribute for GLMs.
* Reorganization of Booster parameters.

Bug-fixes:

* Enforce user-specific n_jobs for multiclass SVM.
* Fixed PY_SSIZE_T_CLEAN warnings for newer versions of Python.
* Fixed bug when serializing compressed trees in heterogeneous ensemble.
* Fixed race condition for exact regression trees.
* Fixed segfault when calling decision_function for multiclass SVM.
* Fixed memory issue for boosting machines with subsample<1.

Snap ML v1.7.8 (Nov. 19, 2021)
==================================

Bug-fixes:

* Support older machines that do not have AVX2 instructions.

Snap ML v1.7.7 (Jul. 21, 2021)
==============================

* Added support for A100 GPUs
* Fixed unit-tests that were failing on IBM Power™ systems when using multiple GPUs


Snap ML v1.7.6 (Jun. 18, 2021)
==============================

* Relaxed numpy dependency to be >= 1.18.5


Snap ML v1.7.5 (Jun. 17, 2021)
==============================

* Relaxed numpy dependency to be >= 1.19.0
* Added support for reading ONNX files generated on IBM Z™ systems


Snap ML v1.7.4 (Jun. 11, 2021)
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


Snap ML v1.7.0 (Feb. 22, 2021)
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

