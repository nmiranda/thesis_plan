# snmachine 2016

## Data types

"To test and compare methods, we use existing supernova
simulations from the Supernova Photometric Classification
Challenge (SPCC; Kessler et al. 2010a, 2010b), which are
simulated DES light curves built from an existing library of
non-Ia templates and using both SALT2 (Guy et al. 2007) and
MLCS2k2 (Jha et al. 2007) type Ia models."

# snmachine 2022

## Photometric classification approaches:
- parametric fits
- template fits
- machine learning models:
    - neural networks
    - boosted decision trees
    - support vector machines
    - gradient boosting
    
## Test set representativeness

Usually test sets are biased towards lower redshifts.

Work done towards overcoming this lack of representativeness:
- Revsbech et al.2017; 
- Boone 2019; 
- Muthukrishna et al. 2019; 
- Pasquet et al. 2019; 
- Carrick et al. 2021
 
 ## Observing strategies

 They consider:
 - Season length
 - survey footprint
 - single-visit exposure time
 - inter-night gaps
 - cadence of repeat visits in different passbands

## Data types

 "In this work we provide observing
strategy recommendations to improve photometric classification
of SNe in particular, so we restrict ourselves to the PLAsTiCC
classes SN Ia, SN Ibc, and SN II; Table 1 shows a breakdown of
the numbers of SNe in each class."

## Data pipeline

1. season selection
2. 2D gaussian process fit
3. wavelet decomposition
4. PCA dimension reduction of wavelet space

Note: they use redshift and uncertainty as features for classification.

## Classification

LightGBM model, boosting decision tree.

5-fold cross validated grid. one-dimensional grid search and then multi-dimensional grid search.

Metric: PLASTICC log-loss

## Augmentation

