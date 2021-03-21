### Data Quality Assessment
Get the R script
```
wget https://raw.githubusercontent.com/roblanf/minion_qc/master/MinIONQC.R -O MinIONQC.R
```
Install R on Unix first
Run MinIONQC on nanopore data:

```
cd ~/workdir
mkdir -p ~/workdir/MinIONQC
Rscript ~/MinIONQC.R -i basecall -q 12 -o MinIONQC -p 14
```

This will create several analysis plots. After that, you can load the plots in your web browser by using a file browser.
Again, check out the corresponding home page to learn more about all generated results: https://github.com/roblanf/minion_qc

**FastQC**
FastQC aims to provide a simple way to do some quality control checks on raw sequence data coming from high throughput sequencing pipelines.
```
cd ~/workdir
mkdir -p ~/workdir/fastqc/nanopore_fastqc
mkdir -p ~/workdir/fastqc/illumina_fastqc
fastqc -t 14 -o ~/workdir/fastqc/nanopore_fastqc ~/workdir/basecall/basecall.fastq.gz
fastqc -t 14 -o ~/workdir/fastqc/illumina_fastqc ~/workdir/data/illumina/Illumina_R1.fastq.gz ~/workdir/data/illumina/Illumina_R2.fastq.gz
```
After that, you can load the reports in your web browser. Open a file browser, go to your workdir/fastqc/ directory and double click the html file.
**Handle adapter contamination**
As we see some strange GC content at the 5’ end of our nanopore reads, we can alter the way the plots are generated and turn off the grouping of reads into bins. Notice, this will generate very huge plots! To avoid this, we will first trim our reads to the first 100 base positions and do the analysis only on that:
So the first bases may indicate an adaptor contamination. For workflows including de novo assembly refined with nanopolish or medaka adaptor trimming is not necessary, but in other workflow scenarios this can be important to do and good there are tools which can handle this, as e.g. porechop.
References
FastQC https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
Porechop https://github.com/rrwick/Porechop
Generating Error Profiles
**Mapping the data**
GraphMap is a novel mapper targeted at aligning long, error-prone third-generation sequencing data. It is designed to handle Oxford Nanopore MinION 1d and 2d reads with very high sensitivity and accuracy, and also presents a significant improvement over the state-of-the-art for PacBio read mappers.
GraphMap was also designed for ease-of-use: the default parameters can handle a wide range of read lengths and error profiles, including: Illumina, PacBio and Oxford Nanopore. Currently, graphmapper provides two core modules, an aligner and an overlapper. We’re using the aligner here for the mapping procedure.
The shortened usage message of the aligner:
```
graphmap align --help
```
See following for tutorial:
https://denbi-nanopore-training-course.readthedocs.io/en/latest/read_qc/ReadMapping.html