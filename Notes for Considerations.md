# Guppy basecaller

https://community.nanoporetech.com/protocols/Guppy-protocol/v/gpb_2003_v1_revt_14dec2018/setting-up-a-run-configurations-and-parameters

Choosing a config file for Guppy

Config files are named as follows:

	<strand type>_<pore version>_<speed>_<custom tags>.cfg

For example, a config file for high accuracy DNA basecalling on an R9.4.1 pore at 450 bases per second would be called dna_r9.4.1_450bps_hac.cfg. It may not be clear what pore and speed you are using, which is why directly choosing a config file is generally left to expert users. All other users should select flow cell and kit instead.

___
Why are the total basecalled file sum different from the array job or single job?

--> Solved, some of the raw data fast5 reads have the same name in the passed and failed directories, when they get put together in one directory some get deleted
___
The harder it is for a scientist to use a system compared to an ad-hoc hack, script, or perhaps a suboptimal stand-alone tool, the lower the widespread acceptance of a workflow system is in the wider bioinformatics and computational biology community. In general, we therefore recommend further development of lightweight and
Spjuth et al. Biology Direct (2015) 10:43
Page 11 of 12
layered systems, where at least the basic functionality is easily accessed. More specifically:
• Maintain as much reproducibility as possible without sacrificing usability and simplicity of design and execution. 
• Keep things simple, lightweight, easy to install and integrate with Bash and scripting languages. 
• Workflows should be easily executed, with little or no change in local and distributed environments (HPC and cloud). 
• Encourage attempts for further data flow tandardization and data versioning as well as standardized software management. 
• Put more effort into (biological) testing, validation, continuous delivery and deployment of the software. In other words, spend more effort on quality assurance.
