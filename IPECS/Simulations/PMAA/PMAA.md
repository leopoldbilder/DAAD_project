
units real
boundary p p p
atom_style full
region mybox block -500.000000 500.000000 -500.000000 500.000000 -500.000000 500.000000
create_box 2 mybox bond/types 1 angle/types 0 dihedral/types 0 extra/special/per/atom 20 extra/bond/per/atom 20 extra/angle/per/atom 20
#variable string MAA type 1
#variable Na type 2
molecule pol PMAA.mol
mass 1 78.0000
mass 2 11.0000
dielectric 81.2
bond_style harmonic
bond_coeff 1 0.690 3.492
pair_style lj/cut/coul/long 4.568 500.0
pair_coeff 1 1 0.596 3.6  4.04
pair_coeff 2 2 0.108 2.31 2.59 
kspace_style pppm 1e-6
create_atoms 0 single 0 0 0 mol pol 123
velocity all create 300.0 4928459
pair_modify shift yes mix arithmetic
fix nvt all langevin 300 300 100.0 6138895 gjf vfull
fix nve all nve
dump xtc all xtc 1000 PMAA.xtc 
thermo		1000
timestep 10.0
run		100000
write_data PMAA.data
