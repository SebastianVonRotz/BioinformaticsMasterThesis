#### Meeting 06.04.20 10:00
Questions and infos
* ~~16S Workflows comparable?~~    
  Yes can be used as reference, but pipeline should be applicable for amplicons in general
* ~~Bonito works on the GPU~~   
  Cluster Fine but use of GPU in general is not common in bioinformatics pipeline, so far
* ~~Flappie is build with cmake and other dependencies what is the correct way here?~~   
  Just keep trying, but not a priority
* ~~Should I compare the basecalling methods with a real pipeline?~~   
  Focus more on the CRISPR workflow, but it should be applicable for other workflows too

Make "Support"(it SW can still be used) a parameter (e.g. porechop is not supported)
Basecalling demultiplexing assembly focus on CRISPR Workflow
Propose a workflow in the end
EP2ME Plattform probalably not good if just Blast used for 16S not good with low accuracy of 80% (end up in another family)
  Quality check?
Q7 what is the quality score here? Q7 vs Q14 (https://drive5.com/usearch/manual/quality_score.html)
Check actual Workflow, get data, try go end of the process
chimeras detected in the works of Samuel and Simon
Recreate CRISPR Workflow, probably most of the steps are similar to other amplicon based pipelines
Work with reference based methods is better than de novo
de novo not the best approach
First steps are always the same
Goal is getting a fully automated workflow