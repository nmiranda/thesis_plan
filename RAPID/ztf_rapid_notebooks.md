# `ztf_rapid` notebook content

## `class_balancing_results_with_real_data.ipynb`

It loads serialized data `/home/miranda/ztf-rapid/data/processed/test_none/test_none.npz` and the model `/home/miranda/ztf-rapid/models/test_none/test_none.hdf5`.

It generates a confusion matrix and a clssification report from it.

It loads serialized data `/home/miranda/ztf-rapid/data/processed/test_under/test_under_01.npz` and the model `/home/miranda/ztf-rapid/models/test_under/test_under_01.hdf5`.

It generates a confusion matrix and a clssification report from it.

It loads serialized data `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz` and the model `/home/miranda/ztf-rapid/models/test_over/test_over_01.hdf5`.

It generates a confusion matrix and a clssification report from it.

I think this notebook is loading predictions with regular, undersampled and oversampled models and data, and then displaying the results.

## `classification_noisify.ipynb`

Run location: `localhost`

Input data:

- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test_noisify/test_noisify.npz`

Methods:

- `ztf_rapid.noisify_dataset`
- `ztf_rapid.make_datasets`
- `ztf_rapid.plot_raw_lightcurve`
- `ztf_rapid.plot_processed_lightcurve`

Purpose:

This notebook generates lightcurve plots for a lightcurve and also for its noisified version.

## `conpare_features_fits.ipynb`

Run location: `localhost`

Input data:

- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_cesium_features.fits`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_fats_features_p48r.fits`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_tsfresh_features_p48r.fits`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_tsfresh_features_names_p48r.csv`

Purpose:

This notebook loads fits files with features calculed via frameworks `cesium` and `fats`, displays the list of features calculated, and checks if the common ones (like the standard deviation) have the same values.

## `compare_features_lc.ipynb`

Run location: `localhost`

Input data:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Methods:
- `ztf_rapid.plot_raw_lightcurve`
- `np.std`
- `featurize.featurize_single_ts` from `cesium`
- `FeatureSpace.calculateFeature` from `FATS`
- `extract_features` from tsfresh
- `light_curve.StandardFeviation` from https://github.com/light-curve/light-curve-python

Purpose:

This notebook takes a single lightcurve from the dataset and compares the standard deviation values that different frameworks calculate over it.

## `explore.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Output:
- Lightcurve plot
- `/home/nmiranda/workspace/ztf_rapid/reports/figures/ZTF19aaksrlb_raw.svg`

Purpose:

This notebook plots a single raw lightcurve from the input data set.

## `explore_processed.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_none/test_none.npz`

Methods:
- `ztf_rapid.plot_processed_lightcurve`

Output:
- `/home/nmiranda/workspace/ztf_rapid/reports/figures/ZTF19aaksrlb_processed.svg`

Purpose:

This notebook loads a set of processed (?) lightcurves and plots one of them.

## `exploring_ztf.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Purpose:

This notebook just displays the 5 most common types in the input data set, and one lightcurve's table.

## `hyper_rapid.ipynb`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/processed/test_none/test_none.npz`

Purpose:

This notebook uses the `kerastuner` module to do hyper-parameter optimization of a RAPID model and then prints the optimal hyperparameters.

## `lightcurve_length.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_none/test_none.npz`
- `/home/nmiranda/workspace/ztf_rapid/models/test_none/test_none.hdf5`

Methods:
- `ztf_rapid.get_pred_label` with `time_index=10`
- `ztf_rapid.get_pred_label_peak`
- `ztf_rapid.get_pred_label` with `time_index=-1`
- `ztf_rapid.get_y_true`
- `ztf_rapid.predict`
- `ztf_rapid.plot_confusion_matrix`

Purpose:

This notebook plots a confusion matrix for the classification prediction at three different moments of the lightcurve: `time_index=10`, peak, and `time_index=10`.

