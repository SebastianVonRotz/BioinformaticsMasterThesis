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
### Processing of D4 and D5 on EPI2ME

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

### Data processing of D4 and D5

[[D4_and_D5_processing_kraken2]]

#### Define Graphs for Workflow Comparison
* [x] Barcoding Comparison of EPI2ME vs qcat
* [x] Overview of quality of reads D4 and D5 in comparison (Histogram)
* [x] Overview of classification success with filtered reads (length and quality) for EPI2ME and Kraken2
___
### Data processing of D4 and D5 for DB Compariosn
[[D4_and_D5_processing_DB_Comparison]]




