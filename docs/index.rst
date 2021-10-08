.. Continuum membrane model documentation master file, created by 
   M. Ying on Oct. 7, 2021.

Documentation for NERDSS - Continuum Membrane
=============================================

Continuum membrane is tool in NERDSS to extend the scope of the model to non-linear membranes established with triangular mesh and optimized using and energy function. 

Installation
------------

Continuum membrane is included in NERDSS. Please refer to `User guide`_ for NERDSS. Additional dependencies for continuum membrane model are:

#. C++ 11
#. `Armadillo`_ (linear algebra package)
#. OpenMP (only required in need of parallelization)

Compile Continuum Membrane
--------------------------
The main code of continuum membrane model is ‘continuummodel_maincode.cpp’. ‘funcitons_file1.cpp’ and ‘functions_file2.cpp’ list all the functions utilized by the model membrane. Specifically, the functions for setting up triangular mesh are listed ‘functions_file2.cpp’. The functions for calculating the system energy and the vertex force are defined in ‘functions_file1.cpp’.

Use the following code to compile the file. Note 'output_file' can be renamed accordingly.

.. code-block:: console

   g++ continuummodel_maincode.cpp -larmadillo -fopenmp -o output_file

* if parallelization is not needed:

   .. code-block:: console
   
      g++ continuummodel_maincode.cpp -larmadillo -o output_file
      
* if multiple verision of C++ is installed, to specify C++ version:

   .. code-block:: console
   
      g++ continuummodel_maincode.cpp --std=c++11 -larmadillo -o output_file

   
Then to run the code:

.. code-block:: console

   ./output_file

Cite Continuum Membrane
-----------------------

If you use or modify continuum membrane model, in addition to citing NERDSS, please be kind and cite us:

1. Continuum Membrane Implementation
Fu, Y., Yogurtcu, O.N., Kothari, R., Thorkelsdottir, G., Sodt, A.J. & Johnson, M.E. (2019) An implicit lipid model for efficient reaction-diffusion simulations of protein binding to surfaces of arbitrary topology. *J Chem Phys.* 151 (12), 124115. doi:`10.1063/1.5120516`_

2. Membrane energies and insertion
Fu, Y., Zeno, W., Stachowiak, J. & Johnson, M.E. A continuum membrane model predicts curvature sensing by helix insertion. Submitted (2021) Available on `bioRxiv`_

.. _`User guide`: https://github.com/mjohn218/NERDSS/blob/master/NERDSS_USER_GUIDE.pdf
.. _`Armadillo`: http://arma.sourceforge.net/
.. _`10.1063/1.5120516`: https://pubmed.ncbi.nlm.nih.gov/31575182/
.. _`bioRxiv`: https://www.biorxiv.org/content/10.1101/2021.04.22.440963v1.full
