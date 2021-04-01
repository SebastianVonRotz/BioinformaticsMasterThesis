# Workflow
### Goal
* [x] Basecall Dataset_1, Dataset_2 and Dataset_3 with Guppy
* [x] Get the runtime of each basecalling procedure
* [x] Installation of MinionQC
* [x] Check if MinIONQC can be run on VS Code
* [x] MinION QC disable the printing in order to resolve the x11 error
* [x] Check Nanoplot
* [x] Assess the basecalled datasets data with Nanoplot
* [x] Demultiplex data with guppy
* [x] Assess the basecalling and demultiplexing
* [x] Install qcat for demultiplexing
* [x] Demultiplex with qcat all of the datasets
* [x] Use Nanofilt for filtering the demultiplexed Datasets
* [x] Basecall Dataset_4, Dataset_5
* [x] Rename the Dataset_5 files processed with the array and put them into one directory
* [x] Reprocess D4 and D5 with the new setup
* [x] Test guppy_array with array prep input path (DATA\_PATH\_OUT=$DATA\_PATH\_IN../${DATASET\_NAME}\_Array/)
* [x] Create Plots of the stats from Kraken2 (see "Notebook_Kraken2_plots")
* [x] Classifiy D4/5 with Kraken2 and SILVA
* [x] Classifiy D4/5 with Kraken2 and RDP
* [x] Define Comparison of the different databases
* [ ] Use centrifuge for classification
* [ ] Create an excel overview of the data processing (matrix)
* [ ] Process data for the DB Comparison with Kraken2

# Log
[[dataprocessing_log_before_v0.1]]
___
# v0.1 !!!
**From here on commands and the setup changes drastically, the new setup is outlined in [[workpackage_03]]**
___
### Reprocessing of D4
The data is reprocessed in step by step manner. The id name is **sbs_01** (Step by Step 01) and the name of the dataset is **Dataset4**

[[D4_reprocessing_log]]

### Reprocessing of D5
The data is reprocessed in step by step manner. The id name is **Step_01** and the dataset name is **Dataset_5**

[[D5_reprocessing_log]]

___
### Processing of D4 and D5 on EPI2ME for Workflow Comparison

[[D4_and_D5_processing_epi2me]]

#### Comparison of HPC Workflow with EPI2ME

Dataprocessing of EPI2ME:
* basecalling_guppy_job_sbs_01 (fastq files)
* EPI2ME Fastq 16S (Barcoding, QC-Report,Filtering, Taxonomic Classification)
* csv exports
* R for Data processing and Graphs (Filter by length)

Dataprocessing on HPC:
* basecalling_guppy_job_sbs_01 (fastq files)
* demultiplexing_qcat_tax_wf_comp_01 (demultiplexing)
* filter_trim_nanofilt_tax_wf_comp_01 (q > 7 length 1000 -2000)
* classification_kraken2_nanofilt_tax_wf_comp_01
* r_kraken2_report_nanofilt_tax_wf_comp_01
* R for Data processing and Graphs (Filter by length)

### Data processing of D4 and D5 with POND for Workflow Comparison

[[D4_and_D5_processing_kraken2]]

#### Define Graphs for Workflow Comparison
* [x] Barcoding Comparison of EPI2ME vs qcat
* [x] Overview of quality of reads D4 and D5 in comparison (Histogram)
* [x] Overview of classification success with filtered reads (length and quality) for EPI2ME and Kraken2
___
### Data processing of D4 and D5 for DB Compariosn
[[D4_and_D5_processing_DB_Comparison]]

### Data processing of D1 for CRISPR Anlysis

copy all fast5 file in one dir the data

	mkdir Dataset_1

	find Dataset_1_old/ -name "*.fast5" -exec cp {} Dataset_1/ \;
	
**!!! Somehow the size of the new directory is smaller than the old one?!?!**
	
Setup the env file
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_1
DATA_PATH_IN=../data/Dataset_1/
RUN_NAME_IN=crispr_d1_01
RUN_NAME_OUT=crispr_d1_01
FLOWCELL=FLO-MIN106
KIT=SQK-PBK004

FILES_PER_SUBDIR=20

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin/guppy_barcoder

QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1500
NANOFILT_MAX_LENGTH=2500

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB_SILVA=../local_apps/kraken2/Kraken_Installation/SILVA/
PATH_KRAKEN2_DB_RDP=../local_apps/kraken2/Kraken_Installation/RDP/
PATH_KRAKEN2_DB_GG=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportText
PATH_KRAKEN2KRONA=../local_apps/lskScripts/scripts/kraken2-translate.pl

UDOCKER_PATH=../local_apps/udocker
```
	
run the basic data processing workflow

	task run-wf wf_basic_processing.sh

### Data processing of D2 for CRISPR Anlysis

copy all fast5 file in one dir the data

	mkdir Dataset_2
	
I realized that some of the passed and failed fasta files do have the same name, therefore I renamed the ones in the failed folder

	cd /cfs/earth/scratch/voro/data/Dataset_2_old/ZHAW_run_0007d/20191030_0900_MN19154_FAL53437_be571480/fast5_fail
	
	for i in *; do mv "$i" 1_"$i"; done
	
Now use the same command again and check that the filesize increased (yes, from 15.9 GB to 19.7 GB)

	find Dataset_2_old/ -name "*.fast5" -exec cp {} Dataset_2/ \;
	
**!!! Somehow the size of the new directory is smaller than the old one?!?!**
	
Setup the env file
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_2
DATA_PATH_IN=../data/Dataset_2/
RUN_NAME_IN=crispr_d2_01
RUN_NAME_OUT=crispr_d2_01
FLOWCELL=FLO-MIN106
KIT=SQK-PBK004

FILES_PER_SUBDIR=20

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin/guppy_barcoder

QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1500
NANOFILT_MAX_LENGTH=2500

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB_SILVA=../local_apps/kraken2/Kraken_Installation/SILVA/
PATH_KRAKEN2_DB_RDP=../local_apps/kraken2/Kraken_Installation/RDP/
PATH_KRAKEN2_DB_GG=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportText
PATH_KRAKEN2KRONA=../local_apps/lskScripts/scripts/kraken2-translate.pl

UDOCKER_PATH=../local_apps/udocker
```
	
run the basic data processing workflow

	task run-wf wf_basic_processing.sh


