# Master Thesis Notes of Sebastian von Rotz
Here are all the notes are presented for my master thesis **"Evaluation and development of a bioinformatics workflow for amplicon sequencing with nanopore long read technology"**, which is conducted at the EGSB group at ZHAW. The notes can be navigated in a non hyrarchical manner as the notes are structured with Obsidian md.

### POND-Framework
One major result of this thesis the the POND-Framework. This framework enables a simple script based aproach for automated processing of nanopore data on a remote server with a Slurm Workload Manager. It requires a unix shell for setting the alias commands and the installation of the tools needed for each processing steps. The tools are either available as a modules on slurm or are installed with a local user. Every script can be run in a step by step manner, but the user has check that the the dependent scripts are processed before each other. The automation is implemented with the dependency command in the slurm envrionment.  
  
The Framework is hosted as a separate repository with a detailed guide and descriptions under:  
**https://github.com/SebastianVonRotz/POND**

## Overview and Tasks
Current working tasks and ToDos are managed here. Also the most important notes and logging files are listed.  
#### Thesis Tasks and Markdown Presentation
[[tasks_master_thesis]]  
[[tasks_master_thesis]]  
[[Work_Time_and_Task_Log]]  
#### Varia
[[Links_and_Infos_around_Thesis_Topics]] 
[[Notes_for_Considerations]]  
[[Tools_for_Master_Thesis]]  
[[Thesis_Presentation]]  

## Workpackages
Workpackages are the main bulk of logging the ongoing work on the thesis. This includes the logging of steps in order to process the data and every step along the way to the results which are included in the thesis.
#### Data Processing
[[workpackage_01]] 
#### Installation of Tools and Programs
[[workpackage_02]] 
#### Define Structure of Framework
[[workpackage_03]] 
#### Define Graphs and Visualizations
[[workpackage_04]]


## Result R Markdown Notebook
Here the Markdown Notebooks are shown. This is based on the export of those notebooks as pdf pages.
#### Workflow Comparison
[[Workflow_Comparison.pdf]]

## Specific Tasks 
Tasks are containing notes on trainings needed to implement the framework and writing processing scripts. Furthermore a lot of logging is presented which helped to manage the workload around the thesis.
#### Workflow and Data
[[ma_task_03_OverviewPerformedWorkflows]]  
[[ma_task_07_DataAndWorkflowVisualization]]  
[[ma_task_05_MasterThesisSetup]]  
[[ma_task_02_DescribeDataSources]]  
[[ma_task_15_GithubCommands]]  

#### Publication Processing and Tools
[[ma_task_04_BioinformaticsToolList]]
[[ma_task_06_AddNewPublicationCategList]]
[[ma_task_08_TheoryReadPublications]]
[[ma_task_14_TrackWritingOfThesis]]
[[ma_task_01_ReannotatePublicationToolList]] #Done

####  Training and Notes
[[ma_task_12_hpcCommands]] #Done
[[ma_task_11_NanoporeTraining]] #Done
[[ma_task_10_BashTraining]] #Done
[[ma_task_13_RegularExpressions]] #Done
[[ma_task_09_BashCommands]] #Done

## Meeting Notes
Here the the meetings with supervisor and involved researcher are listed.  
  
[[joel_18.01.2021| Meeting - 07]]  
[[joel_07.12.2020| Meeting - 06]]  
[[joel_28.10.2020| Meeting - 05]]  
[[joel_fabio_10.08.2020| Meeting - 04]]  
[[joel_06.04.2020| Meeting - 03]]  
[[joel_18.03.2020| Meeting - 02]]  
[[joel_20.02.2020 | Meeting - 01]]  

## Archived
Depreciated notes  
  
[[raw_data_crispr_run]]  
[[trackmodule_2_review]]  
[[naming_framework]]

# Motto
**If There is a problem with vairables and path check first if the files are all in unix!!!**
