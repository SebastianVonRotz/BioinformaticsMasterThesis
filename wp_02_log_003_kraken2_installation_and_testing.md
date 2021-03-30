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