| Students/Group | Project Type | Predictive Models | Dataset | Folder Name |
|:--------------:|:------------:|:-----------------:|---------|-------------|
|  Michelangelo Esposito              |      Forest Cover Type        |  <h3>Online learning:</h3><ul><li>- [x] Adaptive Random Forest</li><li>- [x] Hoeffding Tree   </li><li>- [x] Naive Bayes</li></ul><h3>Batch learning:</h3><ul><li>- [x] Random Forest</li><li>- [x] Decision Tree   </li><li>- [x] Naive Bayes</li></ul> |   [Link](https://archive.ics.uci.edu/ml/datasets/covertype)            |     ./Michelangelo-Esposito-Forest-CoverType        |
|                |              |                   |         |             |

# Forest Cover Type dataset analysis

## Summary
[- Context of the project](#Context-of-the-project).\
[- Dataset analysis](#Dataset-analysis).\
[- Online-learning](#Online-learning).\
[- Batch-learning](#Batch-learning).

This project contains an analysis of UCI's Forest Cover Type dataset and was developed for the "IoT Data Analytics" university course.  The dataset is available at the following [link](https://archive.ics.uci.edu/ml/datasets/covertype).

# Context-of-the-project
The main focus of this project is to employ **online machine learning** techniques to analyse the performances of various classifiers on a data stream. This stream does not produce real-time data, but it is generated from a csv/arff file in order to use the online approach.
The platform chosen for the initial analysis is **MOA, Massive Online Analysis**; the three classifiers employed during this phase are:
- **Adaptive Random Forest.**
- **Hoeffding Tree.**
- **Naive Bayes.**

At this point, a first comparison among the three classifiers was made, in order to analyse their performances and costs measured.
Then, the **Scikit Multiflow** library in Python was used to repeat the saem online lerarning process, in order to further elaborate on MOA's efficieny and also obtain some kind of comparison in terms of accuracy, execution times, etc.
Finally, a traditional batch approach was employed to additionally assess the potential gap with online learning. The chosen library is **Scikit Learn** in Python, The three batch classifiers used are:
- **Random Forest.**
- **Decision Tree.**
- **Naive Bayes.**

# Dataset-analysis
The dataset used for this study is available for free on the UCI Machine Learning Repository website and its employment revolves around predicting forest cover type from cartographic variables only; no images or other kinds of data are present in this dataset. The actual forest cover type for a given observation (30 x 30 meters cell) was determined from US Forest Service (USFS) Region 2 Resource Information System (RIS) data. Independent variables were derived from data originally obtained from US Geological Survey (USGS) and USFS data. The data was not originally scaled and contains binary columns of data for qualitative independent variables, such as wilderness areas and soil types. A total of over 580,000 entries are present in the dataset, each with the following attributes:
- Elevation in meters.
- Aspect in degrees azimuth.
- Slope in degrees.
- Horizontal distance to nearest surface water.
- Vertical distance to nearest surface water.
- Horizontal distance to nearest roadway.
- Hill shade index at 9am, summer solstice.
- Hill shade index at noon, summer solstice.
- Hill shade index at 3am, simmer solstice.
- Horizontal distance to nearest wildfire ignition points.
- Wilderness area designation.
- Soil type designation.
- Forest cover type designation (dependent attribute). The seven cover types, with the respective number of entries, are: 
    - Spruce/Fir: 211840.
    - Lodgepole Pine: 283301.
    - Ponderosa Pine: 35754.
    - Cottonwood/Willow: 2747.
    - Aspen: 9493.
    - Douglas-fir: 17367.
    - Krummholz: 20510.

Before employing classification techniques on the dataset, its composition was analyzed, as well as the distribution of the various features, and its values.
**Note** that, for the online classification part, no balancing or optimization techniques were considered, since it was assumed that the entries from the dataset were being streamed in real time from a source of some kind, such as iot sensors. On the other hand, for the batch learning approach we aimed at obtaining the best results by applying various pre-processing techniques.

First of all, the distribution of the various values was analyed. It was immediately noticeable that there was a large imbalance among the seven cover types. The respective percentages are the following:
- Lodgepole Pine: 48.76%
- Spruce/Fir: 36.46%
- Ponderosa Pine: 6.15%
- Krummholz: 3.53%
- Douglas-fir: 2.99%
- Aspen: 1.63%
- Cottonwood/Willow: 0.47%

<p align="center">
    <img src="./Figures/README/Distribution.png" alt="Distribution" />
</p>

The next thing to look out for was skewness. Skewness is a quantifiable measure of how distorted a data sample is from the normal distribution. While most of the attribute present minimal skewness, some of the soil types suffer much more from this problem, especially “Soil_Type15”.
<p align="center">
    <img src="./Figures/README/Skewness.png" alt="Skewness" />
</p>

The distribution of the four wilderness areas and of the 40 soil types has also been analysed, finding an unbalanced distribution mostly in favour of the two most present tree types.

A final aspect worth considering is the correlation between the different features. Correlation explains how one or more features are related to each other; it gives us a general idea about the degree of the relationship of two features.
The next table is the result of computing correlation values among the continuous attributes of our dataset.
<p align="center">
    <img src="./Figures/README/Correlation.png" alt="Correlation" />
</p>

# Online-learning
**We do not report the results obtained with the various classifiers here. They are insted reported in the main document**. 
In order to use the dataset in online fashion, and simulate real-time learning, its entries are streamed from the arff file to MOA. Later on we also employed Scikit Multiflow to check whether or not the two techniques would produce similar results.
Each of the three classifier's run produced a set of parameters on which to evaluate the model; furthermore, every 100,000 processed instances, intermediary results were logged, in order to measure the growth of the predictor over time.

Various graphs and tables were used to assess the performances of the classifiers.

# Batch-learning
**We do not report the results obtained with the various classifiers here. They are insted reported in the main document.** 
To further expand on the analysis of the goodness of the results obtained in MOA and Scikit Multiflow, we decided to compare these findings with other analysis techniques using batch learning. In particular, the focus shifted towards one of the most widely used libraries for machine learning, python’s Scikit Learn. 
As a result of the previous analysis, different preprocessing techniques and evaluation methods were applied on the dataset, namely:
- **Removal of strongly correlated attributes**.
- **Data balancing via over-sampling.**
- **Hyperparameters tuning.**
- **Train/test splitting vs 10-fold Cross Validation**.
- **Overfitting and Underfitting analysis**

Various graphs and tables were used to assess the performances of the classifiers.
