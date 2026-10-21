# **The MetaCentrum webinar series - SW installation**

This readme was created by Jiří Vorel (vorel@cesnet.cz).

The information provided in this webinar is current as of 21 October 2026.

The course is held online and is taught in Czech.

<p align="center"><img src="./figures/04_meta_webinar4_flyer.png", width="400"></p>

## Useful links
- [MetaCentrum](https://www.metacentrum.cz/cs/)
- [CESNET](https://www.cesnet.cz/)
- [e-INFRA CZ](https://www.e-infra.cz/)
- [e-INFRA CZ documentation](https://docs.e-infra.cz/)
- [Contact for MetaCentrum user support](https://docs.metacentrum.cz/en/docs/support)
- [MetaCentrum documentation](https://docs.metacentrum.cz/)
- [MetaCentrum monitoring page](https://my.metacentrum.cz/personal-view)
- [MetaCentrum hands-on courses](https://github.com/CESNET/metacentrum-hands-on)
- [MetaCentrum past seminars](https://metavo.metacentrum.cz/cs/seminars/)

# Precompiled binary

```shell
wget https://github.com/COMBINE-lab/salmon/releases/download/v2.8.0/salmon-cli-x86_64-unknown-linux-gnu.tar.xz
```

```shell
tar -xf salmon-cli-x86_64-unknown-linux-gnu.tar.xz
```

```shell
mv salmon-cli-x86_64-unknown-linux-gnu/ salmon
```

```shell
salmon/salmon --help
```

```shell
salmon/salmon quant -t nucl_ref_for_salmon.fa -p 1 -a mapped_reads_sorted_for_salmon.bam -o output.txt
```

```shell
export PATH=/storage/brno2/home/vorel/WEB_INSTALL/salmon/:$PATH
```

```shell
salmon quant -t nucl_ref_for_salmon.fa -p 1 -a mapped_reads_sorted_for_salmon.bam -o output.txt
```

```shell
module ava salmon
```

```shell
module ava salmon/
```

```shell
export MODULEPATH=/storage/brno2/home/vorel/WEB_INSTALL/:$MODULEPATH
```

```shell
module ava salmon
```

```shell
#!/bin/bash
#PBS -l walltime=1:0:0
#PBS -l select=1:ncpus=4:mem=10gb:scratch_ssd=5gb
#PBS -N Salmon_test_job

trap "clean_scratch" TERM EXIT
cd $SCRATCHDIR
cp /storage/brno2/home/vorel/WEB_INSTALL/nucl_ref_for_salmon.fa $SCRATCHDIR
cp /storage/brno2/home/vorel/WEB_INSTALL/mapped_reads_sorted_for_salmon.bam $SCRATCHDIR

# How to start Salmon?

# 1)
cp /storage/brno2/home/vorel/WEB_INSTALL/salmon/salmon $SCRATCHDIR
./salmon quant -t nucl_ref_for_salmon.fa -p 1 -a mapped_reads_sorted_for_salmon.bam -o output.txt

# 2)
/storage/brno2/home/vorel/WEB_INSTALL/salmon/salmon quant -t nucl_ref_for_salmon.fa -p 1 -a mapped_reads_sorted_for_salmon.bam -o output.txt

# 3)
export PATH=/storage/brno2/home/vorel/WEB_INSTALL/salmon/:$PATH
salmon quant -t nucl_ref_for_salmon.fa -p 1 -a mapped_reads_sorted_for_salmon.bam -o output.txt

# 4)
export MODULEPATH=/storage/brno2/home/vorel/WEB_INSTALL/:$MODULEPATH
module add salmon_2.8.0_local
salmon quant -t nucl_ref_for_salmon.fa -p 1 -a mapped_reads_sorted_for_salmon.bam -o output.txt

cp output.txt /storage/brno2/home/vorel/WEB_INSTALL/ || export CLEAN_SCRATCH=false
```

# Precompiled binary with a dependency

```shell
wget https://github.com/s-andrews/FastQC/releases/download/v0.13.0/fastqc_v0.13.0.zip
```

```shell
unzip -q fastqc_v0.13.0.zip
```

```shell
export PATH=/storage/brno2/home/vorel/WEB_INSTALL/FastQC/:$PATH
```

```shell
fastqc --help
```

```shell
fastqc -t 1 raw_reads_example.fq
```

```shell
module ava openjdk/
```

```shell
module add openjdk/21
```

```shell
fastqc -t 1 raw_reads_example.fq
```

# Debian library

```shell
dpkg -l libgsl28
```

```shell
apt-get download libgsl28
```

```shell
ar -x libgsl28_2.8+dfsg-5_amd64.deb
```

```shell
tar -xf data.tar.xz
```

```shell
ls usr/lib/x86_64-linux-gnu/
```

```shell
export LD_LIBRARY_PATH=/storage/brno2/home/vorel/WEB_INSTALL/usr/lib/x86_64-linux-gnu/:$LD_LIBRARY_PATH
```

# Python pip

```shell
mkdir my_pip_libs
```

```shell
cd my_pip_libs/; pwd; cd ..
```

```shell
module add python/3.11.11
```

```shell
pip3 list
```

```shell
export PYTHONUSERBASE=/storage/brno2/home/vorel/WEB_INSTALL/my_pip_libs
```

```shell
pip3 install torch --user
```

```shell
qsub -I -l walltime=01:00:00 -l select=1:ncpus=1:mem=10gb:scratch_local=10gb
```

```shell
cd /storage/brno2/home/vorel/WEB_INSTALL/
```

```shell
module add python/3.11.11
```

```shell
export PYTHONUSERBASE=/storage/brno2/home/vorel/WEB_INSTALL/my_pip_libs
```

```shell
export TMPDIR=$SCRATCHDIR
```

```shell
pip3 install torch --user
```

```shell
pip3 list
```

# Activation on a different node

```shell
module add python/3.11.11
```

```shell
pip3 list
```

```shell
export PYTHONUSERBASE=/storage/brno2/home/vorel/WEB_INSTALL/my_pip_libs
```

```shell
export PATH=$PYTHONUSERBASE/bin:$PATH
```

```shell
export PYTHONPATH=$PYTHONUSERBASE/lib/python3.11/site-packages:$PYTHONPATH
```

```shell
pip3 list
```

```shell
pip3 install program1 program2 program3 --user
```

```shell
pip3 install -r requirements.txt --user
```

# Python venv

```shell
module add python/3.11.11
```

```shell
python3 -m venv /storage/brno2/home/vorel/WEB_INSTALL/my_python_venv
```

```shell
source my_python_venv/bin/activate
```

```shell
which pip3.11
```

```shell
pip3 list
```

```shell
pip3 install pandas
```

```shell
pip3 list
```

```shell
deactivate
```

# Activation on a different node

```shell
source /storage/brno2/home/vorel/WEB_INSTALL/my_python_venv/bin/activate
```

```shell
pip3 list
```

```shell
deactivate
```

# R package

```shell
mkdir my_R_libs
```

```shell
module ava r/
```

```shell
module add r/4.5.1
```

```shell
export R_LIBS_USER=/storage/brno2/home/vorel/WEB_INSTALL/my_R_libs
```

```shell
R
```

```shell
.libPaths()
```

```shell
installed.packages()
```

```shell
install.packages("BiocManager",lib="/storage/brno2/home/vorel/WEB_INSTALL/my_R_libs")
```

```shell
BiocManager::install("BiocStyle",lib="/storage/brno2/home/vorel/WEB_INSTALL/my_R_libs")
```

```shell
install.packages("ggplot2")
```

# Mamba manager

```shell
mamba env list
```

```shell
mamba create --prefix /storage/brno2/home/vorel/WEB_INSTALL/ncbi_env bioconda::blast
```

```shell
mamba activate /auto/brno2/brno2/vorel/WEB_INSTALL/ncbi_env
```

```shell
blastn -help
```

```shell
mamba deactivate
```

```shell
mamba create --prefix /storage/brno2/home/vorel/WEB_INSTALL/ncbi_env bioconda::blast -y
```

```shell
mamba create --prefix /storage/brno2/home/vorel/WEB_INSTALL/ncbi_env -c bioconda blast
```

```shell
mamba create --prefix /storage/brno2/home/vorel/WEB_INSTALL/ncbi_env -c bioconda blast==2.16.0
```

```shell
mamba create --prefix /storage/brno2/home/vorel/WEB_INSTALL/my_env_mix -c bioconda -c conda-forge blast samtools spades trimmomatic
```

```shell
mamba activate /auto/brno2/brno2/vorel/WEB_INSTALL/my_env_mix
```

```shell
blastn ...
```

```shell
samtools ...
```

```shell
spades.py ...
```

```shell
trimmomatic ...
```

```shell
mamba deactivate my_env_mix
```

# Singularity/Apptainer

```shell
ls -l /cvmfs/singularity.metacentrum.cz/
```

```shell
wget https://data.broadinstitute.org/Trinity/TRINITY_SINGULARITY/trinityrnaseq.v2.15.2.simg
```

```shell
singularity exec trinityrnaseq.v2.15.2.simg Trinity --help
```

```shell
singularity exec trinityrnaseq.v2.15.2.simg Trinity --seqType fq --max_memory 10G --single raw_reads_example.fq
```

```shell
qsub -I -l walltime=01:00:00 -l select=1:ncpus=1:mem=20gb:scratch_local=15gb
```

```shell
cd $SCRATCHDIR
```

```shell
singularity build ariba_sing.img docker://sangerpathogens/ariba:latest
```

```shell
singularity exec ariba_sing.img ariba --help
```

# Build your own Singularity image

```shell
ssh builder
```

```shell
cd $SCRATCHDIR
```

```shell
singularity build -f -s my_test_sing.sbox docker://debian:trixie
```

```shell
singularity shell -f -w my_test_sing.sbox
```

```shell
apt-get update && apt-get upgrade -y
```

```shell
apt-get install -y python3 python3-venv
```

```shell
python3 --version
```

```shell
which python3
```

```shell
python3 -m venv /opt/venv
```

```shell
source /opt/venv/bin/activate
```

```shell
pip3 --version
```

```shell
pip3 install numpy scipy pandas
```

```shell
python -c "import numpy,scipy,pandas as p;[print(f'{m.__name__} - {m.__version__} - OK') for m in (numpy,scipy,p)]"
```

```shell
deactivate
```

```shell
exit
```

```shell
singularity build -f my_image_pylibs.sif my_test_sing.sbox
```

```shell
singularity exec my_image_pylibs.sif /opt/venv/bin/python -c "import numpy,scipy,pandas as p;[print(f'{m.__name__} - {m.__version__} - OK') for m in (numpy,scipy,p)]"
```
# Building and compiling

```shell
qsub -I -l walltime=01:00:00 -l select=1:ncpus=2:mem=10gb:scratch_local=10gb
```

```shell
export TMPDIR=$SCRATCHDIR
```

```shell
cd /storage/brno2/home/vorel/WEB_INSTALL/
```

```shell
wget https://github.com/samtools/samtools/releases/download/1.24/samtools-1.24.tar.bz2
```

```shell
tar -xf samtools-1.24.tar.bz2
```

```shell
mkdir samtools_install
```

```shell
cd samtools-1.24
```

```shell
./configure --help
```

```shell
./configure --prefix=/storage/brno2/home/vorel/WEB_INSTALL/samtools_install/
```

```shell
make -j2
```

```shell
make -j2 install
```

```shell
cd ../samtools_install/
```

```shell
export PATH=/storage/brno2/home/vorel/WEB_INSTALL/samtools_install/bin/:$PATH
```

```shell
samtools --version
```

```shell
qsub -I -l walltime=01:00:00 -l select=1:ncpus=2:mem=10gb:scratch_local=10gb
```

```shell
export TMPDIR=$SCRATCHDIR
```

```shell
cd /storage/brno2/home/vorel/WEB_INSTALL/
```

```shell
mkdir samtools_install_intel
```

```shell
rm -rf samtools-1.24
```

```shell
tar -xf samtools-1.24.tar.bz2
```

```shell
cd samtools-1.24
```

```shell
module add intel-oneapi-compilers
```

```shell
export CC=icx
```

```shell
./configure --prefix=/storage/brno2/home/vorel/WEB_INSTALL/samtools_install_intel/
```

```shell
make -j2
```

```shell
make -j2 install
```

```shell
cd ../samtools_install_intel/
```

```shell
export PATH=/storage/brno2/home/vorel/WEB_INSTALL/samtools_install_intel/bin/:$PATH
```

```shell
samtools --version
```

```shell
qsub -I -l walltime=01:00:00 -l select=1:ncpus=2:mem=10gb:scratch_local=10gb
```

```shell
export TMPDIR=$SCRATCHDIR
```

```shell
cd /storage/brno2/home/vorel/WEB_INSTALL/
```

```shell
module add aocc
```

```shell
mkdir samtools_install_aocc
```

```shell
rm -rf samtools-1.24
```

```shell
tar -xf samtools-1.24.tar.bz2
```

```shell
cd samtools-1.24
```

```shell
export CC=clang
```

```shell
./configure --prefix=/storage/brno2/home/vorel/WEB_INSTALL/samtools_install_aocc/
```

```shell
make -j2
```

```shell
make -j2 install
```

```shell
cd ../samtools_install_aocc/
```

```shell
export PATH=/storage/brno2/home/vorel/WEB_INSTALL/samtools_install_aocc/bin/:$PATH
```

```shell
samtools --version
```
