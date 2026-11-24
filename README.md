# econ5200-lab16-regularization

# Regularization: Selection, Shrinkage and Valid Intervals

## Objective
I studied how LASSO behaves when it is used to choose control variables, and whether the confidence intervals that follow actually cover the true treatment effect.

## Methodology
- Simulated data with a true treatment effect of 1.0 and 100 candidate control variables.
- Ran the usual two-step procedure: LASSO selects the controls, then OLS on the selected controls gives the treatment estimate and a 95% interval.
- Repeated this over 200 simulated samples and recorded how often the interval contained 1.0.
- Wrote double selection (Belloni, Chernozhukov and Hansen 2014) myself. It keeps controls that predict the outcome and also controls that predict the treatment. I ran it on the same 200 samples and recorded coverage and the average number of controls kept.
- Compared the LASSO coefficients with the known true coefficients to measure shrinkage, then refit OLS on the selected variables (post-LASSO OLS) to see whether coefficient sizes recovered.
- Wrote my own cross-validation loop over the penalty, looping over the folds by hand and fitting the scaler inside each fold so no information leaks from the held-out data. I checked it against GridSearchCV.

## Key Findings
- **Standard LASSO then OLS:** the nominal 95% interval covered the true effect in 95% of 200 samples.
- **Double selection:** coverage was 88.5%, with 26.5 controls kept on average.
- **Shrinkage:** the mean shrinkage of the LASSO coefficients was 4.6%. Post-LASSO OLS brought the coefficient sizes back.
- **Cross-validation:** my loop matched GridSearchCV, with lambda = 0.0501 and CV MSE = 1.0173.
