### Annotate genome (not yet done, requires a lot of dependencies)
Create the genome file for annotation
```
mkdir Annotation
cat ~/workdir/results/racon_medaka_pilon/pilon_round4.fasta | sed -e 's/>tig.*/>genome_sequence/g' > ~/workdir/Annotation/genome.fasta
```