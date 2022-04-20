# (Label) Data Source Curation for Supervised Photometric Classification

<!-- This topic would be more focused on developing a solution (an architecture and API) rather than testing a scientific hypothesis.

The idea is that several ML models have been proposed in the community for  -->

Several machine learning models have been proposed and are in use in the community for supervised photometric classification. They all differ in several aspects, such as:

- The contents of the data they need as an input (e.g. features, raw data);
- The temporal quality of the data they use (static, dynamic);
- The number of classes in their classification (binary, multi-class);
- The goal of their scientific use case (e.g. SNe Ia vs. other SNe, transients vs. other variables)

Having this in mind, it would be highly desirable to have a system (architecture + API) where one is able to easily perform certain basic tasks, such as:

- Have a catalogue of existing sources of labeled data;
- Query across all the available data sources for labels:
    - assigned to certain objects;
    - assigned during a certain time window;
    - from a specific type of data source;

Furthermore, one would use this system to define certain strategies for integrating labels from different sources. These strategies can then be used to implement automatic decision-making routines (in the form of triggers, callbacks or hooks), or to train further classification models.

For instance, let's this use case:

> For each transient in the data set, obtain a label with a supernovae sub-type (to use as target for training) if available, following the following strategy:
> * If there is a label from a data source where visual inspection by an expert has taken place, consider that one as the final type. Otherwise,
> * It there is a label from a data source where spectrography of candidates has taken place, consider that one as the final type. Otherwise,
> * If there is a machine learning model that has already classified this candidate with a confidence of more than 80%, consider that one as the final type. Otherwise,
> * Return no label.
>
> And in if any of the previous steps there is more than one label source that fits the condition, take as label the type in which the majority agrees upon.

One could then imagine other cases where, for instance, one manually assigns weights (or other quantifiers of priority) to certain label data sources, or more complicated cases where these weights are lefts as parameters for automatically optimizing for the best strategy.

## Docstrings

One could imagine a use case where one wants to add a spectrograph data archive as a new label data source:
```
# Add a spectrograph data archive as a new label data source.
>>> manager.register_datasource(
        name='spectrograph01',
        endpoint='https://spectrograph01/query?',
        type='spectrograph'
        )
New label data source 'spectrograph01' registered.
```

Or maybe use the classification results of a machine learning model already running in a broker as a label data source:
```
# Add machine learning model classification results as a new label data source.
>>> manager.register_datasource(
        name='randomforest01',
        endpoint='https://broker01/randomforest/query?',
        type='ml'
        )
New label data source 'randomforest01' registered.
```

Of course the above might be done programatically in a better way by implementing an interface or inheriting from a base class.

Then one could imagine querying across all available data sources according to different requirements:

```
>>> # Get all labels for SNe Ia from all sources
... manager.get_labels(label_type='SN', label_subtype='Ia')
[Label1,
Label2,
Label3,
...
Label100]
>>> # Get all labels from all sources for a particular object
... manager.get_labels(candidate_id='ZTF00001')
[Label1,
Label2,
Label3]
>>> # Get all labels from all spectrographs assigned between two dates
... manager.get_labels(
...     source_type='spectrograph',
...     start_date='01.01.2022',
...     end_date='31.12.2022)
[Label1,
Label2,
Label3,
...
Label100]
```

Finally, one could use this API to programatically define a strategy for selecting a label:

```python
def example_strategy(manager: LabelSourceManager, candidate_id: list[str]) -> Label:

    # Get consensus for labels from visual inspection data sources
    visual_inspection_labels = manager.get_labels(
        candidate_id=candidate_id,
        source_type='visual_inspection'
    )
    for label in visual_inspection:
        if (consensus := visual_inspection_labels.get_consensus(min_num=2)):
            return consensus

    # Get consensus for labels from spectrographic data sources
    spectrograph_labels = manager.get_labels(
        candidate_id=candidate_id,
        source_type='spectrograph'
    )
    for label in spectrograph_labels:
        if (consensus := spectrograph_labels.get_consensus(min_num=3)):
            return consensus

    # Get consensus for labels from machine learning data sources
    ml_labels = manager.get_labels(
        candidate_id=candidate_id,
        source_type='machine_learning',
        min_confidence='0.8'
    )
    for label in ml_labels:
        if (consensus := ml_labels.get_consensus(min_num=4)):
            return consensus

    # If there is no consensus in all off the above, return None
    return None

```
