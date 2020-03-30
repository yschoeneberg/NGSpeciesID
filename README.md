NGSpeciesID
===========

NGSpeciesID is a tool for clustering and consensus forming of targeted ONT reads. This repository is a modified version of [isONclust](https://github.com/ksahlin/isONclust), where consensus and polishing feautures have been added.

NGSpeciesID is distributed as a python package supported on Linux / OSX with python v3.6. [![Build Status](https://travis-ci.org/ksahlin/NGSpeciesID.svg?branch=master)](https://travis-ci.org/ksahlin/NGSpeciesID).

Table of Contents
=================

  * [INSTALLATION](#INSTALLATION)
    * [Using conda](#Using-conda)
    * [Testing installation](#testing-installation)
  * [USAGE](#USAGE)
    * [Output](#Output)
    * [Parameters](#Parameters)
  * [CREDITS](#CREDITS)
  * [LICENCE](#LICENCE)



INSTALLATION
----------------

**NOTE**: If you are experinencing issues (e.g. [this one](https://github.com/rvaser/spoa/issues/26)) with the third party tools  [spoa](https://github.com/rvaser/spoa) or [medaka](https://github.com/nanoporetech/medaka) in the all-in-one installation instructions below, please install the tools manually with their respective installation instructions [here](https://github.com/rvaser/spoa#installation) and [here](https://github.com/nanoporetech/medaka#installation).  

### Using conda
Conda is the preferred way to install NGSpeciesID.

1. Create and activate a new environment called NGSpeciesID

```
conda create -n NGSpeciesID python=3.6 pip 
conda activate NGSpeciesID
```

2. Install NGSpeciesID 

```
pip install NGSpeciesID
conda install --yes -c conda-forge -c bioconda medaka==0.11.5 openblas==0.3.3 spoa
```
3. You should now have 'NGSpeciesID' installed; try it:
```
NGSpeciesID --help
```

Upon start/login to your server/computer you need to activate the conda environment "NGSpeciesID" to run NGSpeciesID as:
```
conda activate NGSpeciesID
```



### Testing installation

Assuming you are in the NGSpeciesID directory, you can try the installation with

``` 
python NGSpeciesID --ont  --fastq  test/sample_h1.fastq --outfolder  ~/tmp/sample_h1 --consensus --medaka
```


USAGE
-------

NGSpeciesID needs a fastq file generated by an Oxford Nanopore basecaller.

```
NGSpeciesID --ont --consensus --medaka --fastq [reads.fastq] --outfolder [/path/to/output] 
```
The argument `--ont` simply means `--k 13 --w 20`. These arguments can be set manually without the `--ont` flag. Specify number of cores with `--t`. 


### Output

The output consists of clustering and consensus information.

* The final cluster information is given in a tsv file `final_clusters.tsv` present in the specified output folder.
* Draft spoa consensus sequences of each of the clusters are given as consensus_reference_X.fasta (where X is a number).
* A folder named “medaka_cl_id_X” is created for each spoa consensus. Each medaka outfolder contains medakas output, including the final polished consensus named (by medaka) as “consensus.fasta”.


In the cluster TSV-file, the first column is the cluster ID and the second column is the read accession. For example:

```
0 read_X_acc
0 read_Y_acc
...
n read_Z_acc
```
if there are n reads there will be n rows. Some reads might be singletons. The rows are ordered with respect to the size of the cluster (largest first).



CREDITS
----------------

Please cite [1] when using NGSpeciesID.

1. TBA



LICENCE
----------------

GPL v3.0, see [LICENSE.txt](https://github.com/ksahlin/NGSpeciesID/blob/master/LICENCE.txt).


