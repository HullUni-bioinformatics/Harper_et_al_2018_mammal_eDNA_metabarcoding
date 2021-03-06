# Harper *et al.* (2019) Mammal eDNA metabarcoding

Data processing workflow and supplementary data for:

Harper *et al.* (2019) Environmental DNA (eDNA) metabarcoding of pond water as a tool to survey conservation and management priority mammals. *Biological Conservation*, __238__, 108225. https://doi.org/10.1016/j.biocon.2019.108225

Permanently archived at: [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.2561415.svg)](https://doi.org/10.5281/zenodo.2561415)


## Contents

Curated reference databases used in analyses (GenBank format) [(here)](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Reference_database). The notebooks used to create these reference databases can be found [(here)](https://github.com/HullUni-bioinformatics/Curated_reference_databases).

Notebooks to run metaBEAT pipeline [(here)](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Jupyter_notebooks)

NCBI Sequence Read Archive (SRA) accession numbers for raw Illumina data [(here)](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Data/Sample_accessions.tsv)

Taxonomic assignment results [(here)](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Data/Taxonomic_Assignment_Results)

R scripts used to analyse metaBEAT output and produce figures [(here)](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/R_scripts)

Sample metadata needed to run analyses in R [(here)](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Data/Sample_Metadata)


## Instructions to set up dependencies for data processing and analyses

To facilitate full reproducibility of our analyses, we provide Jupyter notebooks illustrating our workflow and all necessary associated data in this repository.

Illumina data was processed (from raw reads to taxonomic assignment) using the [metaBEAT](https://github.com/HullUni-bioinformatics/metaBEAT) pipeline. The pipeline relies on a range of open bioinformatics tools, which we have wrapped up in a self-contained docker image that includes all necessary dependencies [here](https://hub.docker.com/r/chrishah/metabeat/).


## Setting up the environment

In order to retrieve scripts and associated data (reference sequences, sample metadata etc.), start by cloning this repository to your current directory:

```
git clone --recursive https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding.git
```

In order to make use of our self contained analysis environment, you will have to install Docker on your computer. Docker is compatible with all major operating systems, but see the Docker documentation for details. On Ubuntu, installing Docker should be as easy as:

```
sudo apt-get install docker.io
```

Once Docker is installed, you can enter the environment by typing:

```
sudo docker run -i -t --net=host --name metaBEAT -v $(pwd):/home/working chrishah/metabeat /bin/bash
```

This will download the metaBEAT image (if not yet present on your computer) and enter the 'container' i.e. the self contained environment (**NB:** ```sudo``` may be necessary in some cases). With the above command, the container's directory ```/home/working``` will be mounted to your current working directory (as instructed by ```$(pwd)```). In other words, anything you do in the container's ```/home/working``` directory will be synced with your current working directory on your local machine.


## Data processing workflow as Jupyter notebooks

Raw illumina data has been deposited on the NCBI SRA:
- Study: SRP164740
- BioProject: PRJNA495011
- BioSample accessions: SAMN10195928 - SAMN10196255
- SRA accessions: SRR7986451 - SRR7986778
 

The sample specific accessions can be found [here](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Data/Sample_accessions.tsv). Before following the workflow for data processing, you'll need to download the raw reads from the SRA. To download the raw read data, you can follow the steps in this [Jupyter notebook](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/raw_reads/How_to_download_from_SRA.ipynb).

With the data in place, you should be able to fully reproduce our analyses by following the steps outlined in the [Jupyter notebooks](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Jupyter_notebooks).

The workflow illustrated in the notebooks assumes that the raw Illumina data is present in a directory ```raw_reads``` at the base of the repository structure and that the files are named according to the following convention: 'sampleID-marker', followed by '_R1' or '_R2' to identify the forward/reverse read file respectively. SampleID must correspond to the first column in the file ```Sample_accessions.tsv``` [here](https://github.com/HullUni-bioinformatics/Harper_et_al_2018_mammal_eDNA_metabarcoding/tree/master/Data/Sample_accessions.tsv).
