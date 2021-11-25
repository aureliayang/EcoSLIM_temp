# Last Change:  2021-07-20 22:29:28
CUF=ecoslim_thrustscan.o \
	ecoslim_cuRAND_de.o \
    ecoslim_device_utility.o \
    ecoslim_create_subgrid.o \
    ecoslim_compaction.o \
    ecoslim_particles_loop.o \
	ran1.mod.o \
    vtk_write.o \
	vtk_write_points.o \
    pfb_read.o \
	pfb_write.o \
    EcoSLIM_CUDA_MPI.cuf

all: test

test: ecoslim_cthrustscan.o ${CUF}
	mpif90 -o $@ $^  -lstdc++

ecoslim_cthrustscan.o: ecoslim_cthrustscan.cu
	nvcc -c $^ -o $@ -std=c++14
ecoslim_cuRAND_de.o: ecoslim_cuRAND_de.cuf
	mpif90 -c $^ -o $@
ecoslim_thrustscan.o: ecoslim_thrustscan.cuf
	mpif90 -c $^ -o $@
ecoslim_create_subgrid.o: ecoslim_create_subgrid.f90
	mpif90 -c $< -o $@
ecoslim_device_utility.o: ecoslim_device_utility.cuf
	mpif90 -c $^ -o $@
ecoslim_compaction.o: ecoslim_compaction.cuf
	mpif90 -c $< -o $@
ecoslim_particles_loop.o: ecoslim_particles_loop.cuf ecoslim_cuRAND_de.o
	mpif90 -c $< -o $@
ran1.mod.o: ran1.mod.f90
	mpif90 -c $^ -o $@
vtk_write.o: vtk_write.f90
	mpif90 -c $^ -o $@
vtk_write_points.o: vtk_write_points.f90
	mpif90 -c $^ -o $@
pfb_read.o: pfb_read.f90
	mpif90 -c $^ -o $@
pfb_write.o: pfb_write.f90
	mpif90 -c $^ -o $@

.PHONY: clean
clean:
	rm *.o *.mod test \
	slurm* \
	SLIM*.txt \
	null \
	Device_Utility.txt \
	CMakeLists.txt \
	Load* \
	Log* \
	P*bin \
	E*bin \
	fort.12