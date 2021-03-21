#### Nanofilt installation (PIP install commands deduced with "PIP freeze install")
```
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