### Demutiplexing of guppy_job data D4
Adapt the script: "demultiplexing_qcat.sh"
from

		DATA_PATH_IN=../results/$DATASET_NAME/basecalling_guppy_array_$RUN_NAME_IN/
	
to

		DATA_PATH_IN=../results/$DATASET_NAME/basecalling_guppy_job_$RUN_NAME_IN/


Then changed it back after running the script		

```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=tax_wf_comp_01
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
	
	task run-script demultiplexing_qcat.sh

### Demutiplexing of guppy_job data D5
Adapt the script: "demultiplexing_qcat.sh"
from

		DATA_PATH_IN=../results/$DATASET_NAME/basecalling_guppy_array_$RUN_NAME_IN/
	
to

		DATA_PATH_IN=../results/$DATASET_NAME/basecalling_guppy_job_$RUN_NAME_IN/


Then changed it back after running the script		

```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_5
DATA_PATH_IN=../data/Dataset_5/
RUN_NAME_IN=sbs_01
RUN_NAME_OUT=tax_wf_comp_01
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
	
	task run-script demultiplexing_qcat.sh
	

### D4 filter_trim_nanofilt.sh
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=tax_wf_comp_01
RUN_NAME_OUT=tax_wf_comp_01
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


### D5 filter_trim_nanofilt.sh
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_5
DATA_PATH_IN=../data/Dataset_5/
RUN_NAME_IN=tax_wf_comp_01
RUN_NAME_OUT=tax_wf_comp_01
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

### D4 classification_kraken2_nanofilt.sh
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=tax_wf_comp_01
RUN_NAME_OUT=tax_wf_comp_01
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
```

### D5 classification_kraken2_nanofilt.sh
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_5
DATA_PATH_IN=../data/Dataset_5/
RUN_NAME_IN=tax_wf_comp_01
RUN_NAME_OUT=tax_wf_comp_01
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
```

### D4 r_kraken2_report_nanofilt.sh 
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=tax_wf_comp_01
RUN_NAME_OUT=tax_wf_comp_01
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
```

### D5 r_kraken2_report_nanofilt.sh 
```
REMOTE_PATH=/cfs/earth/scratch/voro/scripts

DATASET_NAME=Dataset_4
DATA_PATH_IN=../data/Dataset_4/
RUN_NAME_IN=tax_wf_comp_01
RUN_NAME_OUT=tax_wf_comp_01
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
```

