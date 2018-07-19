# WHALES descriptors

This repository contains all the necessary files to compute Weighted Holistic Atom Localization and Entity Shape (WHALES) descriptors starting from an rdkit supplier file.

For more information regarding the method, have a look at:

Grisoni et al., "Scaffold hopping from natural products to synthetic mimetics by holistic molecular similarity", *Nature Communications Chemistry*, 2018
available at: xxxxx

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

The following prerequisites are needed:

*[Python 2.7*](https://www.python.org/download/releases/2.7/)

*[RDKit](http://www.rdkit.org/docs/Install.html)

*[NumPy](https://scipy.org/install.html)

*[pandas](https://pandas.pydata.org)

It is suggested to run all the calculations within an RDKit environment. 
The environment can be created with conda as follows:
```
conda create -n whales_env python=2.7*
activate whales_env
```
The RDKit repositories can be listed with the following command:
```
anaconda search -t conda rdkit
```
Choose then the best installation according to the platform:
```
conda install -c https://conda.anaconda.org.nickvandewiele rdkit
```

### Installing

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

## Using the package

### Importing molecular files
RDKit suppliers have to be used as the input for WHALES calculation, for instance:

```
from rdkit import Chem # imports package
suppl = Chem.SDMolSupplier(filename) # generates an rdkit supplier file
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

Molecules for which calculation errors were encountered, the descriptor values were set to -999. 

### Export descriptors values as a .txt file

The results can be exported as a plain txt file as follows:

```
import numpy as np
np.savetxt([save_name + '_whales.txt'], res, delimiter=' ', newline='\n') # for descriptors
np.savetxt([save_name + '_labels.txt'], labels, delimiter=' ', newline='\n') # for labels
```


## Authors

* **Francesca Grisoni** (https://github.com/grisoniFr)

Contributors to the WHALES descriptors project:
* Francesca Grisoni, University of Milano-Bicocca & ETH-Zurich
* Prof. Dr. Gisbert Schneider, ETH Zurich, gisbert.schneider@pharma.ethz.ch
* Dr. Viviana Consonni, University of Milano-Bicocca
* Prof. Roberto Todeschini, University of Milano-Bicocca


See also the list of [contributors](https://github.com/FrancescaGrisoni/whales_descriptors/contributors) who participated in this project.

## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.
See the [LICENSE.md](LICENSE.md) file for additional details. 

