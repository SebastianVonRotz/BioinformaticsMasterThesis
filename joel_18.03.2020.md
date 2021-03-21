#### Telcon 18.03.2020
~~Data aquisition
Maybe create documentation for ont guppy~~
~~use module spider + name of application -> look if it is available~~
~~Goal of defining a more dynamic file for running jobs~~
~~Compare the most actual basecalling methods (Mail Fabio, Bonito, FlipFlop)
Try to make bonito running -> Python dependencies? How install with PIP (Tell Joel if I started)~~
~~Check Mail notes
Still keep Nanofilt
Canu is a good start but maybe use other assemblers
Send Proposal
Propose a date in 2 Weeks~~
```
PIP install [
biopython==1.75
NanoFilt==2.6.0
numpy==1.17.4
pandas==0.25.3
python-dateutil==2.8.1
pytz==2019.3
six==1.13.0
]
```
#### Worked for the user
```
[12:07] Pothier Joël (poth)
    #!/bin/bash
#
# Install private copy of nanofilt based on the central Python dependencies
#
# Load modules (all required by Python and PIP)
module load slurm/17.11.8
module load gcc/7.3.0
module load python/3.6.5
module load py-pip/19.0.3-py3.6
#
# Load modules (all required by NanoFilt)
module load openblas/0.3.5
module load py-biopython/1.73-openblas-py3.6
module load py-numpy/1.16.2-openblas-py3.6
module load py-pandas/0.24.1-openblas-py3.6
module load py-dateutil/2.5.2-py3.6
module load py-pytz/2017.2-py3.6
module load py-six/1.12.0-py3.6
#
# Create private install into /cfs/earth/scratch/<loginname>/python
pip3 install nanofilt
```
#### Track Module 2 Content
**1st Part:**
* Amplicon Sequencing with nanopore
* Processing asbects bioinformatic what are available Workflows
* High Error rate of the Reads, does it compensate with higher coverage
* Summarize conceptual workflows to get a accurate sequence
* How many samples can be multiplexed?
* Common used Barcodes
* Summarize Idea
* Amplicon sequencing
* Technical Background NanoPore
* Sequencing output NanoPore
* BaseCalling -> GPU need (SW - ont-guppy-cpu)
* BaseCalling on Workstation, time need too big    
**2nd Part:**  
* Workflow with Amplicon
* Spacer Phylogeny

####  Question
* ~~Theo mentioned comparing different technologys? (For identification?)~~ Everything about Amplicon sequencing workflows with Nanopore
*  Why not use updated CRISPR finder platform (https://crisprcas.i2bc.paris-saclay.fr/)?
*  ~~Where can I find guppy for the nanopore Training~~ On the training site
*  ~~Train a Guppie Model to reduce basecall Error?~~ Better check literature first
*  ~~Docker?~~Probably not used within HPC environment, may propose it
*  ~~Summer school ideas?~~
*  ~~Possible to work on my personal computer?~~ Use Putty and work on the HPC
*  ~~Book for stronger base and broader knowledge~~
*  ~~Reagarding the workflow, goal to bring it in an only script based approach?~~
*  ~~Regarding 2nd Part should I get in contact with Fabio?~~
