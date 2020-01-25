![repo version](https://img.shields.io/badge/Version-v.2.0-green)
![python version](https://img.shields.io/badge/python-v.3.6.8-blue)
![license](https://img.shields.io/badge/license-CC_BY_4.0-orange)


# WHALES descriptors

This repository contains all the necessary files to compute Weighted Holistic Atom Localization and Entity Shape (WHALES) descriptors starting from an rdkit supplier file.

For more information regarding the method, have a look at:

Francesca Grisoni, Daniel Merk, Viviana Consonni, Jan A. Hiss, Sara Giani Tagliabue, Roberto Todeschini & Gisbert Schneider "Scaffold hopping from natural products to synthetic mimetics by holistic molecular similarity", *Nature Communications Chemistry* 1, 44, 2018. (Freely available at this [link](https://www.nature.com/articles/s42004-018-0043-x))

## Table of Contents
1. [Getting started](#getting started) 
2. [Using the Code](#using the code)
4. [Authors](#authors)
5. [License](#license)
6. [Papers using WHALES descriptors](#papers) 
6. [How to cite](#cite) 


## What is new in version 2
in progress

You can access the previous version (WHALES v.1.1) at the following [here](https://github.com/grisoniFr/whales_descriptors/tree/v.1.1)

## Getting Started <a name="getting started"></a>

These instructions will get you a copy of the project up and running on your local machine.

### Prerequisites <a name="Prerequisites"></a>

The following prerequisites are needed:

*[Python 2.7*](https://www.python.org/download/releases/2.7/)

*[RDKit](http://www.rdkit.org/docs/Install.html)

*[NumPy](https://scipy.org/install.html)

*[pandas](https://pandas.pydata.org)

A guide to the correct installation is provided in the following paragraph.

### Preliminary steps

Install conda from the [official website](https://www.anaconda.com/download/). Once conda is installed, it can be used to generate the environment and download RDKit. If you already have RDKit and pandas up and running, you can move to the next paragraph. 

It is suggested to run all the calculations within an RDKit environment. 
The environment can be created with conda as follows:
```
conda create -n whales_env python=2.7*
activate whales_env
```
The RDKit repositories can be listed with the following command:
```
conda install -c rdkit rdkit
```
Alternatively, you can also try with the following:
```
anaconda search -t conda rdkit
```
Choose then the best installation for py27 according to the platform. For instance:
```
conda install -c https://conda.anaconda.org/nickvandewiele rdkit
```
Now install the necessary prerequisites
```
sudo apt-get install python-setuptools
sudo apt install git
python -m pip install --user pandas
```

### Installation <a name="Installation"></a>

The repository can be cloned as follows

```
git clone https://github.com/grisoniFr/WHALES_descriptors.git
```

Change directory to your local Git repository and to the main WHALES folder e.g., < git_repository\current_user>\WHALES-descriptors\ 

Then, install the package as follows:
```
sudo python setup.py install
```
To check whether the installation went well, type 
```
python 
import whales_descriptors
quit()
```
If no errors are displayed, WHALES package has been succesfully installed. 

## Using the code <a name="using the code"></a>

### Importing molecular files
RDKit suppliers have to be used as the input for WHALES calculation, for instance:

```
python # start python
from rdkit import Chem # imports package
suppl = Chem.SDMolSupplier(filename) # generates an rdkit supplier file
```
If the molecules are more than approx. 10,000, it is suggested to use ForwardMolSupplier, instead:
```
suppl = Chem.ForwardSDMolSupplier(filename) 
```
Note that geometrical coordinates have to be specified/computed in order to calculate WHALES descriptors.

### Utilizing WHALES descriptors
The WHALES package can be imported as follows:
```
from whales_descriptors import do_whales
```
and used to calculate the descriptors for the supplier molecules

```
x, labels = do_whales.main(suppl, charge_threshold=0, do_charge=True, property_name='')
```
Specified parameters:
* suppl: rdkit supplier
*    charge_threshold: to neglect atoms with absolute partial charges lower than the threshold (default = 0)
*    do_charge: if True, Gasteiger-Marsili partial charges are computed with rdkit
*    property_name: name of the column containing partial charges of the sdf file (mandatory if do_charge is False)

Returns:
* x (n_mol,p): descriptor matrix, each row corresponds to a molecule
* labels (1,p): descriptor labels

N.B. If a calculation error occurs for a given molecule (e.g., no partial charges computed), the corresponding descriptor values are set to -999. 

### Export descriptors values as a .txt file

The results can be exported as a plain txt file as follows:

```
import numpy as np
np.savetxt(save_name + '_whales.txt', x, delimiter=' ', newline='\n') # for descriptors
np.savetxt(save_name + '_labels.txt', labels, delimiter=' ', newline='\n',fmt='%s') # for labels
```
where "save_name" is a user-defined name, e.g., "WHALES_descriptors".

## Authors <a name="authors"></a>

* **Francesca Grisoni** (https://github.com/grisoniFr)

Contributors to the WHALES descriptors project:
* Francesca Grisoni, University of Milano-Bicocca & ETH-Zurich
* Prof. Dr. Gisbert Schneider, ETH Zurich, gisbert.schneider@pharma.ethz.ch
* Dr. Viviana Consonni, University of Milano-Bicocca
* Prof. Roberto Todeschini, University of Milano-Bicocca


See also the list of [contributors](https://github.com/FrancescaGrisoni/whales_descriptors/contributors) who participated in this project.

## Papers using WHALES descriptors <a name="papers"></a>

* Grisoni et al. 2018 "Scaffold hopping from natural products to synthetic mimetics by holistic molecular similarity", *Nature Communications Chemistry* 1, 44. ([link](https://www.nature.com/articles/s42004-018-0043-x))
* Merk et al. 2018 "Scaffold hopping from synthetic RXR modulators by virtual screening and de novo design", *Med. Chem. Commun.*, 9, 1289-1292. ([link](https://pubs.rsc.org/en/content/articlepdf/2018/md/c8md00134k))
* Merk et al. 2018. "De Novo Design of Bioactive Small Molecules by Artificial Intelligence", *Mol. Inf.*, 1700153. ([link](https://onlinelibrary.wiley.com/doi/epdf/10.1002/minf.201700153))
* Merk et al. 2018. "Tuning artificial intelligence on the de novo design of natural-product-inspired retinoid X receptor modulators". *Communications Chemistry*, 1, 1-9 ([link](https://www.nature.com/articles/s42004-018-0068-1)).
* Merk et al. 2018. "Discovery of Novel Molecular Frameworks of Farnesoid X Receptor Modulators by Ensemble Machine Learning." *ChemistryOpen*. 7-14. ([link](https://onlinelibrary.wiley.com/doi/full/10.1002/open.201800156))
* Grisoni et al. 2019. "Design of Natural‐Product‐Inspired Multitarget Ligands by Machine Learning". *ChemMedChem*, 14, 1129-1134. ([link](https://onlinelibrary.wiley.com/doi/abs/10.1002/cmdc.201900097))

(Last update: January 2020)

## License <a name="license"></a>

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.
See the [LICENSE.md](LICENSE.md) file for additional details. 

## How to cite <a name="cite"></a>
If you use this code (or parts thereof), please cite it as:

```
@article{grisoni2018scaffold,
  title={Scaffold hopping from natural products to synthetic mimetics by holistic molecular similarity},
  author={Grisoni, Francesca and Merk, Daniel and Consonni, Viviana and Hiss, Jan A and Tagliabue, Sara Giani and Todeschini, Roberto and Schneider, Gisbert},
  journal={Communications Chemistry},
  volume={1},
  number={1},
  pages={1--9},
  year={2018},
  doi={10.1038/s42004-018-0043-x},
  url={https://doi.org/10.1038/s42004-018-0043-x},
  publisher={Nature Publishing Group}
}
```

