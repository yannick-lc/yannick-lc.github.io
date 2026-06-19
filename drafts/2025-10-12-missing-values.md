# Todo: find title

Classic problem: missing values in dataset.

What to do?
- Discard? May discard too much and miss important patterns
- Replace then. E.g. with average: but maybe inaccurate. May bias model.
More precise: predict! E.g. linear regression.

1 missing: fine, build one model.
2 missings: 2 models then. But sometimes, 1 input variable missing. May actually need 4 models.
3 missings: getting annoying. 3 predictors, 3 sets of variables per model -> 9 models.

[Maybe insert chart?]

You see where this is going.

How about one model that handles everything for us?

