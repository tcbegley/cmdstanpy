# CmdStanPy

[![codecov](https://codecov.io/gh/stan-dev/cmdstanpy/branch/master/graph/badge.svg)](https://codecov.io/gh/stan-dev/cmdstanpy)


CmdStanPy is a lightweight pure-Python interface to CmdStan which provides access to the Stan compiler and all inference algorithms.  It supports both development and production workflows. Because model development and testing may require many iterations, the defaults favor development mode and therefore output files are stored on a temporary filesystem. Non-default options allow all aspects of a run to be specified so that scripts can be used to distributed analysis jobs across nodes and machines.

CmdStanPy is distributed via PyPi: https://pypi.org/project/cmdstanpy/

### Goals

- Runs all CmdStan methods.

- Clean interface to CmdStan; can run with any version above 2.19, keeps up with new releases.

- Easy to install,
  + minimal Python library dependencies: numpy, pandas
  + Python code doesn't interface directly with C++; calls CmdStan executables via subprocess module.

- Low memory overhead - by default, minimal memory used above that required by CmdStanPy; objects run CmdStan programs and track CmdStan input and output files.

- Modular - CmdStanPy does inference; other packages do analysis and visualization.


### Source Repository

CmdStanPy and CmdStan are available from GitHub: https://github.com/stan-dev/cmdstanpy and https://github.com/stan-dev/cmdstan


### Docs

The latest release documentation is hosted on  https://mc-stan.org/cmdstanpy, older release versions are available from readthedocs:  https://cmdstanpy.readthedocs.io

### Licensing

The CmdStanPy, CmdStan, and the core Stan C++ code are licensed under new BSD.

### Example

::

    import os
    from cmdstanpy import cmdstan_path, CmdStanModel

    # specify locations of Stan program file and data
    bernoulli_stan = os.path.join(cmdstan_path(), 'examples', 'bernoulli', 'bernoulli.stan')
    bernoulli_data = os.path.join(cmdstan_path(), 'examples', 'bernoulli', 'bernoulli.data.json')

    # instantiate a model; compiles the Stan program by default
    bernoulli_model = CmdStanModel(stan_file=bernoulli_stan)

    # obtain a posterior sample from the model conditioned on the data
    bernoulli_fit = bernoulli_model.sample(chains=4, data=bernoulli_data)

    # summarize the results (wraps CmdStan `bin/stansummary`):
    bernoulli_fit.summary()
