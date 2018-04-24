# ECOL-346-HPC-demo
Excercise for ECOL-346 Bioinformatics class

## 1. Set up your work environment and get all the code

### a. Go to UA Dashboard 
https://ood.hpc.arizona.edu/pun/sys/dashboard

### b. Start an Interactive Jupyter Notebook
- Choose 1 hour, 1 core, standard queue
- Make sure your account is correct
- Connect to Jupyter 

### c. Create new terminal or Jupyter Notebook
We are doing this so we don't get slowed down on the login node.

Use a Bash kernel Jupyter Notebook if you want to have notes to look back on!

### d. Clone the demo repository
```
git clone https://github.com/agladstein/ECOL-346-HPC-demo.git
cd ECOL-346-HPC-demo
```

### e. Clone SimPrily
```
git clone https://github.com/agladstein/SimPrily.git
```

### f. Double check you got SimPrily correctly
```
python SimPrily/simprily.py --help
```

#### If SimPrily does not work, use the Singularity image
Load the Singularity module
```
module load singularity
```

Use Singularity to pull the Image
```
cd SimPrily
singularity pull docker://agladstein/simprily
```

Try SimPrily with the Singularity container
```
singularity exec simprily.simg python /app/simprily.py --help
```



## 2. Run simulations

__ALWAYS TEST SMALL FIRST!___

### a. Try to run 1 simulation in interactive session
```
cd SimPrily
python simprily.py -p examples/eg1/param_file_eg1.txt -m examples/eg1/model_file_eg1.csv -i test -o output
```

*If you had to use the Singularity containter, run like this:*
```
singularity exec simprily.simg python /app/simprily.py -p examples/eg1/param_file_eg1.txt -m examples/eg1/model_file_eg1.csv -i test -o output
```

Make sure you have results in:
`output/results/`

### b. Submit 1 job of 1 simulation to Ocelote

Open simprily_simple.pbs, and change `group` to your group.

What queue are we running on?  
How many cores are we asking for?   
How many wall hours are we asking for?  

`cd` back to `ECOL-346-HPC-demo` and submit the job
```
qsub simprily_simple.pbs
```

Check the status of the queue
```
qstat -u [user-name]
```

Once it completed, check your `simprily1.o*` file for any errors, and check `SimPrily/output/results/`

*You might need to use the singularity container. If you do, change the pbs script as needed.*

### c. Submit 1000 simulations to Ocelote

#### Single Core
Open simprily_batch.pbs, and change `group` to your group.

What is different about this pbs script?  
How are we running 1000?  
How many cores are we asking fo?  
How many wall hours are we asking for?  

Submit the job
```
qsub simprily_batch.pbs
```

Check the status of the queue
```
qstat -u [user-name]
```

Check the progress of your batch job
```
qstat -t [jobid]
```

```
qstat -f [jobid]
```

Once it completed, check one of the `simprilyB.o*` file for any errors, and check `output/` for results


#### Multi core
Open simprily_parallel.pbs, and change `group` to your group.

What is different about this pbs script?  
How are we running 1000?  
How many cores are we asking for?  
How many wall hours are we asking for?  

Submit the job
```
qsub simprily_parallel.pbs
```

Check the status of the queue
```
qstat -u [user-name]
```

Check the progress of your batch job.  
How many jobs do you expect?
```
qstat -t [jobid]
```

```
qstat -f [jobid]
```

Once it completed, check one of the `simprilyP.o*` file for any errors, and check `output/` for results


__For this use case, which is better - single core or multi core?__


## Bonus!

Combine the results into one file.