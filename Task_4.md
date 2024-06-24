## Task 4: Downstream analysis the result
### Step 1. Read Literature - Radial distribution functions (RDF)
The atomic structure can be characterized by many parameters. One ordinary parameter used is radial distribution functions. Read the following reference to understand what it is.

https://chem.libretexts.org/Bookshelves/Biological_Chemistry/Concepts_in_Biophysical_Chemistry_(Tokmakoff)/01%3A_Water_and_Aqueous_Solutions/01%3A_Fluids/1.02%3A_Radial_Distribution_Function

The system we are going to study is Silicon (Si). We are going to study different phases of Si, including liquid, crystal and amorphous phases. Read these literatures to find the differences in the RDFs of these three phases. Please work together and write a few paragraphs in a report to describe the differences and email to me.

https://arxiv.org/html/2401.09869v1

https://journals.aps.org/prb/pdf/10.1103/PhysRevB.71.094102

### Step 2. Run Python on expanse
Firstly, you need to start an interactive job in case the memory provided by the log node is not enough.
```
srun --partition=debug  --pty --account="csd877" --nodes=1 --ntasks-per-node=2 --mem=8G -t 00:30:00 --wait=0 --export=ALL /bin/bash
```
This command is going to require 1 node with 2 core in the queue named `debug`. The memory required is 8G for each core. And the time required is 30 min. You can change these parameters as you need.

Before using python, you need to load python envrionment
```
module load cpu/0.15.4  gcc/10.2.0 python/3.8.5
```
Then you should load python 3.8.5 to the envrionment. To check the version of python
```
python --version
```
To install packages we need for the following calculation:
```
pip install lammps_logfile matplotlib ase
```
To check whether you installed the package correctly,

```
python
>>> import lammps_logfile
```
If there is no any errors, you should good to go. Then you can exist python
```
exit()
```
Check this link if you are not able to install lammps_logfile correctly. https://github.com/henriasv/lammps-logfile
### Step 3. Plot time VS energy & time VS temperature
Go to the test directory you run in Task 2. We are going to read the log file and plot the data.
```
cd test
```
Copy the file `step_temp.py` under the tools directory
```
cp tools/step_temp.py lammps/
```
Go to lammps directory
```
cd lammps
```
run the python script `step_temp.py`.
```
python step_temp.py
```
If the code go through, you should get a picture file named step_temp.png. To check it, the easiest way is using the Expanse Portal. But since the Expase Portal can only read directory scratch and home directories, you need to copy this file to scratch or home directory. I would suggest using scratch directory.
```
cp step_temp.png /expanse/lustre/scratch/YOUR_URSERNAME/temp_project
```
Then go to the expanse portal >> Files >> Scratch
![image](https://github.com/yjia5/Enlace_Training_2024_summer/assets/53623594/7b64c51f-2379-4735-bb78-48df0866787d)

You should be able to find the file. You can open it in website or download it.

Now let's understand what is writen in the python script step_temp.py
```
import lammps_logfile                          # load module
import os                                      # load module
print(os.getcwd())                             # show the current directory
log = lammps_logfile.File("./log.lammps")      # read the file named log.lammps
x = log.get("Step")                            # read the data in the colume of "Step" and save into the variable x
y = log.get("Temp")                            # read the data in the colume of "Temp" and save into the variable y

print(y)                                       # print out variable y
print(len(x))                                  # print out the length of x
import matplotlib.pyplot as plt                # import module
plt.plot(x[2:]/1000,y[2:])                     # plot x vs y
plt.xlabel("Time (ps)")                        # set up x label
plt.ylabel("Temperature (K)")                  # set up y label
plt.savefig("./step_temp.png")                 # save the figure into file step_temp.png
plt.show()                                     # show the figure

```
You can find that this python code read the log file of lammps `log.lammps`. In specific this set of data
![image](https://github.com/yjia5/Enlace_Training_2024_summer/assets/53623594/cb6851a1-804e-48f3-b05c-07ddc4fa4873)

The figure used the columes headed with `Step` and `Temp`. Now it is your turn to revise the script to plot a figure of `Step` VS `TotEng`. Please work together and plot these two figures and save them into your report.

### Step 4. Visualize 
To visualize the trajectory of molecular dynamic simulations, you need to download the software OVITO (https://www.ovito.org/). Please install it to your own computer. 

Then we need to download the file `dump.melt` to your own computer. As present above, you can copy it to scratch directory and download it through the portal.

Then you just need to open this `dump.melt` file by OVITO. You can see how the atoms move by pressing start butten (the triangle) at the right corner.
![image](https://github.com/yjia5/Enlace_Training_2024_summer/assets/53623594/56f74d97-43d3-4368-b25f-adc7023c990a)
You can also stop the movie by pressing this butten again. Please play around with the other few buttons to see what happend.

Observe the positions of atoms, please try to screenshot the atoms structures you believe they are in liquid or amorphous (the beginning structure at step 0 is amorphous). Save these figures to your report.

### Step 5. Calculate RDF
Copy the python script to your own folder
```
cp /expanse/lustre/projects/csd877/yjia3/share/lmp_Si_test/tools/plot_rdf.py ./
```
to run the script,
```
python plot_rdf.py
```
If the code runs successfully, you should have a file created named `Si_RDF.png`, which is the RDF of the last snapshot saved in trajectory output `dump.melt`.
The code decide which snapshot to plot by the line:
```
selected_indice = '-1:
```
Open the file `plot_rdf.py` and change to the index of the snapshot you want to plot. You can revise it to any number in the range between 0 (the first snapshot) and the length of trajectory minus 1 (the last snapshot). In python, you can also index the last one with -1 as writen in the script.

Please plot the RDF of amorphous snapshot (The first snapshot) and liquid snapshot you choose. Save the figures to your report.

Finally, write captions to your figures and describe them with a few words to make sure I can understand what they are. After the report is finished, please email to me.

