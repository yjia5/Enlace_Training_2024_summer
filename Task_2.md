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
you should find a folder named `lmp_Si_test` under your 

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
