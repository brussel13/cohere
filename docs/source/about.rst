=====
About
=====

The Cohere package provides tools for phase retrieval of coherent diffraction data to images. It has been developed in the context of Bragg Coherent Diffraction Imaging (BCDI) with a focus on 3D data from rocking curve and energy scan coherent diffraction data of small crystalline objects. While application to 2D and 1D data is not gauranteed to work, there is intention to support such data and bugs will be squashed as they are found.

Cohere is divided into four source code packages.  The cohere_core is the computational API.  All of the operations of the processing workflow are defined in cohere_core and the execution of a defined phase retrieval workflow is done. A leading feature of cohere_core is that the algorithm codes are developed using an abstraction layer above specific computational toolkits. This allows the computaional library to be defined at run-time.  Adding a new library to cohere_core is done by defining the interface functions for cohere_core in the library.  Therefore, any algorithms that exist in cohere_core will immediately function with the new computational library.  Currently cohere_core supports numpy, cupy (nvidia GPU) and PyTorch (CPU/GPU). The cohere_core source code is contained within the cohere git repository and can installed from PyPi as cohere_core. 

The user interface to cohere_core is defined in the cohere_ui source package.  Cohere_ui defines the four basic operations of a complete, end-to-end, coherent diffraction phase retrieval workflow.  The beamline specific preprocessing steps are done on the raw data using the beamline_preprocess program.  Generic data preprocessing operations are executed in the standard_preprocessing program.  Phase retrieval is executed with run_reconstruction and generation of geometry corrected visualization and image proprocessing is managed by the beamline specific beamline_vizualization program.  Each of these steps is available as a stand alone program or the can be configured and executed through the provided GUI. A Jupyter Notebook interface is also included and is being slowly improved. The PyPi package cohere_ui is available for installation. 

The codes specific to individual instruments are contained in the cohere_beamlines source package. Code for reading and preprocessing raw data from specific beamline detectors, definitions of diffractometer circles, definitions of detector properties and geometric corrections to visualize images on orthogonal grids are provided in the separate beamline modules of the cohere_beamlines package.  Cohere_beamlines is currently used by the beamline_preprocessing and beamline_vizualization programs in the workflow, but they can also be imported into codes for specific algorithms that may have beamline specific considerations.  Beamline instruments are defined using the *xrayutilities* package notation and angle calculations are done using the *QConversion* module of *xrayutilities*. A non-exhaustive list of supported beamlines include APS 34-ID-C, APS 1-ID-E, PetraIII P10, ESRF ID01.



The reconstruction has very good performance, in particular when utilizing GPU. User has a choice to run on cpu or GPU by choosing the processing library. 
The solution offers parallel processing for fast reconstruction of multiple starting points.

A powerful feature that can deliver good reconstruction result offered by the cohere package is genetic algorithm (GA).

The tools are supplemented by another package cohere-ui which contains users scripts ready to use and easy to modify. 
Refer to :ref:`api_cohere_ui` for instructions on how to use the supplemental software. Combined together both of the packages: cohere_core and cohere_ui offer a full solution from beamline preprocessing data followed by standard preprocessing data, reconstruction, and beamline postprocessing that enables visualization of the results.
The cohere_core project handles standard preprocessing on beamline data that has appied instrument correction, and reconstruction. These processes apply to any beamline.
The beamline preprocessing, where the raw data is corrected for beamline specific instrument, and beamline postprocessing (visualization) are handled in cohere_ui suplemental project.
Currently cohere_ui supports the following beamlines: aps_1ide, aps_34idc, esrf_id01, Petra3_P10.  There are other beamlines that are not currently included in the repository, just ask us if you are looking for something.


Another supplemental package cohere_examples provides examples with configuration files and data for the supported beamlines.

The cohere is written in Python as this choice offers simplicity of development, and thus the tool can be expanded by community.
