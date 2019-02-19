# Bembel
## Table of contents
1. [Introduction](#introduction)
2. [What is a Bembel?](#whatis)
3. [Features](#features)
4. [How to Run it](#example)
5. [Publications & Preprints](#publications)
6. [Contributers](#contributors)
7. [About the People](#people)

## 1. Introduction <a name="introduction"></a>

Bembel is a Boundary Element Method Based Engineering Library written in C and C++ to solve boundary value problems governed by the Laplace, Helmholtz or electric wave equation [3,4,5]. It was written as part of a cooperation between the TU Darmstadt and the University of Basel, coordinated by H. Harbrecht, S. Kurz and S. Schöps. The code is based on the Laplace BEM of J. Dölz, H. Harbrecht and M. Multerer, [2,6] as well as the spline and geometry framework of F. Wolf. 

We plan to release a version of the code here under the GNU GPLv3 **before the end of March 2019**.

## 2. What is a Bembel <a name="whatis"></a>

A traditional German ceramic, as depicted in our logo. Quoting [Wikipedia](https://en.wikipedia.org/wiki/Apfelwein):

> *Most establishments also serve Apfelwein by the Bembel (a specific Apfelwein jug), much like how beer can be purchased by the pitcher in many countries. The paunchy Bembel (made from salt-glazed stoneware) usually has a basic grey colour with blue-painted detailing.*

## 3. Features <a name="features"></a>

Current key features include

* Approaches induced by the Laplace, Helmholtz and Maxwell single layer operator, where the Maxwell approach is also known under the name *Method of Moments*,
* Arbitrary parametric mappings for the geometry representation, as default realized as NURBS-mappings from files in the [GeoPDEs](http://rafavzqz.github.io/geopdes/) format,
* Higher-order (currently up to 14) B-Spline functions as Ansatz spaces, as in the framework of isogeometric analysis for electromagnetics [1,4],
* An embedded interpolation-based fast multipole method for compression [2,4], equivalent to the H2 matrix format, 
* Compatibility of the compressed matrix with the [Eigen](http://eigen.tuxfamily.org/) linear algebra library.

Planned features include octave wrappers and a full Calderon operator for scalar problems.

## 4. How to Run it <a name="example"></a>

We ship a version of Eigen3 with our repository since its unsupported modules are not available in many installations of Eigen via standard repositories. 
We do not rely on any other external libraries, except for the standard template library, so Bembel should compile out of the box. Under Linux, you may simply change to `template_build/` and run the `compile.sh` shell script, which just calls `cmake ..` and `make -j4`. Afterwards, we recommend running `test.sh` which will call test routines, as well as examples for the computation of a Laplace, Helmholtz, and Maxwell problem, generating .pdf's with nice convergence plots. However, depending on your system, this may take a while.

The general structure of the repository looks as follows.

* `template_build/` includes the before mentioned scripts, as well as
    * `template_build/data/` contains some geometries for the examples
    * `template_build/latex_templates/` contains some `.tex` files for convergence plots of the examples
* `src/` contains the source code
    * `src/include` contains the `.hpp` header files for the high level c++ wrappers
        * `src/include/includeC` contains the `.h` header files of the low-level routines We recommend to include only `.hpp` headers when writing custom applications.
        * `src/include/geom` contains geometry files of the pre-GeoPDE-import era. It will be deleted in future releases
        * `src/include/eigen3` includes the header-only Eigen linear algebra library. If you have it installed, including the unsupported modules, feel free to delete it.
    * `src/spline` contains the spline framework. Here, the routines for basis functions and geometry representation can be found. It contains a subfolder with automated tests, which are run by `tests.sh`
    * `src/test` contains a test suite which is run by `tests.sh`
    * `src/bemlibC` contains the `.cpp`-files for the library. Many routines were first written in C and later ported to C++. For this reason, there are some redundancies, especially w.r.t. linear algebra, since legacy versions of the code did not utilize the Eigen library. We plan to clean this up in future releases
    * `src/examples` contains examples with **detailed comments**, which correspond to the executables compiled when calling `compile.sh`
* `assets` only contains things relevant for GitHub pages

When using our code, we recommend starting with understanding the code in `src/examples`, followed by learning the capabilities of the high-level classes in `.hpp` files.

## 5. Publications & Preprints <a name="publications"></a>

[1] A. Buffa, J. Dölz, S. Kurz, S. Schöps, R. Vázques and F. Wolf. *Multipatch Approximation of the de Rham Sequence and its Traces in Isogeometric Analysis*. Submitted. [To the preprint](https://arxiv.org/abs/1806.01062).

[2] J. Dölz, H. Harbrecht and M. Peters. *An interpolation-based fast multipole method for higher-order boundary elements on parametric surfaces*. [To the paper](https://onlinelibrary.wiley.com/doi/pdf/10.1002/nme.5274).

[3] J. Dölz, H. Harbrecht, S. Kurz, S. Schöps and F. Wolf. *A fast isogeometric BEM for the three dimensional Laplace- and Helmholtz problems*. [To the paper](https://www.sciencedirect.com/science/article/pii/S0045782517306916). [To the preprint](https://arxiv.org/abs/1708.09162).

[4] J. Dölz, S. Kurz, S. Schöps and F. Wolf. *Isogeometric Boundary Elements in Electromagnetism: Rigorous Analysis, Fast Methods, and Examples*. Submitted. [To the preprint](https://arxiv.org/abs/1807.03097).

[5] J. Dölz, S. Kurz, S. Schöps and F. Wolf. *A Numerical Comparison of an Isogeometric and a Classical Higher-Order Approach to the Electric Field Integral Equation*. Submitted. [To the preprint](https://arxiv.org/abs/1807.03628).

[6] H. Harbrecht and M. Peters. *Comparison of fast boundary element methods on parametric surfaces*. [To the paper](https://www.sciencedirect.com/science/article/pii/S0045782513000819).

## 6. Contributors <a name="contributors"></a>

**Current maintainers** are J. Dölz, M. Multere, F. Wolf.

**Other contributors** include D. Andric (geometry import), H. Harbrecht (legacy C-codebase, quadrature routines).

## 7. About the People <a name="people"></a>

* [Jürgen Dölz](https://www.mathematik.tu-darmstadt.de/fb/personal/details/juergen_doelz.de.jsp) currently holds a postdoc position at the [Department of Mathematics](https://www.mathematik.tu-darmstadt.de/fb/index.de.jsp) at TU Darmstadt. While contributing to Bembel, he was supported by SNSF Grants 156101 and 174987, as well as the Graduate School of Computational Engineering at TU Darmstadt and the Excellence Initiative of the German Federal and State Governments and the Graduate School of Computational Engineering at TU Darmstadt.
* [Helmut Harbrecht](https://cm.dmi.unibas.ch/) currently holds a professorship at the [Departement Mathematik und Informatik](https://dmi.unibas.ch/de/home/) at the University of Basel.
* [Stefan Kurz](https://www.temf.tu-darmstadt.de/temf/mitarbeiter/mitarbeiterdetails_57408.en.jsp) currently holds a professorship at the [Institute TEMF](https://www.temf.tu-darmstadt.de/temf/index.en.jsp) at TU Darmstadt and is a research expert at [Bosch](https://www.bosch.com/research/know-how/research-experts/prof-dr-stefan-kurz/).
* [Michael Multerer](https://www.ics.usi.ch/index.php/people-detail-page/297-prof-michael-multerer) currently holds a professorship at the Institute of Computational Science at the Università della Svizzera italiana in Lugano. While contributing to Bembel, he was supported by SNSF Grant 137669. He may also be found [on GitHub](https://github.com/muchip).
* [Sebastian Schöps](https://www.cem.tu-darmstadt.de/cem/group/ref_group_details_27328.en.jsp) currently holds a professorship at the [Institute TEMF](https://www.temf.tu-darmstadt.de/temf/index.en.jsp) at TU Darmstadt. He may also be found [on GitHub](https://github.com/schoeps).
* [Felix Wolf](https://www.cem.tu-darmstadt.de/cem/group/ref_group_details_57665.en.jsp) is currently a PhD student at the [Institute TEMF](https://www.temf.tu-darmstadt.de/temf/index.en.jsp) at TU Darmstadt. While contributing to Bembel, he was supported by DFG Grants SCHO1562/3-1 and KU1553/4-1, as well as the Graduate School of Computational Engineering at TU Darmstadt and the Excellence Initiative of the German Federal and State Governments and the Graduate School of Computational Engineering at TU Darmstadt. He may also be found [on GitHub](https://github.com/coffeedrinkingpenguin).