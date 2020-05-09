# LGNpy

![Build Status](https://travis-ci.org/ostwalprasad/lgnpy.svg?branch=master) ![PyPI - License](https://img.shields.io/pypi/l/lgnpy) ![PyPI - Python Version](https://img.shields.io/pypi/pyversions/lgnpy) [![Documentation Status](https://readthedocs.org/projects/lgnpy/badge/?version=latest)](https://lgnpy.readthedocs.io/en/latest/?badge=latest)

## Representation, Learning and Inference for Linear Gaussian Networks

Features-
1. Network Representation
2. Parameter Learning through Pandas dataframe
3. Network related EDA
4. Inference with Evidence

### Installation

_______

```bash
$ pip install lgnpy
```

or clone the repository.

```bash
$ pip install https://github.com/ostwalprasad/lgnpy
```



### References:

___

[Probabilistic Graphical Models - Principles and Techniques ](https://mitpress.mit.edu/books/probabilistic-graphical-models), Daphne Koller, Chapter 7.2

[Gaussian Bayesian Networks](https://cedar.buffalo.edu/~srihari/CSE674/Chap7/7.2-GaussBNs.pdf), Sargur Srihari



### Getting Started

________

#### 	1. Create Network

<img src="docs/images/network.png" width="200" >

```python
import pandas as pd
imoprt numpy as np
from lgnpy import LinearGaussian

lg = LinearGaussian()
lg.set_edges_from([('A', 'D'), ('B', 'D'), ('D', 'E'), ('C', 'E')])
```

####	2 Create Data and assign to it to network.

​	Create synthetic data for network using pandas and bind network with the data. There's no need to separately calculate means and covariance matrix.

```python
np.random.seed(42)
n=100
data = pd.DataFrame(columns=['A','B','C','D','E'])
data['A'] = np.random.normal(5,2,n)
data['B'] = np.random.normal(10,2,n)
data['D'] = 2*data['A'] + 3*data['B'] + np.random.normal(0,2,n)
data['C'] = np.random.normal(-5,2,n)
data['E'] = 3*data['C'] + 3*data['D'] + np.rando	m.normal(0,2,n)

lg.set_data(data)
```

####	3. Set Evidence(s)

 Evidence are optional and can be set before running inference.

```
 lg.set_evidences({'A':5,'B':10})
```

####	4. Run Inference 

For each node, CPT (Conditional Probability Distribution) is defined as::<br/>

<img src="docs/images/cpd.png" align="left" width="210" ><br/>

where, it's parameters  are calculated using conditional distribution of parent(s) and nodes: <br/>

<img src="docs/images/betas.png" align="left" width="180" > <br/><br/>

`run_inference()` returns means and variances of each nodes.<br/>



   ```
lg.run_inference(debug=False)
   ```

   



