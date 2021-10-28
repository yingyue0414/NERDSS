.. Continuum membrane model documentation master file, created by 
   M. Ying on Oct. 7, 2021.

Documentation for NERDSS - Continuum Membrane
=============================================

Continuum membrane is tool in NERDSS to extend the scope of the model to non-linear membranes established with triangular mesh and optimized using and energy function. 

1. Installation
------------

Continuum membrane is included in NERDSS. Please refer to `User guide`_ for NERDSS. Additional dependencies for continuum membrane model are:

#. C++ 11
#. `Armadillo`_ (linear algebra package)
#. OpenMP (only required in need of parallelization)

2. Compile Continuum Membrane
--------------------------
The main code of continuum membrane model is ``continuummodel_maincode.cpp``. ``funcitons_file1.cpp`` and ``functions_file2.cpp`` list all the functions utilized by the model membrane. Specifically, the functions for setting up triangular mesh are listed ``functions_file2.cpp``. The functions for calculating the system energy and the vertex force are defined in ``functions_file1.cpp``.

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

3. Input Parameters
----------------------

The input file is ``continuum_membrane/input.params``. Parameters are broken down to geometric parameters, physical properties, insertion mode, and advanced parameters.

+==================================================+==================================================================================+
| Parameter                                        | Description                                                                      |
+==================================================+==================================================================================+
| Geometric  | ``lMeshSide``                       | Target side length of the triangular mesh (nm).                                  |
| Parameters |                                     | This only servers as a reference scale.                                          |
|            |                                     | The mesh side length set up by the algorithm may vary.                           |
|            +--------------+----------------------+----------------------------------------------------------------------------------+
|            | Sphere model | ``isSphere``         | Set ``true`` to enable sphere mode.                                              |
|            |              +----------------------+----------------------------------------------------------------------------------+
|            |              | ``rSphere``          | Target radius of sphere (nm).                                                    |
|            |              |                      | This is the radius of spherical frame to set up the triangular mesh.             |
|            |              |                      | The radius of the resulting membrane represented by the triangular mesh may vary |
+------------+--------------+----------------------+----------------------------------------------------------------------------------+
| Physical   | ``c0Insertion``                     | Curvature of the membrane at the insertion area.                                 |
| Properties +-------------------------------------+----------------------------------------------------------------------------------+
|            | ``c0Membrane``                      | Spontaneous curvature of the membrane.                                           |
|            +-------------------------------------+----------------------------------------------------------------------------------+
|            | ``kcMembraneBending``               | Membrane bending constant in the energy function (pN*nm).                        |
|            +-------------------------------------+----------------------------------------------------------------------------------+
|            | ``usMembraneStretching``            | Membrane streching modulus in the energy function (pN/nm).                       |
|            +-------------------------------------+----------------------------------------------------------------------------------+
|            | ``uvVolumeConstraint``              | Volume constraint coefficient in the energy function (pN/nm^2).                  |
+------------+-------------------------------------+----------------------------------------------------------------------------------+
| Insertion  | ``isInsertionIncluded``             | Set ``true`` to include insertion.                                               |
| Mode       +-------------------------------------+----------------------------------------------------------------------------------+
|            | ``sigma``                           | 2*sigma (nm) is the length scale of decaying insertion curvature,                |
|            |                                     | or in other words expansion of non-spontaneous curvature due to insertion.       |
+------------+--------------+----------------------+----------------------------------------------------------------------------------+
| Advacned   | Optimization | ``numMaxIterations`` | Number of maximum iterations allowed.                                            |
| Parameters |              +----------------------+----------------------------------------------------------------------------------+
|            |              | ``criterionForce``   | Force criteria to determine if adequate optimization is accomplished (pN).       |
|            +--------------+----------------------+----------------------------------------------------------------------------------+
|            | Algorithm    | ``gaussQuadratureN`` | Default Gauss Quadrature used in integral approximation.                         |
+------------+--------------+----------------------+----------------------------------------------------------------------------------+

4. Triangular Mesh Setup
-----------------------
The first step for continuum membrane is to set up the triangular mesh model to approximate the geometry of the membrane. A brief framework is generated by dividing the geometric framework given by the geometric parameters (such as ``rSphere`` in sphere mode) into large triangular cells. Next, Loop's  subdivision method (`F. Cirak et al., 2000`_) is applied to further divide the brief framework into smaller cells to better approximate the given geometry.

5. Energy Function and Optimization
-----------------------

The goal for the continuum membrane model is to minimize the membrane energy evaluated by the energy function, which is the sum of membrane bending energy, area constraint energy (or elastic area change energy), and volume constraint energy:

.. math::

   dE_B = \\frac{1}{2}\\kappa (2H-C_0)^2 dS

6. Cite Continuum Membrane
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
.. _`F. Cirak et al., 2000`: http://multires.caltech.edu/pubs/thinshell.pdf