## `lightcurve_length_dbis.ipynb`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/processed/test_none/test_none.npz`
- `/home/miranda/ztf-rapid/models/test_none/test_none.hdf5`
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz`
- `/home/miranda/ztf-rapid/models/test_over/test_over_01.hdf5`

Methods:
- `ztf_rapid.get_pred_label` with `time_index=10`
- `ztf_rapid.get_pred_label_peak`
- `ztf_rapid.get_pred_label`
- `ztf_rapid.get_y_true`
- `ztf_rapid.predict`
- `ztf_rapid.plot_confusion_matrix`

Purpose:

I think that overall, this notebook compares prediction results with and without oversampling at different points of the lightcurve time.

## `multiple_models.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_01.npz`
- `/home/nmiranda/workspace/ztf_rapid/models/test_*` (multiple)

Methods:
- `ztf_rapid.predict`
- `ztf_rapid.true_pred_ensemble`
- `ztf_rapid.plot_confusion_matrix`
- `ztf_rapid.plot_confusion_matrix`

Purpose:

This notebook plots a confusion matrix with predicted labels obtained from aggregating classifications from multiple models.

## `multiple_models_dbis.ipynb`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/processed/test_01.npz`
- `/home/miranda/ztf-rapid/models/test_*.hdf5` (multiple)
- `/home/miranda/ztf-rapid/data/processed/test_under/test_under_01.npz`
- `/home/miranda/ztf-rapid/models/test_under/test_under_*` (multiple)
- `/home/miranda/ztf-rapid/data/processed/test_none/test_none.npz`
- `/home/miranda/ztf-rapid/models/test_none/test_none*` (multiple)
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_001.npz`
- `/home/miranda/ztf-rapid/models/test_over/test_over_*.hdf5` (multiple)

Methods:
- `ztf_rapid.predict`
- `ztf_rapid.runs_result_dataframe`
- `ztf_rapid.result_class_distribution`
- `ztf_rapid.true_pred_ensemble`
- `ztf_rapid.plot_confusion_matrix`

Purpose:

This notebook plots confusion matrices obtained by aggregating predictions from multiple models. Some of the true and pred labels are obtained with `ztf_rapid.true_pred_ensemble`. Some others with `ztf_rapid.predict` to each model and then `np.argmax(y_pred[:,-1,:], axis=1)` and `np.argmax(y_true[:,0,:], axis=1)`.

It also does the same with the oversampled data.

## `noisify_explore.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Methods:
- `ztf_rapid.plot_joint_real_noisified`

Purpose:

This notebook plots a magnitude vs magnitude error plot for simulated data with different parameters for noisification.

## `oversampling_100_runs.ipynb`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/processed/test_over_001.npz`
- `/home/miranda/ztf-rapid/models/test_over_100/test_over/test_*.hdf5`

Methods:
- `ztf_rapid.predict`
- `ztf_rapid.runs_result_dataframe`
- `ztf_rapid.result_class_distribution`
- `ztf_rapid.true_pred_ensemble`

Purpose:

This notebook plots a confusion matrix with the aggregated classification of 100 models.

## `oversampling_brightest.ipynb`

Run location: `dbis`

Input: 
- `/home/miranda/ztf-rapid/data/processed/test_over_001.npz`
- `/home/miranda/ztf-rapid/models/test_over_100/test_over/test_over_001.hdf5`
- `/home/miranda/ztf-rapid/models/test_over_100/test_over/test_over_002.hdf5`
- `/home/miranda/ztf-rapid/models/test_over_100/test_over/test_over_003.hdf5`

Methods:
- `ztf_rapid.select_bright_sources`
- `ztf_rapid.predict`
- `ztf_rapid.pred_to_categorical`
- `ztf_rapid.target_to_categorical`
- `ztf_rapid.plot_confusion_matrix`

Purpose:

This notebook seems to be selecting the brightest sources of oversampled data input and then classifying it with some of the models from the multiple 100 run.

## `plasticc_dbis_scores.ipynb`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_none/test_plasticc_none.npz`
- `/home/miranda/ztf-rapid/models/test_plasticc_none/test_plasticc_none.hdf5`
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_over/test_plasticc_over_01.npz`
- `/home/miranda/ztf-rapid/models/test_plasticc_over/test_plasticc_over_01.hdf5`
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_under/test_plasticc_under_01.npz`
- `/home/miranda/ztf-rapid/models/test_plasticc_under/test_plasticc_under_01.hdf5`

Methods:
- `ztf_rapid.predict`
- `ztf_rapid.get_pred_label`
- `ztf_rapid.get_y_true`
- `ztf_rapid.plot_confusion_matrix`

Purpose:

This notebook is plotting confussion matrices for classification with regular data and model, with oversampled data and model, and with undersampled data and model.

## `plot_lc_scores.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_none/test_none.npz`
- `/home/nmiranda/workspace/ztf_rapid/models/test_none/test_none.hdf5`

Methods:
- `ztf_rapid.predict`
- `ztf_rapid.plot_lightcurve_scores`

Purpose:

This notebook plots the classification scores for a lightcurve across time.

## `plot_rcf_lightcurves.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Methods:
- `ztf_rapid.plot_raw_lightcurve`

Ouptut:
- `/home/nmiranda/workspace/ztf_rapid/reports/figures/rcf_lightcurves` (dir)

