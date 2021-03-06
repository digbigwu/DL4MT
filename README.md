This is a work-in-progress implementation of Dual Learning for Machine Translation by He et al. published in NIPS 2016 (https://papers.nips.cc/paper/6469-dual-learning-for-machine-translation.pdf, https://arxiv.org/abs/1611.00179). It was developed in part by participants at the 3rd Machine Translation Marathon in the Americas (http://www.statmt.org/mtma17/).

# Requirements: #

This code is based on Nematus (https://github.com/rsennrich/nematus) - please ensure you can run Nematus before proceeding. 


The default language model is KenLM. You need both kenlm and the python wrapper
(pip install https://github.com/kpu/kenlm/archive/master.zip)

You need a version of python with 
 * Theano (tested with Theano-0.9.0.dev4) 
 * contextlib2 (tested with 0.5.4)
 * Pyro4 (pip install Pyro4) 
 * ipdb (pip install ipdb). 

I used anaconda to install Theano and contextlib2. 

Theano should be compiled for a GPU. Tested with CUDA v ?? and cuDNN 5.1, but probably best to use a newer version.

# Installation #
1. Clone the repo
2. Modify nematus/config.py
    1. python_loc : The location of the python executable (2.7)
    2. cuda_loc : CUDA home (/usr/local/cuda)
    3. KENLM_PATH : Location of KenLM install (exclude bin from the path, included with moses, if you have moses installed, simply point to your moses dir)
    4. wmt16_systems_dir : Download this http://data.statmt.org/rsennrich/wmt16_systems/ and point to the download location (wget -r --cut-dirs=2 -e robots=off -nH -np -R index.html* http://data.statmt.org/rsennrich/wmt16\_systems/ )
3. Install the kenlm python wrapper : `pip install --user https://github.com/kpu/kenlm/archive/master.zip`
4. Install other stuff : `pip install --user contextlib2 Pyro4`

# Test Data: #
Various tests/examples depend on Rico's wmt16 trained systems. Create a directory for the data, then cd into it and run the one of the following commands:
1. Command for just en-de,de-en systems (required):
* `wget -r --cut-dirs=2 -e robots=off -nH -np -R index.html* http://data.statmt.org/rsennrich/wmt16_systems/en-de/`
* `wget -r --cut-dirs=2 -e robots=off -nH -np -R index.html* http://data.statmt.org/rsennrich/wmt16_systems/de-en/`
2. If you wanted all of the language pairs (optional):
* `wget -r --cut-dirs=1 -e robots=off -nH -np -R index.html* http://data.statmt.org/rsennrich/wmt16_systems/`


# Setup: #

There are a number of files that need configuration.

An attempt was made to put all configuration items in nematus/config.py - put paths to your python, CUDA, etc here.

At the moment, configuring the training script requires changing values in nematus/train_dual.py - put paths to your data, initialized Nematus models, and trained language models here.

The language model required here is a kenlm model with a small wrapper around it.
* use nematus/train_lm.py to train a kenlm model
* use nematus/wrap_kenlm.py to wrap an existing kenlm binary model

# Testing the build: #
./run_tests.py  (THIS WILL FAIL - data paths are all broken)

# Running the code: #
./run_train_dual.py sample_config.py

***

Originator Reference Number: RH-17-117200 Case Reviewer: Brian Brackens Case
Number: 88ABW-2017-3032 The material was assigned a clearance of CLEARED on 20
Jun 2017.

***

This software and any accompanying documentation is released "as is."  
The U.S. government makes no warranty of any kind, express or implied,
concerning this software and any accompanying documentation, including,
without limitation, any warranties of merchantability or fitness for a
particular purpose.  In no event will the U.S. government be liable for any
damages, including any lost profits, lost savings or other incidental or
consequential damages arising out of the use, or inability to use, this
software or any accompanying documentation, even if informed in advance of
the possibility of such damages.

***

