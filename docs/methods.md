All data for this project is retrieved from previous experiments done by the Gilestro Lab group. Computationally intensive work in this project was performed on remote servers. Catch22 analysis was performed locally. Highly comparative time-series analysis (HCTSA) was submitted as jobs to be run on the Imperial Research Computing Service with 4 CPUs and 64 GB memory. Data processing, exploratory analysis and visualisation tasks were carried out using Python or MATLAB on a 16 GB MacBook Pro.

## 2.1 Ethoscope Data

Data was downloaded from the remote database of the Gilestro Lab group. The dataset describes 210 male CantonS flies that were raised at 25˚C on standard yeast and sugar media, then each fly was placed into a 70 mm × 5 mm × 3 mm (length × external diameter × internal diameter) glass tube containing food. Groups of 20 flies were placed each Ethoscope in 25˚C incubators and were video recorded under a 12-hour light and 12-hour dark conditions over several days. The experiment was originally designed for sleep-deprivation studies, but sleep distributions was not applied until 4 days of normal conditions. Day 1-3 (hour 24-96) was therefore extracted (day 0 was also omitted to allow time for flies to adjust), and data was binned to 60 seconds used for shorter downloading and analysis time.

## 2.2 Data Processing and Exploration

The Ethoscope generates five variables (X, Y, Phi, W, and H) for each recording of fly activity over time. It also produces the maximum and mean velocities calculated from the distance travelled by the fly over unit time. Movement in the vertical axis is restricted as the fly moves within a longitudinal tube, so the Y variable is omitted. The oval mask does not have any directionality, hence the raw Phi values which are between 0 and 180 were normalised into values between 0 and 90 to describe whether a fly is horizontal or vertical. Additionally, area of the oval mask was calculated from the W and H values. These variables of potential interest, namely the `mean velocity`, `x`, `y`, `phi`, `w`, `h` and `area`, were used for exploratory analysis to identify which ones may be indicative of unique sleeping patterns. 


## 2.3 Time Series Analysis

### 2.3.1 Feature Extraction

### 2.3.2 Low Dimensional Representation

### 2.3.3 Classification

### 2.3.4 Feature Interpretation


<!-- |               |             Classifier                || -->
<!-- | Variable      | SVM     | Decision Tree | KNN          |
| ------------  | ------- | ------------- | ------------ |
| mean_velocity | 73.91%  | 68.15%        | 69.53%       |
| x             | 67.89%  | 62.86%        | 59.21%       |
| phi           | 60.91%  | 57.97%        | 57.35%       |
| area          | 74.86%  | 71.97%        | 67.48%       | -->