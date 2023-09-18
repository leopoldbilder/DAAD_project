
units real
boundary p p p
atom_style full
region mybox block -500.000000 500.000000 -500.000000 500.000000 -500.000000 500.000000
create_box 2 mybox bond/types 1 angle/types 0 dihedral/types 0 extra/special/per/atom 20 extra/bond/per/atom 20 extra/angle/per/atom 20
#variable string MAA type 1
#variable Na type 2
molecule pol PDMAEMA.mol
mass 1 157.21
mass 2 35.453
dielectric 81.2
bond_style harmonic
bond_coeff 1 0.57 5
pair_style lj/cut/coul/long 4.568 500.0
pair_coeff 1 1 0.7 4.0 4.49 
pair_coeff 2 2 0.1 4.3 4.8 
kspace_style pppm 1e-6
create_atoms 0 single 0 0 0 mol pol 123

velocity all create 300.0 4928459
pair_modify shift yes mix arithmetic
fix nvt all langevin 300 300 100.0 6138895 gjf vfull
fix nve all nve
dump xtc all xtc 10000 PDMAEMA.xtc
thermo      10000
timestep 2
run     50000000
write_data PDMAEMA.data