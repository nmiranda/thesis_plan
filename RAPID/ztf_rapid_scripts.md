# `/ztf_rapid/` script contents

## `plasticc-dbis-none.sh`

Run location: `dbis`

Command:
- `make-dataset-plasticc`

Args:
- `/home/miranda/ztf-rapid/data/raw/plasticc_train_metadata.csv.gz`
- `/home/miranda/ztf-rapid/data/raw/plasticc_train_lightcurves.csv.gz`
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_none/test_plasticc_none.npz`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_none/test_plasticc_none.npz`
- `/home/miranda/ztf-rapid/models/test_plasticc_none/test_plasticc_none.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_plasticc_none`

## `plasticc-dbis-over.sh`

Run location: `dbis`

Command:
- `make-dataset-plasticc`

Args:
- `/home/miranda/ztf-rapid/data/raw/plasticc_train_metadata.csv.gz`
- `/home/miranda/ztf-rapid/data/raw/plasticc_train_lightcurves.csv.gz`
- `/home/miranda/ztf-rapid/data/interim/test_plasticc_over/test_plasticc_over.npz`

Command:
- `augment-dataset`

Args:
- `/home/miranda/ztf-rapid/data/interim/test_plasticc_over/test_plasticc_over.npz`
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_over/test_plasticc_over_01.npz`
- `--rand 42`
- `--strategy oversample`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_over/test_plasticc_over_01.npz`
- `/home/miranda/ztf-rapid/models/test_plasticc_over/test_plasticc_over_01.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_plasticc_over`

## `rcf-cesium-fits-dbis.py`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/interim/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv_nozeroes.pkl`

Methods:
- `cesium.featurize.featurize_time_series`

Output:
- `/home/miranda/ztf-rapid/data/interim/rcf_cesium_features_{band}.fits` (multiple)

## `rcf-fats-fits.py`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/interim/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv_nozeroes.pkl`

Defined methods:
- `get_features`

Methods:
- `FATS.Feature.FeatureSpace`

Output:
- `/home/miranda/ztf-rapid/data/interim/rcf_fats_features_{band}.fits` (multiple)

## `rcf-no-zeroes.py`

Run location: `dbis`

Input:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`

Output:
- `/home/miranda/ztf-rapid/data/interim/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv_nozeroes.pkl`

Purpose:

This scripts gets rid of negative fluxes from the input data.

## `test-dbis-none.sh`

Run location: `dbis`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/processed/test_none/test_none.npz`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_none/test_none.npz`
- `/home/miranda/ztf-rapid/models/test_none/test_none.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_none`

## `test-dbis-over.sh`

Run location: `dbis`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test_over`
- `/home/miranda/ztf-rapid/data/interim/test_over/test_over.npz`

Command:
- `augment-dataset`

Args:
- `/home/miranda/ztf-rapid/data/interim/test_over/test_over.npz`
- `/home/miranda/ztf-rapid/data/processed/test_plasticc_over/test_plasticc_over_01.npz`
- `--rand 42`
- `--strategy oversample`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz`
- `/home/miranda/ztf-rapid/models/test_over/test_over_01.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_over`

## `test-dbis.sh`

Run location: `dbis`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test`

Command:
- `augment-dataset`

Args:
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/processed/test_01.npz`
- `--rand {}` (multiple)

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_01.npz`
- `/home/miranda/ztf-rapid/models/test_01.hdf5 /home/miranda/ztf-rapid/reports/figures/test`

## `test-dbis-under.sh`

Run location: `dbis`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test_under`
- `/home/miranda/ztf-rapid/data/interim/test_under/test_under.npz`

Command:
- `augment-dataset`

Args:
- `/home/miranda/ztf-rapid/data/interim/test_under/test_under.npz`
- `/home/miranda/ztf-rapid/data/processed/test_under/test_under_01.npz`
- `--rand 42`
- `--strategy undersample`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_under/test_under_01.npz`
- `/home/miranda/ztf-rapid/models/test_under/test_under_01.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_under`

## `test-noisify-augtest-dbis.sh`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test_noisify`
- `/home/miranda/ztf-rapid/data/interim/test_noisify/test_noisify.npz`
- `--nocv`

