##### Vary the 	--num_callers  --cpu_threads_per_caller and measure the time
	
	PATH_IN=/cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
	
	
	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109

**Uses:4 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    1
cpu mode:           ON
threads per caller: 4

Found 1 fast5 files to process.
Init time: 3307 ms

Caller time: na



	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 1 --cpu_threads_per_caller 24
	
**Uses: 24 cores up to 100%**
	
	ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    1
cpu mode:           ON
threads per caller: 24

Found 1 fast5 files to process.
Init time: 3256 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 209452** ms, Samples called: 27619692, samples/s: 131866
	


	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 2 --cpu_threads_per_caller 12


**Uses: 24 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    2
cpu mode:           ON
threads per caller: 12

Found 1 fast5 files to process.
Init time: 6421 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 261516 ms**, Samples called: 27619692, samples/s: 105614


	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 3 --cpu_threads_per_caller 8

**Uses: 24 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    3
cpu mode:           ON
threads per caller: 8

Found 1 fast5 files to process.
Init time: 9617 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 287261 ms**, Samples called: 27619692, samples/s: 96148.4


	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 4 --cpu_threads_per_caller 6


**Uses: 24 cores up to 100%**

**ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    4
cpu mode:           ON
threads per caller: 6

Found 1 fast5 files to process.
Init time: 12760 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 468687 ms**, Samples called: 27619692, samples/s: 58929.9**

	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 6 --cpu_threads_per_caller 4
	
**Uses: 20 cores up to 100%**
	
ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    6
cpu mode:           ON
threads per caller: 4

Found 1 fast5 files to process.
Init time: 19230 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 403432 ms**, Samples called: 27619692, samples/s: 68461.8
	



	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 8 --cpu_threads_per_caller 3
	
**Uses: 24 cores up to 100%**


ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    8
cpu mode:           ON
threads per caller: 3

Found 1 fast5 files to process.
Init time: 25510 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 431489 ms**, Samples called: 27619692, samples/s: 64010.2


	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 12 --cpu_threads_per_caller 2

**Uses: 24 cores up to 100%**
	
ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    12
cpu mode:           ON
threads per caller: 2

Found 1 fast5 files to process.
Init time: 38079 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 512908 ms**, Samples called: 27619692, samples/s: 53849.2
	
	
	

	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 24 --cpu_threads_per_caller 1
	
**Uses: 24 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5_tiny/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    24
cpu mode:           ON
threads per caller: 1

Found 1 fast5 files to process.
Init time: 76330 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
**Caller time: 660512 ms**, Samples called: 27619692, samples/s: 41815.6
___

num_callers / cpu_threads
1 / 24		209452 ms 
2 / 12		261516 ms
3 / 8 		287261 ms
4 / 6		468687 ms
6 / 4		403432 ms
8 / 3		431489 ms
12 / 2		512908 ms
24 / 1		660512 ms






___
Settings for the --num_callers --cpu_threads_per_caller, should be more towards one caller with as many threads as possible
___