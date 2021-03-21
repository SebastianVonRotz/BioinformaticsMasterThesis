Before Login, one has to be in the ZHAW Network (VPN)

	ssh voro@head.hpc.zhaw.ch
	vorovoro

Top Node after loging

	cd /archive

Copy folders with content

	cp -avr /home/vivek/letters /usb/backup

Access the shared folder with additional programs

	cd cfs/earth/scratch/iunr/egsb/shared
	cd /cfs/earth/scratch/voro/

See available SW modules

	module avail

Find a specified module or command

	Module spider "name of application"

Load and unload modules (example with 2 modules)

	module load gcc/7.3.0 python/3.6.5  
	module unload python/3.6.5

Single task on one node (using one CPU)

	#!/bin/bash
	#
	# The #SBATCH lines below are //not// commented out! These lines are read by the Slurm preprocessor. They need to start with a '#' character to work.
	#
	#SBATCH --job-name=example-job-name
	#SBATCH --output=/cfs/earth/scratch/<login name>/.../<mydir>/result.%j.%N.out
	#SBATCH --chdir=/cfs/earth/scratch/<login name>/.../<mydir>
	# Optional: Get an email notification on job completion:
	#SBATCH --mail-type=end
	#SBATCH --mail-user=<login name>@zhaw.ch
	#
	#SBATCH --nodes=1
	#SBATCH --ntasks=1
	#SBATCH --cpus-per-task=1
	#SBATCH --time=HH:MM:SS
	#SBATCH --partition=single
	#SBATCH --qos=single

	module load USS/2019
	module load slurm
	module load <example module>

	example-app

Run the job

	sbatch my-app-submission-script.sh
	squeue
	sstat -j jobid
	scancel <jobid>

look a the queue

	sbatch my-app-submission-script.sh
	squeue
	sstat -j jobid
	scancel <jobid>

Get infos on the job

	sbatch my-app-submission-script.sh
	squeue
	sstat -j jobid
	scancel <jobid>

cancel job

	sbatch my-app-submission-script.sh
	squeue
	sstat -j jobid
	scancel <jobid>

Global scratch directory with envrionmental variable for starting jobs (in there one places the data)

	/cfs/earth/scratch/<login-name>
	$LSFM_CLUSTER_SCRATCH_JOB_PATH


If you want to login directly into a node for testing use the following command

	srun -J "interactive job" --pty --partition=single --qos=single --chdir=$LSFM_CLUSTER_SCRATCH_USER_PATH /bin/bash
	
In order to login for a running node use

	ssh node012