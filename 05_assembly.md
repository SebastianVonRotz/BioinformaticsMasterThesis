### Assembly (did not yet work)
Assembly with canu
Canu is a fork of the Celera Assembler, designed for high-noise single-molecule sequencing (such as the PacBio RS II/Sequel or Oxford Nanopore MinION). Documentation can be found here:     http://canu.readthedocs.io/en/latest/  
Error correction with the parameter:  
-correct       - generate corrected reads    
followed by trimming and assembly with the following parameters:    
-trim-assemble - generate trimmed reads and then assemble them    
You could also run the assembly completely in one step by leaving out both of these parameters. Running it in two steps has the advantage, that both steps can be tested individually for good parameters without running both each time again.  
**Install Canu**  
Downloaded the Canu software directly as follos:

```
wget https://github.com/marbl/canu/releases/download/v2.0/canu-2.0.Linux-amd64.tar.xz
tar -xJf canu-2.0.*.tar.xz
```
**Generate corrected reads**  
The correction stage selects the best overlaps to use for correction, estimates corrected read lengths, and generates corrected reads:  
```
~/software/canu-2.0/*/bin/canu -correct -d ~/workdir/correct_small -p assembly   genomeSize=3m useGrid=false -nanopore-raw   ~/workdir/basecall_small/basecall.fastq.gz
```
Have a look at the generated contigs
```
grep '>' ~/workdir/assembly_small/assembly.contigs.fasta
```