## A Follow-up (or slight alternative) to STACCATO

STACCATO (Revsbech et al., 2018) basically proceeds by 6 steps:

1. Fits the light curves by using Gaussian processes;
2. Computes a propensity score for all light curves in the training set and forms groups by quintiles of this score;
3. Augments the light curves of each group by selecting light curves from other groups or by re-sampling from the GP within the group;
4. Time-aligns and normalizes the light curve;
5. Computes features for the light curves (diffusion maps with Nystrom extension);
6. Classifying in each training group using a separate random forest classifier.

The idea of a follow-up to this would be to replace the Gaussian process augmentation with augmentation via noisification (or k-corrections), and the diffusion map features with either the same features we used for SNGuess, or with performing “feature-less” classification with a tool like RAPID. 

The STACCATO source code is in the R programming language, so all of the steps would have to be re-implemented. The steps would then be the following:

1. Compute a propensity score for all light curves and partition them in groups according to quintiles of this score;
2. Augment the light curves using the noisification (or k-corrections) approach;
3. And then classify within each partition according one of two alternatives:
    - Use “featureless” deep learning classifier like RAPID, or
    - Calculate SNGuess features and apply a random forests/ boosted trees classifier.

Afterwards, we would compare our results of classifying within each quintile with the ones obtained by STACCATO.

Even if our results are worse than the ones obtained by STACCATO, we could argue that our method requires less pre-processing and that it does not require a validation procedure for the augmentation phase.

Some caveats I see to this approach:

1. I’m not sure whether augmentation by noisification (or k-correction), would be enough to give more coverage in ranges of the relevant feature space. For instance, Figures 12 and 13 talk in terms of coverage of redshift vs. brightness. Would noisification (or k-corrections) give us a less-biased data set for these two variables (features)?
2. There are some aspects of the general procedure of STACCATO that are still not clear for me. For instance, why do the partitions in Figure 13 seem to have different boundaries in the redshift vs brightness plot?
3. Even if at this point I understand the general steps of STACCATO, I still may have to get deeper (study carefully, time(!!)) into some of the things they do (some of them we will not do), in order to have a valid ground for comparison and to re-implement for our case if necessary. This includes the calculation of the propensity score, their diffusion maps procedure (they optimize the parameters via cross-validation), light curve normalization (flux standardization, time zero estimation).
4. There is a follow-up of STACCATO called StratLearn (Autenrieth et al., 2021). The paper contains hard statistics concepts, and I have not yet studied it carefully. However, it seems that they do not rely on augmentation nor in a validation set (?) for pre-processing. This may invalidate the point mentioned before about a possible advantage of our alternative method in the case we don’t generate a better classification.

### Docstrings 

Here are some of the methods we would need to implement for this project:

<!-- ```python
def propensity_score(light_curve: LightCurve) -> float:
    """Returns a propensity score 
    """
``` -->

<!-- ```python
def split_propensity_quintiles(light_curves: list[LightCurve]) -> Tuple[list[LightCurve],...]:
    """Returns the input light curve data set (a list) split into five different quintiles (lists) according to propensity score.

    :param light_curves: The input data set. A list of light curves
    
    :return: A tuple of 5 lists (data sets). The input data set split into 5 data sets according to propensity score quintiles.
    """
``` -->

<!-- ```python
def calculate_snguess_features(light_curves: list[LightCurve]) -> DataFrame:
    """Calculate SNGuess features for a list of light curves.

    :param light_curves: A data set of light curves

    :return: A table with the features.
``` -->
...
```python
class PropensityScoreModel(Object):
    """This is a class that stores a state of logistic regresion for propensity score calculation for further use.
    """
```
...
```python
    def fit(self, training_data: list[LightCurve], test_data: list[LightCurve], covariates: list[str]):
        """Calculates the parameters of the logistic regression for propensity score calculation.

        :param data: Training light curve data set.
        :param data: Test light curve data set.
        :param covatiates: A list of the names of the features to use as covariates for propensity score calculation.
        """
```
...
```python
    def split_propensity_quintiles(self, light_curves: list[LightCurve]) -> Tuple[list[LightCurve],...]:
        """Returns the input light curve data set (a list) split into five different quintiles (lists) according to propensity score.

        :param light_curves: The input data set. A list of light curves
        
        :return: A tuple of 5 lists (data sets). The input data set split into 5 data sets according to propensity score quintiles.
        """
```
...
```python
class NoisificationModel(object):
    """Saves a state of the Noisification model for further application to light curve data sets.

    :param level: Level of noisification.
    """
```
...
```python
    def fit_and_augment(self, light_curves: list[LightCurve], num_lc: int) -> list[LightCurve]:
        """Randomly selects light curves from the input list and generates an augmented synthetic light curve data set  of by noisification from them.

        :param light_curves: List of real light curves to uses as basis for augmentation
        :param num_lc: Number of synthetic light curves to generate as an output

        :return: A list of synthetic lightcurves.
```

These methods would be used as follows (SNGuess-like features case):

```
# Calculate the features for the whole light curve data set.

>>> features = calculate_snguess_features(light_curves)

# Split feature dataframe in training and testing

...

# Fit the propensity score over features

>>> prop_score_model = PropensityScoreModel()
>>> prop_score_model.fit(features_training, features_test, covariates)

# Split the training and testing data sets in quintiles
>>> train_quints = prop_score_model.split_propensity_quintiles(features_training)
>>> test_quints = prop_score_model.split_propensity_quintiles(features_training)

# Augment the quintiles with less light curves by noisification

...

>>> noise_model = NoisificationModel()
>>> quints_aug[0] = noise_model.fit_and_augment(test_quints[0], len(train_quints[0]))

...

# Train the classification model over the augmented training data quintiles and evaluate over corresponding testing data quintiles

...

# Display or plot results

...

```