
units real
boundary p p p
atom_style full
region mybox block -500.000000 500.000000 -500.000000 500.000000 -500.000000 500.000000
create_box 3 mybox bond/types 2 angle/types 2 dihedral/types 0 extra/special/per/atom 20 extra/bond/per/atom 20 extra/angle/per/atom 20
#variable string MAA type 1
#variable Na type 2
molecule pol PMAA_PEG.mol
mass 1 86.09
mass 2 44
mass 3 11.0000
dielectric 81.2
bond_style harmonic
bond_coeff 1 0.690 3.492
bond_coeff 2 0.46 5.414
pair_style lj/cut/coul/long 4.568 500.0
pair_coeff 1 1 0.596 3.6 4.04 #PMAA atoms
pair_coeff 2 2 0.596 3.6 4.04 #PEG/PEO atoms
pair_coeff 3 3 0.108 2.31 2.59 #Na atoms
angle_style cosine
angle_coeff 1 1.09
angle_coeff 2 0.42
kspace_style pppm 1e-6
create_atoms 0 random 77000 123456 NULL mol PMAA 1234
velocity all create 300.0 4928459
pair_modify shift yes mix arithmetic
fix nvt all langevin 300 300 100.0 6138895 gjf vfull
fix nve all nve
dump xtc all xtc 1000 PMAA_PEG.xtc 
thermo		100000
timestep 2.0
run		50000000
write_data PMAA_PEG_concentrated.data