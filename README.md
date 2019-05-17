# QUBIC2: A novel biclustering algorithm for analyses of transcriptomic data. 

## Abstract
QUBIC2 is a novel biclustering algorithm for analyses of gene expression data from bulk and single-cell RNA-Sequencing. This introductory vignette provides an overview of installation and usage.

## Environment
We will assum you have the following installed:

- A C++ 11 compatible compiler such as >=g++4.8(might work in g++-4.7, though untested)

- make which is also installed on most machines

## Input

The input to QUBIC2 is the expression matrix:

- Rows correspond to genes and columns correspond to conditions.
- Expression units: the preferred expression values are RPKM/FPKM/CPM.
- The data file should be tab delimited.
- The first row and first column should be the names of conditions and genes, respectively.

# Usage

## Installation

Download the source code from https://github.com/maqin2001/qubic2 ,which will be a file named  qubic2-master.zip. Put it in any directpry, and type

```
```

Go to the ‘qubic2-master’ folder

```
```

Type make to compile the source code:

```
```

Then the compiled codes are within the qubic2-master directory.

**Note:** You may fail to compile QUBIC2 if the compiler version is too old. To check the version, you may type gcc -v

## Example dataset

This tutorial run on several real/simulated dataset to illustrate the results obtained at each step. You will find them under the qubic2-master/data folder. In the following, we will mainly use the  "example" file(microarry data from E. coli, with 100 genes and 100 samples) and  "RPKM_testing_1" file (simulated RNA-seq data, with 10 genes and 1000 conditions).

## Discretization

The first step in QUBIC2 is data discretization, and you may choose to use one of the following three discretization methods:

1. quantile-based
2. mixture of Gaussian distribution based
3. left-truncated mixture of Gaussian distribution

QUBIC adopted option1. For more details, please refer to (Li et al. 2009). Option2 is designed for microarray data, and Option3 is for RNA-seq or scRNA-seq which contain abundant zeros. For details regarding the model behind Option2 and Option3, please refer to (Wan et al. 2018).

- To conduct Option1, type

```
```

You will get two output files, namely example.chars and example.rules, and the discretized data is in the example.chars.

- To conduct Option2, type

```
```

You will get four output files, namely example.chars, example.em.chars,  example.original.chars and example.rules,. The discretized data to be used in the following biclustering is the example.chars file.

- To conduct Option3, type

```
```

You will get four output files, namely RPKM_testing_1.chars,RPKM_testing_1.em.chars,  RPKM_testing_1.original.chars and RPKM_testing_1.rules. The discretized data to be used in the following biclustering is the RPKM_testing_1.chars file.

**Note:** For each option, you may also add a -q parameter(0<q<=0.5. default:0.06), e.g.,
```
```
```
```
```
```

## Biclustering

The second step of QUBIC2 is biclustering. Given the discretization is done and discretized data is at hand, we offer the following options:

- KL (refers to KL objective function + regular expansion)
```
```
You will get a file named example.chars.blocks, which contains the output biclusters.

- KLDual (refers to KL objective function + Dual expansion)
```
```
You can find the output biclusters in the example.chars.blocks file.

- Dual (refers to 1.0 objective function + Dual expansion)
```
```
The output biclusters are in the example.chars.blocks file.

- 1.0 biclustering (refers to 1.0 objective function + regular expansion)
```
```

The output biclusters are in the example.chars.blocks file.

**Note**

1. The -d argument is important as it tells the program that the input for biclustering is discretized data
2. Current example cases take two steps to finish the whole process: discretization and biclustering. For the first step we use a -F argument to tell that we just want to do discretization, and for the sencond step we use a -d argument.
3. You may also conduct discretization + biclustering with one command line, just use  ./qubic -i ./data/example or ./qubic -i ./data/RPKM_testing_1 and add the parameters for specific discreitzaion mehtods, e.g., ./qubic -i ./data/example -n or ./qubic -i ./data/RPKM_testing_1 -R. However, as the discretization usually takes a long time and sometimes you may need to adjust biclustering parameters, we recommend to run discretization first, and then run biclustering under different parameters. In this case, you don’t need to wast time on discretization.

## Refences

Li, Guojun, Qin Ma, Haibao Tang, Andrew H Paterson, and Ying Xu. 2009. “QUBIC: A Qualitative Biclustering Algorithm for Analyses of Gene Expression Data.” Nucleic Acids Research 37 (15). Oxford University Press: e101–e101.

Wan, Changlin, Wennan Chang, Yu Zhang, Fenil Shah, Sha Cao, Xin Chen, Melissa Fishel, Qin Ma, and Chi Zhang. 2018. “LTMG (Left Truncated Mixture Gaussian) Based Modeling of Transcriptional Regulatory Heterogeneities in Single Cell Rna-Seq Data a Perspective from the Kinetics of MRNA Metabolism.” BioRxiv. Cold Spring Harbor Laboratory. doi:10.1101/430009.

## Contact ##

Any questions, problems, bugs are welcome and should be dumped to
Qin Ma <Qin.Ma@osumc.edu>

