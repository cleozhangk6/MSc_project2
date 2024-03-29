
## 3.1 Exploratory Analysis

### 3.1.1 Patterns of each Variable

There are six variables of interest after processing of Ethoscope data: `mean velocity` of locomotion, `x` coordinate of the oval mask centre, normalised `phi` angle as well as the width `w`, height `h`, and `area` of the mask. To intuitively look for potential characteristics of each variable, the mean and confidence interval of variable value averaged over 210 fly recordings were computed and plotted over time [(Figure 3)](#fig3). <a onclick="check('__tabbed_1_1')">Figure 3A</a> shows that `mean velocity` is highly cyclical, which is expected as the *Drosophila* activity level follows a circadian rhythm. Fly with a velocity value under 1 is considered to be immobile, and long periods of immobility (i.e., sleep) are typically observed during the mid-day (hour 2-9) and early-night (hour 14-18).  Interestingly, the `x` and `phi` variables also display a similar pattern that has lower mean values at these sleep periods <a onclick="check('__tabbed_1_2')">(Figure 3B&nbsp;</a><a onclick="check('__tabbed_1_3')">& 3C)</a>, although the corresponding degree of uncertainty is much higher. For `w`, `h` and `area`, a sudden change in value when switching to dark is seen <a onclick="check('__tabbed_1_4')">(Figure 3D&nbsp;</a><a onclick="check('__tabbed_1_5')">& 3E&nbsp;</a><a onclick="check('__tabbed_1_6')">& 3F)</a>. This could be the result of a technical defect as the camera becomes less capable of detecting fly boundaries in dim lighting. The overall area may be larger during night than day due to this problem. 


#### <p class="hide-title">F3. Variables over Time</p><a name="fig3"></a>
=== "A) mean velocity"
    <iframe src="../graph/mean_velocity_overtime.html" class="pvot"></iframe>
    <p class="fig-cap"><b>Figure 3A. Mean Velocity of Movement Over Time.</b> The central red line is the mean velocity averaged over all flies. The upper and lower bounds represent the confidence interval. Time spent in dark conditions are highlighted in grey. </p>
=== "B) x"
    <iframe src="../graph/x_overtime.html" class="pvot"></iframe>
    <p class="fig-cap"><b>Figure 3B. X Position Over Time.</b> The central red line is the mean velocity averaged over all flies. The upper and lower bounds represent the confidence interval. Time spent in dark conditions are highlighted in grey. </p>
=== "C) phi"
    <iframe src="../graph/phi_overtime.html" class="pvot"></iframe>
        <p class="fig-cap"><b>Figure 3C. Phi Angle Over Time.</b> The central red line is the mean velocity averaged over all flies. The upper and lower bounds represent the confidence interval. Time spent in dark conditions are highlighted in grey. </p>
=== "D) w"
    <iframe src="../graph/w_overtime.html" class="pvot"></iframe>
    <p class="fig-cap"><b>Figure 3D. Width of Oval Mask Over Time.</b> The central red line is the mean velocity averaged over all flies. The upper and lower bounds represent the confidence interval. Time spent in dark conditions are highlighted in grey. </p>
=== "E) h"
    <iframe src="../graph/h_overtime.html" class="pvot"></iframe>
    <p class="fig-cap"><b>Figure 3E. Height of Oval Mask Over Time.</b> The central red line is the mean velocity averaged over all flies. The upper and lower bounds represent the confidence interval. Time spent in dark conditions are highlighted in grey. </p>
=== "F) area"
    <iframe src="../graph/area_overtime.html" class="pvot"></iframe>
    <p class="fig-cap"><b>Figure 3F. Area of Oval Mask Over Time.</b> The central red line is the mean velocity averaged over all flies. The upper and lower bounds represent the confidence interval. Time spent in dark conditions are highlighted in grey. </p>




### 3.1.2 Classifying Set Periods in Mid-day and Early-night

Previous studies have shown that the *Drosophila* brain activity level is lower during night-time sleep than day-time sleep [^9], suggesting that deeper sleep stages are more likely to occur during the night. To exploratively investigate whether our multivariate data reflects this hypothesis, time series were extracted from specific times during the mid-day and early-night for HCTSA analysis. Initially, 20-min periods were taken and subjected to feature extraction, but over 30% of HCTSA operations were not able to yield good-quality features as most operations were designed for analysing longer time series. Therefore, 60-min periods were taken from hour 6-7 (mid-day) and hour 13-14 (early-night), and they were labelled as ‘light’ and ‘dark’ accordingly. Since HCTSA only supports single-variable analysis, a HCTSA computation was done for each of the `mean velocity`, `x`, `phi` and `area` variables, producing four different feature matrices. Three different classifiers were used: linear support vector machine (SVM), decision tree, and K-nearest neighbours (kNN) [(Table 1)](#tab1). SVM consistently yielded the highest classification accuracy amongst the three. Of the four variables included, `mean velocity` and `area` time series are the most distinguishable between the two time periods. However, the high classification rates for `area` may be due to bias in image recognition, and so only the `mean velocity` is considered.  

#### <p class="hide-title">T1. Classifcation rates</p><a name="tab1"></a>
<center><table style="border:none;"> </br>
<b>Table 1. Classification Rates for Time Periods between Mid-day vs Early-night</b>
  <thead>
    <tr>
        <th></th>
        <th colspan=3>
        <span id="thspan"> Mean Accuracy of 10-fold Classification <span>
        </th>
    </tr>
    <tr>
        <th>Variable</th>
        <th>SVM</th>
        <th>Decision Tree</th>
        <th>kNN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td>mean velocity</td>
        <td>73.91%</td>
        <td>68.15%</td>
        <td>69.53%</td>
    </tr>
    <tr>
        <td>x</td>
        <td>67.89%</td>
        <td>62.86%</td>
        <td>59.21%</td>
    </tr>
    <tr>
        <td>phi</td>
        <td>60.91%</td>
        <td>57.97%</td>
        <td>57.35%</td>
    </tr>
    <tr>
        <td>area</td>
        <td>74.86%</td>
        <td>71.97%</td>
        <td>67.48%</td>
    </tr>
  </tbody>
</table></center>


## 3.2 Sleep Data Curation

### 3.2.1 Identifying Sleep Sessions

Sleep can not only occur during mid-day and early-night but also at any time throughout the day. It would therefore be useful to robustly define and extract sleep sessions from the data for a more stringent analysis. Initially, the five-minute rule [^7] was applied to identify sleep, where periods of at least five continuous minutes of inactivity are labelled as asleep. However, using this metric alone to extract sleep sessions for time series analysis has two limitations: 1) successive inactive periods may be disrupted by short bursts of activities, resulting in fragmented sleep periods and hence fewer time series data of at least 60-min available for HCTSA feature extraction, 2) it could potentially filter out lighter sleep stages, and the remaining `mean velocity` time series would inherently all have little fluctuations, making it difficult to distinguish between them.

