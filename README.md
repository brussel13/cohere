[![Documentation Status](https://readthedocs.org/projects/cohere/badge/?version=latest)](http://cohere.readthedocs.io/en/latest/?badge=latest)

Project home page: [https://cohere.readthedocs.io/](https://cohere.readthedocs.io/)

The Cohere package provides tools for phase retrieval of coherent diffraction data to images. It has been developed in the context of Bragg Coherent Diffraction Imaging (BCDI) with a focus on 3D data from rocking curve and energy scan coherent diffraction data of small crystalline objects. While application to 2D and 1D data is not gauranteed to work, there is intention to support such data and bugs will be squashed as they are found.

Cohere is divided into four source code packages.  The cohere_core is the computational API.  All of the operations of the processing workflow are defined in cohere_core and a defined phase retrieval workflow is executed. A leading feature of cohere_core is that the algorithm codes are developed using an abstraction layer above specific computational toolkits. This allows the computaional library to be defined at run-time.  Adding a new library to cohere_core is done by defining the interface functions for cohere_core using the new library.  Therefore, any algorithms that exist in cohere_core will immediately function with the new computational library.  Currently cohere_core supports numpy, cupy (nvidia GPU) and PyTorch (CPU/GPU). The reconstruction has very good performance, in particular when utilizing GPU. The solution offers concurrent processing for fast reconstruction of multiple starting points. The cohere_core source code is contained within the cohere git repository and can installed from PyPi as cohere_core. 

The user interface to cohere_core is defined in the cohere_ui source package.  Cohere_ui defines the four basic operations of a complete, end-to-end, coherent diffraction phase retrieval workflow.  The beamline specific preprocessing steps are done on the raw data using the beamline_preprocess program.  Generic data preprocessing operations are executed in the standard_preprocessing program.  Phase retrieval is executed with run_reconstruction and generation of geometry corrected visualization and image proprocessing is managed by the beamline specific beamline_vizualization program.  Each of these steps is available as a stand alone program or the can be configured and executed through the provided GUI. Individual steps can be skipped or  A Jupyter Notebook interface is also included and is being slowly improved. The PyPi package cohere_ui is available for installation. 

The codes specific to individual instruments are contained in the cohere_beamlines source package. Code for reading and preprocessing raw data from specific beamline detectors, definitions of diffractometer circles, definitions of detector properties and geometric corrections to visualize images on orthogonal grids are provided in the separate beamline modules of the cohere_beamlines package.  Cohere_beamlines is currently used by the beamline_preprocessing and beamline_vizualization programs in the workflow, but they can also be imported into codes for specific algorithms that may have beamline specific considerations.  Beamline instruments are defined using the *xrayutilities* package notation and angle calculations are done using the *QConversion* module of *xrayutilities*. A non-exhaustive list of supported beamlines include APS 34-ID-C, APS 1-ID-E, PetraIII P10, ESRF ID01.

Finally, a set of example datasets are included in the cohere_examples repository. These are full data sets, in their raw form from the beamlines, and include resonable cohere configurations to process the data through all for steps of the cohere workflow.

Important features:
- Genetic Algorithm (GA) - powerful feature that can deliver good reconstruction result by using GA principles. Based on research "Three-dimensional imaging of dislocation propagation during crystal growth and dissolution, Supplementary Information" by Jesse N. Clark et. al.
- Artificial Intelligence initial guess for reconstruction - uses AI to find reconstructed object that is subsequently used as input to further reconstruction. The work is built on the research by Yudong Yao, et. al: "AutoPhaseNN: Unsupervised Physics-aware Deep Learning of 3D Nanoscale Bragg Coherent Diffraction Imaging". 
A trained model must be provided when using this feature. User can download trained model by clicking the following link
https://g-29c18.fd635.8443.data.globus.org/cherukara/cohere-trained_model.hdf5
- AutoAlien1 algorithm - a method to remove aliens by automatic means during standard data preprocessing. Based on work "Removal of spurious data in Bragg coherent diffraction imaging: an algorithm for automated data preprocessing" by Kenley Pelzer et. al.
- Multipeak - support for an experiment where data is collected for adjacent peaks simultaneously and reconstructing this multipeak scenario. The research is in experimental stage. Implemented by Jason (Nick) Porter.
- chrono CDI - allows the oversampling requirement at each time step to be reduced. The increased time resolution will allow imaging of faster dynamics and of radiation-dose-sensitive samples. Based on work "Coherent diffractive imaging of time-evolving samples with improved temporal resolution" by A. Ulvestat et. al.


Author(s)

Barbara Frosik - Principal Software Engineer at Argonne National Laboratory

Ross Harder - Scientist at Argonne National Laboratory

License

Copyright (c) UChicago Argonne, LLC. All rights reserved. See LICENSE file.
