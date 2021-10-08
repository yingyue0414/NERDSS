.. Continuum membrane model documentation master file, created by 
   M. Ying on Oct. 7, 2021.

Documentation for NERDSS - Continuum Membrane
=============================================

Continuum membrane is tool in NERDSS to extend the scope of the model to non-linear membranes established with triangular mesh and optimized using and energy function. 

Installation
------------

Continuum membrane is included in NERDSS. Please refer to `User guide`_ for NERDSS.

Compile Continuum Membrane
--------------------------
The code of continuum membrane model is programmed in C++ with Armadillo library and parallelization OpenMP.

The main code is ‘continuummodel_maincode.cpp’, and ‘funcitons_file1.cpp’ and ‘functions_file2.cpp’ list all the functions this membrane utilize. Specifically, the functions for setting up triangular mesh are listed ‘functions_file2.cpp’, and the functions for calculating the system energy and the vertex force are defined in ‘functions_file1.cpp’.

To compile the file:
.. code::
   g++ continuummodel_maincode.cpp -larmadillo -fopenmp -o out
Then to run the code:
.. code::
   ./out

Cite Continuum Membrane
-----------------------

If you use or modify continuum membrane model, in addition to citing NERDSS, please be kind and cite us:

1. Continuum Membrane Implementation
Fu, Y., Yogurtcu, O.N., Kothari, R., Thorkelsdottir, G., Sodt, A.J. & Johnson, M.E. (2019) An implicit lipid model for efficient reaction-diffusion simulations of protein binding to surfaces of arbitrary topology. *J Chem Phys.* 151 (12), 124115. doi:`10.1063/1.5120516`_

2. Membrane energies and insertion
Fu, Y., Zeno, W., Stachowiak, J. & Johnson, M.E. A continuum membrane model predicts curvature sensing by helix insertion. Submitted (2021) Available on bioRxiv:`https://www.biorxiv.org/content/10.1101/2021.04.22.440963v1.full`_

.. _`User guide`: https://github.com/mjohn218/NERDSS/blob/master/NERDSS_USER_GUIDE.pdf
