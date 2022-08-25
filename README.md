# Integrating adaptive meshing into a PDE-constrained optimisation model

## Algorithm
This codebase is an extension based on the codebase writter by Dr Joseph Wallwork.
Please click here to see the codebase: https://github.com/pyroteus/opt_adapt  
## Tree
Here is the main directory tree of the algorithm in this report:  
```
opt_adapt  
├ demos  
  ├ heat_eq_constant_source  
       └ setup.py  
  ├ heat_eq_variable_source  
       └ setup.py  
  ├ stokes  
       └ setup.py  
  ├ opt_go.py  
  ├ opt_hessian.py  
  ├ opt_uniform.py  
  ├ plot_different_mesh_adaptation.py  
  └ plot_different_optimization_methods.py  
├ opt_adapt  
  ├ matrix.py  
  ├ opt.py  
  └ utils.py  
```
## Packages
Here are packages needed in this algorithm: Firedrake, Pyroteus, Numpy, Time, matplotlib.

## Installation 
Firedrake is a finite element package, to install Firedrake, please see https://firedrakeproject.org/download.html  

Pyroteus is a goal-oriented error estimation and mesh adaptation package, to install Pyroteus, please see https://docs.google.com/document/d/1g6PYZp428SbAC0BNsOoBnIVitc5Uh-9bOejAh_tU-ZA/edit  


## Parameters
Before we run the algorithm, let's familiar with the parameters of this algorithm that could chosen by users.  
| Parameter | Type | Default value |  Details | 
| --- | --- | --- |  --- |  
| ``--method`` | string | ``gradient_descent`` |There are 5 optimization methods available: ``gradient_descent``, ``adam``, ``bfgs``, ``lbfgs``,``newton``|
| ``--n`` | int | ``1`` |  The level of the initial mesh elements. |
| ``--target`` | float | ``1000.0`` | The target metric complexity. (Not available for the algorithm that without mesh adaptaion) |
| ``--maxiter `` | int | ``100`` | The maximum of iterations. |
| ``--gtol`` | float | ``1.0e-05`` | The tolerance of gradient of objective function values. |
| ``--lr`` | float | For ``gradient_descent``, the default value is ``0.01``. For the other four methods, the default value is ``1``.  | The initial step length. |
| ``--lr_min`` | float | ``1.0e-08`` | The minimum step length.  |
| ``--disp`` | int | ``1`` | The level of printing. |

We also need to select the folder of the example we want to optimize, for the paper, we focus on the heat equation with a constant source: ``heat_eq_constant_source``. In addition, we mentioned the examples ``heat_eq_variable_source`` and ``stokes`` in disscussion part.
## Run the algorithm

Then, we run the setup file with mesh adaptation technique and optimization routine, here are options: ``opt_uniform.py``, ``opt_hessian.py``, and ``opt_go.py``. You also could change the vaules of parameters in above table. For example, run:  
  
  
``python3 opt_hessian.py heat_eq_constant_source --method bfgs --n 2 --lr 1``  
  
  
The data will be saved for plotting.
## Plot convergence
Also, we could run the two plotting files ``plot_different_optimization_methods.py`` and ``plot_different_mesh_adaptation.py`` based on the data saved before. These tow files will plot the objective function value against iteration numbers and CPU time.  
  
  
``python3 plot_different_optimization_methods.py heat_eq_constant_source --run uniform --n 2``  
``python3 plot_different_mesh_adaptation.py heat_eq_constant_source --method bfgs --n 2 ``  
  
  
The file ``plot_different_optimization_methods.py`` is plotting different optimization methods and users need to choose the mesh adaptation methods. For parameters ``--run``, there are three options: ``go``, ``hessian``, ``uniform``. For ``plot_different_mesh_adaptation.py``, users need to choose the optimization methods form ``gradient_descent``, ``adam``, ``bfgs``, ``lbfgs``,``newton``.