To overcome these limitations, another metric for defining sleep sessions was developed. In addition to the five-minute rule, short bursts (&le; 5min) of activities are allowed between inactive sleep periods and are still labelled as asleep. This allows longer periods of sleep to be extracted for HCTSA analysis and classification. Examples of the time series produced are shown in [Figure 4](#fig4). It can be seen that bursts of activity occur periodically during both day-sleep and night-sleep, and nuances between the two are searched for using HCTSA analysis.

#### <p class="hide-title">F4. Time Series plot</p><a name="fig4"></a>
<center>
<iframe src="../graph/plotTS_24.html" class="pts"></iframe>
<p class="fig-cap"><b>Figure 4. Snippets of Time Series Extracted for HCTSA Analysis.</b> 10 time series for each of the two classes was randomly selected and plotted over time. Note, the y range of the time series is normalised to be between 0-1 and does not represent the absolute values. </p>
</center>

## 3.3 Classifying Sleep at Different Parts of the Day 

### 3.3.1 Two-class classification

Sleep sessions that are at least 60-min long were selected from `mean velocity` data, and the first 60-min of which were extracted. This is to allow all time series to be the same length so that classification would not rely on length-dependent features but on more intrinsic properties. A total of 991 time series (M=991) were produced; 388 of which are day-time sleep and 603 of which are night-time sleep, and they were labelled as ‘light’ or ‘dark’ accordingly. HCTSA successfully computed 5202 features (N=5202) on each time series. Thus, a 991 x 5202 (M x N) feature matrix was generated for this two-class data. Classification on the full feature space using a 10-fold linear SVM classifier yielded a mean balanced accuracy of 73.01%. 

To visualise and examine the feature space, dimensionality reduction algorithms including principal component analysis (PCA) and t-distributed stochastic neighbour embedding (t-SNE) were employed. Two-dimensional representations by the two methods are shown in [Figure 5](#fig5). Additionally, a linear SVM classification was performed on each dimensional space, and the individual and combined classification accuracies are indicated on the axis.  In the PCA plot, time series data for night-time sleep (red dots) are more spread out than those for day-time sleep (blue dots) <a onclick="check('__tabbed_2_1')">(Figure 5A)</a>. Interestingly, night-time sleep data embedded by t-SNE follows a bimodal distribution to some degree, with one of the peak positions being similar to that for day-time sleep data <a onclick="check('__tabbed_2_2')">(Figure 5B)</a>. This provides the first evidence that two types of sleep may exist: one occurs mostly at night and the other can occur at both day and night. 

#### <p class="hide-title">F5. PCA & T-SNE</p><a name="fig5"></a>
=== "A) PCA"
    <center><iframe src="../graph/plotPCA_24.html" class="plow"></iframe></center>
    <p class="fig-cap"><b>Figure 5. Low Dimensional Representations of the Feature Space for the Two-Class Problem.</b> A) 2D principal component analysis (PCA) plot for the normalised feature space. Data points are coloured by the two class labels. A 1D plot for each principal component (PC) is also included. Linear SVM classifications are performed on the reduced space. In each axis label, the proportion of variance explained by the PC and the raw classification accuracy are provided in parentheses. Combined accuracy for the 2D space is indicated in the plot title.</p>
=== "B) t-SNE"
    <center><iframe src="../graph/plotTSNE_24.html" class="plow"></iframe></center>
    <p class="fig-cap"><b>Figure 5. Low Dimensional Representations of the Feature Space for the Two-Class Problem.</b> B) 2D t-distributed Stochastic Neighbour Embedding (t-SNE) plot for the normalised feature space. Data points are coloured by the two class labels. A 1D plot for each t-SNE component is also included. Linear SVM classifications are performed on the reduced space. In each axis label, the proportion of variance explained by the t-SNE component and the raw classification accuracy are provided in parentheses. Combined accuracy for the 2D space is indicated in the plot title.</p>

