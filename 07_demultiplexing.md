#### De-Multiplexing After Basecalling
```
#!/bin/bash
#
#SBATCH --job-name=guppy_barcoder_example
#
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=4
#SBATCH --cpus-per-task=8
#
# Adjust reasonable time
#SBATCH --time=48:00:00
#
# You may also use the single partition/qos if one node is sufficient
#SBATCH --partition=single
#SBATCH --qos=single
#
# Notification settings
#SBATCH --mail-type=end
#SBATCH --mail-user=poth@zhaw.ch
#
# Maybe    restrict possible nodes    using --exclude=node00[1-8],node40[1-8]    to only    use the    newest compute nodes e.g. in case you need the memory.

# Load modules of dependencies
#module purge
module load slurm

# Add bin dir for guppy PATH:
export PATH=$PATH:/cfs/earth/scratch/poth/localapps/ont-guppy-cpu/bin

# Run the guppy application here
#guppy_barcoder --help
#guppy_barcoder --print_kits
guppy_barcoder -i ./run_0010/basecalling -s ./run_0010/demultiplexed --flowcell FLO-MIN106 --kit SQK-LSK109
```