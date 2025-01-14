# prisms-toolbox

<B>Phase field to dislocation dynamics (PF2DD)</B>

PF2DD is a tool that converts vtk format data (generated by Phase Field simulations https://github.com/prisms-center/phaseField) to precipitate input files used for the dislocation dynamics (Paradis https://ipo.llnl.gov/technologies/paradis). With PF2DD, users can transfer meshed data precipitate information file generated by Phase Field simulation to an analytic description that is supported by Paradis.

This code is under PRedictive Integrated Structural Materials Science (PRISMS) Center [http://www.prisms-center.org/]
  at University of Michigan which is supported by the U.S. Department
  of Energy (DOE), Office of Basic Energy Sciences, Division of Materials Sciences
  and Engineering under Award #DE-SC0008637 

<I>Installation:</I>

1) Install Armadillo (version 8.600.0 or later)<br>
  + Armadillo is a C++ library for linear algebra & scientific computing 
  + Download and install Armadillo following instructions from https://gitlab.com/conradsnicta/armadillo-code/
  + If the installed Armadillo is not in the default library path, please specify its path of lib and include in the Makefile 

2) Install NLopt library (version 2.4.2 or later) <br>
  + NLopt is a free/open-source library for nonlinear optimization
  + Download and install NLopt based on [https://nlopt.readthedocs.io/en/latest/#download-and-installation]
  + If the installed NLopt is not in the default library path, please specify its path of lib and include in the Makefile 

2) Install PhaseField Integration tools<br> 
  + IntegrationTools specifies an interface for easily passing functions and fields, referred to as ‘PFunctions’ and ‘PFields’, to a computer program. 
  + Download and install the PhaseField Integration tools by the link https://github.com/prisms-center/IntegrationTools   

3) After installing Armadillo, NLopt and PhaseField Integration tools<br>	
  go to directory and compile  
  + cd path_to_PF2DD/PF2DD/srcs ; make all 
  + the execuble file is pf2dd.exe 

<I>Getting started:</I>

1) In the PF2DDMain.cpp, the main() function specifies a typical workflow in the PF2DD 

  + loadvtk()             : load vtk file. after load vtk file, it generates a .txt file for a fast restart 
  + loadtxt()             : load txt file to get precipitate meshed data
  + findPrecs()           : find precipitate in the configurations.
  + fitEllipTestInit()    : fit ellipse shape precipitate, and it trys different initial configurations for fitting 
  + outMatrix()           : save the geometric matrixs of precipiates 
  + loadmtx()             : load matrix files  
  + outParadisDat()       : write a Paradis .dat file

2) Each function has an description of its utility on its function defination

3) The defaults fit the center positions and ellipse shape of precipiates, user can define custom the fitting by 
using a fixed center fitting or a sphere shape precipitate, for example use function runCMAESFixCenter() and runCMAESSphere(), please refer specific functions for details  

4) The code uses CMA-ES as defaults optimization routine. Users can also specify other optimization routines that are supported by the NLopt library, for details please go to function runOpt() that shows an example of how to apply the NLopt optimization routine in PF2DD

5) In the python directory, there is python code PF2DDtl.py that can plot and check the fitting results that generates from PF2DD codes. 
The routine in PF2DDtl.py is called by different arguments by -t in the command line. Please refer to the python code for details. 

6) In the test directory, there is a vtk file test_nonuniform.vtk for test PF2DD   

7) We summarized a description of purpose and methods of the PF2DD in PH2DD_Demo.pdf, located in the PF2DD/demo directory