To investigate whether classification is driven by certain types of features, HCSTA features were divided into subsets based on the type of properties they measure and then compared by the accuracies of linear SVM classification [(Figure 6)](#fig6). Notably, location- and spread-dependent features yielded the highest accuracies. Location-dependent features are those that change under mean shifts of a time series, while spread-dependent features are those that change under rescaling about their mean [^15]. Both types describe basic statistics of the distribution of time series. This indicates that the differences between day-time sleep and night-time sleep may be explained by simple features rather than complex dynamical properties of the time series. 


#### <p class="hide-title">F6. Feature Dependence</p><a name="fig6"></a>
<center><iframe src="../graph/plotDepend_24.html" height="470" width="800" frameBorder="0"></iframe></center>
<p class="fig-cap"><b>Figure 6. Comparison of Feature-Set Dependence for the Two-Class Problem.</b> Subsets of the HCTSA features were extracted based on the types of analysis they conduct. Linear SVM classification was then performed on each subset of features and on the subset-excluded sets, and their balanced accuracies were compared with that of the full feature set ('all').</p>

</br>
Next, each of the 5202 features was individually assessed for their ability to separate the two labelled classes using linear SVM classification. The performance distribution was compared to a set of randomized null features to evaluate the statistical significance of the result [(Figure 7)](#fig7). It is shown that only a relatively small number of features yield high classification accuracies. 

#### <p class="hide-title">F7. Distribution of Accuracies</p><a name="fig7"></a>
<center><iframe src="../graph/plotPermutation_24.html" height="500" width="1000" frameBorder="0"></iframe></center>
<p class="fig-cap"><b>Figure 7. Distribution of Accuracies across all features.</b> The histogram represents real distribution of accuracies. Red dashed line indicates the classification accurarcy of a set of randomized null features. Blue dashed line indicates the mean accuracy of the real feature set. </p>

</br>
The 16 most discriminative features and their class distributions are visualized in [Figure 8](#fig8). The ‘dark’-labelled data of several features, including `[894] EN_DistributionEntropy_raw_ks`, `[6141] PP_Compare_rav3_kscn_adiff` and `[6253] PP_Compare_resample_2_1_swms`, have exhibited the bimodal distribution that was observed in the previous t-SNE plot <a href="#fig5" onclick="check('__tabbed_2_2')">(Figure 5B)</a>. It can be more clearly seen from these features that the data are roughly organised into two clusters, one containing almost exclusively ‘dark’ labels and the other containing both ‘dark’ and ‘light’ labels. 


#### <p class="hide-title">F8. Top Features</p><a name="fig8"></a>
![pic](img/plotTopFeatures_24.jpg)
<p class="fig-cap"><b>Figure 8. Top 16 Features for the Two-Class Problem.</b> Each subplot shows the normalised class distribution of a feature. The title of each subplot includes the corresponding feature name, operation number, and classification accuracy. </p>


### 3.3.2 Three-class classification

Referring back to the `mean velocity` over time plot in <a href="#fig3" onclick="check('__tabbed_1_1')">Figure 3A</a>, low-activity periods also occur during late-night (hour 20-22) but with higher average velocities than early-night sleep. It is therefore hypothesized that the two clusters seen for night-time sleep data may attribute to differences in early-night and late-night sleep. Therefore, the same dataset used in [section 3.3.1](#331-two-class-classification) were re-labelled with ‘light’, ‘dark (ZT_12-18)’ and ‘dark (ZT_18-24)’. The numbers of time series data for each class are 388, 477 and 126, respectively, indicating that sleep takes place predominately during the first part of the night. Three-class classification using linear SVM was performed on the 991 x 5202 feature matrix, yielding a mean balanced accuracy of 58.65%. A confusion matrix was created and visualised to determine how well the labels are distinguished from one another [(Figure 9)](#fig9). It is shown that ‘dark (ZT_12-18)’ and ‘light’ are well-discerned with true-positive rates over 70%, but ‘dark (ZT_18-24)’ is much more ambiguous. 


#### <p class="hide-title">F9. Confusion Matrix</p><a name="fig9"></a>
<center>
![pic](img/plotConfuse_33.png){ width="500" }
</center>
<p class="fig-cap"><b>Figure 9. Confusion Matrix for the Three-Class Problem.</b> Each cell contains the number of observations made. Diagonal cells represent the correctly predicted observations which have blue colours. Row summary on the right calculates the percentage of correctly predicted observations over the total number of cases in a class, indicating the raw classification accuracy for each class.</p>

</br>
Low-dimensional embedding of the three-class feature space are visualized in <a onclick="check('__tabbed_3_1')">Figure 10A&nbsp;</a><a onclick="check('__tabbed_3_2')">& 10B</a>. In contrast to classification on the full feature space, ‘dark (ZT_18-24)’ data seems to be discriminable from the other two classes in low-dimensional space according to distributions in the first components of PCA and t-SNE. 

#### <p class="hide-title">F10. PCA & T-SNE</p><a name="fig10"></a>
=== "A) PCA"
    <iframe src="../graph/plotPCA_33.html" class="plow"></iframe>
    <p class="fig-cap"><b>Figure 10. Low Dimensional Representations of the Feature Space for the Three-Class Problem.</b> A) 2D principal component analysis (PCA) plot for the normalised feature space. Data points are coloured by the three class labels. A 1D plot for each principal component (PC) is also included. Linear SVM classifications are performed on the reduced space. In each axis label, the proportion of variance explained by the PC and the raw classification accuracy are provided in parentheses. Combined accuracy for the 2D space is indicated in the plot title.</p>
=== "B) t-SNE"
    <iframe src="../graph/plotTSNE_33.html" class="plow"></iframe>
    <p class="fig-cap"><b>Figure 10. Low Dimensional Representations of the Feature Space for the Three-Class Problem.</b> B) 2D t-distributed Stochastic Neighbour Embedding (t-SNE) plot for the normalised feature space. Data points are coloured by the three class labels. A 1D plot for each t-SNE component is also included. Linear SVM classifications are performed on the reduced space. In each axis label, the proportion of variance explained by the t-SNE component and the raw classification accuracy are provided in parentheses. Combined accuracy for the 2D space is indicated in the plot title.</p>





#### <p class="hide-title">F11. Top Features</p><a name="fig11"></a>

Each feature is individually assessed, and class distributions of the top 16 performing features are visualised in <a href="#fig11" onclick="check('__tabbed_4_1')">Figure 11A</a>. Distributions of the two ‘dark’ classes are noticeably segregated, and ‘dark (ZT_12-18)’ data points are mostly found in one cluster. This confirms the hypothesis that night-sleep patterns are different between early- and late-night. In addition, most of these features produced similar distributions, with ‘dark (ZT_18-24)’ having the highest mean and ‘dark (ZT_12-18)’ the lowest. To understand the similarities between top features, a pairwise correlation matrix was computed for the top 40 features <a href="#fig11" onclick="check('__tabbed_4_2')">(Figure 11B)</a>. The matrix was clustered by the absolute correlation coefficient values, leading to only 3 clusters. Hence, these features are largely related to each other and measure similar properties of the time series. The most representative features based on classification performance and feature dependency are: `[17] burstiness_Goh`, `[3262] DN_CompareKSFit_rayleigh_olapint`, `[632] SY_SlidingWindow_ent_ent`, and `[6112] PP_Compare_rav2_kscn_peaksepx`. 

=== "A) Top 16 Features"
    ![pic](img/plotTopFeatures_33.jpg)
    <p class="fig-cap"><b>Figure 11A. Top 16 Features for the Three-Class Problem.</b> Each subplot shows the normalised class distribution of a feature. The title of each subplot includes the corresponding feature name, operation number, and classification accuracy. </p>
=== "B) Pairwise Correlation Matrix of 40 Top Features "
    ![pic](img/plotFeatureMatrix_33.jpg){ width="700" }
    <p class="fig-cap"><b>Figure 11B. Pairwise Dependencies between  Top 40 Features for the Three-Class Problem.</b> Operation number, feature name and classification accuracy are shown on the left. Green boxes indicate clusters of highly correlated features. Other coloured boxes highlight representive features, labelled with the name and type of property they measure. </p>


Lastly, the four representative features are individually inspected to understand in detail how each assigns values to time series [(Figure 12)](#fig12). For each feature, the operation was run on un-normalised time series (rather than the unit interval normalized values in the HCTSA feature matrix) to produce a distribution plot of the actual outputs. Keywords that describe the type of property the feature measures are indicated in the plot title. Snippets of time series ordered by the output values are also plotted to help interpret how the classes are distinguished. 

#### <p class="hide-title">F12. Features of Interest</p><a name="fig12"></a>
<!-- <iframe src="../graph/plotSingle17_33.html" height="400" width="500" frameBorder="0">
</iframe> -->
=== "A) Burstiness"
    <iframe src="../graph/plotFeatureSum17_33.html" height="500" width="1000" frameBorder="0">
    </iframe>
    <p class="fig-cap"><b>Figure 12. Single Feature Analysis for the Three-Class Problem.</b> A) Distributions of raw burstiness values for the three classes and overall data are plotted on the left. Snippets of time series ordered by the output values are shown on the right. </p>
=== "B) Compare Distribution"
    <iframe src="../graph/plotFeatureSum3262_33.html" height="500" width="1000" frameBorder="0">
    </iframe>
    <p class="fig-cap"><b>Figure 12. Single Feature Analysis for the Three-Class Problem.</b> B) Distributions of raw values obtained by comparing kernal-smoothed and fitted distribution of time series are plotted on the left. Snippets of time series ordered by the output values are shown on the right. </p>
=== "C) Sliding Window"
    <iframe src="../graph/plotFeatureSum632_33.html" height="500" width="1000" frameBorder="0">
    </iframe>
    <p class="fig-cap"><b>Figure 12. Single Feature Analysis for the Three-Class Problem.</b> C) Distributions of raw values obtained by applying a sliding window to time series are plotted on the left. Snippets of time series ordered by the output values are shown on the right. </p>
