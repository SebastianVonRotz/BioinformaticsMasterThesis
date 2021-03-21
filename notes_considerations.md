# Guppy basecaller

https://community.nanoporetech.com/protocols/Guppy-protocol/v/gpb_2003_v1_revt_14dec2018/setting-up-a-run-configurations-and-parameters

Choosing a config file for Guppy

Config files are named as follows:

	<strand type>_<pore version>_<speed>_<custom tags>.cfg

For example, a config file for high accuracy DNA basecalling on an R9.4.1 pore at 450 bases per second would be called dna_r9.4.1_450bps_hac.cfg. It may not be clear what pore and speed you are using, which is why directly choosing a config file is generally left to expert users. All other users should select flow cell and kit instead.

___
Why are the total basecalled file sum different from the array job or single job?