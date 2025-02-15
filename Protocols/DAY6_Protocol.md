# DAY6_Protocol : Genomics

AIM 
> To do Hybrid assembly of pair-end reads

> Combining power of single reads and long reads

```
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=32G
#SBATCH --time=5:00:00
#SBATCH --job-name=01_fastqc
#SBATCH --output=01_fastqc.out
#SBATCH --error=01_fastqc.err
#SBATCH --partition=base
#SBATCH --reservation=biol217

module load gcc12-env/12.1.0
module load micromamba/1.4.2
eval "$(micromamba shell hook --shell=bash)"
cd $WORK
micromamba activate .micromamba/envs/01_short_reads_qc



# creata new folder for output of qc 
mkdir -p $WORK/genomics/1_short_reads_qc/1_fastqc_raw
for i in ./add/absolute/path/*.gz; do fastqc $i -o ./add/absolute/path/output_dir/ -t 16; done

micromamba deactivate
jobinfo
