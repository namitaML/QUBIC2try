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




