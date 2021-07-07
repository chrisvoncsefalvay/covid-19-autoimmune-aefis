# A case-control study of autoimmune AEFIs following COVID-19 vaccination reported to VAERS: supplementary materials

[![DOI](https://zenodo.org/badge/382702502.svg)](https://zenodo.org/badge/latestdoi/382702502)

Data and companion notebooks for the paper [_A case-control study of autoimmune AEFIs following COVID-19 vaccination reported to VAERS_ by Chris von Csefalvay](https://www.medrxiv.org/content/10.1101/2021.07.06.21260074).

If you intend to report on this paper, please scroll down for a **media summary**.

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

## Media summary

### What is this research about?

This research looks at adverse effects following immunisation ('side effects') reported over the years. Specifically, it looks at a class of adverse events called 'autoimmune disorders', which comprises disorders like lupus (SLE), rheumatoid arthritis or Crohn's disease that involves the body's own immune system attacking its own cells.

### Why is this research important?

Because autoimmunity is a significant concern for people opting against the COVID-19 vaccine. Autoimmune disorders are painful, enduring and may be devastating to a person's earning potential. In some rare cases, some autoimmune disorders can be serious or fatal.

### What does this research show?

The findings show that **there are no unknown autoimmune safety signals with the COVID-19 vaccine**. A 'safety signal' means an event that is associated (see below for what that specifically means!) with the COVID-19 vaccine. We consider a symptom a potential safety signal if it has a Reporting Odds Ratio of 2 or above. This means that if a person reports a symptom, it is only a safety signal if it is twice as likely that they received a COVID-19 vaccine than a non-COVID-19 vaccine. Note that this does not mean a causal relationship. Studies of this kind do not prove causality, they only help us identify possible issues that can then be looked at in more detail using other methods.

This research has found three symptoms to have potential safety signals: psoriasis, myasthenia gravis and autoimmune thrombocytopaenia.

The association with psoriasis and myasthenia gravis was relatively weak. The increased frequency of these conditions is explained by the fact that largely affect people who have been prioritised for vaccinations (mainly older people and people with certain other illnesses ('comorbidities') such as various cancers). These factors make people more liable to developing psoriasis and myasthenia gravis. For this reason, despite the safety signal, there appears to be no cause for concern.

The Reporting Odds Ratio for autoimmune thrombocytopaenia was higher. In autoimmune thrombocytopaenia, patients develop antibodies against platelets, a type of blood cell important for coagulation (clotting). This may result in haemorrhages (bleeding), usually relatively harmless (such as bruises or pinprick bleeds) but in some cases quite severe, such as strokes and gastrointestinal bleeds. This is a known side effect: a number of papers have reported cases of autoimmune thrombocytopaenia following the COVID-19 vaccine. This is sometimes referred to as 'vaccine induced prothrombotic immune thrombocytopenia' or 'VIPIT'. Scientists are working to understand why this happens. **The higher Reporting Odds Ratio does not mean this is a particularly high risk – compared to the number of vaccines given, the risk of VIPIT is very, very, very low. Rather, the higher Reporting Odds Ratio means that this is a side effect that is more unique to the COVID-19 vaccine. This research does NOT support abstaining from the vaccine because of the risk of VIPIT if other clinical indications would support vaccination.**

Altogether, this research shows that there are **no unexpected autoimmune safety signals** with the COVID-19 vaccine, and people who are concerned about autoimmunity can be reassured that the vaccine is **safe**.

### How was the research conducted?

This is a case-control study. We looked at all the reports received by VAERS between 01 January 1995 and 02 July 2021 in respect of any vaccine administered in the United States. "Cases" were people who reported an autoimmune disease (as defined by a list of diagnoses). To each case, we matched a number of "controls". We then calculated, for each condition, the likelihood that a patient presenting with that condition would have received a COVID-19 vaccine rather than a non-COVID-19 vaccine. 

Controls were matched by age group and by reported gender (M, F, Unknown/unspecified/other). This reduces the confounding of these factors somewhat, but cannot completely eliminate higher-order effects (effects that 'follow on', e.g. higher age increases the likelihood of certain conditions). People in worse physical health, people who are older and people who had certain other health conditions (comorbidities) were prioritised for the COVID-19 vaccine. Because these factors are not reported in a structured way, we cannot control for them.

### What are the limitations of the research?

This research was conducted based on approx. 7 months' worth of COVID-19 vaccination data. There is a risk that certain adverse events may not show up in such a short time.

This research also used VAERS as a data source. VAERS is what is called a 'passive surveillance system': users have to volunteer information about their adverse effects. The Emergency Use Authorizations of the COVID-19 vaccines have made it mandatory to report certain severe adverse effects, but even so, not all adverse reactions may be reported. Severe adverse effects may be more likely to be reported than mild adverse effects. Public perceptions of a certain vaccine may influence reporting. Lay reporters may not label their symptoms accurately.

Data from VAERS must be analysed appropriately. In particular, percentages that are displayed on the VAERS site are fractions of all reports, not of all administered vaccines (a difference of several orders of magnitude for the COVID-19 vaccine).

## Citing this research

Please cite this paper as:

```
von Csefalvay, C. (2021). A case-control study of autoimmune AEFIs following COVID-19 vaccination reported to VAERS. medRxiv, doi:10.1101/2021.07.06.21260074.
```
