## Task 4: Downstream analysis the result
### Step 1. Read Literature - Radial distribution functions (RDF)
The atomic structure can be characterized by many parameters. One ordinary parameter used is radial distribution functions. Read the following reference to understand what it is.

https://chem.libretexts.org/Bookshelves/Biological_Chemistry/Concepts_in_Biophysical_Chemistry_(Tokmakoff)/01%3A_Water_and_Aqueous_Solutions/01%3A_Fluids/1.02%3A_Radial_Distribution_Function

The system we are going to study is Silicon (Si). We are going to study different phases of Si, including liquid, crystal and amorphous phases. Read these literatures to find the differences in the RDFs of these three phases. Please work together and write a few paragrphas to describe the differences.

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

### Step 4. Visualize 
### Step 5. Calculate RDF



