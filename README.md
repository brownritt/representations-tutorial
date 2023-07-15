# Representations Tutorial

## Content overview

This tutorial covers different ways of representing or transforming multi-channel time series data. Two notable types of methods are **time-frequency transforms** (e.g. Fourier, wavelet) that emphasize temporal structure in the data, and **dimensionality reduction** (e.g. PCA, UMAP) that emphasize spatial (cross-channel) structure over time. Some methods such aa **coherence analysis** combine elements of the above, by first transforming individual channels and then relating parameters of the transforms across channels.

Some of these methods preserve all of the information in the raw data and just represent it in a new form, while most are "lossy"; the trick is to filter out the right non-essential detail, so that whatever is left reveals key components of scientific interest.

The topics covered in this tutorial are very broad, and the treatment is not comprehensive. Instead, the goal is to introduce a number of examples and minimally sufficient code snippets, unified through the concept of representations of signals through linear combinations. Some later tutorials will expand these foundational ideas, and participants may find a subset of the examples to be a useful starting point for their own projects.

The main content is in the Jupyter notebook `eeg_representations.ipynb`. Some introductory discussion is in `eeg_representations_slides.pdf` and some supplemental details about complex exponentials is in `Complex_exponentials.pdf`.

Some of the content appeared originally as part of the Carney Institute Brainstorm EEG Challenge Workshop, August 2022. The workshop included non-public data and information; this repo retains only general (and updated) content on Fourier transforms and similar topics.


## Learning Objectives

At the end of the tutorial, participants will be able to:

- Describe a general approach for transforming data representations using linear combinations, and form useful approximations by dropping terms

- Find Fourier and wavelet transforms of EEG time series data, and convert to power spectra

- Describe limitations to interpreting power spectra, e.g. that high power does not necessarily imply existence of a oscillator, and phase is discarded

- Describe the dual resolution relation `(sample rate, recording duration)<->(Nyquist frequency, frequency resolution)`, in connection to the uncertainty principle

- Improve statistical properties of power spectrum estimates through multitaper methods and background normalization

- Find spectrograms of EEG time series data, and choose trade-offs between window length, window step, and resolution parameters

- Find instantaneous amplitude and frequency using Hilbert analysis of a narrow band signal

- Project multichannel data onto lower dimensional subspaces using principal components analysis, guided by an ordered decomposition of variance


## Setup and Runtime Instructions

First step is to clone the repo using any of the [standard approaches](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).

If one has the [Anaconda](https://www.anaconda.com) python distribution, the easiest way to get the python dependencies is to create a `conda` environment. From within Anaconda Navigator, go to the Environments tab, and use the GUI to create a new environment from the file `environment_representations.yml` (note: this file is "minimal" in that it does not include exact versioning; it will try to install the most recent versions of each of the packages).

Alternatively, from the command line:
```
conda env create -f environment_representations.yml
```

Either way, the environment `representation_tutorial` should be created and contain all the necessary packages. One can then activate the environment from within Navigator, or from the command line
```
conda activate representation_tutorial
```

If one prefers to make virtual environments and install dependencies from `pip`, there is also a `requirements.txt` file, that contains exact package versions but also some additional software (in the original workshop, dependencies were combined across multiple tutorials by different people, and I have not frozen a version specific to my tutorial).

The tutorial consists of a single Jupyter notebook, `eeg_representations.ipynb`, which can be run from within Navigator (be sure to select the correct environment first), or from the command line
```
jupyter notebook
```

There are also two PDFs:
- slides on motivation and backgroun of [time-frequency representations](eeg_representations_slides.pdf)
- an informal handout on the [complex exponential](Complex_exponentials.pdf) version of the Fourier transform
