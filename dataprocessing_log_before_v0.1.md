### Connection to the server
Open the fstp connected server in the VS Code Terminal

### fast5 inspection

	cd /cfs/earth/scratch/voro/scripts
	sbatch 1_fast5assessment.sh

### Basecalling

	cd /cfs/earth/scratch/voro/scripts
	sbatch wf_01_basecalling_Guppy.sh

JobID: 960335 
Runtime: 3-22:27:26 

### 2nd Basecalling
manually from the termnal: wf_01_basecalling-guppy_D2.sh wf_01_env

JobID: 960375 
Runtime: 21:05:31

### 3rdnd Basecalling
From here on the setup for executing command files is established an not direct login to the hpc server is necessary

	mkdir -p ../results/Dataset_3/wf_01_basecalling-guppy_D3/
	task upload-script wf_01_basecalling-guppy_D3.sh wf_01_env
	task run-hpc-script wf_01_basecalling-guppy_D3.sh wf_01_env

JobID: 960381 
Runtime: 22:45:59

### Installation of MinIONQC
task conn-hpc
Install the packages
task upload-script wf_01_MinIONQC_install.sh wf_01_env
task run-hpc-script wf_01_MinIONQC_install.sh wf_01_env
curl https://raw.githubusercontent.com/roblanf/minion_qc/master/MinIONQC.R > MinIONQC.R
Adapted the R-Script with
![[Pasted image 20201007153304.png]]
Run the script
	
	task upload-script wf_01_MinIONQC.sh wf_01_env
	task run-hpc-script wf_01_MinIONQC.sh wf_01_env
 Problem with MinIONQ

	[voro@head01 scripts]$ Rscript MinIONQC.R -i ../results/Dataset_test/wf_02_basecalling-guppy_1/sequencing_summary.txt
	During startup - Warning messages:
	1: Setting LC_CTYPE failed, using "C"
	2: Setting LC_COLLATE failed, using "C"
	3: Setting LC_TIME failed, using "C"
	4: Setting LC_MESSAGES failed, using "C"
	5: Setting LC_MONETARY failed, using "C"
	6: Setting LC_PAPER failed, using "C"
	7: Setting LC_MEASUREMENT failed, using "C"
	INFO [2020-10-07 15:07:24] Loading input file: ../results/Dataset_test/wf_02_basecalling-guppy_1/sequencing_summary.txt
	INFO [2020-10-07 15:07:24] MinION flowcell detected
	INFO [2020-10-07 15:07:24] wf_02_basecalling-guppy_1: creating output directory:../results/Dataset_test/wf_02_basecalling-guppy_1
	INFO [2020-10-07 15:07:24] wf_02_basecalling-guppy_1: summarising input file for flowcell
	INFO [2020-10-07 15:07:24] wf_02_basecalling-guppy_1: plotting length histogram
	Error in grDevices::png(..., res = dpi, units = "in") : 
	  X11 is not available
	Calls: single.flowcell ... withCallingHandlers -> ggsave -> dev -> <Anonymous>
	Execution halted

### Nanoplot 
Is already installed on the cluster
	
	task upload-script wf_01_Nanoplot_D3.sh wf_01_env
	task run-hpc-script wf_01_Nanoplot_D3.sh wf_01_env

JobID: 960412
	
	task upload-script wf_01_Nanoplot_D1.sh wf_01_env
	task run-hpc-script wf_01_Nanoplot_D1.sh wf_01_env

JobID: 960429

	task upload-script wf_01_Nanoplot_D2.sh wf_01_env
	task run-hpc-script wf_01_Nanoplot_D2.sh wf_01_env

JobID: 960430

### Demultiplexing with Guppy
guppy_barcoer is already installed

	task upload-script wf_01_demultiplexing_guppy_D1.sh wf_01_env
	task run-hpc-script wf_01_demultiplexing_guppy_D1.sh wf_01_env

JobID: 960428
Runtime: 07:56:42

	task upload-script wf_01_demultiplexing_guppy_D2.sh wf_01_env
	task run-hpc-script wf_01_demultiplexing_guppy_D2.sh wf_01_env

