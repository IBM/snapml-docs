Installation Guide
##################

Snap ML can be installed using pip.

.. code-block:: bash

    pip install snapml

* Your pip version should be at least 19.3.
* We currently support Python 3.7, 3.8 and 3.9.
* The OpenMP runtime must also be installed on your system.

Complete instructions for all supported platforms are provided below.

Ubuntu
======

On Ubuntu we support Intel™ (x86_64), IBM Power™ (ppc64le) and IBM Z™ (s390x) architectures.

To install Snap ML:

.. code-block:: bash

    apt-get install -y libgomp1
    pip install snapml

In order to use GPU acceleration one should have CUDA 10.2 (or higher) installed.

If using IBM Z™ (s390x), please see addition notes :ref:`below<Znotes>`.

RHEL/CentOS
===========

On RHEL/CentOS we support Intel™ (x86_64), IBM Power™ (ppc64le) and IBM Z™ (s390x) architectures.

To install Snap ML:

.. code-block:: bash

    yum install -y libgomp
    pip install snapml    

In order to use GPU acceleration one should have CUDA 10.2 (or higher) installed.

If using IBM Z™ (s390x), please see addition notes :ref:`below<Znotes>`.

.. _Znotes:

IBM Z™ (s390x)
==============

While Snap ML provides binary wheels for s390x on PyPI, the dependencies of Snap ML (e.g., scipy, numpy, scikit-learn) do not.
It can take a long time to install from PyPI because these dependencies need to be compiled from source. 
Therefore, on s390x we recommend using Anaconda to install the dependencies and then install Snap ML from PyPI:

.. code-block:: bash

    conda create -n snapenv python=3.10 numpy scipy scikit-learn
    conda activate snapenv
    pip install snapml

MacOS
=====

On MacOS we support the Intel™ (x86_64) architecture.

To install Snap ML:

.. code-block:: bash

    brew install libomp
    pip install snapml

GPU acceleration is not currently supported on MacOS.

Please note that there are `known issues <https://github.com/dmlc/xgboost/issues/7039>`_ with libomp v12.0.0 on MacOS that lead to segfaults. 
For the time being, We recommend using libomp v11.1.0.


Windows
=======

On Windows we support the Intel™ (amd64) architecture.

To install Snap ML, one should firstly download and install the `Microsoft Visual C++ Redistributable for Visual Studio 2019 <https://aka.ms/vs/16/release/VC_redist.x64.exe>`_.
Next, install the Snap ML package via pip:

.. code-block:: bash

    pip install snapml

GPU acceleration is not currently supported on Windows.