=== "D) Rolling Average"
    <iframe src="../graph/plotFeatureSum6112_33.html" height="500" width="1000" frameBorder="0">
    </iframe>
    <p class="fig-cap"><b>Figure 12. Single Feature Analysis for the Three-Class Problem.</b> D) Distributions of raw values obtained by comparing rolling averaged time series are plotted on the left. Snippets of time series ordered by the output values are shown on the right. </p>

`[17] burstiness_Goh` and `[3262] DN_CompareKSFit_rayleigh_olapint` are both location- and spread dependent features that measure time series distribution, and their resulting plots are extremely similar <a onclick="check('__tabbed_5_1')">(Figure 12A&nbsp;</a><a onclick="check('__tabbed_5_2')">& 12B)</a>. `[632] SY_SlidingWindow_ent_ent` is a measure of stationarity which slides a window along the time series, calculates the distribution entropy of each window and outputs an overall histogram entropy value <a onclick="check('__tabbed_5_3')">(Figure 12C)</a>. Therefore, it is also a measure of distribution and is highly correlated to `[17] burstiness_Goh`. On the other hand, `[6112] PP_Compare_rav2_kscn_peaksepx` is a combination of `[3262] DN_CompareKSFit_rayleigh_ olapint` and `[632] SY_SlidingWindow_ent_ent`, which applies a running average transformation (window length = 2) to the time series and quantifies differences between the kernel-smoothed and fitted distribution of the processed data <a onclick="check('__tabbed_5_4')">(Figure 12D)</a>. As a result, all four operations evaluates similar properties of the time series. Of which, `[17] burstiness_Goh` produces the highest classification accuracy and so is considered for further interpretation in the [Discussion](discussion.md) page.

</br>
*[SVM]: Support Vector Machine
*[kNN]: K-nearest neighbours
*[HCTSA]: Highly Comparative Time Series Analysis
*[Catch22]: Canonical Time-series Characteristics
*[PCA]: Principal Component Analysis
*[t-SNE]: t-distributed Stochastic Neighbour Embedding

 
[^9]: van Alphen B, Yap MHW, Kirszenblat L, Kottler B, van Swinderen B. A Dynamic Deep Sleep Stage in Drosophila. J Neurosci. 2013 Apr 17;33(16):6917–27. 
[^7]: Cirelli C, Bushey D. Sleep and wakefulness in Drosophila melanogaster. Ann N Y Acad Sci. 2008;1129:323–9.
[^15]:Fulcher BD, Little MA, Jones NS. Highly comparative time-series analysis: the empirical structure of time series and their methods. J R Soc Interface. 2013 Jun 6;10(83):20130048.