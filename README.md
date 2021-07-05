# A case-control study of autoimmune AEFIs following COVID-19 vaccination reported to VAERS: supplementary materials

Data and companion notebooks for the paper _A case-control study of autoimmune AEFIs following COVID-19 vaccination reported to VAERS_ by Chris von Csefalvay (fc.).

## Contents

### Supplementary S1: Reporting odds ratios and counts of autoimmune AEFIs

`supplementary/odds_ratios.csv` contains a CSV summary of RORs of autoimmune AEFIs, as well as case counts. 

The columns `a`, `b`, `c` and `d` form the row-wise contingency table for a given side effect, corresponding to the 
commonly used labelling of such contingency tables (`a` and `c` are exposed, `a` and `b` are symptomatic).

### Notebook

The notebook is under `src/A case-control study of autoimmune AEFIs following COVID-19 vaccination reported to VAERS.ipynb`.

## Running the code

### Environment setup

You will need to set up a Python environment running Python 3.8. 
The package requirements are in `src/requirements.txt` – install them using `pip install -r src/requirements.txt`.

### Pymatch hack

You will need to manually hack `Matcher.py`, substituting the `_scores_to_accuracy` static method with the following:

```python
    @staticmethod
    def _scores_to_accuracy(m, X, y):
        preds = [1.0 if i >= .5 else 0.0 for i in m.predict(X)]
        return (y.to_numpy().T == preds).sum() * 1.0 / len(y)
```

This is a [known bug](https://github.com/benmiroglio/pymatch/pull/43) with pymatch.

### Source data

The analysis is based on source data from VAERS from 1995 to 2021, with the 2021 cut-off date of 2 July, 2021.
You can obtain this data set [here](https://vaers.hhs.gov/data/datasets.html?). 
If you do not use the same data set, your results may slightly diverge.
Extract the summmary ZIP file, and copy all tables beginning with `1995` or above into the `data/` folder.

### Running the analysis

Simply run the analysis notebook to perform the analysis. Note that this may take some time – running the matching process can take up to an hour on a relatively new computer, too.

## Citing this resource

Ideally, you should be citing the paper (see above), but if you wish to cite to this specific repo, use the Zenodo DOI.