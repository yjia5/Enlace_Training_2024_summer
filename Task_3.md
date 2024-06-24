## Task 3. Learn Lammps

### Step 1. Read Literature-Born–Oppenheimer approximation
Did you watch the movie Oppenheimer? The fundation of molecular dynamic is built by J. Robert Oppenheimer. The main idea is that the electrons move much faster than nuclei. Therefore, when we consider about the motion of electrons, we believe the nuclei are fixed. On the other hand, if we consider about the motion of nuclei, we believe they are moving in the force field created by the electrons. As a result, the motion of electrons and nuclei are seperated and the whole complex system is divided into two smaller systems to study. More detailes can be read by the references or any book including Born-Oppenheimer approximation:

https://en.wikipedia.org/wiki/Born%E2%80%93Oppenheimer_approximation

Section 9-1 of book Physical Chemistry_A Molecular Approach (Donald A. McQuarrie, John D. Simon)

### Step 2. Learn the parameters of lammps
Lammps (https://www.lammps.org/#gsc.tab=0) is a software implementing classical molecular dynamics, which means the quantum properties of nulcei are neglected and the force field exerted on the nuclei by electrons is modeled as a function of position of nuclei. Therefore, nuclei's motion is determined by Newton's second law, or say, the nuclei are classical particles. There are many parameters to set up in Lammps. For your research, you only need the ones I put into the input file `in.tersoff` provided in Task 2. To learn a software, the best way is to start from an example and read the document page of each parameter, which is the main content of this task.

Here are simple instructions:

(1) The comment line start from #. The charaters behind of # are neglected by lammps.

(2) Focuse on the ones labeled as "Will change in the future".
```
units           metal  # Do not need to change in the future. the group of units used in this calculations. For style metal, these are the units: mass = grams/mole distance = Angstroms time = picoseconds ... read https://www.afs.enea.it/software/lammps/doc17/html/units.html

atom_style      atomic # Do not need to change in the future. Roughly decide what kind of force field can be used. https://docs.lammps.org/atom_style.html
atom_modify     map array # Do not need to change in the future. Determine the method used to decide neighoring list.
atom_modify     sort 0 0.0 # Do not need to change in the future. Determine the frequency to modify the neighboring list.
boundary        p p p # Do not need to change in the future. Periodic boundary conditions
read_data       pure-Si-444.lmp # Will change in the future. The file including the the atomic structure we are going to study
pair_style      tersoff # Will change in the future. Determine the force field used by the calculation. 
pair_coeff      * * Si.tersoff Si # Will change in future. Determine the force field used by the calculation.
timestep        1.0e-3 # Do not need to change in the future. The time length (0.0001 ps) of each step in the nuclei motion
thermo          500 # Will change in the future. Determine the frequency of writing into an output file `log`
dump            1 all atom 1000 dump.melt # will change in the future. Determine the frequency of writing into an output file including the trajectory of nuclei `dump.melt`
restart         10000 tmp.restart # will change in the future. Determine the frequency of writing a new restart file. Good habit for a long run.
fix             24 all npt temp 300 3000 0.1 iso 1.0 1.0 1000 # will change in the future. Determine the ensemble of this calculation. For this perticular one, it is a NPT ensemble. The starting temperature is 300K. And the final temperature is 3000K. The pressure is 1.0 atm.
run             300000 # Will change in the future. Determine how many steps to run the molecular dynamic simulation.
```
(3) If you want to know more about how does the software work, read this small course
https://nanohub.org/resources/7570

## Step 3. Rerun lammps by changing parameters
