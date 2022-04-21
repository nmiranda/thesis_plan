# Additional Experiments for SNGuess

We have submitted an article with a description of our model, SNGuess, and we have recently received comments from a referee.

SNGuess consists of a gradient boost tree classifier model that receives as an input a combination of simple photometric time series (light curve) features and photometric detection alert metadata.

One of the most relevant features in SNGuess classification results is the distance to a known galaxy. The question is then, does SNGuess really perform better than a simpler model that only uses this value to predict the likelyhood of a candidate being a supernova?

On the same note, if the weighing of candidates is dominated by the distance to nearest object, does this bias the selection of SNGuess towards a particular SN type? This considering that SNe from unusual types tend to appear around diffuse galaxies that are not in any previous catalogue.

One may also want to apply SNGuess, with a different set of features, to other data sets such as PLASTICC or ELASTICC.

## Docstrings

```python
# Load training data
training_data = pd.read_csv('snguess_features_class.csv')

# Perform cuts to training data
training_data = data_cuts(training_data)

# Load test data features
test_data_features = pd.read_csv('snguess_hu_tns_msip.csv')

# Load test data labels
bts_transients = pd.read_csv('bts_transients.csv')

# Merge test data features and labels
test_data = merge_test_features_labels(test_data_features, bts_transients)

# Extract 
X_train = 
y_train = 
X_test = 
Y_test = 

# Fit LogReg model to training data set
logreg = LogisticRegression()
logreg.fit(X_train, y_train)

# Predict over test data set
y_pred = logreg.predict(X_test)
print('Accuracy of logistic regression classifier on test set: {:.2f}'.format(logreg.score(X_test, y_test)))

# Plot ROC curve
plot_roc_curve(y_test, logreg)


```