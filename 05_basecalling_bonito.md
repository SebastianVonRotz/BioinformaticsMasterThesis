The model is available under: https://github.com/nanoporetech/bonito

With these commands at home (https://docs.python.org/3/tutorial/venv.html)
```
python3 -m venv tutorial-env
source tutorial-env/bin/activate
pip install wheel
pip install ont-bonito
```

```
#!/bin/bash
#
#SBATCH --job-name=guppy-batch_basecalling
#
#SBATCH --nodes=1 
#SBATCH --ntasks-per-node=1 
#SBATCH --cpus-per-task=12
#
#SBATCH --time=96:00:00 
#SBATCH --partition=single 
#SBATCH --qos=single
#
#SBATCH --mail-type=end 
#SBATCH --mail-user=voro@zhaw.ch
#
# Install private copy of ont-bonito based on the central Python dependencies
#
# Load modules (all required by Python and PIP)
module load USS/2020
module load gcc/7.3.0
module load python/3.6.5-pe5.26
module load py-numpy/1.17.3-openblas-py3.6-pe5.26
#
# Load modules (ont-bonito)
python3 -m venv tutorial-env
source tutorial-env/bin/activate
pip install wheel
pip install ont-bonito
pip list
bonito basecaller
bonito basecaller dna_r9.4.1 ../data/fast5_tiny > basecalls.fasta
```

AssertionError:
Found no NVIDIA driver on your system. Please check that you
have an NVIDIA GPU and installed a driver from
http://www.nvidia.com/Download/index.aspx