# **The MetaCentrum webinar series - Introduction to MetaCentrum**

This readme was created by Jiří Vorel (vorel@cesnet.cz).

The information provided in this webinar is current as of 23 June 2026.

The course is held online and is taught in Czech.

<p align="center"><img src="./figures/01_meta_webinar1_flyer.png", width="400"></p>

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
- [Linking an ORCID iD to an e-INFRA CZ account](https://docs.account.e-infra.cz/en/docs/access/orcid)


## RStudio demo

```shell
getwd()
```

```shell
version
```

```shell
install.packages("pheatmap")
```

```shell
library(pheatmap)
```

```shell
data <- read.delim("Heat_map_exam.txt", 
                   sep = "\t", 
                   header = TRUE, 
                   stringsAsFactors = FALSE)
```

```shell
head(data, 10)
```

```shell
rownames(data) <- data$PG_ID
data$PG_ID <- NULL

data[] <- lapply(data, function(x) {
  as.numeric(gsub(",", ".", x))
})

data_log <- log10(data + 1)

pheatmap(
  data_log,
  scale = "row",  
  cluster_rows = FALSE,
  cluster_cols = FALSE,
  fontsize = 8,
  main = "Heatmap",
  angle_col = 0
)
```


## Jupiter notebook demo (Python 3)

```shell
import os
os.getcwd()
```

```shell
pip install matplotlib --quiet
```

```shell
from matplotlib import pyplot as plt
x = ['A', 'B', 'C', 'D', 'E']
y = [10, 5, 8, 4, 2]
plt.bar(x, y)
plt.show()
```

## Galaxy demo
- Draft genome of E. coli ([SRR15334628](https://trace.ncbi.nlm.nih.gov/Traces/?run=SRR15334628))
- Illumina paired-end reads

 ## Batch job example
```shell
#!/bin/bash
 #PBS -N Dorado_basecalling
 #PBS -l select=1:ncpus=32:mem=480gb:scratch_ssd=100gb
 #PBS -l walltime=6:0:0
 #PBS -m bae
 #PBS -M vorel@cesnet.cz

 # Test whether a scratch directory exists.
 test -n "$SCRATCHDIR" || { echo >&2 "Variable SCRATCHDIR is not set!"; exit 1; }

 # The scratch directory should be cleaned automatically.
 trap "clean_scratch" TERM EXIT

 # Redirect all potential temporary files to the scratch directory.
 export TMPDIR=$SCRATCHDIR

 # Copy the input files to the scratch directory.
 scp storage-plzen1.metacentrum.cz:imic_course/converted_reads.pod5 $SCRATCHDIR
 scp storage-plzen1.metacentrum.cz:imic_course/dorado_0.9.1.tar.gz $SCRATCHDIR
 cp /storage/plzen1/home/$USER/imic_course/haemonchus_contortus.PRJEB506.WBPS19.genomic.fa $SCRATCHDIR
 cp -r /storage/plzen1/home/$USER/imic_course/dna* $SCRATCHDIR

 # Navigate to the scratch directory.
 cd $SCRATCHDIR

 # Extract the Dorado archive.
 tar -xzf dorado_0.9.1.tar.gz

 # Set the necessary paths and load the dependency module.
 export PATH=$SCRATCHDIR/dorado_0.9.1/bin:$PATH
 export LD_LIBRARY_PATH=$SCRATCHDIR/dorado_0.9.1/lib:$LD_LIBRARY_PATH
 module add minimap2/2.22 || { echo >&2 "Module load failed!"; exit 2; }
 unset CUDA_VISIBLE_DEVICES

 # Start Dorado.
 dorado basecaller dna_r9.4.1_e8_sup@v3.3 converted_reads.pod5 -v --min-qscore 5 --trim all \
 --reference haemonchus_contortus.PRJEB506.WBPS19.genomic.fa --modified-bases 5mCG_5hmCG > dorado_basecalled_mapped_batch_job.bam

 # Copy the final result back to storage.
 scp dorado_basecalled_mapped_batch_job.bam storage-plzen1.metacentrum.cz:~/imic_course || export CLEAN_SCRATCH=false
```

## Batch job example
```shell
qsub -I -N Test_job -l select=1:ncpus=2:mem=4gb:scratch_local=1gb -l walltime=1:00:00
```

## Foldify and AlphaFind protein sequence example
```shell
>sp|A0PK11|CLRN2_HUMAN_Clarin-2_OS=Homo_sapiens
MPGWFKKAWYGLASLLSFSSFILIIVALVVPHWLSGKILCQTGVDLVNATDRELVKFIGDIYYGLFRGCKVRQCGLGGRQSQFTIFPHLVKELNAGLHVMILLLLFLALALALVSMGFAILNMIQVPYRAVSGPGGICLWNVLAGGVVALAIASFVAAVKFHDLTERIANFQEKLFQFVVVEEQYEESFWICVASASAHAANLVVVAISQIPLPEIKTKIEEATVTAEDILY
```

## Access S3 storage

```shell
s3cmd ls
```
```shell
s3cmd ls s3://meta-archive
```
```shell
s3cmd mb s3://testbucket
```
```shell
s3cmd ls
```
```shell
s3cmd ls s3://testbucket
```
```shell
s3cmd rb s3://testbucket
```
```shell
s3cmd ls
```
```shell
s3cmd put dorado_basecalling.sh s3://meta-archive
```
```shell
s3cmd ls s3://meta-archive
```
```shell
s3cmd put -r Folder_example s3://meta-archive
```
```shell
s3cmd ls s3://meta-archive
```
```shell
s3cmd ls s3://meta-archive/Folder_example/
```
```shell
s3cmd get s3://meta-archive/dorado_basecalling.sh
```
```shell
s3cmd get s3://meta-archive/dorado_basecalling.sh
```
```shell
s3cmd get --skip-existing s3://meta-archive/dorado_basecalling.sh
```
```shell
s3cmd get --force s3://meta-archive/dorado_basecalling.sh
```
```shell
s3cmd del s3://meta-archive/dorado_basecalling.sh
```
```shell
s3cmd del -r s3://meta-archive/Folder_example/
```
