## Task 2: Submit jobs on SDSC

To notice, you need to replace YOUR_ID with your ACCESS ID.
### S1: Create a directory to save your first job
```
cd /expanse/lustre/projects/csd877/YOUR_ID
mkdir test
cd test
pwd
```
Q1: Do you still remember what these commands mean?

### S2: Copy a folder from my directory
using `cp which_file_you_want_to_copy to_where_you_want_to_save_the_copy` (which mean copy) to copy a file or folder. To copy a folder, you need to add `-r` following `cp`, for example
```
cp -r /expanse/lustre/projects/csd877/yjia3/share/lmp_Si_test ./
```
Here I use `.` to represent CURRENT DIRECTORY. 
```
ls
```
you should find a folder named `lmp_Si_test` under your own test directory

### S3. run lammps job
```
cd lmp_Si_test
cd lammps
ls
```
`lammps` folder contains all required input file to run a lammps simulation. `in.tersoff` is a input file to set up parameters for lammps. `SiC.tersoff` includes parameters determine the classical potential between atoms. `pure-Si-444.lmp` is a file including atomic positions of the material structure. `lammps.submit` is a bash scripts to submit jobs.

To submit a job to queque:
```
sbatch lammps.submit
```
This command is going to return a `JOB_ID` (integers). To check the status of the job
```
squeue -u YOUR_ID
```
, which will list all jobs in the queque.

### S4. Customize submitting script
Submitting script is nothing but a buch of linux command (or shell language program). Let's read this file with `vi` eidtor
```
vi lammps.submit
```
Then you can see the contents of this file:
```
#!/bin/bash
#SBATCH -A csd877                  # This is our project ID. Do not change this
#SBATCH --job-name=Si              # job name, you can all anything you like
#SBATCH --partition=debug          # queque's name. "debug" is a queque to debug your code. "compute" is the main computing queque
#SBATCH --nodes=1                  # the number of node you require, 1 is enough for your following research
#SBATCH --ntasks-per-node=2        # the number of cores for each node your require. 128 is maximum. Smaller value will give higher priority in the queque
#SBATCH --cpus-per-task=1          # do not need to change this
#SBATCH --output=Si.o%j.%N         # the name of standard output
#SBATCH --export=ALL               # do not need to change this
#SBATCH --constraint="lustre"      # do not need to change this
#SBATCH -t 00:30:00                # maximum time to run this job you required. Smaller value will give higher priority in the queque

module purge                       # load required libraries. Do not need to change the following 4 rows for your research
module load slurm
module load cpu/0.15.4  gcc/10.2.0 openmpi/4.0.4
module load lammps/20200721-openblas

mpirun -np 2 lmp < in.tersoff      # parallely run the code lmp, with in.tersoff file as the input. -np 2 means run on 2 cores (same value as --ntasks-per-node)
```

