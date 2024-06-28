## Task 5: Depict the phase diagram of Silicon
### Step 1. Meet with Vivian
Vivian will present the recent studies on the phase diagram of silicon and assign you the target of your internship, which is to determine the phase transition temperature.

### Step 2. PLot the time VS energy & time VS temperature
To easily download file from portal, we are going to do calculation directly under the `scratch` folder (do not need to copy the files under `project` folder to `scratch` folder anymore)

```
cd /expanse/lustre/scratch/YOUR_USER_NAME/temp_project
```
Copy the file shared by Vivian.

```
cp -r /expanse/lustre/projects/csd877/yjia3/share/phase_diagram ./
ls
```
Then you should have your `phase_diagram` folder. 
Omar plots the figures for the lower temperature one.
Viridiana plots the figures for the higher temperature one.
Put the results into the slides. You should also find the figure of RDF Vivian has plotted under the folder, please also add them into your slides. If there is not such a RDF figure, please plot it by yourselves.

### Step 3. More runs with the increament of temperatures
You need to edit the file `run.sh`, `in.tersoff`. The exact examples are given in folder `0.2`. 

```
cd 0.2
```

If you want to add calculations of temperature 1825K, 1850K, 1875K. Then we need to restart from 1800K. Under the folder 1800K, you can find a restart file, whose name has the format of `tmp.restart.XXX`. This file contains the informations needed to restart from the last run. To restart from this file, we need to replace the line 
```
read_data      a-Si-0.2-G.lmp
```
with
```
read_restart    ../1800/tmp.restart.9000000
```
`../1800/tmp.restart.9000000` is the relative path to the restart file and `..` means the upper directory. Since we are going to firstly run the calculation of temperature 1825K, so you also need to change the temperature to 1825K.
```
fix             24 all npt temp 1825 1825 0.1 iso 1.0 1.0 1000
`
Then to submit multiple runs in once, you need the `run.sh` file and revise it accordingly. You only need to change these 3 lines.
```
total=18000000 # change this one with the XXX value of the restart file
temp=1825 # change this one with the first temperature to calculate

for i in 1825 1850 # change this one with the temperatures you are going to calculate
```

After you finish the revision. You can submit multiple jobs by just use the following command

```
./run.sh
```




