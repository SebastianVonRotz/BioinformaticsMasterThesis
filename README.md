# Master Thesis Notes of Sebastian von Rotz
This website contains all of the notes of my master thesis **"Evaluation and development of a bioinformatics workflow for amplicon sequencing with nanopore long read technology"**, which is conducted at the EGSB group at ZHAW. The notes can be navigated in a non hyrarchical manner as the notes are structured with Obsidian md. The picture below shows the structure of the notes:
![[Pasted image 20210611093752.png]]

## POND-Framework
One major result of this thesis the the POND-Framework. This framework enables a simple script based aproach for automated processing of nanopore data on a remote server with a Slurm Workload Manager. It requires a unix shell for setting the alias commands and the installation of the tools needed for each processing steps. The tools are either available as a modules on Slurm or are installed with a local user. Every script can be run in a step by step manner, but the user has check that the the dependent scripts are processed before each other. The automation is implemented with the dependency command in the Slurm environment.  
  
The Framework is hosted as a separate repository with a detailed guide and descriptions under:  
**https://github.com/SebastianVonRotz/POND**

## Overview and Tasks
Current working tasks and ToDos are managed here. Also the most important notes and logging files are listed.  

### Thesis Tasks and Markdown Presentation
[[Tasks Master Thesis]]  
[[Work Time and Task Log]]  

## Workpackages
Workpackages are the main bulk of logging the ongoing work on the thesis. This includes the logging of steps in order to process the data and every step along the way to the results which are included in the thesis.
### Data Processing
[[WP - 01]] 
### Installation of Tools and Programs
[[WP - 02]] 
### Defines Tasks around the Thesis
[[WP - 03]] 
### Training and Notes on Commands
[[WP - 04]]
### R Notebooks
[[WP - 05]]

### Varia
[[Links and Infos around Thesis Topics]]  
[[Notes for Considerations]]  
[[Tools for Master Thesis]]  
[[Thesis Presentation]]  
# Result R Markdown Notebook
Here the Markdown Notebooks are shown. This is based on the export of those notebooks as pdf pages.
## Workflow Comparison
[[pdf_jpg_test]]  
[[pdf_jpg_test2]]

# Meeting Notes
Here the the meetings with supervisor and involved researcher are listed.  
[[Meeting - 08]]  
[[Meeting - 07]]  
[[Meeting - 06]]  
[[Meeting - 05]]  
[[Meeting - 04]]  
[[Meeting - 03]]  
[[Meeting - 02]]  
[[Meeting - 01]]  

# Archived
Depreciated notes  are stored here
[[archived]]



### Check first if Problem arises
**If There is a problem with vairables and path check first if the files are all in unix format!!!**


