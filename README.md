# Master Thesis Notes of Sebastian von Rotz
Here are all the notes are presented for my master thesis **"Evaluation and development of a bioinformatics workflow for amplicon sequencing with nanopore long read technology"**, which is conducted at the EGSB group at ZHAW. The notes can be navigated in a non hyrarchical manner as the notes are structured with Obsidian md.

### POND-Framework
One major result of this thesis the the POND-Framework. This framework enables a simple script based aproach for automated processing of nanopore data on a remote server with a Slurm Workload Manager. It requires a unix shell for setting the alias commands and the installation of the tools needed for each processing steps. The tools are either available as a modules on slurm or are installed with a local user. Every script can be run in a step by step manner, but the user has check that the the dependent scripts are processed before each other. The automation is implemented with the dependency command in the slurm envrionment.  
  
The Framework is hosted as a separate repository with a detailed guide and descriptions under:  
**https://github.com/SebastianVonRotz/POND**

## Overview and Tasks
Current working tasks and ToDos are managed here. Also the most important notes and logging files are listed.  
### Thesis Tasks and Markdown Presentation
[[Tasks Master Thesis]]  
[[Work Time and Task Log]]  
### Varia
[[Links and Infos around Thesis Topics]] 
[[Notes for Considerations]]  
[[Tools for Master Thesis]]  
[[Thesis Presentation]]  

## Workpackages
Workpackages are the main bulk of logging the ongoing work on the thesis. This includes the logging of steps in order to process the data and every step along the way to the results which are included in the thesis.
### Data Processing
[[WP - 01]] 
### Installation of Tools and Programs
[[WP - 02]] 
### Define Structure of Framework
[[WP - 03]] 
### Define Graphs and Visualizations
[[WP - 04]]

# Result R Markdown Notebook
Here the Markdown Notebooks are shown. This is based on the export of those notebooks as pdf pages.
#### Workflow Comparison
[[pdf_jpg_test]]  
[[pdf_jpg_test2]]

# Specific Tasks 
Tasks are containing notes on trainings needed to implement the framework and writing processing scripts. Furthermore a lot of logging is presented which helped to manage the workload around the thesis.
#### Workflow and Data
[[Task - 05 - Setup of the Mater Thesis]]  
[[ma_task_02_DescribeDataSources]]  
[[ma_task_15_GithubCommands]]  

#### Publication Processing and Tools
[[ma_task_04_BioinformaticsToolList]]
[[ma_task_06_AddNewPublicationCategList]]
[[ma_task_08_TheoryReadPublications]]
[[ma_task_14_TrackWritingOfThesis]]
[[ma_task_01_ReannotatePublicationToolList]]

####  Training and Notes
[[ma_task_12_hpcCommands]]
[[ma_task_11_NanoporeTraining]]
[[ma_task_10_BashTraining]]
[[ma_task_13_RegularExpressions]]
[[ma_task_09_BashCommands]]

## Meeting Notes
Here the the meetings with supervisor and involved researcher are listed.  
  
[[joel_18.01.2021| Meeting - 07]]  
[[joel_07.12.2020| Meeting - 06]]  
[[joel_28.10.2020| Meeting - 05]]  
[[joel_fabio_10.08.2020| Meeting - 04]]  
[[joel_06.04.2020| Meeting - 03]]  
[[joel_18.03.2020| Meeting - 02]]  
[[Meeting - 01]]  

## Archived
Depreciated notes  

[[raw_data_crispr_run]]  
[[trackmodule_2_review]]  
[[naming_framework]]
[[ma_task_07_DataAndWorkflowVisualization]]  
[[ma_task_03_OverviewPerformedWorkflows]]  

# Motto
**If There is a problem with vairables and path check first if the files are all in unix!!!**
