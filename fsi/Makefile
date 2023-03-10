########################################################################
# Fast Auxiliary Space Preconditioners (FASP)
# 
# This is the Makefile for (Navier-)Stokes test problems! 
#
########################################################################

########################################################################
# Compilers and dependences
########################################################################
AR=ar ruc

##########################
# Use GNU compilers
##########################
# CC=gcc
# CPP=g++
# FC=gfortran

##########################
# Use Intel compilers
##########################
CC=icx
CPP=icx
FC=ifx

INCLUDE=-I ../../faspsolver/base/include -I ../include
FASPLIB=../../faspsolver/lib/libfasp.a
TESTLIB=../lib/libfasp4ns.a
FSRCDIR=.

#BLASLIB=-isysroot /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX12.1.sdk -framework Accelerate

##########################
# Use UMFPACK solver
##########################
#SOLVERDIR = /Users/zhangcs/Packages
#SOLVERLIB = -L$(SOLVERDIR)/lib -lsuitesparseconfig -lumfpack -lamd -lcholmod -lcolamd -lcamd -lccolamd

##########################
# Use MKL solver
##########################
SOLVERDIR = /public1/soft/oneAPI/2022.1/mkl/latest
SOLVERLIB = /public1/soft/oneAPI/2022.1/mkl/latest/lib/intel64/libmkl_rt.so /public1/soft/oneAPI/2022.1/compiler/latest/linux/compiler/lib/intel64/libiomp5.so /public1/soft/oneAPI/2022.1/compiler/latest/linux/compiler/lib/intel64/libimf.so -lm -Wl,-rpath,::::::::::::::

SOLVERINCLUDE = -I$(SOLVERDIR)/include

########################################################################
# Do not modify beyond this line
########################################################################

########################################################################      
# Compiling options                                                             
########################################################################        
BOPT=-O3 -fopenmp #-g -Wall

COPTS=$(BOPT)
CDEFS=-DWITH_BLAS=1 -DWITH_UMFPACK=1 -DWITH_SuperLU=0
CINCLUDES=$(INCLUDE) $(SOLVERINCLUDE)
CFLAGS=$(CDEFS) $(COPTS) $(CINCLUDES)

FOPTS=$(BOPT)
FDEFS=$(CDEFS)
FINCLUDES=$(CINCLUDES)
FFLAGS=$(FDEFS) $(FOPTS) $(FINCLUDES)

########################################################################
# Set libraries
########################################################################
LIBS=$(TESTLIB) $(FASPLIB) $(BLASLIB) $(SOLVERLIB) 

########################################################################
# Link options
########################################################################
LINKOPTS=$(BOPT)
FLFLAGS=-lm $(LINKOPTS) $(LIBS)

########################################################################
# Rules for compiling the source files
########################################################################
.SUFFIXES: .c .cc .cpp .for .f .f77 .f90 .f95
#
FSRC := $(foreach dir,$(FSRCDIR),$(wildcard $(FSRCDIR)/*.for))
FSRC += $(foreach dir,$(FSRCDIR),$(wildcard $(FSRCDIR)/*.f))
FSRC += $(foreach dir,$(FSRCDIR),$(wildcard $(FSRCDIR)/*.f77))
FSRC += $(foreach dir,$(FSRCDIR),$(wildcard $(FSRCDIR)/*.f90))
FSRC += $(foreach dir,$(FSRCDIR),$(wildcard $(FSRCDIR)/*.f95))
CSRC := $(foreach dir,$(CSRCDIR),$(wildcard $(CSRCDIR)/*.c))
CSRC += $(foreach dir,$(EXTRDIR),$(wildcard $(EXTRDIR)/*.c))
#
OBJSF := $(patsubst %.for,%.o,$(FSRC))
OBJSF += $(patsubst %.f,%.o,$(FSRC))
OBJSF += $(patsubst %.f77,%.o,$(FSRC))
OBJSF += $(patsubst %.f90,%.o,$(FSRC))
OBJSF += $(patsubst %.f95,%.o,$(FSRC))
OBJSC := $(patsubst %.c,%.o,$(CSRC))
#
.for.o:
	@$(FC) -c $< -o $@ $(FFLAGS)
	@echo 'Building F object $@'
	@$(AR) $(TESTLIB) $@
#
.f.o:
	@$(FC) -c $< -o $@ $(FFLAGS)
	@echo 'Building F object $@'
	@$(AR) $(TESTLIB) $@
#
.f90.o:
	@$(FC) -c $< -o $@ $(FFLAGS)
	@echo 'Building F90 object $@'
	@$(AR) $(TESTLIB) $@
#
.f95.o:
	@$(FC) -c $< -o $@ $(FFLAGS)
	@echo 'Building F95 object $@'
	@$(AR) $(TESTLIB) $@
#
.c.o:
	@$(CC) -c $< -o $@ $(CFLAGS)
	@echo 'Building C object $@'
	@$(AR) $(TESTLIB) $@
#
.cpp.o:
	@$(CPP) -c $< -o $@ $(CFLAGS)
	@echo 'Building CPP object $@'
	@$(AR) $(TESTLIB) $@
#
.cc.o:
	@$(CPP) -c $< -o $@ $(CFLAGS)
	@echo 'Building CPP object $@'
	@$(AR) $(TESTLIB) $@
#
########################################################################
# List of all programs to be compiled
########################################################################

.DEFAULT_GOAL := all

# Everything
$(TESTLIB): $(OBJSC) $(OBJSF)

########################################################################
# Link
########################################################################

all: $(TESTLIB) fasp4ns fasp4ell

########################################################################
# Some test problems
########################################################################

fasp4ns:
	@$(FC) -o fasp4ns.ex fasp4ns.o $(FLFLAGS)
	@echo 'Building executable $@'

fasp4ell:
	@$(FC) -o fasp4ell.ex fasp4ell.o $(FLFLAGS)
	@echo 'Building executable $@'

########################################################################
# Clean up
########################################################################

.PHONY : clean distclean help

clean:
	rm -f *.o

distclean:
	make clean
	rm -f *~ *.ex *.out
	rm -rf *.ex.dSYM

help:
	@echo "======================================================"
	@echo " Fast Auxiliary Space Preconditioners (FASP)"
	@echo "======================================================"
	@echo " "
	@echo " make            : build all exe files "
	@echo " make headers    : build the header file automatically"
	@echo " make clean      : clean all obj files "
	@echo " make allclean   : clean all obj, exe, bak, out files "
	@echo " make help       : show this screen "
	@echo " "