Command:
- `noisify`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test_noisify/test_noisify.npz`
- `/home/miranda/ztf-rapid/data/processed/test_noisify_augtest/test_noisify_augtest.npz`
- `--epc 2000`
- `--augtest`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_noisify_augtest/test_noisify_augtest.npz`
- `/home/miranda/ztf-rapid/models/test_noisify_augtest/test_noisify_augtest.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_noisify_augtest`

## `test-noisify-dbis.sh`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test_noisify`
- `/home/miranda/ztf-rapid/data/interim/test_noisify/test_noisify.npz`
- `--nocv`

Command:
- `noisify`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test_noisify/test_noisify.npz`
- `/home/miranda/ztf-rapid/data/processed/test_noisify/test_noisify.npz`
- `--epc 2000`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_noisify/test_noisify.npz`
- `/home/miranda/ztf-rapid/models/test_noisify/test_noisify.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_noisify`

## `test-noisify.sh`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test_noisify`
- `/home/miranda/ztf-rapid/data/interim/test_noisify/test_noisify.npz`
- `--nocv`

Command:
- `noisify`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test_noisify/test_noisify.npz`
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_noisify/test_noisify.npz`
- `--epc 100`

Command:
- `train-model`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_noisify/test_noisify.npz`
- `/home/nmiranda/workspace/ztf_rapid/models/test_noisify/test_noisify.hdf5`
- `/home/nmiranda/workspace/ztf_rapid/reports/figures/test_noisify`

## `test-none.sh`

Command:
- `make-dataset`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test_none`
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_none/test_none.npz`

Command:
- `train-model`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_none/test_none.npz`
- `/home/nmiranda/workspace/ztf_rapid/models/test_none/test_none.hdf5`
- `/home/nmiranda/workspace/ztf_rapid/reports/figures/test_none`

## `test-no-parallel.sh`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/interim/test/test.npz`

Command:
- `augment-dataset`

Args:
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz`
- `--rand 42`
- `--strategy undersample`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz`
- `/home/miranda/ztf-rapid/models/test_over/test_over_01.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_over`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz`
- `/home/miranda/ztf-rapid/models/test_over/test_over_02.hdf5`
- `/home/miranda/ztf-rapid/reports/figures/test_over`

## `test-over-100.sh`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/interim/test/test.npz`

Command:
- `augment-dataset`

Args:
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_{}.npz` (multiple)
- `--rand {}` (multiple)
- `--strategy oversample`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_{}.npz` (multiple)
- `/home/miranda/ztf-rapid/models/test_over/test_over_{}.hdf5` (multiple)
- `/home/miranda/ztf-rapid/reports/figures/test_over`

Note:

This script uses GNU Parallel for parallel processing.

## `test-over.sh`

Command:
- `make-dataset`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test_over`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test_over/test_over.npz`

Command:
- `augment-dataset`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test_over/test_over.npz`
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_over/test_over_01.npz`
- `--rand 42` (multiple)
- `--strategy oversample`

## `test-parallel.sh`

Command:
- `make-dataset`

Args:
- `/home/miranda/ztf-rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/interim/test/test.npz`

Command:
- `augment-dataset`

Args:
- `/home/miranda/ztf-rapid/data/interim/test`
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz`
- `--rand 42` (multiple)
- `--strategy undersample`

Command:
- `train-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_over/test_over_01.npz`
- `/home/miranda/ztf-rapid/models/test_over/test_over_{}.hdf5` (multiple)
- `/home/miranda/ztf-rapid/reports/figures/test_over`

Note:

This script uses GNU Parallel

## `test.sh`

Command:
- `make-dataset`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/raw/rcf_marshallc_sncosmo_200114_2018classupdate_addedcv.pkl`
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test`

Command:
- `augment-dataset`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/interim/test`
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_under/test_under_{}.npz` (multiple)
- `--rand 42`
- `--strategy undersample`

Command:
- `train-model`

Args:
- `/home/nmiranda/workspace/ztf_rapid/data/processed/test_under/test_under_{}.npz` (multiple)
- `/home/nmiranda/workspace/ztf_rapid/models/test_under/test_under_{}.hdf5` (multiple)
- `/home/nmiranda/workspace/ztf_rapid/reports/figures/test`

## `test-tune.sh`

Command:
- `tune-model`

Args:
- `/home/miranda/ztf-rapid/data/processed/test_none/test_none.npz`
- `/home/miranda/ztf-rapid/reports/data`
- `/home/miranda/ztf-rapid/reports/data/test.json`