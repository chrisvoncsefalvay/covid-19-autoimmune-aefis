# Autoimmune adverse effects following COVID-19 vaccination: a reporting disproportionality analysis

### Pymatch hack

You will need to manually hack `Matcher.py`, substituting the `_scores_to_accuracy` static method with the following:

```python
    @staticmethod
    def _scores_to_accuracy(m, X, y):
        preds = [1.0 if i >= .5 else 0.0 for i in m.predict(X)]
        return (y.to_numpy().T == preds).sum() * 1.0 / len(y)
```

This is a [known bug](https://github.com/benmiroglio/pymatch/pull/43) with pymatch.