Purpose:

This notebook saves to a folder the plots of all lightcurves.

## `process_plasticc_data.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/plasticc_train_metadata.csv.gz`
- `/home/nmiranda/workspace/ztf_rapid/data/raw/plasticc_train_lightcurves.csv.gz`

Methods:
- `ztf_rapid.plasticc_make_datasets`

Purpose:

This notebook loads the training PLASTICC challenge data and makes a RAPID dataset from them.

## `rcf_cesium_fits.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Methods:
- `cesium.time_series.TimeSeries`
- `cesium.featurize.featurize`

Output:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_cesium_features.fits`

Purpose:

This notebook calculates the cesium features from the input data set, for every band separately, aggregates the results in a single table, and then writes the table to a FITS table.

## `rcf_cesium_fits_2.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv_nozeroes.pkl`

Methods:
- `cesium.featurize.featurize_time_series`

Purpose:

This notebook calculates the cesium features for some (a single? several? 10?) time series.

## `rcf_fats_fits.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Methods:
- `FATS.Feature.FeatureSpace`
- `ztf_rapid.get_mag`
- `ztf_rapid.get_mag_err`
- `ztf_rapid.generate_fits_features_band`

Output:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_fats_features.fits`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_fats_features_p48r.fits`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_fats_features_p48g.fits`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_fats_features_p48i.fits`

Purpose:

This notebook calculates FATS features over input data and saves the results to a fits file.

## `rcf_no_zeroes.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Output:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv_nozeroes.pkl`

Purpose:

This notebook eliminates all of the negative fluxes from the data set and saves the result in a new dataset.

## `rcf_to_supernnova_pretrained.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/nmiranda/workspace/SuperNNova/Predictions_rcf_supernnova.csv`

Output:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/rcf_supernnova.csv`

Purpose:

This notebook seems to be reading the data set, transforming it into a format that SuperNNova understands, loading SuperNNova predictions over this dataset, and then displaying some results. The SuperNNova predictions seem to have been done with a pre-trained model.

## `rcf_to_supernnova_train.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Purpose:

This notebook seems incomplete. Apparently, this notebook's purpose was to train a SuperNNova model with the ZTF input data.

## `rcf_tsfresh_fits-dbis`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Defined methods:
- `to_timeseries`
- `lc_data_to_pandas_ts`
- `drop_single_value_columns`
- `extract_tsfresh_features`
- `features_to_fits`

Output:
- `/home/miranda/ztf-rapid/data/interim/rcf_tsfresh_features_{band}.fits'`
- `/home/miranda/ztf-rapid/data/interim/rcf_tsfresh_features_names_{band}.csv`

Purpose:

This notebook extracts features from input data and generates fits files with values in tables.

## `rcf_tsfresh_fits.ipynb`

Run location: `localhost`

Purpose:

See `rcf_tsfresh_fits.ipynb`.

## `snguess_to_fits.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/snguess_features.csv`

Output:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/snguess_features.fits`

Purpose:

This notebook reads an input file with features from SNGuess and saves them in a fits file table.

## `testnoisify_results.ipynb`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/processed/test_noisify/test_noisify.npz`
- `/home/miranda/ztf-rapid/models/test_noisify/test_noisify.hdf5`
- `/home/miranda/ztf-rapid/data/interim/test_noisify/test_noisify.npz`
- `/home/miranda/ztf-rapid/data/processed/test_noisify_augtest/test_noisify_augtest.npz`
- `/home/miranda/ztf-rapid/models/test_noisify_augtest/test_noisify_augtest.hdf5`

Methods:
- `ztf_rapid.predict`
- `ztf_rapid.get_pred_label`
- `ztf_rapid.get_y_true`
- `ztf_rapid.plot_confusion_matrix`

Purpose:

This notebook plots confusion matrices with the results of classification over what seem to be data sets augmented by adding noise.

## `untitled.ipynb`

Run location: `localhost`

Input:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_01.npz`
- `/home/nmiranda/workspace/ztf_rapid/models/test_*.hdf5` (multiple)
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_under/test_under_01.npz`
- `/home/nmiranda/workspace/ztf_rapid/models/test_under/test_under_*` (multiple)

Methods:
- `ztf_rapid.predict`
- `ztf_rapid.true_pred_ensemble`
- `ztf_rapid.plot_confusion_matrix`
- `sklearn.preprocessing.MinMaxScaler`

Purpose:

This notebook plots confusion matrices for aggregated classification with what seem to be regular data and models (`test_*`), and then the same but with undersampled data sets. It also plays around with `MinMaxScaler`.

