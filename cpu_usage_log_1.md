##### Vary general setting

	PATH_IN=/cfs/earth/scratch/voro/data/Dataset_test/fast5/
	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test

**Uses: 1 core up to 60%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:
model file:
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         1000
chunks per runner:  20
records per file:   4000
num basecallers:    1
cpu mode:           ON
threads per caller: 4

Found 110 fast5 files to process.
Init time: 103 ms

Caller time: 140434 ms, Samples called: 4167783804, samples/s: 2.96779e+07

	PATH_IN=/cfs/earth/scratch/voro/data/Dataset_test/fast5/
	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109

**Uses: 5 cores 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    1
cpu mode:           ON
threads per caller: 4

Found 110 fast5 files to process.
Init time: 3336 ms

Caller time: Not finished

___
!!! Setting "--flowcell FLO-MIN106 --kit SQK-LSK109" activates a more intensive basecalling !
___

##### Vary --num_callers

	PATH_IN=/cfs/earth/scratch/voro/data/Dataset_test/fast5/
	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 2


**Uses: 8 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    2
cpu mode:           ON
threads per caller: 4

Found 110 fast5 files to process.
Init time: 6428 ms

Caller time: Not finished


	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 3

**Uses: 12 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    3
cpu mode:           ON
threads per caller: 4

Found 110 fast5 files to process.
Init time: 9667 ms

Caller time: Not finished


	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 4

**Uses: 16 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    4
cpu mode:           ON
threads per caller: 4

Found 110 fast5 files to process.
Init time: 12804 ms

Caller time: Not finished

	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 6
	
**Uses: 24 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    6
cpu mode:           ON
threads per caller: 4

Found 110 fast5 files to process.
Init time: 19214 ms

Caller time: Not finished

##### Vary --cpu_threads_per_caller

	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --cpu_threads_per_caller 8

**Uses: 8-9 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    1
cpu mode:           ON
threads per caller: 8

Found 110 fast5 files to process.
Init time: 3350 ms

Caller time: Not finished

	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --cpu_threads_per_caller 12

**Uses: 13 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    1
cpu mode:           ON
threads per caller: 12

Found 110 fast5 files to process.
Init time: 3282 ms

Caller time: Not finished


##### Vary --cpu_threads_per_caller --cpu_threads_per_caller

	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 3 --cpu_threads_per_caller 8

**Uses: 25 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    3
cpu mode:           ON
threads per caller: 8

Found 110 fast5 files to process.
Init time: 9659 ms

Caller time: Not finished


	$GUPPY_BASECALLER_PATH -i $PATH_IN -s ./test --flowcell FLO-MIN106 --kit SQK-LSK109 --num_callers 3 --cpu_threads_per_caller 4
	
**Uses:12 cores up to 100%**

ONT Guppy basecalling software version 4.2.2+effbaf8
config file:        /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/dna_r9.4.1_450bps_hac.cfg
model file:         /cfs/earth/scratch/voro/local_apps/ont-guppy-cpu/data/template_r9.4.1_450bps_hac.jsn
input path:         /cfs/earth/scratch/voro/data/Dataset_test/fast5/
save path:          ./test
chunk size:         2000
chunks per runner:  512
records per file:   4000
num basecallers:    3
cpu mode:           ON
threads per caller: 4

Found 110 fast5 file
Init time: 9726 ms

Caller time: Not finished

___
!!! Setting The CPU usage is calculated by --num_callers  x --cpu_threads_per_caller = used amount of cpu cores
___