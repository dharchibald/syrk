HOME       := /u/rvdg
BLAS_LIB   := $(HOME)/blis/lib/libblis.a
FLAME_LIB  := $(HOME)/flame/lib/libflame.a
FLAME_INC  := $(HOME)/flame/include

# indicate where the object files are to be created
CC         := gcc
FC         := gfortran
LINKER     := $(CC)
CFLAGS     := -O3 -Wall -I$(FLAME_INC) -I$(CBLAS_INC) -m64 -msse3 
FFLAGS     := $(CFLAGS) 

# set the range of experiments to be performed
NREPEATS   := 3#       number of times each experiment is repeated.
NFIRST     := 100#     smallest size to be timed.
NLAST      := 1500#    largest size to be timed.
NINC       := 100#     increment between sizes.

LDFLAGS    := -lpthread -m64 -lm  -fopenmp

# indicate where the FLAME include files reside

# add files in which your implementations are coded
TEST_OBJS  := driver.o syrk_ac_unb_var1.o syrk_ac_blk_var1.o

# $%.o: %.c
#	$(CC) $(CFLAGS) -c $< -o $@
# $%.o: %.f
#	$(FC) $(FFLAGS) -c $< -o $@

driver.x: $(TEST_OBJS)  $(LAPACK_OBJS)
	$(LINKER) $(TEST_OBJS) $(LAPACK_OBJS) $(FLAME_LIB) $(LAPACK_LIB) $(BLAS_LIB) $(LDFLAGS) -o driver.x

test:   driver.x
	echo "$(NREPEATS) $(NFIRST) $(NLAST) $(NINC)" | ./driver.x > output.m

clean:
	rm -f *.o *~ core *.x output.m
