	[voro@head01 scripts]$ kraken2-build --db GREENGENES --special greengenes
	/cfs/earth/scratch/voro/local_apps/kraken2/scripts/GREENGENES /cfs/earth/scratch/voro/local_apps/kraken2/scripts
	/cfs/earth/scratch/voro/local_apps/kraken2/scripts/GREENGENES/data /cfs/earth/scratch/voro/local_apps/kraken2/scripts/GREENGENES /cfs/earth/scratch/voro/local_apps/kraken2/scripts
	--2020-12-31 13:39:10--  ftp://greengenes.microbio.me//greengenes_release/gg_13_5/gg_13_5.fasta.gz
			   => 'gg_13_5.fasta.gz'
	Resolving greengenes.microbio.me (greengenes.microbio.me)... 169.228.46.98
	Connecting to greengenes.microbio.me (greengenes.microbio.me)|169.228.46.98|:21... connected.
	Logging in as anonymous ... Logged in!
	==> SYST ... done.    ==> PWD ... done.
	==> TYPE I ... done.  ==> CWD (1) /greengenes_release/gg_13_5 ... done.
	==> SIZE gg_13_5.fasta.gz ... 272134013
	==> PASV ... done.    ==> RETR gg_13_5.fasta.gz ... done.
	Length: 272134013 (260M) (unauthoritative)

	100%[============================================================================================================>] 272,134,013 19.1MB/s   in 17s    

	2020-12-31 13:39:29 (15.5 MB/s) - 'gg_13_5.fasta.gz' saved [272134013]

	--2020-12-31 13:39:41--  ftp://greengenes.microbio.me//greengenes_release/gg_13_5/gg_13_5_taxonomy.txt.gz
			   => 'gg_13_5_taxonomy.txt.gz'
	Resolving greengenes.microbio.me (greengenes.microbio.me)... 169.228.46.98
	Connecting to greengenes.microbio.me (greengenes.microbio.me)|169.228.46.98|:21... connected.
	Logging in as anonymous ... Logged in!
	==> SYST ... done.    ==> PWD ... done.
	==> TYPE I ... done.  ==> CWD (1) /greengenes_release/gg_13_5 ... done.
	==> SIZE gg_13_5_taxonomy.txt.gz ... 9538069
	==> PASV ... done.    ==> RETR gg_13_5_taxonomy.txt.gz ... done.
	Length: 9538069 (9.1M) (unauthoritative)

	100%[============================================================================================================>] 9,538,069   2.95MB/s   in 3.1s   

	2020-12-31 13:39:46 (2.95 MB/s) - 'gg_13_5_taxonomy.txt.gz' saved [9538069]

	gzip: gg_13_5_taxonomy.txt already exists; do you wish to overwrite (y or n)? y
	/cfs/earth/scratch/voro/local_apps/kraken2/scripts/GREENGENES /cfs/earth/scratch/voro/local_apps/kraken2/scripts
	/cfs/earth/scratch/voro/local_apps/kraken2/scripts
	Creating sequence ID to taxonomy ID map (step 1)...
	Sequence ID to taxonomy ID map already present, skipping map creation.
	Estimating required capacity (step 2)...
	Estimated hash table requirement: 89335220 bytes
	Capacity estimation complete. [45.564s]
	Building database files (step 3)...
	Taxonomy parsed and converted.
	CHT created with 12 bits reserved for taxid.
	Completed processing of 1262986 sequences, 1769520677 bp
	Writing data to disk...  complete.
	Database files completed. [3m34.453s]
	Database construction complete. [Total: 4m20.045s]
	[voro@head01 scripts]$ Connection reset by 192.168.232.60 port 22