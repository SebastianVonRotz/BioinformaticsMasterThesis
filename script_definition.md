#### basecalling_guppy_array.sh
##### Description
Basecalling raw data with array jobs
##### Prerequisites and Dependencies: 	
* The raw data has to be in subdirectories
* Local installation of guppy
##### Input and file type: 					  
* Raw Data in subdirectories
* .fast5
##### Output and file type: 				
* Basecalled Data in one directory
* .fastq

#### demultiplexing_guppy_array.sh
##### Description
Uses guppy barcoder for demultiplexing fastq files according to their barcode
##### Prerequisites and Dependencies: 	
* The fastq data has to be in one folder
* Local installation of guppy
##### Input and file type: 					  
* Raw Data in one directory
* .fastq
##### Output and file type: 				
* Barcoded data in subdirectory
* barcoded .fastq

#### demultiplexing_qcat_array.sh
##### Description
Uses qcat for demultiplexing fastq files according to their barcode
##### Prerequisites and Dependencies: 	
* The fastq data has to be in one folder
* Local installation of qcat
##### Input and file type: 					  
* Raw Data in one directory
* .fastq
##### Output and file type: 				
* Barcoded data in one directory
* barcoded .fastq

#### nanoplot_fastq.sh
##### Description
Creates several statistical graphs and plots, as an input it uses fastq files
##### Prerequisites and Dependencies: 	
* The fastq data has to be in one folder
* Module is available on HPC
##### Input and file type: 					  
* Raw Data in one directory
* .fastq
##### Output and file type: 				
* Plots and stats data in one directory
* Plots
* Texts

#### nanoplot_sum.sh
##### Description
Creates several statistical graphs and plots, as an input it uses the summary file (creates more informatin than nanoplot_)
##### Prerequisites and Dependencies: 	
* The summary file has to be in one folder
* Module is available on HPC
##### Input and file type: 					  
* Raw Data in one directory
* summary.txt
##### Output and file type: 				
* Plots and stats data in one directory
* Plots
* Texts

#### filter_trim_nanofilt.sh
##### Description
Filters fastq data based on sequence maxmin length and quality score
##### Prerequisites and Dependencies: 	
* Module available on HPC
##### Input and file type: 					 
* .fastq
##### Output and file type: 				
* .fastq

#### basecalling_guppy_job.sh
##### Description
Basecalling raw data with a single job
##### Prerequisites and Dependencies: 	
* The raw data has to be in one directory
* Local installation of guppy
##### Input and file type: 					  
* Raw Data in one directory
* .fast5
##### Output and file type: 				
* Basecalled Data in one directory
* .fastq

#### job_array_prep.sh
##### Description
Creates a copy of a raw data directory and puts the data in subdirectories
##### Prerequisites and Dependencies: 	
* Target raw data directory fast5 files have to be in one directory
##### Input and file type: 					  
* One target directory
* .fast5 files
* Number of files per subdirectory
##### Output and file type: 				
* New directory with .fast5 files in subdirectory
* .fast5

#### classification_kraken2_raw.sh
##### Description
Classifies ready with a given or custom database
##### Prerequisites and Dependencies: 	
* Database needs to be setup (e.g. Greengenes)
##### Input and file type: 					  
* .fastq file
##### Output and file type: 				
* OUTPUT
* REPORT

#### classification_kraken2_nanofilt.sh
##### Description
Classifies ready with a given or custom database is designed for the output of the Nanofilt Script
##### Prerequisites and Dependencies: 	
* Database needs to be setup (e.g. Greengenes)
##### Input and file type: 					  
* .fastq file
##### Output and file type: 				
* OUTPUT
* REPORT

#### krona_plots.sh
##### Description
Creates krona plots, based on tranformation of the Report from kraken2
##### Prerequisites and Dependencies: 	
* Local installation of krona-tools
##### Input and file type: 					  
* REPORT
##### Output and file type: 				
* kronaplot.html

#### r_kraken2_report.sh
##### Description
Create stats based on the Report output from kraken2
##### Prerequisites and Dependencies: 	
* Local installation R
* Rscript: kraken2_report_stats.R
##### Input and file type: 					  
* REPORT from kraken
##### Output and file type: 				
* r_stats

#### r_kraken2_report_nanofilt.sh
##### Description
Create stats based on the Report output from kraken2 (but filtered)
##### Prerequisites and Dependencies: 	
* Local installation R
* Rscript: kraken2_report_stats.R
##### Input and file type: 					  
* REPORT from kraken
##### Output and file type: 				
* r_stats