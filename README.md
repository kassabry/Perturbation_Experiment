# Perturbation Modeling Framework for Novel Design of SRC Kinase Inhibitors 

Verkhivker Lab at Chapman University

Authors: 

* Steven Agajanian
* Ryan Kassab 
* Keerthi Krishnan 
* Gennady Verkhivker

This repository contains the framework and code for instilling molecular transformations of kinase inhibitors using targeted perturbation modeling. The software written is a combination of utilizing the ChemVAE architecture developed by Jennifer Wei, Benjamin Sanchez-Lengeling, Dennis Sheberla, Rafael Gomez-Bomberelli, and Alan Aspuru-Guzik (https://github.com/aspuru-guzik-group/chemical_vae/blob/master/aux_data/banner.png?raw=true)[doi:10.1021/acscentsci.7b00572](http://pubs.acs.org/doi/abs/10.1021/acscentsci.7b00572) as well as perturbation modeling architecture developed by the Verkhivker Lab at Chapman University to perform our molecular transformation experiments. Below is a brief description of the folders and files present in the repository.

Files/Folders:

* perturbation_experiment.ipynb file: Notebook containing the software for the use of variational autoencoder, the perturbation modeling experiments, and the post processing analysis
* Fingerprinting_Similarity.ipynb: Notebook containing examples of similarity testing and implementation
* chemvae and models: Folders containing the models and architecture used to build and compile ChemVAE
* data: data folder containing molecular data of our kinase inhibitors and GDB small molecule baseline retrieved from ZINC and GDB-17 database in SMILES format
* examples: folder containing intro_to_chemvae.ipynb, a notebook with starter code on use of variational autoencoder
* graphs: folder containing graphs for different stages of analysis in pipeline
* results: folder containing files of any raw and curated generated data from experimentation
* supplemental_info: Folder containing supplemental information of experiment results, such as final similarity data of generated molecules to known SRC Inhibitors, graphs represented chemical analysis of generated data, graphs containing analysis of chemical properties from initial data, and preliminary generated data, and a suppemental information guide. 
* environment.yml: environment file to help set up ChemVAE environment with proper dependencies and tools
* requirements.txt: text file stating dependencies for certain packages in environment set-up


To have the proper set-up for the variational autoencoder framework, please refer to the directions on ChemVAE below and refer to their github link (https://github.com/aspuru-guzik-group/chemical_vae/blob/master/aux_data/banner.png?raw=true) and paper (http://pubs.acs.org/doi/abs/10.1021/acscentsci.7b00572) for more information on ChemVAE: 

# ChemVAE Framework Set Up: 

## Questions, problems?
Make a [github issue](https://github.com/aspuru-guzik-group/chemical_vae/issues/new) :smile:. Please be as clear and descriptive as possible.

## How to install
### Requirements: 
An [Anaconda python environment](https://www.anaconda.com/download) is recommend.
Check the environment.yml file, but primarily:
- Python >= 3.5
- Keras >= 2.0.0 && <= 2.0.7
- Tensorflow == 1.1
- RDKit
- Numpy

Jupyter notebook is required to run the ipynb examples.
Make sure that the [Keras backend](https://keras.io/backend/) is set to use Tensorflow

### via Anaconda (recommended way)
Create a conda enviroment:
```
conda env create -f environment.yml
source activate chemvae
python setup.py install
```
### via pip
Assuming you have all the requirements:

`pip install git+https://github.com/aspuru-guzik-group/chemical_vae.git`

## Example: ZINC dataset

This repository contains an example of how to run the autoencoder on the zinc dataset.

First, take a look at the zinc directory. Parameters are set in the following jsons
  - **exp.json**  - Sets parameters for location of data, global experimental parameters number of epochs to run, properties to predict etc. 

For a full description of all the parameters, see hyperparameters.py ; parameters set in exp.json will overwrite parameters in hyperparameters.py, and parameters set in params.json will overwrite parameters in both exp.json and hyperparameters.py

Once you have set the parameters, run the autoencoder using the command from directory with exp.json: 

`
python -m chemvae.train_vae
`

_(Make sure you copy examples directories to not overwrite the trained weights (*.h5))_

## Components
train_vae.py : main script for training variational autoencoder
    Accepts arguments -d ...
    Example of how to run (with example directory here)

- **models.py** - Library of models, contains the encoder, decoder and property prediction models.
- **tgru_k2_gpu.py** - Custom keras layer containing custom teacher forcing/sampling 
- **sampled_rnn_tf.py** - Custom rnn function for tgru_k2_gpu.py, written in tensorflow backend.
- **hyperparameters.py** - Some default parameter settings for the autoencoder
- **mol_utils.py** - library for parsing SMILES into one-hot encoding and vice versa
- **mol_callbacks.py** - library containing callbacks used by train_vae.py
  - Includes Weight_Annealer callback, which is used to update the weight of the KL loss component
- **vae_utils.py** - utility functions for an autoencoder object, used post processing.

## Authors:
This software is written by Jennifer Wei, Benjamin Sanchez-Lengeling, Dennis Sheberla, Rafael Gomez-Bomberelli, and Alan Aspuru-Guzik (alan@aspuru.com). 
It is based on the work published in https://arxiv.org/pdf/1610.02415.pdf by
 
 * [Rafa Gómez-Bombarelli](http://aspuru.chem.harvard.edu/rafa-gomez-bombarelli/),
 * [Jennifer Wei](http://aspuru.chem.harvard.edu/jennifer-wei),
 * [David Duvenaud](https://www.cs.toronto.edu/~duvenaud/),
 * [José Miguel Hernández-Lobato](https://jmhl.org/),
 * [Benjamín Sánchez-Lengeling](),
 * [Dennis Sheberla](https://www.sheberla.com/),
 * [Jorge Aguilera-Iparraguirre](http://aspuru.chem.harvard.edu/jorge-aguilera/),
 * [Timothy Hirzel](https://www.linkedin.com/in/t1m0thy),
 * [Ryan P. Adams](http://people.seas.harvard.edu/~rpa/'),
 * [Alán Aspuru-Guzik](http://aspuru.chem.harvard.edu/about-alan/)


Feel free to reach out to us with any questions! 
