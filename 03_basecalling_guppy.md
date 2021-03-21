### Basecalling with Guppy
**Install guppy first**
To install the CPU-only version of Guppy.
Installing from the tar.gz archive file, follow the instructions below:
Download the .tar.gz archive file.
```
wget https://mirror.oxfordnanoportal.com/software/analysis/ont-guppy-cpu_3.4.5_linux64.tar.gz
```
This can be found on the Software Downloads page of the Nanopore Community.
Unpack the archive:
To unpack the CPU-only version of Guppy:
```
 tar -xf ont-guppy-cpu_xxx_linux64.tar.gz
```
Get the list of the available flow cells
```
~/software/ont-guppy-cpu/bin/guppy_basecaller --print_workflows
```
Our dataset was generated using the FLO-MIN106 flowcell, and the LSK109 kit, so we can use the dna_r9.4.1_450bps_hac model.
```
~/software/ont-guppy-cpu/bin/guppy_basecaller --compress_fastq -i ~/workdir/data/fast5_tiny/ -s ~/workdir/basecall_tiny/ --cpu_threads_per_caller 14 --num_callers 1 -c dna_r9.4.1_450bps_hac.cfg
```
**Inspect the output**
The directory contains the following output:
```
ls -l ~/workdir/basecall_tiny/
```
So we have one fastq file in our directory - since we started with one fast5 file. Ususally, we should merge all resulting fastq files into a single file:
```
cat ~/workdir/basecall_tiny/*.fastq.gz > ~/workdir/basecall_tiny/basecall.fastq.gz
```
In order to get the number of reads in our fastq file, we can count the number of lines and divide by 4:
```
zcat ~/workdir/basecall_tiny/basecall.fastq.gz | wc -l | awk '{print $1/4}'
```
Copy files (here the full results are copied)
```
cp -r ~/workdir/results/basecall_small/ ~/workdir/.
cp -r ~/workdir/results/basecall/ ~/workdir/.
```
And again, we are merging all fastq files:
```
cat ~/workdir/basecall/*runid*.fastq.gz > ~/workdir/basecall/basecall.fastq.gz
cat ~/workdir/basecall_small/*runid*.fastq.gz > ~/workdir/basecall_small/basecall.fastq.gz
```
If you want, you can check again for the number of reads:
```
zcat ~/workdir/basecall_small/basecall.fastq.gz | wc | awk '{print $1/4}'
```
or
```
zcat ~/workdir/basecall/basecall.fastq.gz | wc | awk '{print $1/4}'
```