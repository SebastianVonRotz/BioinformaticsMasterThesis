# General
### Goals
* [x] Basecall a test dataset with guppy and two different settings for the hpc
* [x] Assess the runtime with different script settings
* [x] Setup and test the Nanofilt application
* [x] Basecall with splitting of data or use of slurm job arrays (https://github.com/colindaven/guppy_on_slurm)
* [ ] Basecall a test dataset with bonito and two different settings for the hpc
* [x] Check if output to commandline of qcat can be redirected
* [x] Install Kraken2
* [x] Use the array for basecalling the Dataset_4 and Dataset_5
* [x] Create a script for working with kraken2
* [x] Install Krona Tools for Kraken2 Output
* [x] Check Guppy by adapting --numcaller / Change input size of the amount and size of input files
* [x] Based on numcaller x threads per caller vary these amounts and check which ones the fastest
* [ ] With optimal settings of numcaller and threads per caller the amount of input files and their sizes should be varied
* [x] Write new Scripts for processing kraken2 reports with R
* [x] Adapt all scripts in order to generate output dirs based on the names of the scripts
* [ ] Adapt prep array file in order to always generate a certain amount of dirs (e.g. 20, also check what happens if less than 20 dirs are generated)
* [x] Create plots for the soilsample comparison
* [x] Solve the id Problem of the Greengenes DB
* [x] Exchange Soil data with Moritz
* [x] Use the different output of kraken2 to generate the correct krona plots
* [x] Adapt krona-tools for the option with the script
* [x] Install RDP and SILVA DB
* [x] Define the version of the DB Dowloaded by kraken2
* [x] Checkout Pavian
* [x] Checkout Centrifuge
* [ ] Checkout Bracken
* [x] Create classificaton plot for each rank (Percent of reads covered by rank)
* [ ] Define on how to compare the different Databases and Classifications
 
# Log
### Transfer Datasets
Copy data into the new dataset folders
`
ssh voro@head.hpc.zhaw.ch
cd /cfs/earth/scratch/voro/data
cp -a run_0004/. Dataset_1 
cp -a run_0007d/. Dataset_2
cp -a run_0009/. Dataset_3 
mv run_0009 /raw_data
mv run_0007 /raw_data
mv run_0007b /raw_data
mv run_0007c /raw_data
mv run_0007d /raw_data
`
Test Data is from
https://denbi-nanopore-training-course.readthedocs.io/en/latest/data.html
`
mkdir -p ../results/Dataset_test/basecalled_para_1/
mkdir -p ../results/Dataset_test/basecalled_para_2/
task upload-script ma_workflow_02 basecalling-guppy_para_1.sh
task upload-script ma_workflow_02 basecalling-guppy_para_2.sh
task run-hpc-script basecalling-guppy_para_1.sh
task run-hpc-script basecalling-guppy_para_2.sh
`

Commit:
Expanded task functions, adapted directory structure and added new scripts

### 1st to 12th basecalling test
[[basecalling_test_log]]

### Nanofilt Setup
First create demultiplexed test dataset

 	task upload-script wp_01_demultiplexing_qcat.sh wp_01_env
	task run-hpc-script wp_01_demultiplexing_qcat.sh wp_01_env
	
JobID: 960593

Create the nanoplot and stats

 	task upload-script wp_01_nanoplot.sh wp_01_env
	task run-hpc-script wp_01_nanoplot.sh wp_01_env
	
JobID: 960598

Test the Nanofilt script


In order to correctly display the basename of the $fq it has to be put in brackets!

	#for fq in $DATAPATH_FILTER_TRIM_NANOFILT_IN*.fastq
	#  do
	#    echo $fq 
	#    echo $DATAPATH_FILTER_TRIM_NANOFILT_OUT$(basename $fq)
	#  done

	# DATAPATH_FILTER_TRIM_NANOFILT_IN=../results/Dataset_test/wp_01_demultiplexing_qcat/
	# DATAPATH_FILTER_TRIM_NANOFILT_OUT=../results/Dataset_test/wp_01_filter_trim_nanofilt/

	#cat ../results/Dataset_test/wp_01_demultiplexing_qcat/barcode04.fastq | NanoFilt --maxlength 5000 > ../results/Dataset_test/wp_01_filter_trim_nanofilt/barcode04.fastq 

	#for fq in *.fastq
	#  do
	#    cat $fq | NanoFilt ... > filtered_${fq}
	#  done

	#for fq in $DATAPATH_FILTER_TRIM_NANOFILT_IN*.fastq
	#  do
	#    echo $fq
	#  done
	#fq=../results/Dataset_test/wp_01_demultiplexing_qcat/barcode04.fastq
	#cat $fq | NanoFilt --maxlength 5000 > ../results/Dataset_test/wp_01_filter_trim_nanofilt/barcode04.fastq 

	#for dir in /tmp/*/     # list directories in the form "/tmp/dirname/"
	#do
	#    dir=${dir%*/}      # remove the trailing "/"
	#    echo ${dir##*/}    # print everything after the final "/"
	#done

Infos from website

	You could pipe them all through NanoFilt and generate one output file only:
	cat *.fastq | NanoFilt ... > new_output.fastq
	This is going to be the slowest option, but perhaps the cleanest.
	Note that you could also pipe directly to an aligner:
	cat *.fastq | NanoFilt ... | minimap2 -a genome.fa | samtools sort -o new_output.bam
	You could use a bash loop and process them sequentially:

	for fq in *.fastq
	  do
		cat $fq | NanoFilt ... > filtered_${fq}
	  done

	You could use gnu parallel, with a certain number of simultaneous jobs (8 in my example)
	ls *.fastq | parallel -j 8 'cat {} | NanoFilt > filtered_{}'


Running code

 	task upload-script wp_01_filter_trim_nanofilt.sh wp_01_env
	task run-hpc-script wp_01_filter_trim_nanofilt.sh wp_01_env

JobID: 960616

### qcat output redirection

Adapt the script by adding "2>&1" at the end of the qcat command, this switches the terminal output from the error to the output file

		task upload-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		task run-hpc-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		
JobID: 960720

Further adapt the bash script with " SBATCH --output=qcat_output" and added line "cp qcat_output $DATAPATH_DEMULTPLEXING_QCAT_OUT", "rm qcat_output"

		task upload-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		task run-hpc-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		
JobID: 960730

### Kraken2 Installation

Installation according to https://github.com/DerrickWood/kraken2/wiki/Manual

used

	git clone https://github.com/DerrickWood/kraken2.git

Into the folder

	/cfs/earth/scratch/voro/local_apps/
	
Created folder for installation

	/cfs/earth/scratch/voro/local_apps/kraken2/Kraken_Installation

Installation with

	./install_kraken2.sh Kraken_Installation
	
Output:

	Kraken 2 installation complete.
	
### Slurm Job Array and Job acceleration

##### try 1
How many files and how many array

	nfiles = $(ls Dataset_4 | wc -l)
	narr=10

Divide by the amount of arrays and add remeinder so that fo all the data it is accounted

	ndata=$(expr $(ls Dataset_4 | wc -l) / 10 + $(ls Dataset_4 | wc -l) % 10)
	
Create an array for each ndata amount


	ls Dataset_4 | xargs -n $ndata | > ndata_list.txt
	readarray name_arr < ndata_list.txt

access the array 

	echo ${name_arr[0]}
	
		
##### try 2

	arraypath=Dataset_4
	
	mkdir $arraypath/array_dir
	
	ls $arraypath > $arraypath/array_dir/ndata_list.txt
	
	ndata=$(expr $(ls $arraypath | wc -l) / 10 + $(ls $arraypath | wc -l) % 10)
	
	split -d -l $ndata ndata_list.txt
	
	
	for file in $(cat x0$SLURM_ARRAY_TASK_ID); do mkdir -p "dir_x0$SLURM_ARRAY_TASK_ID" cp "Dataset_4/$file" x0$SLURM_ARRAY_TASK_ID_dir/; done
	
All of the tries are not really robust, rather than splitting the Dataset one should accelerate the guppy basecaller. See Tests above!


### Create Array job with renaming and relocating

		task upload-script wp_01_basecalling_guppy_array_1.sh wp_01_env
		task run-hpc-script wp_01_basecalling_guppy_array_1.sh wp_01_env

Rename did not work yet !!!

	"prename" to "rename"

Rename command on HPC is different than form the package isntalled on wsl
	
### Kraken2 Setup for usage
Run according to:
https://github.com/DerrickWood/kraken2/blob/master/docs/MANUAL.markdown

Run before building the database (Solution found at https://www.linuxquestions.org/questions/debian-26/perl-warning-setting-locale-failed-locale-not-available-4175641949/)

	export LC\_ALL=C
	perl -e exit
	
At the installtion the command

	cp $KRAKEN2_DIR/kraken2{,-build,-inspect} $HOME/bin

can not be run on the hpc, so the paths to the src and scripts have to be manually exported (Found at https://ask.csdn.net/questions/2661611)

	export PATH=$PATH:/cfs/earth/scratch/voro/local_apps/kraken2/scripts
	export PATH=$PATH:/cfs/earth/scratch/voro/local_apps/kraken2/src

Not the database can be downloaded and setup for building

	kraken2-build --db GREENGENES --special greengenes

[[kraken2_greengenes_installation_output]]

Acess to functions is not properly working! -> The correct directory is the Kraken_Installation directory!!!!!!!!

Inspect the database (you have to be in: "/cfs/earth/scratch/voro/local_apps/kraken2/Kraken_Installation")

	kraken2-inspect --db ../scripts/GREENGENES/ | head -5
	
	
Test the database with:

	../kraken2 --db ../../scripts/GREENGENES/ ../../../../results/Dataset_5/wf_01_basecalling-guppy_array_D5/df5_array.fastq > df5_classification.txt
 
Output:

	perl: warning: Setting locale failed.
	perl: warning: Please check that your locale settings:
			LANGUAGE = (unset),
			LC_ALL = (unset),
			LANG = "C.UTF-8"
		are supported and installed on your system.
	perl: warning: Falling back to the standard locale ("C").
	Loading database information... done.
	379638 sequences (381.03 Mbp) processed in 34.772s (655.1 Kseq/m, 657.47 Mbp/m).
	  256332 sequences classified (67.52%)
	 
### Setup a script for Kraken2
The new script is:

	wp_01_classification_kraken2_1.sh

run the script for testing

		task upload-script wp_01_classification_kraken2_1.sh wp_01_env
		task run-hpc-script wp_01_classification_kraken2_1.sh wp_01_env

### Install Krona for creating plot of kraken2 output
Installation according to: https://github.com/marbl/Krona/wiki/Installing

get data

	wget https://github.com/marbl/Krona/releases/download/v2.7.1/KronaTools-2.7.1.tar

untar 

	tar -xvf KronaTools-2.7.1.tar 

go in dir

	cd KronaTools-2.7.1/

create bin

	mkdir bin

install

	./install.pl --prefix bin

Output:

	perl: warning: Setting locale failed.
	perl: warning: Please check that your locale settings:
			LANGUAGE = (unset),
			LC_ALL = (unset),
			LANG = "C.UTF-8"
		are supported and installed on your system.
	perl: warning: Falling back to the standard locale ("C").
	Creating links...

	Installation complete.

	Run ./updateTaxonomy.sh to use scripts that rely on NCBI taxonomy:
	   ktClassifyBLAST
	   ktGetLCA
	   ktGetTaxInfo
	   ktImportBLAST
	   ktImportTaxonomy
	   ktImportMETAREP-BLAST

	Run ./updateAccessions.sh to use scripts that get taxonomy IDs from accessions:
	   ktClassifyBLAST
	   ktGetTaxIDFromAcc
	   ktImportBLAST
   
   Want to run the command "ktImportTaxonomy" according to https://www.gitmemory.com/issue/DerrickWood/kraken2/114/524767339. Therefore have to run update taxonomy
   
  	 ./updateTaxonomy.sh
	 
Test the command in a test directory
copy a report

	cp ../../../../results/Dataset_5/wf_01_classification_kraken2_D5/BC04.fastq_REPORT .

extract the column

	cut -f3,5 BC04.fastq_REPORT > krona_BC04.in

create the html file


	/cfs/earth/scratch/voro/local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy  krona_BC04.in -o krona_BC04.html -t 2 -m 1
	
___
# !!!!!!!!!!!
# v0.1
**From here on commands and the setup changes drastically, the new setup is outlined in [[workpackage_03]]**
# !!!!!!!!!!!
___
### Test the new File structure

Adapted the env file

	REMOTE_PATH=/cfs/earth/scratch/voro/scripts
	DATASET_NAME=Dataset_Test
	DATA_PATH_IN=../data/Dataset_test/fast5_small_subdir/
	RUN_NAME=Test_001
	FLOWCELL=FLO-MIN106
	KIT=SQK-RAD002
	GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller

Run the following commands

	task upload-script basecalling_guppy_array.sh
	task run-hpc-script basecalling_guppy_array.sh
	
### Test the resource allocation of the guppy basecaller
Log in to the hpc
 
 	task conn-hpc
	
Run an interactive job

		srun -J "interactive job" --pty --partition=parallel --qos=parallel --cpus-per-task=32 --chdir=$LSFM_CLUSTER_SCRATCH_USER_PATH /bin/bash
		
Define the input data

	PATH_IN=/cfs/earth/scratch/voro/data/Dataset_test/fast5/

Define the guppy basecaller path
	
	GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
	
Define the guppy command and run it
	
	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test
	
Log in with another terminal into the same node

	ssh node012
	
And use htop to see the use of the cores

	htop

##### Findings_1:
	
[[cpu_usage_log_1]]

* Setting The CPU usage is calculated by --num_callers  x --cpu_threads_per_caller = used amount of cpu cores
* Setting "--flowcell FLO-MIN106 --kit SQK-LSK109" activates a more intensive basecalling !

##### Findings_2:

[[cpu_usage_log_2]]

* Settings for the --num_callers --cpu_threads_per_caller, should be more towards one caller with as many threads as possible


# Kraken2 R scripts

The Report of Kraken2 is structured like this

1.  **Percentage** of reads covered by the clade rooted at this taxon
2.  **Number of reads** covered by the clade rooted at this taxon
3.  **Number of reads** assigned directly to this taxon
4.  A rank code, indicating **(U)nclassified, (D)omain, (K)ingdom, (P)hylum, (C)lass, (O)rder, (F)amily, (G)enus, or (S)pecies**. All other ranks are simply **“-“**.
5.  [NCBI Taxonomy](https://www.ncbi.nlm.nih.gov/taxonomy) ID
6.  The indented scientific name


### kraken2_report_stats.R
1. Load the data according to the argument 1
2. Rename the headers into "read_coverage_percentage", "read_coverage_number", "assigned_read_number", "rank", "NCBI_ID", "Name"
3. Create several statistics
4. Save them according to the argument 2

### r_kraken2_report.sh

Also a new scripts needs to be defined for running on the hpc

	r_kraken2_report.sh
	
### r_kraken2_plots.R

The script **r_kraken2_plots.R** uses the output of  **r_kraken2_report.sh (with kraken2_report_stats.R)**, but the data processing is** performed locally** on the computer and not on the HPC
1. Load every barcode sample
2. Load the sample ids
3. combine data and sample ids
4. create plots for presenting the changes of coverage


### Kraken2/Greengenes ID Trouble

File: `gg_13_5_accessions.txt`
Maps IDs: `gg_id --> accession`
Description:

gg_13_5_accessions.txt.gz
    - A mapping from Greengenes IDs to external databases
    - This is primarily Genbank references, but includes a few hundred
        links to IMG genome IDs as there was not an automatic means to infer
        some of the NCBI accessions.


File: `seqid2taxid.map`
Maps IDs: `seqid --> gg_id`

Description:
seqid2taxid.map
	- the two columns in seqid2taxid.map - the first is the Greengenes ID, and the second is the Kraken 2 ID
	- https://github.com/DerrickWood/kraken2/issues/47
	- There are some instances where multiple Greengenes IDs are associated with the same Kraken 2 id


File: `gg_13_5_taxonomy.txt`
Maps IDs: `gg_id --> 7-level`
Description:

gg_13_5_taxonomy.txt
    - Full taxonomy for every sequence in the release.
    - All taxonomy strings are strictly 7 level and prefixed


File: `gg_13_5_img.txt`
Maps IDs: `gg_id --> img_genome_id`
Description:

gg_13_5_img.txt
    - A mapping specifically between Greengenes IDs and IMG Genomes.
    - Performed by accession not nearest neighbor
	
### Process of ID mapping	 
Strategies:
* Use accesssion mapping to taxon mapping
* Use the taxonomy string and an ncbi interface
* Use the IMG_genome_ID to ncbi_taxon_ID mapping
* **Use the rank_names of gg and ncbi for mapping**

Other links:
* python taxon access http://etetoolkit.org/docs/2.3/tutorial/tutorial_ncbitaxonomy.html#setting-up-a-local-copy-of-the-ncbi-taxonomy-database
* krona-tools to gg problem desc. https://bioinformatics.stackexchange.com/questions/9304/how-to-apply-rdp-greengenes-and-other-special-taxonomies-in-krona

###### Currently Doing:
* Get the name.dmp
https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/
* Get the taxonomy file from gg https://greengenes.secondgenome.com/?prefix=downloads/greengenes_database/gg_13_5/
* Check the taxon number on https://www.ncbi.nlm.nih.gov/taxonomy/

The R file shows the procedure:

	gg_id_mapping.R
	
Result is the file:

	taxon_id2krona_id.map

### Adapt kraken2 output for krona-Tools
According to https://github.com/marbl/Krona/issues/117 

	task conn-hpc
	
	cd ../local_apps/
	
	git clone https://github.com/lskatz/lskScripts
	
Go to:

	/cfs/earth/scratch/voro/local_apps/lskScripts/scripts/test
	
Test the script with:

copy a Kraken2 report

	cp ../../../../results/Dataset_4/classification_kraken2_raw_sbs_01/BC04.fastq_REPORT .

___
Run in order not get an error when running perl (Error is only visual on the command line)

	export LC\_ALL=C
	perl -e exit
___

Use the script to generate an adapted report for krona

	../kraken2-translate.pl BC04.fastq_REPORT > BC04.fastq_REPORT_ADAPTED
	
Check if the output can be processed by krona tools
	
	../../../krona/KronaTools-2.7.1/bin/bin/ktImportText BC04.fastq_REPORT_ADAPTED -o BC04.html
	
**!!! Output looks correct !!!**

 Also generate bad output for comparison:
	
	../../../krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy -m 3 -t 5 BC04.fastq_REPORT -o BC04_2.html
	
**!!! Output is bad as expected !!!**
	
Lets also look into adapting the krona report with the ncbi taxons:
upload the BC04.fastq_REPORT_TAXON created with the gg_id_mapping.R script
	
	../../../krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy -m 3 -t 5 BC04.fastq_REPORT_TAXON -o BC04_3.html
 
**!!! Output only approximetaly get half of the taxa based on the taxon conversion!!!**

# Install Silva and RDP db
Go to

	cd ../local_apps/kraken2/Kraken_Installation/

run

	kraken2-build --db SILVA --special silva
	
and run

		kraken2-build --db RDP --special rdp

Define DB Path in the env file


# Install Pavian

Installation according to: https://github.com/fbreitwieser/pavian
 Run the following in R
 
	 if (!require(remotes)) { install.packages("remotes") }
	remotes::install\_github("fbreitwieser/pavian")
 
 Then Start the Tool with:
 
	 pavian::runApp(port=5000)
	 
** Interesting graph for Sample Level Compariosn**

# Build and Test Centrifuge DB
### Build SILVA DB
Copy necessary data first

	cp ../../kraken2/Kraken_Installation/SILVA/seqid2taxid.map .
	cp ../../kraken2/Kraken_Installation/SILVA/taxonomy/nodes.dmp .
	cp ../../kraken2/Kraken_Installation/SILVA/taxonomy/names.dmp  .
	cp ../../kraken2/Kraken_Installation/SILVA/data/SILVA_138.1_SSURef_NR99_tax_silva.fasta .

rename SILVA_138.1_SSURef_NR99_tax_silva.fasta to SILVA.fasta, because the 138.1 is read as 132
	
	module load gcc/6.4.0 centrifuge/1.0.3

	centrifuge-build --conversion-table seqid2taxid.map --taxonomy-tree nodes.dmp --name-table names.dmp SILVA.fasta TEST
	
Last line output:

	Total time for call to driver() for forward index: 00:24:39
	
Inspect the db

	centrifuge-inspect -n TEST
	
### Classifiy sample with SILVA db
copy data
	
	cp ../../../../results/Dataset_4/demultiplexing_qcat_sbs_01/BC04.fastq .

classifiy with centrifuge

	centrifuge -x ../TEST BC04.fastq -S silva_classification --report-file silva_report

Make kraken like report

	centrifuge-kreport -x ../TEST silva_classification > kraken2_report
	
### Build RDP DB
Copy all the necessary data

**The database is currenlty build only with the current_Bacteria_unaligned.fna**

Run

	centrifuge-build --conversion-table seqid2taxid.map --taxonomy-tree nodes.dmp --name-table names.dmp current_Bacteria_unaligned.fna  RDP
	
Stopped at:

	  bucket 1: 80%
	  bucket 1: 90%
	  bucket 1: 100%
	  Sorting block of length 330867562 for bucket 1
	  (Using difference cover)