### Inspect the fast5 files
Install HDF5 Tools
```
sudo apt install hdf5-tools
```
Inspect the files
h5dump -- Enables a user to examine the contents of an HDF5 file and dump those contents to an ASCII file.
h5ls -- Lists specified features of HDF5 file contents.
In order to get the complete content of a fast5 in readable form, you can use:
```
h5dump data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5 | more
```
To get an overview on all reads, you could use the h5ls command:
```
h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5
```
Which you can simply count to get the number of reads in your fast5 file:
```
h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5 | wc -l
```
n order to inspect what is stored for an individual read, you can specify that read, as if it were a directory using h5ls:
```
h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_a3d14887-0d45-4ef5-8a20-42af8257053d
```
or (group2):
```
h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_0061d165-af04-4c39-ad5e-8c4ebe3caa80

```
Let’s assume, we are interested in the raw data of a specific read:

```
h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_a3d14887-0d45-4ef5-8a20-42af8257053d/Raw
```
or (group2):
```
h5ls data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_0061d165-af04-4c39-ad5e-8c4ebe3caa80/Raw
```
So we have reached the actual raw data (indicated by “Dataset”). To view a dataset, h5ls has a ‘-d’ option:
```
h5ls -d data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_a3d14887-0d45-4ef5-8a20-42af8257053d/Raw/Signal
```
or (group2):
```
h5ls -d data/fast5_tiny/GXB01322_20181217_FAK35493_GA10000_sequencing_run_Run00014_MIN106_RBK004_46674_0.fast5/read_0061d165-af04-4c39-ad5e-8c4ebe3caa80/Raw/Signal
```