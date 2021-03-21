### 1st basecalling

	task upload-script wp_01_basecalling-guppy_1.sh wp_01_env
	task run-hpc-script wp_01_basecalling-guppy_1.sh wp_01_env

JobID: 960382
Runtime: 01:00:48

### 2nd basecalling

	task upload-script wp_01_basecalling-guppy_2.sh wp_01_env
	task run-hpc-script wp_01_basecalling-guppy_2.sh wp_01_env

JobID: 960383
Runtime: 01:58:46

### 3rd basecalling

	task upload-script wp_01_basecalling_guppy_3.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_3.sh wp_01_env

JobID: 960437
Runtime: 00:59:58

### 4rd basecalling

	task upload-script wp_01_basecalling_guppy_4.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_4.sh wp_01_env

JobID: 960438
Runtime: 00:32:35

### 5th basecalling

	task upload-script wp_01_basecalling_guppy_5.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_5.sh wp_01_env

JobID: 960579
Runtime: 00:32:36

___
From here the content of the scripts are more similar because of a switch to the small Dataset

### 6th basecalling (6 core)
	#SBATCH --nodes=1 
	#SBATCH --ntasks-per-node=1 
	#SBATCH --cpus-per-task=6

	task upload-script wp_01_basecalling_guppy_6.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_6.sh wp_01_env

JobID: 962140
Runtime: 04:44:40

### 7th basecalling (12 core)
	#SBATCH --nodes=1 
	#SBATCH --ntasks-per-node=1 
	#SBATCH --cpus-per-task=12

	task upload-script wp_01_basecalling_guppy_7.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_7.sh wp_01_env

JobID: 962141
Runtime: 04:44:52

### 8th basecalling (24 core)
	#SBATCH --nodes=1 
	#SBATCH --ntasks-per-node=1 
	#SBATCH --cpus-per-task=24

	task upload-script wp_01_basecalling_guppy_8.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_8.sh wp_01_env

JobID: 962142
Runtime: 04:34:10

### 9th basecalling (2 nodes 24 core)
	#SBATCH --nodes=2 
	#SBATCH --ntasks-per-node=1 
	#SBATCH --cpus-per-task=24

	task upload-script wp_01_basecalling_guppy_9.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_9.sh wp_01_env

JobID: 962144
Runtime: 03:07:38

### 10th basecalling (1 node 24 cores 10x array)
Guppy needs a directory as an input !!!

	#SBATCH --nodes=1 
	#SBATCH --ntasks-per-node=1 
	#SBATCH --cpus-per-task=24
	#SBATCH --array=1-10

	task upload-script wp_01_basecalling_guppy_10.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_10.sh wp_01_env

JobID: 962265
Runtimes: 
00:31:45
00:27:45
00:28:16
00:30:47
...

Not all of the content is available!!! maybe also put output files into other directories! (Probably the output of the other guppy outputs get overwritten!!!)

### 11th basecalling (4 node 24 cores)

	#SBATCH --nodes=1 
	#SBATCH --ntasks-per-node=1 
	#SBATCH --cpus-per-task=24

	task upload-script wp_01_basecalling_guppy_11.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_11.sh wp_01_env

JobID: 962317
Runtime: 03:04:42

### 12th basecalling (1 node 24 cores 10x array)
With separated output folders

	#SBATCH --nodes=1 
	#SBATCH --ntasks-per-node=1 
	#SBATCH --cpus-per-task=24
	#SBATCH --array=1-10

	task upload-script wp_01_basecalling_guppy_12.sh wp_01_env
	task run-hpc-script wp_01_basecalling_guppy_12.sh wp_01_env

JobID: 962396
Runtimes: 
00:21:26
00:28:09
00:27:29
...
**This looks god now**

___
**Rewoded Naming scheme on 27.10.2020, discrepancy in the Output of the past run Jobs with new naming schemes can occur**
___