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