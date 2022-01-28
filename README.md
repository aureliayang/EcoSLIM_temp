# EcoSLIM

* The parflow model for tests in the paper can be found at https://github.com/reedmaxwell/EcoSLIM/tree/master/Examples/Hillslope_Simulations/paper_cases  
* The CPU version code (i.e., the origional OpenMP code) used in the paper can be found at https://github.com/reedmaxwell/EcoSLIM  Please refer to the introduction of input file on this website for rerun of CPU tests in the paper.  
* Please refer to paper_results for all data generated in the paper https://doi.org/10.6084/m9.figshare.19090181.v3
* For this GPU version code, an example of the input files is given in the Example folder. Please refer to the following introduction for the input file slimin.txt. Please pay particular attention for **p_redis, path, and cycle_f** which are parameters for scheme 1, 3, and 2 of load balancing. Please keep subinfo.txt unchanged if you use fewer than 16 GPUs.  

## Input file  
* **runname,** EcoSLIM run name
* **pname,** Path of ParFlow files
* **DEMname,** pfb file name of DEM
* **nx,** Dimension in x direction
* **ny,** Dimension in y direction
* **nz,** Dimension in z direction
* **nCLMsoil,** Layers coupled between CLM and ParFlow
* **ppx,** Split in x direction, like P in ParFlow
* **qqy,** Split in y direction, like Q in ParFlow, ppx\*qqy is the total number of GPUs used. 
* **p_redis,** parameter for load balancing scheme 1. For example, if it is 24, it means particle transfer every 24 hours.
* **path,** parameter for load balancing scheme 3. For example, if it is 24, it means dynamic domain decompostiion every 24 hours.
* **cycle_f,** parameter for load balancing scheme 2. For example, if it is 24, it means cyclic mapping every 24 hours.
* **np_ic,** Number of particles per cell at the start of simulation
* **np,** Maximum particle number on one GPU permitted during run time 
* **dx,** grid-cell size in x direction
* **dy,** grid-cell size in y direction
* **dz,** grid-cell size in z direction from bottom to top, separated by comma
* **pfdt,** ParFlow dt, need double-check in the code for mass balance
* **pft1,** ParFlow start time
* **pft2,** ParFlow end time
* **tout1,** EcoSLIM start number; it is 0 for cold start; it is the last completed timestep for hot start
* **n_cycle,** The cycles to use ParFlow files
* **add_f,** The time interval to add particles
* **ipwrite,** For output, not relevant in this paper
* **ibinpntswrite,** For output, not relevant in this paper
* **etwrite,** For output, not relevant in this paper
* **icwrite,** For output, not relevant in this paper
* **V_mult,** Velocity multiplier. Not supported now and only used for transfer test.
* **clmtrans,** clm evap trans?
* **clmfile,** clm output file?
* **iflux_p_res,** The number of particles added into the domain if PME > 0
* **denh2o,** density of water
* **moldiff,** Molecular diffusivity
* **dtfrac,** Numerical stability information
* **nind,** Number of subsurface indicator
* **Indname,** pfb file of indicator
## Build
    <table>  
      <tr>
        <td>Compiler</td>
        <td>nvhpc/21.5</td>
      </tr> 
      <tr>
        <td>CUDA</td>
        <td>cudatoolkit/11.3</td>
      </tr> 
      <tr>
        <td>MPI</td>
        <td>openmpi/cuda-11.3/nvhpc-21.5/4.1.1</td>  
      </tr>  
    </table>  

* Build in the src folder:  
  ```
  make
  ```


