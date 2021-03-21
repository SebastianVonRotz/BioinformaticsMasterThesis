### Master Tasks:
#### Current
~~Write Methods~~  
~~Write Results until Filtering tools~~  
~~Implement Result Pictures~~  
Define DB Comparison with Kraken2  
Process data with Kraken2  
Implement Workflow for Processing Crispr Data  
~~Update Github with POND and update README~~  

#### General
* [x] Check Template of Stefans Latex setup
* [x] Checkout uDocker
* [x] Check if only flowcell and kits are used (All other users should select flow cell and kit instead)
* [x] Create a wiki of the obsidian notes on github pages or obsidian publish
* [x] Define the Goals for the Thesis!
* [ ] How to check dependencies on the server
* [ ] Consolidate structure of the obsidian notes
* [ ] Send Excel and Visio files to the Github Repository
* [ ] Think about how to present dependencies of the tools for the user


#### Presentations
* [ ] Transfer ppt into markdown presentation
* [ ] Change Master Thesis Output to the Vercell Website!

#### Github Repos
* [ ] Define User requirements in detail
* [ ] Finish Vercel Setup
	* [x] Enable strict line breaks
	* [x] Bring all markdown files into one dir
	* [x] Bring all pictures into assets
	* [ ] Change main md file to README.md
* [ ] Write new tasks
	* [x] Task Init (Create dirs)
	* [x] Task Task Help (like: https://github.com/janikvonrotz/dotfiles/blob/master/task) (replace docu in github)
	* [x] Task list scripts (same as help but shows available scripts)
	* [ ] Task verify (Check all tools / check if path exists / check if dataset and dataname in exits)
	* [ ] Task run-wf (run a workflow
	* [x] Task list (list scripts and workflows)
* [x] Comment the env file (check if command)
* [x] Adjust scripts with the grep command
* [x] Explain Datatransfer in the README
* [ ] Create Tool dependencies
	* [x] List the version with which the setup has been tested #Current 
	* [ ] Create a short install guide
#### Scripts and Workflows
* [ ] Create a for loop based basecalling for automated subdir detection (no adjustment of amount of arrays)
* [ ] Create a workflow script
* [ ] Is there a way to navigate arround the not flexible number of arrays for the workflow -> Geert

#### Writing
* [x] Write Generations of Sequencing 
* [ ] Add Pictures to the Generatios of Sequencing section
* [ ] Write Nanopore Technology section #Current

#### Dataset 16S rRNA
* [ ] Check out installed centrifuge
* [x] Do classification with Kraken2 and Greengenes DB
* [x] Classifiy the filered reads with Kraken2
* [x] Install Krona Tools for Visualization
* [x] Create Scripts for processing Kraken2 results
* [x] Create a krona script and process all D4/5 Datasets
* [x] Create a scirpt for processing the Kraken2 results
* [ ] Create a compariosn of the Kraken2 Stats
* [ ] Solve the taxid problem with the greengenes db #Current 
* [ ] [[joel_18.01.2021]]
* [ ] Reprocess Dataset 4/5 with EPI2ME (2020.04.06 -> Should have Genus Names)
* [ ] Filter the EPI2ME and Kraken2 Results for length and quality, then Compare workflows
* [ ] There is also data available run on the Illumina MiSeq

#### Dataset amoA Gene
* [ ] Replicate workflow with centrifuge
* [ ] Eventually automate it

#### Automated Workflow
* [ ] Do the assessment of hdf5 file (evntually with Nanoplot)
* [ ] Give histogram of barcodes (before and after filtering)
* [ ] Finish the first automated Workflow Setup #Current
* [ ]  Write Task Command for Workflow
* [ ]  Start automated Workflow for Dataset 6

#### General Workflow and Workpackages
* [ ] Setup GPU basecalling with Guppy

#### Tools which should be installed on the cluster
* [ ] qcat
* [ ] Kraken2
* [ ] guppy 4.4

#### Dataset Priority
* 16S RNA 1st priority
* amoA 2nd priority
* Crispr 2nd priority

### Done
* [x] Install Kraken2
* [x] Start basecalling of Dataset 4
* [x] Start basecalling of Dataset 5
* [x] Check if it is possible to submit a job wenn another is finished
* [x] Start writing
* [x] Start setting up the presentation for the ACLS
* [x] Install Kraken2 and DB
* [x] Start Writing Thesis
* [x] Check guppy performance and start array job
* [x] Transfer publications into Citavi
* [x] Finish Data source Overview
* [x] Create overview of the processed data
* [x] Bring all data to the quality filtered demultiplexed form
* [x] Use Kraken2 for raw demultiplexed dataset 4 and 5
* [x] Check the prename function and finalize array basecalling
* [x] Check Github repository
* [x] Finalize Data description of Dataset 4 and 5
* [x] Array output naming needs to be different!
* [x] Check with geert why the array output is not according to the description
* [x] Does one have to add an additional array because the last points to the slurm job?
* [x] Get a Citavi License key
* [x] Check if there will be container support on the hpc
* [x] Create Presentations with AE and PPT
* [x] Call Geert for the dependency workflow setup
* [x] Test the workflow crash setup
* [x] Local installation of guppy 4.4
* [x] Test Array guppy output not correct!
* [x] Check why arrays are not creating the subfolders
* [x] Create the presentation for the ACSL
* [x] Start basecalling of Dataset 5
* [x] Setup Arrays for faster processing
* [x] Discuss Tasks with Moritz
* [x] kraken / centrifuge already installed on hpc
* [x] Check available literature on amplicon mapping
* [x] Assess the workflows of the data already done 
* [x] Check on how to wait for finished sbatch run
* [x] Work on automated Workflow
* [x] Choose Taxonomy ID Tool for 16S RNA workflow
* [x] Eventually download data for 16S RNA workflow
* [x] Place the workflow publications from the computer on one drive
* [x] Filter and Trim with Nanofilt
* [x] Think about new file structure based on name of dataset for creting the directory and a manifest file
* [x] Finalize Filtering and Trimming excel
* [x] Check if Nanofilt still runs without x-permission on the files
* [x] Write Terminal Output into file (from the qcat application) --> Mail to Geert
* [x] Reintegrate the category table 
* [x] Sent Aufgabenstellung 
* [x] Lukas als dritter Korrektor?
* [x] Outline for Master Thesis and hand it in!
* [x] Setup new working place at IUNR
* [x] Write a description of the data
* [x] Find the corresponding thesis and publication to the data
* [x] Write about source of the data
* [x] Start transferring relevant papers into Citavi
* [x] Check Tool categorization
* [x] Re-annotate categorised Publications
* [x] Learn to write custom bioinformatics Software
* [x] Regex und Rosalind Training!
* [x] Bash Training
* [x] Ask on which node one can tryout running programs
* [x] Create workflow diagrams with the mermaid plugin
* [x] Use content ma_task_10_BashTraining for updating ma_task_09_BashCommands
* [x] Install qcat
* [x] reorder citavi knowledge elements
* [x] Entry bash commands and reorganize
* [x] Change workflow 2 and 3 to Workpackage 1 and 2
* [x] finish demultiplexing of datasets 1-3
* [x] Define quality cut off when data is basecalled -> Visio Workflow
* [x] Create overview of the Workspace setup
* [x] Check assignments to barcodes
* [x] Create a workflow diagram with mermaid plugin and load it to Github
* [x] Create ToDos for the Meeting
* [x] Turn wp_02 into a task
* [x] Read on Nanopore technology