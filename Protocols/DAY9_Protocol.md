# DAY9_Protocol : Viromics
    We didn't ran the command instead we observed and intepreted the results


## MVP Pipeline
```
## 

module load gcc12-env/12.1.0
module load micromamba/1.3.1
micromamba activate MVP
cd $WORK/MVP_test
mvip MVP_00_set_up_MVP -i ./WORKING_DIRECTORY/ -m input_file_timeseries_final.csv  --genomad_db_path ./WORKING_DIRECTORY/00_DATABASES/genomad_db/ --checkv_db_path ./WORKING_DIRECTORY/00_DATABASES/checkv-db-v1.5/
mvip MVP_00_set_up_MVP -i ./WORKING_DIRECTORY/ -m input_file_timeseries_final.csv  --skip_install_databases
mvip MVP_01_run_genomad_checkv -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_02_filter_genomad_checkv -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_03_do_clustering -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_04_do_read_mapping -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv --delete_files
mvip MVP_05_create_vOTU_table -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_06_do_functional_annotation -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_07_do_binning -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv --force_outputs
mvip MVP_100_summarize_outputs -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
```


## iPHoP
```
module load miniconda3/4.12.0
conda activate GTDBTk
export GTDBTK_DATA_PATH=./GTDB_db/GTDB_db

gtdbtk de_novo_wf --genome_dir fa_all/ \
--bacteria --outgroup_taxon p__Patescibacteria \
--out_dir output/ \
--cpus 12 --force --extension fa

gtdbtk de_novo_wf --genome_dir fa_all/ \
--archaea --outgroup_taxon p__Altarchaeota \
--out_dir output/ \
--cpus 12 --force --extension fa

module load micromamba/1.3.1
micromamba activate iphop_env
iphop add_to_db --fna_dir fa_all/ \
--gtdb_dir ./output/ \
--out_dir ./MAGs_iPHoP_db \
--db_dir iPHoP_db/

iphop predict --fa_file ./MVP_07_Filtered_conservative_Prokaryote_Host_Only_best_vBins_Representative_Unbinned_vOTUs_Sequences_iPHoP_Input.fasta \
--db_dir ./MAGs_iPHoP_db \
--out_dir ./iphop_output -t 12


```






## Viromics result
1)	11 proviruses and 846 viruses respectively were found in BGR_140717 sample

2)	559 Caudoviricetes were found in the BGR_140717 sample


3)	1 High Quality and Complete virus was found in the BGR_140717 sample whereas 564 Low Quality viruses and 3 Medium Quality viruses were reported in the same sample.


4)	The Id of complete virus is
BGR_140717_NODE_168_lenght_31258_cov_37.020094

The length of the complete virus is 31258
There are 10 hallmark genes present in this complete virus.


5) 50 High Quality viruses were found after binning.

6) Based on the Direct terminal repeat regions on both ends of the genome, following viral contigs were found which are complete circular genomes:
> BGR_140717_NODE_168_length_31258_cov_37.020094
> BGR_140121_NODE_54_length_34619_cov_66.823718
> BGR_131021_NODE_96_length_46113_cov_32.412567
