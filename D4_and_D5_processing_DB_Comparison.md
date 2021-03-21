### Env File for D4 Processing
	REMOTE_PATH=/cfs/earth/scratch/voro/scripts

	DATASET_NAME=Dataset_4
	DATA_PATH_IN=../data/Dataset_4/
	RUN_NAME_IN=db_comp_01
	RUN_NAME_OUT=db_comp_01
	FLOWCELL=FLO-FLG001
	KIT=SQK-16S024

	FILES_PER_SUBDIR=20

	GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
	GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin/guppy_barcoder

	QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

	NANOFILT_QSCORE=7
	NANOFILT_MIN_LENGTH=1000
	NANOFILT_MAX_LENGTH=2000

	PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
	PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/
	PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportText
	PATH_KRAKEN2KRONA=../local_apps/lskScripts/scripts/kraken2-translate.pl

### Commands for D4 Processing
task run-script job_array_prep.sh
task run-script pre_basecalling_guppy_array.sh
task run-script basecalling_guppy_array.sh
task run-script demultiplexing_qcat.sh
task run-script nanoplot_fastq.sh
task run-script filter_trim_nanofilt.sh



### Env File for D5 Processing
	REMOTE_PATH=/cfs/earth/scratch/voro/scripts

	DATASET_NAME=Dataset_5
	DATA_PATH_IN=../data/Dataset_5/
	RUN_NAME_IN=db_comp_01
	RUN_NAME_OUT=db_comp_01
	FLOWCELL=FLO-FLG001
	KIT=SQK-16S024

	FILES_PER_SUBDIR=20

	GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
	GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin/guppy_barcoder

	QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

	NANOFILT_QSCORE=7
	NANOFILT_MIN_LENGTH=1000
	NANOFILT_MAX_LENGTH=2000

	PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
	PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/
	PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportText
	PATH_KRAKEN2KRONA=../local_apps/lskScripts/scripts/kraken2-translate.pl

### Commands for D5 Processing
task run-wf wf_tax_classification.sh