JobID: 960432
Runtime: 03:10:53

	task upload-script wf_01_demultiplexing_guppy_D3.sh wf_01_env
	task run-hpc-script wf_01_demultiplexing_guppy_D3.sh wf_01_env

JobID: 960433
Runtime: 01:41:45


### Installation of qcat
Connect to hpc

load modules

	module load USS/2020
	module load gcc/7.3.0 python/3.6.5-pe5.26
	module load py-pip/19.3-py3.6-pe5.26

Install with PIP

	pip install --user qcat

Check installation under

	ls /cfs/earth/scratch/voro/python/lib/python3.6/site-packages/

### Demultiplex with qcat

	task upload-script wf_01_demultiplexing_qcat_D1.sh wf_01_env
	task run-hpc-script wf_01_demultiplexing_qcat_D1.sh wf_01_env

JobID: 960447
Runtime: 00:20:59

___
**Rewored Naming scheme on 27.10.2020, discrepancy in the Output of the past run Jobs with new naming schemes can occur**
___

#### Note 07102020
Demultiplexing of guppy seems to be  generating barcode bin according to the extended kit, maybe besides the flow cell and kit description also the barcoding config name has to be incorporated in the demultiplexing command

### Demultiplexing with Guppy (with barcodng config name)
	task upload-script wf_01_demultiplexing_guppy_D1_02.sh wf_01_env
	task run-hpc-script wf_01_demultiplexing_guppy_D1_02.sh wf_01_env

JobID: 960582
Runtime: 
Resulted in a an error and is not able to read the barcoding config name

#### Note 07102020
The additional Bins are probably produced by guppy of wrongly labeled barcodes


### Demultiplex with qcat (continuation)
	task upload-script wf_01_demultiplexing_qcat_D2.sh wf_01_env
	task run-hpc-script wf_01_demultiplexing_qcat_D2.sh wf_01_env

JobID: 960584
Runtime: 00:08:03

	task upload-script wf_01_demultiplexing_qcat_D3.sh wf_01_env
	task run-hpc-script wf_01_demultiplexing_qcat_D3.sh wf_01_env

JobID: 960585
Runtime:00:15:35 

### Filter with Nanofilt
**The script only works with the output of the qcat demultiplexed reads so far!!!**

First data 

	task upload-script wf_01_filter_trim_nanofilt_D1.sh wf_01_env
	task run-hpc-script wf_01_filter_trim_nanofilt_D1.sh wf_01_env
	
JobID: 960619

2nd dataset

	task upload-script wf_01_filter_trim_nanofilt_D2.sh wf_01_env
	task run-hpc-script wf_01_filter_trim_nanofilt_D2.sh wf_01_env
	
JobID: 960714

### Basecall Dataset 4
copy from other dir

	cp -avr /cfs/earth/scratch/iunr/egsb/Data_voro/ZHAW_run_0014a-d/ Raw_Data/

Aggregate all of the fast5 data with

	find Raw_Data/ZHAW_run_0014a-d/ -name "*.fast5" -exec mv {} Dataset_4 \;

Execute the basecalling task

	task upload-script wf_01_basecalling_guppy_D4.sh wf_01_env
	task run-hpc-script wf_01_basecalling_guppy_D4.sh wf_01_env

JobID: 962124
Runtime: 1-07:06:21


### Basecall Dataset 5
Copy from other dir

	cp -avr /cfs/earth/scratch/iunr/egsb/Data_voro/ZHAW_run_0015a-d/ Raw_Data/


Aggregate all of the fast5 data with

	find Raw_Data/ZHAW_run_0015a-d/ -name "*.fast5" -exec mv {} Dataset_5 \;
	
copy the data

	find Raw_Data/ZHAW_run_0015a-d/ -name "*.fast5" -exec cp {} Dataset_5_Array \;	

create subdirectorys

	cd Dataset_5_Array/

	n=0; for f in *.fast5; do d="subdir$((n++ / 20))"; mkdir -p "$d"; mv -- "$f" "$d/$f"; done

command is based on: https://github.com/colindaven/guppy_on_slurm/blob/master/batch_split_to_subdirs.sh


