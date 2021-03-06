# REBOOT: RE-interpreting BOOTstrap supports for phylogenetics

## Introduction

This project aims to evaluate the interpretation of support values generated by Felsenstein's bootstrap (FBP; [Felsenstein 1985]), transfer bootstrap expectation (TBE; [Lemoine et al. 2018]) and other bootstrap methods (e.g. [Minh et al. 2013]). To do so we rely on simulations where the true trees are known. The main idea is to look at the correlation between branch supports inferred by each method and the probability that the branch is true. While FBP is well known to be conservative (i.e., FBP support of >=70% typically means that the branch is true with a probability of >=0.95) ([Hillis and Bull 1993]), none is known about TBE. Thus, we want to assess if the suggested threshold of 70% applies well to TBE or not.


## Simulations

### Birth-death simulations

To replicate the results follow these steps:

1. Run `generate_datasets.R` located in `scripts/` folder (this relies on the `functions.R` script). This generates datasets and runs IQ-TREE on them. 

2. Run `calculate_tbes.R`. This uses [BOOSTER](https://github.com/evolbioinfo/booster/) to calculate TBE and FBP for each dataset).

3. Run `bootstrap_data.R`. This generates the output file `simulated.csv`.

### PANDIT simulations

1. Download the simulated alignments based on the PANDIT database from [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1156452.svg)](https://doi.org/10.5281/zenodo.1156452). 
2. Go to `dna` folder and for each sub-folder `$i`, run IQ-TREE:

        iqtree -s data.$i -m `cat model.$i` -b 100
3. In each sub-folder, create a symbolic links:

        ln -s data.$i alignment.fasta
        ln -s tree.$i phylogram.phy
4. Run `calculate_tbes.R`.     
5. Run `bootstrap_data.R`. This generates the output file `pandit.csv`.

### Making plots from birth-death and PANDIT simulations

1. Run `bootstrap_plots.R`. This combines the output from PANDIT analysis (`pandit.csv`) with the output from birth-death analysis (`simulated.csv`) and makes the plot. 



## References


[Felsenstein 1985]: https://doi.org/10.1111/j.1558-5646.1985.tb00420.x
[Hillis and Bull 1993]: https://doi.org/10.1093/sysbio/42.2.182
[Lemoine et al. 2018]: https://doi.org/10.1038/s41586-018-0043-0
[Minh et al. 2013]: https://doi.org/10.1093/molbev/mst024
