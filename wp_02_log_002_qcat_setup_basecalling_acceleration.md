### qcat output redirection

Adapt the script by adding "2>&1" at the end of the qcat command, this switches the terminal output from the error to the output file

		task upload-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		task run-hpc-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		
JobID: 960720

Further adapt the bash script with " SBATCH --output=qcat_output" and added line "cp qcat_output $DATAPATH_DEMULTPLEXING_QCAT_OUT", "rm qcat_output"

		task upload-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		task run-hpc-script wp_01_demultiplexing_qcat_1.sh wp_01_env
		
JobID: 960730
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
	