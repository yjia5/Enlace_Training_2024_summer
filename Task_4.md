## Task 4: Downstream analysis the result
### Step 1. Read Literature - Radial distribution functions (RDF)
The atomic structure can be characterized by many parameters. One ordinary parameter used is radial distribution functions. Read the following reference to understand what it is.

https://chem.libretexts.org/Bookshelves/Biological_Chemistry/Concepts_in_Biophysical_Chemistry_(Tokmakoff)/01%3A_Water_and_Aqueous_Solutions/01%3A_Fluids/1.02%3A_Radial_Distribution_Function

The system we are going to study is Silicon (Si). We are going to study different phases of Si, including liquid, crystal and amorphous phases. Read these literatures to find the differences in the RDFs of these three phases. Please work together and write a few paragraphs to describe the differences and email to me.

https://arxiv.org/html/2401.09869v1

https://journals.aps.org/prb/pdf/10.1103/PhysRevB.71.094102

### Step 2. Run Python on expanse
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
pip install lammps_logfile
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

### Step 4. Visualize 
### Step 5. Calculate RDF



