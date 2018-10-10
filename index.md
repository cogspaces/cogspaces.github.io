---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
---

The cogspace package allows to reproduce and reuse the multi-study task functional MRI decoding models presented in this [NIPS 2017 paper](http://papers.nips.cc/paper/7170-learning-neural-representations-of-human-cognition-across-many-fmri-studies) and this follow-up [preprint paper](https://arxiv.org/abs/1809.06035).

# Software

## Install

```bash
git clone github.com/arthurmensch/cogspaces
cd cogspaces
pip install -r requirements.txt
python setup.py install
```

## Using the multi-study models


# Provided data

We provide resting-state dictionaries for reducing statistical maps (the first layer of the model), as well as the reduced representation of the input statistical maps, and fetchers for the full statistical maps.

## Resting-state dictionaries

The dictionaries extracted from HCP900 resting-state data can be download running

```python
    from cogspaces.datasets import fetch_dictionaries

    dictionaries = fetch_dictionaries()
    # dictionaries = {'components_64': ...}
```

They may also be downloaded manually 
- [64-components dictionary covering the whole brain](assets/data/modl/components_64.nii.gz)
- [128-components dictionary covering the whole brain](assets/data/modl/components_128.nii.gz)
- [453-components dictionary covering the grey-matter](assets/data/modl/components_453_gm.nii.gz)
- [128-components dictionary loadings over the 453-components dictionary](assets/data/modl/loadings_128_gm.npy)

## Reduced representation of the 35 studies

The loadings of the z-statistic maps over the 453-components dictionary can be loaded running

```python
    from cogspaces.datasets import load_reduced_loadings

    Xs, ys = load_reduced_loadings()
    print(Xs)
    # {'archi': np.array(...), 'hcp': np.array(...)}
    print(ys)
    # {'archi': pd.DataFrame}, ...)
    print(ys['archi'].columns)
    # ['study', 'subject', 'task', 'contrast']
```

The full statistical maps are available on Neurovault, and may be downloaded using

```python
    from cogspaces.datasets import fetch_contrasts

    df = fetch_contrasts('archi')
    print(df.columns)
    # ['z_map', 'study', 'subject', 'task', 'contrast']
    df = fetch_contrasts('all')
```





## Publications

If the model or data proved useful to you, please consider to cite the following papers

- Mensch, A., Mairal, J., Bzdok, D., Thirion, B., & Varoquaux, G. (2017).
Learning Neural Representations of Human Cognition across Many fMRI Studies.
In Advances in Neural Information Processing Systems (pp. 5883-5893).

- Mensch, A., Mairal, J., Thirion, B., & Varoquaux, G. (2018). 
Extracting Universal Representations of Cognition across Brain-Imaging Studies.
arXiv: 1809.06035