#### fast5 inspection
```
#!/bin/bash
#
#SBATCH --job-name=hdf5-test
#
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=8
#SBATCH --time=02:00:00
#SBATCH --partition=single
#SBATCH --qos=single
#SBATCH --mail-type=end
#SBATCH --mail-user=voro@zhaw.ch

module purge
module load USS/2019 gcc/7.3.0 openmpi/3.1.3 hdf5/1.10.4

#######
# h5dump -- Enables a user to examine the contents of an HDF5 file and dump those contents to an ASCII file.
# h5ls -- Lists specified features of HDF5 file contents.
#######
 
# Get the complete content of a fast5 in readable form
######################################################
h5dump data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5 | more
## Returns: Readable output

# Get an overview on all reads
######################################################
#h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5
## Returns: List of reads

# Get the number of reads
######################################################
#h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5 | wc -l
## Returns: Number of reads (426)

# Inspect data stored for an individual read
######################################################
#h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_a3d14887-0d45-4ef5-8a20-42af8257053d
## Returns: Subdirectories for this specific read

# Inspect raw data stored for an individual read
######################################################
#h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_a3d14887-0d45-4ef5-8a20-42af8257053d/Raw
## Returns: Dataset for this specific read

# View the 'Dataset' associated to an individual read in order to see the raw data
######
#h5ls -d data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_a3d14887-0d45-4ef5-8a20-42af8257053d/Raw/Signal
## Returns: Returns raw signal

##### That's it folks!

```