Execute the basecalling task

	task upload-script wf_01_basecalling_guppy_D5.sh wf_01_env
	task run-hpc-script wf_01_basecalling_guppy_D5.sh wf_01_env

JobID: 962252
Runtime: 1-22:13:51

**Info in the outputfile: There were fast5 file loading problems! Failed to load 108 out of 431 fast5 files. Check log file for details.
It was too fast (double the amount of fast5 file size), maybe some data is missing after messing around with the directories while the job was running! -> Restart! (Maybe fast5 file size was bigger because more data was basecalled?)**

* JobID: 962472
* Runtime: 2-09:49:38
* Final output size:  990 mb

**Looks like while messing around with the directory some data has not been processed withthe run 962252 but it is now processed with the run 962472**


Execute the basecalling task with arrays:

	task upload-script wf_01_basecalling_guppy_array_D5.sh wf_01_env
	task run-hpc-script wf_01_basecalling_guppy_array_D5.sh wf_01_env

* JobID: 962465
* Runtimes: 
04:16:19
01:43:12
02:45:59
01:46:07
...
* Final output size: 978 mb

**Why is the file size smaller of the non-array job? (962472)**

### Dataset 5 (array) renaming of the files
An aggregated fastq file is created with the command:

	cd /cfs/earth/scratch/voro/results/Dataset_5/wf_01_basecalling-guppy_array_D5
	
	cat run_subdir*/*.fastq > df5_array.fastq
	

	
### Nanoplot of Dataset  5
	task upload-script wf_01_Nanoplot_D5.sh wf_01_env
	task run-hpc-script wf_01_Nanoplot_D5.sh wf_01_env
	
### Demultiplexing Dataset 4 and 5

		task upload-script wf_01_demultiplexing_guppy_D4.sh wf_01_env
		task run-hpc-script wf_01_demultiplexing_guppy_D4.sh wf_01_env
	
* JobID: 963219

		task upload-script wf_01_demultiplexing_guppy_D5.sh wf_01_env
		task run-hpc-script wf_01_demultiplexing_guppy_D5.sh wf_01_env
	
* JobID: 963260 

### Dataset 5 (array) New Array Script

	task upload-script wf_01_basecalling_guppy_array_D5.sh wf_01_env
	task run-hpc-script wf_01_basecalling_guppy_array_D5.sh wf_01_env


* JobID: 963267
* Runtimes: 
02:52:17
04:00:14
...
* Final output size: 978 mb

### Demultiplexing of D4 and D5 with qcat

		task upload-script wf_01_demultiplexing_qcat_D4.sh wf_01_env
		task run-hpc-script wf_01_demultiplexing_qcat_D4.sh wf_01_env

* JobID: 963358

		task upload-script wf_01_demultiplexing_qcat_D5.sh wf_01_env
		task run-hpc-script wf_01_demultiplexing_qcat_D5.sh wf_01_env

* JobID: 963359

**!!! Forgot to redirect the standard output to a file which has a small report on the qcat demultiplexing !!!**

### Apply filtering and trimming of D4 and D5
Applied the filtering to the output of the demultiplexed files with qcat. Parameters are >q7, minlength 1000, maxlength 2000

		task upload-script wf_01_filter_trim_nanofilt_D4.sh wf_01_env
		task run-hpc-script wf_01_filter_trim_nanofilt_D4.sh wf_01_env

* JobID: 963360

		task upload-script wf_01_filter_trim_nanofilt_D5.sh wf_01_env
		task run-hpc-script wf_01_filter_trim_nanofilt_D5.sh wf_01_env

* JobID: 963361

### Classification with Kraken2 of D4 and D5
The classification was done on the raw demultiplexed data, without quality and length filtering

		task upload-script wf_01_classification_kraken2_D4.sh wf_01_env
		task run-hpc-script wf_01_classification_kraken2_D4.sh wf_01_env
		
* JobID: 963366

		task upload-script wf_01_classification_kraken2_D5.sh wf_01_env
		task run-hpc-script wf_01_classification_kraken2_D5.sh wf_01_env
		
* JobID: 963367
