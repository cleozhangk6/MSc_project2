All data for this project is retrieved from previous experiments done by the Gilestro Lab group. Computationally intensive work in this project was performed on remote servers. Catch22 analysis was performed locally. Highly comparative time-series analysis (HCTSA) was submitted as jobs to be run on the Imperial Research Computing Service with 4 CPUs and 64 GB memory. Data processing, exploratory analysis and visualisation tasks were carried out using Python or MATLAB on a 16 GB MacBook Pro.

## 2.1 Ethoscope Data

Data was downloaded from the remote database of the Gilestro Lab group. The dataset describes 210 male CantonS flies that were raised at 25˚C on standard yeast and sugar media, each fly was then placed into a 70 mm × 5 mm × 3 mm (length × external diameter × internal diameter) glass tube containing food. Groups of 20 flies were placed for each Ethoscope in 25˚C incubators and were video recorded under a 12-hour light and 12-hour dark conditions over several days. The experiment was originally designed for sleep-deprivation studies, but sleep distributions was not applied until 4 days of normal conditions. Day 1-3 (hour 24-96) was therefore extracted (day 0 was also omitted to allow time for flies to adjust), and data was binned to 60 seconds used for shorter downloading and analysis time.

## 2.2 Data Processing and Exploration

The Ethoscope generates five variables (X, Y, Phi, W, and H) for each recording of fly activity over time. It also produces the maximum and mean velocities calculated from the distance travelled by the fly over unit time. Movement in the vertical axis is restricted as the fly moves within a longitudinal tube, so the Y variable is omitted. The oval mask does not have any directionality, hence the raw Phi values which are between 0 and 180 were normalised into values between 0 and 90 to describe whether a fly is horizontal or vertical. Additionally, area of the oval mask was calculated from the W and H values. These variables of potential interest, namely the `mean velocity`, `x`, `y`, `phi`, `w`, `h` and `area`, were used for exploratory analysis to identify which ones may be indicative of unique sleeping patterns. 


## 2.3 Time Series Analysis

### 2.3.1 Feature Extraction

For each time series dataset, three M x 1 cell arrays were created in MATLAB to specify the 1) time series data, 2) class labels, 3) identifiers of the time series. These were used to initialise an HCTSA.mat with an empty M x N table. Catch22 or HCTSA operations were performed on the HCTSA.mat file using the `TS_compute` function. Each operation returned a value for every time series and was saved to the .mat file. The resulting HCTSA matrix was normalised and bad-quality features were removed using the `TS_normalize` function [^1] [^2]. A  Catch22 analysis typically takes about 5-7 minutes (run locally), an HCTSA takes around 3-4 hours (run on a HPC). 

### 2.3.2 Low Dimensional Representations

The HCTSA software provides a `TS_PlotLowDim` function which performs and visualises low-dimensional representations of the feature space. Two dimensionality reduction methods were considered, namely principal component analysis (PCA) and t-distributed stochastic neighbour embedding (t-SNE). 

??? question "Principal Component Analysis (PCA)"
    PCA measures covariance between data points and transforms them onto the so-called principal components (PCs) which are orthogonal lines that capture the most variance of the data. It helps to reduce noise caused by outliers and reveal the underlying relationships between data points [^3].

??? question "t-distributed Stochastic Neighbour Embedding (t-SNE)"
    t-SNE is a nonlinear dimensionality reduction method. It calculates the similarity between each pair of data points, represents them in terms of probability distributions, and then minimises the difference between the probability distributions in the original and lower dimensional space. As a result, it allows detection of local similarities in complex and non-linear datasets [^4].


### 2.3.3 Classification

The `TS_Classify` function was used to classify assigned class labels of a given normalised HCTSA data matrix. Three types of classifiers are considered: linear support vector machine (SVM), decision tree, and k-nearest neighbours (kNN). All classification performances are cross-validated with a fold number of 10 (i.e., dataset is split into 10 groups for training/testing in each random shuffle), giving a mean balanced classification accuracy.

??? question "Linear Support Vector Machine (linear-SVM)"
    SVM is a supervised learning algorithm that finds optimal hyperplanes within the feature space to separate data points of different classes. Linear-SVMs are commonly used whose hyperplane is essentially a straight line [^5]. 
??? question "Descision Tree"
    Decision tree is a supervised learning algorithm that predicts the value or class of an output variable based on several input variables. Data is continuously split according to a certain parameter to create a decision tree. The tree has nodes and leaves, where leaves are the decisions or the output and nodes are where the data is split. This method is commonly used in data mining as it is good for describing and generalising data [^6].
??? question "k-Nearest Neighbours (kNN)"
    kNN is a non-parametric supervised learning algorithm that uses proximity of data points to make predications about the class labels. It identifies the nearest neighbours of a given query point based on a chosen distance metric and assigns a label to the class. The most commonly used metric is the Euclidean distance which measures a straight line between two points [^7].


### 2.3.4 Feature Analysis

The feature sets were compared using the `TS_CompareFeatureSets` function, and top features were probed in detail using several functions including `TS_TopFeatures` and `TS_FeatureSummary`.  Scripts were modified when necessary to obtain appropriate information or visualisations for the analysis. 

</br>
</br>


*[SVM]: Support Vector Machine
*[kNN]: K-nearest neighbours
*[HCTSA]: Highly Comparative Time Series Analysis
*[Catch22]: Canonical Time-series Characteristics
*[PCA]: Principal Component Analysis
*[t-SNE]: t-distributed Stochastic Neighbour Embedding

[^1]: hctsa: A Computational Framework for Automated Time-Series Phenotyping Using Massive Feature Extraction: Cell Systems [Internet]. [cited 2022 Jun 6]. Available from: [https://www.cell.com/cell-systems/fulltext/S2405-4712(17)30438-6](https://www.cell.com/cell-systems/fulltext/S2405-4712(17)30438-6)
[^2]: Fulcher BD, Little MA, Jones NS. Highly comparative time-series analysis: the empirical structure of time series and their methods. Journal of The Royal Society Interface. 2013 Jun 6;10(83):20130048. 
[^3]: Shlens J. A Tutorial on Principal Component Analysis. Educational. 2014 Apr 3;51. 
[^4]: van der Maaten L, Hinton G. Viualizing data using t-SNE. Journal of Machine Learning Research. 2008 Nov 1;9:2579–605. 
[^5]: Support Vector Machine: Principles, Parameters, and Applications - ScienceDirect [Internet]. [cited 2022 Jun 12]. Available from: [https://www.sciencedirect.com/science/article/pii/B9780128113189000272](https://www.sciencedirect.com/science/article/pii/B9780128113189000272)
[^6]: Quinlan JR. Induction of decision trees. Mach Learn. 1986 Mar 1;1(1):81–106. 
[^7]: Altman NS. An Introduction to Kernel and Nearest-Neighbor Nonparametric Regression. The American Statistician. 1992;46(3):175–85. 


