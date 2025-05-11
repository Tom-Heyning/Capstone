# Capstone

The Jupyter notebook [solver.ipynb](solver.ipynb) contains code that implements AFEM using both a residual based estimator and the ZZ estimator. AFEM can be run by first setting the following global variables:

- `sing` is a boolean, setting it to `True` sets the problem to solved as the one containing a singularity, setting it to `False` sets it up as the smooth problem.
- `depth` takes integer values, and controls the amount of AFEM iterations taken.

Then, any of the following functions can be called:

- `runAFEM()` runs AFEM, and is used to collect data surrounding estimator performance. It can take two optional arguments, both of which are preset to `True`.
  - `res` is a boolean, if set to `True` AFEM is run using the residual based estimator.
  - `acc` is a boolean, if set to `True` refinement accuracy scores are calculated and refined during each AFEM iteration.
  
  It returns the final solution, finite element space, mesh, total estimated error per iteration, total true error per iteration, the final per element estimated errors, the final per element true errors, the refinement accuracy, the under refinement rate, the over refinement rate, and the degrees of freedom per iteration.

- `runAFEM_Speed()` runs AFEM, but does not do any of the extra steps data recording steps that `runAFEM()` does each iteration. This speeds up execution, this function is used to compare computation time for both error estimators. It takes the following arguments:
  - `tol` is numerical, it sets the true error tollerance the solution is calculated to meet. 
  - `res` is a boolean, if set to `True` AFEM is run using the residual based estimator. This argument is preset to `True`, so it does not have to be specified.

  It returns the time taken to run AFEM, the amount of AFEM iterations, the final true error, and the final degrees of freedom.
 
- `runAFEM_Uniform()` runs AFEM thrice, it first does so using both the residual and ZZ estimator. Then it runs AFEM without adaptive mesh refinemenet, refining each element each iteration, until the true error is less than that of the ZZ estimator AFEM's final approximation. This function is used to validate whether AFEM improves alogorithm efficiency. It takes no arguments.

  It returns, for each run, the final degrees of freedom and the final error.

Currently, these cells calling these functions have all been commented out, this is done so that upon opening the notebook all cells can be run to ensure all neccessary functions have been defined, without incurring excess time spent running the functions. The cell calling the function that needs to be exected can be uncommented and run after this.

The same has been done for the cells containing code to generate plots.
