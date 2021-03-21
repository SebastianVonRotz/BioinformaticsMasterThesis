#### Basecalling Guppy
There are no subdirectories for the array job yet
connect to the hpc, then

	cd ../data

copy the data

	find Raw_Data/ZHAW_run_0014a-d/ -name "*.fast5" -exec cp {} Dataset_4_Array \;	

create subdirectorys

	cd Dataset_5_Array/

	n=0; for f in *.fast5; do d="subdir$((n++ / 20))"; mkdir -p "$d"; mv -- "$f" "$d/$f"; done

Now there are 12 subdirs, now the script needs to be adapted based on the numbers of subddirs

Adapt the env file accoringly
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4_Array/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024
```

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller

For the guppy array basecaller the subdirs need to be created and the script needs to adapted according to the amount of subdirs. Then the following command is used

	task run-script basecalling_guppy_array.sh

#### Demultiplexing Guppy
Adapt the env file:
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4_Array/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder
QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat
```
Run

	task run-script demultiplexing_guppy.sh

#### Demultiplexing qcat
Adapt the env file:
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4_Array/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder
QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat
```
Run

	task run-script demultiplexing_qcat.sh
	
#### Reporting with Nanoplot fastq
Adapt the env file:
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4_Array/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder
QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat
```
Run

	task run-script nanoplot_fastq.sh


#### Basecalling with guppy single job
Adapt the env file:
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder
QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat
```
Run

	task run-script basecalling_guppy_job.sh

#### Nanofilt
Adapt the env file:
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder
QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```
Run

	task run-script filter_trim_nanofilt.sh

#### Kraken2 raw Greengenes
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder
QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```

Run

	task run-script classification_kraken2_raw.sh     
	
#### Krona Plots
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/

RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder
QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```

run

	task run-script krona_plots.sh

#### Kraken2 nanofilt Greengenes
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

FILES_PER_SUBDIR=20

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder

QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```

Run

	task run-script classification_kraken2_nanofilt.sh     
	
#### Nanofilt sum
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

FILES_PER_SUBDIR=20

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder

QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```

Run

	task run-script nanofilt_sum.sh     
	
#### R kraken2 stats
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

FILES_PER_SUBDIR=20

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder

QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```
run

	task run-script r_kraken2_report.sh
	
#### Renamed the directories
Each result directory is renamed according to the script name with which it is generated 
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

FILES_PER_SUBDIR=20

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder

QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```
#### Reprocessed Krona plots
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01

FLOWCELL=FLO-FLG001
KIT=SQK-16S024

FILES_PER_SUBDIR=20

GUPPY_BASECALLER_PATH=../local_apps/ont-guppy-cpu/bin/guppy_basecaller
GUPPY_DEMULTIPLEXING_PATH=../local_apps/ont-guppy-cpu/bin//guppy_barcoder

QCAT_DEMULTIPLEXING_PATH=../python/bin/qcat

NANOFILT_QSCORE=7
NANOFILT_MIN_LENGTH=1000
NANOFILT_MAX_LENGTH=2000

PATH_KRAKEN2=../local_apps/kraken2/Kraken_Installation/kraken2 
PATH_KRAKEN2_DB=../local_apps/kraken2/scripts/GREENGENES/

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportTaxonomy
```
run

	task run-script krona_plots.sh
	
#### Kraken2 raw SILVA
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_5/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01_SILVA

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
PATH_KRAKEN2_DB=../local_apps/kraken2/Kraken_Installation/SILVA

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportText
PATH_KRAKEN2KRONA=../local_apps/lskScripts/scripts/kraken2-translate.pl
```
Run

	task task run-script classification_kraken2_raw.sh
	
#### Kraken2 raw RDP
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_5/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=sbs_01_RDP

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
PATH_KRAKEN2_DB=../local_apps/kraken2/Kraken_Installation/RDP

PATH_KRONATOOLS=../local_apps/krona/KronaTools-2.7.1/bin/bin/ktImportText
PATH_KRAKEN2KRONA=../local_apps/lskScripts/scripts/kraken2-translate.pl
```
Run

	task task run-script classification_kraken2_raw.sh