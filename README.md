# Fast Auxiliary Space Preconditioners (FASP) for 2x2 BLC matrices: README
# It is suitable for Stokes, Navier-Stokes, Brinkman, DLD, FSI problems

## Build

Now you are ready to set up the build environment with cmake

``` bash
    > mkdir Build; cd Build; cmake .. 
```

To make and install all executables and libraries:

``` bash
    > make install
```

## Directory

The directory structure of fasp4blc is designed as follows:

- `demo/` : Demo examples for Stokes and NS equations
- `dld/` : Solvers for DLD problems (Fictitious Domain method)
- `doc/` : Documentation and website
- `fsi/` : Preconditioners for FSI problems (ALE method)
- `main/` : Main source code for executables
- `modules/` : Cmake files for finding and setting dependencies
- `src/` : Source files
- `vs22/` : Visual studio solution (2022 version)
- CMakeLists.txt: Main cmake script
- LICENSE: License agreement
- README.md: This document
- .clang-format: For automatic source code formatting

## Compatibility

To compile, you need a C99 compiler and a F90 compiler. By default, we use the  
GNU gcc and gfortan, respectively. This package has been tested on the following  
platforms:

- Linux
  - GNU gcc/gfortran:   4.4.x, 4.5.x, 4.6.x, 4.8.x, 4.9.x, 5.0.x
  - Intel icc/ifort:    11.x

- Mac OS X
  - GNU gcc/gfortran:   4.4.x, 4.5.x, 4.6.x, 4.8.x, 4.9.x, 5.0.x
  - Intel icc/ifort:    11.x
  - Apple clang:        6.0.x (without Fortran support)

- Windows XP, 7, 10
  - Intel icc/ifort:    11.1, 12.x, 13.x, 14.x, 2019, 2020, 2022
