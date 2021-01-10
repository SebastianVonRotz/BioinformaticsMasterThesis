

# Tasks
**If There is a problem with vairables and path check first if the files are all in unix!!!**

## General Tasks
[[tasks_master]]
[[acls_presentation]]
[[notes_considerations]]


# Info/General
[[log_master]]
[[ma_topic_links_infos]]


# Workpackages
[[workpackage_01]] Data Processing
[[workpackage_02]] Installing Programs
[[workpackage_03]] Define Structure 
[[workpackage_04]] Define Visualizations


## Specific Tasks 
#### Workflow and Data
[[ma_task_03_OverviewPerformedWorkflows]]
[[ma_task_07_DataAndWorkflowVisualization]]
[[ma_task_05_MasterThesisSetup]]
[[ma_task_02_DescribeDataSources]]

#### Publication Processing and Tools
[[ma_task_01_ReannotatePublicationToolList]] #Done
[[ma_task_04_BioinformaticsToolList]]
[[ma_task_06_AddNewPublicationCategList]]
[[ma_task_08_TheoryReadPublications]]
[[ma_task_14_TrackWritingOfThesis]]


####  Training and Notes
[[ma_task_12_hpcCommands]] #Done
[[ma_task_11_NanoporeTraining]] #Done
[[ma_task_10_BashTraining]] #Done
[[ma_task_13_RegularExpressions]] #Done
[[ma_task_09_BashCommands]] #Done


# MA Tools Overview
[[master_thesis_tool_list]]

# Meeting Notes
[[joel_07.12.2020]]
[[joel_28.10.2020]]
[[joel_fabio_10.08.2020]]
[[joel_20.02.2020]]
[[joel_18.03.2020]]
[[joel_06.04.2020]]


# Archived
[[raw_data_crispr_run]]
[[trackmodule_2_review]]



# Create ssh git remote 

read local ssh key
	
	cat ~/.ssh/id_rsa.pub

Check current remote connection type (type is based on ssh or https)	
	
	git remote get-url origin

remove the current remote connection

	git remote remove origin

Add your ssh key to the github repo

![[Pasted image 20210101141855.png]]

Add the github repo

	git remote add origin  git@github.zhaw.ch:voro/MA-Bioinformatics-Workflows.git

Check if it is added

	git remote -v

Set the push to upstream (https://stackoverflow.com/questions/37770467/why-do-i-have-to-git-push-set-upstream-origin-branch)

	git push --set-upstream origin master