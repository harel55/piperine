# Piperine
Piperine takes in plain text files specifying abstract CRNs and produces sets of DNA sequences. Each sequence set is a possible implementation of the input CRN in 

## Installation 
Piperine has only been tested on Ubuntu and MacOSX Sierra. Windows yet unsupported.
### Python version
Piperine works with only Python 2.7. Make an appropriate [environment](https://pypi.python.org/pypi/virtualenv) if necessary.
### Requirements
Piperine depends on 
-Numpy
-Scipy
-NUPACK (version 3.0.x)
-stickydesign. 
Make sure these are installed before installing Piperine. 
### Preparation for installation
Numpy and Scipy can both be installed easily through pip or conda. NUPACK can be found [here](http://www.nupack.org/) and stickydesign can be found [here](https://github.com/DNA-and-Natural-Algorithms-Group/stickydesign). 
Once NUPACK is installed, make a terminal variable NUPACKHOME that points to installation destination (might be `~/Downloads/nupack3.0.6`). Do this with the commmand `export NUPACKHOME=`_the path to nupack_. 

### Install Piperine

For now, you can only install Piperine from the source files. Clone or download this repository, start a terminal session, and navigate to the repository folder. 

> `git clone git@github.com:DNA-and-Natural-Algorithms-Group/piperine.git`

> `cd piperine`
Execute the following from the command line from within the piperine repo

> `python setup.py install`

During the installation, you will see a prompt that asks 

> Please choose which thermodynamics package to use:

> (1) Nupack mfe (recomended/default)

> (2) Vienna RNAfold

Choose 1. The prompt will then ask if it has guessed the right location for NUPACK, specifically to the executable NUPACKHOME/bin/mfe. If this does not match your expected destination, type in the path to your own NUPACKHOME/bin/mfe and hit enter.

### Use cases
#### Generating sequences

Piperine reads in plaintext files that specify an abstract CRN, converts the CRN into a domain-level DNA specification, then designs sequences implementing the domain-level constraints. An example CRN might be the following, saved in a file called `my.crn`

> ` -> B`

> `B -> A`

> `A + A -> A`

This could then be compiled into DNA sequences by executing the following code in python

> from piperine.designer import run\_designer

> run\_designer('my', 4)

This will tell piperine to generate four candidate sequence sets that each implement the CRN specified in `my.crn`. Piperine will also score each set according to a suite of heuristics intended to quantitate how much a sequence set exhibits pathological sequence motifs. The scores will be saved to a file called `my_scores.csv`. At the bottom of this file, piperine suggests a "winning" sequence set that is most likely to provide good performance in experiments. More detailed information in the winner selection process can be found in the file `score_report.txt`. Sequence sets are indexed starting at 0 and saved to filenames `my`__i__`.crn`, for index __i__.

## TODO
1. Update test suite
1. Improve documentation
1. Make compatible with Python >=2.6
1. Import from external package [peppercompiler](https://github.com/DNA-and-Natural-Algorithms-Group/peppercompiler), rather than package it within piperine
1. Provide built distributions
