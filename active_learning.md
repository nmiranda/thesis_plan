# Active Learning with Multiple Label Sources

Active learning is a concept that has increasingly been explored in recent years, in the context of supervised machine learning models over photometric astronomical data (Ishida et al., 2019; Kennamer et al., 2020, Leoni et al. 2021). 

The literature already shows interesting experimental results with different label query strategies based on previous classifications of the machine learning model (Ishida et al., 2019, Leoni et al. 2021). There are also studies that take into account the limited budget of spectrographic telescopes for retrieving accurate labels for certain objects (Kennamer et al., 2020).

However, to our knowledge, there have been no efforts to design and implement a software architecture that will allow to not only define and execute strategies for active learning, but also integrate different sources for labels into a single unified model.

The objective of this project is to design such an architecture and implement a software system according to it. Furthermore, we will execute experiments to test different active learning strategies with multiple label sources, and compare the results with those that would be obtained with basic single-source strategies.

Some questions that we will look to answer are:

* How does the performance of a classifier under a certain active learning strategy with multiple label sources compare to the case of a basic baseline strategy with a single label source?
* What is the effect in the active learning process of having a big spectrographic telescope vs. that of having several small ones?
* Does having labels assigned by experts by visual inspection improve the active learning process?

## Workflow

Here is a general description of the overall workflow we will develop:

<img src="label_workflow.png" alt="workflow diagram" width="500"/>

1. Alerts are received from the observatory;
2. A machine learning model (possibly previously trained) classifies the alerts and/or assigns a classification score to them;
3. A resource manager makes a decision on which alerts to ask for labels to certain label managers according to some policy;
4. The labels are retrieved and the machine learning model is re-trained;
5. The classification results are used to do scientific analysis.

The system will make use of both real and simulated data, delivered in the form of streams in order to have a realistic experimental setting.

## Modules

### Resource Manager

The resource manager is a module that keeps track of:

* A list of new and currently observed objects by the observatory;
* A list of label managers;
* A label request policy;

### Label Manager

A label manager provides an interface to standardize access to label sources. It has methods that give access to information related to a label, such as:

* Retrieval costs;
* Data requirements;
* Values in different formats;
* Associated accuracies.

Some of the methods that a class that implements this functionality would be:

```python
def cost(self, obj: PhotoObject) -> float:
    """Returns the cost this LabelManager would incur if this object was to be observed.

    :param obj: The object for which to retrieve a cost.

    :return: The cost associated to observe the object.
    """
```
```python
def available(self, obj: PhotoObject) -> bool:
    """Check if the boundaries or domain of this label source allows a label to be retrieved
    for a certain object.

    :param obj: Object for which a label wants to be retrieved.

    :return: Boolean that indicates if a label is available for the object.
    """
```
```python
def predicted_accuracy(self, obj: PhotoObject) -> float:
    """Returns the predicted accuracy that a label retrieved by this label manager would have
    for this object.

    :param obj: Object for which a label wants to be retrieved.

    :return: Predicted accuracy of the label.
    """
```
```python
def get_label(self, obj: PhotoObject) -> Label:
    """Query a label from the label source for an object.

    :param obj: Object for which a label wants to be retrieved.

    :return: Label object (with label value and possibly a certainty score).
    """
```
```python
def current_budget(self) -> int:
    """Current available budget of this label source for further label queries.

    :return: Integer that quantifies the current budget.
    """
```

## Other Concepts

### Active Objects

The system will keep track of the objects that are currently being observed. An object will be considered to be currently observed according to some user-defined criterion (such as a time range for how recently the last observation took place).

At the same time, the system should keep track of the classification scores the machine learning model has assigned to this object so far and the history of labels that have been retrieved for this object, if any.

### Policies

A policy is a strategy followed by the resource manager in order to know for which observed objects to request a label, and to which label manager ask for it. This requests are performed in successive iterations to multiple label managers at the same time.

A policy depends both two kinds of characteristics. First, of properties related to the objects themselves; such as how recently they have been observed, their brightness, and the latest classification score obtained for them. And then, of properties related to the label sources; such as the cost of requesting a label for such an object, the budget of a label source (the amount of requests it can handle per iteration), and how accurate is the label predicted to be.