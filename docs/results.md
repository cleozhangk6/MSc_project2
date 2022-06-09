
## 3.1 Exploratory Analysis

### 3.1.1 Variables of Interest

The Ethoscope generates five variables (X, Y, Phi, W, and H) for each recording of fly activity over time. It also produces the maximum and mean velocities calculated from the distance travelled by the fly over unit time. Movement in the vertical axis is restricted as the fly moves within a longitudinal tube, so the Y variable is omitted. The oval mask does not have any directionality, hence the raw Phi values which are between 0 and 180 were normalised into values between 0 and 90 to describe whether a fly is horizontal or vertical. Additionally, area of the oval mask was calculated from the W and H values. These variables of potential interest, namely the mean velocity, X, Y, Phi, W, H and area, were used for exploratory analysis to identify which ones may be indicative of unique sleeping patterns. 

### 3.1.2 Patterns of each Variable

To intuitively look for potential characteristics of each variable, the mean and confidence interval of variable value averaged over 210 fly recordings were computed and plotted over time [(Figure 3)](#fig3). Figure 3A shows that mean velocity is highly cyclical, which is expected as the *Drosophila* activity level follows a circadian rhythm. Fly with a velocity value under 1 is considered to be immobile, and long periods of immobility (i.e., sleep) are typically observed during the mid-day (hour 2-9) and early-night (hour 14-18). Sleep during the day has also been seen in previous fly studies and is known as the mid-day siesta [^14]. Interestingly, the X and Phi variables also display a similar pattern that has lower mean values at these sleep periods (Figure 3B-C), although the corresponding degree of uncertainty is much higher. For W, H and area, a sudden change in value when switching to dark is seen (Figure 3D-F). This could be the result of a technical defect as the camera becomes less capable of detecting fly boundaries in dim lighting. The overall area may be larger during night than day due to this problem. 

#### <p class="hide-title">F3. Variables over Time</p><a name="fig3"></a>
=== "A) Mean velocity"
    <iframe src="../graph/mean_velocity_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3A. Mean Velocity Over Time</p>
=== "B) X"
    <iframe src="../graph/x_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3B. Mean Velocity Over Time</p>
=== "C) Phi"
    <iframe src="../graph/Phi_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3C. Mean Velocity Over Time</p>
=== "D) W"
    <iframe src="../graph/w_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3D. Mean Velocity Over Time</p>
=== "E) H"
    <iframe src="../graph/h_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3E. Mean Velocity Over Time</p>
=== "F) Area"
    <iframe src="../graph/area_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3F. Mean Velocity Over Time</p>

### 3.1.3 Classifying Set Periods in Mid-day and Early-night

Previous studies have shown that the *Drosophila* brain activity level is lower during night-time sleep than day-time sleep [^9], suggesting that deeper sleep stages are more likely to occur during the night. To exploratively investigate whether our multivariate data reflects this hypothesis, time series were extracted from specific times during the mid-day and early-night for HCTSA analysis. Initially, 20-min periods were taken and subjected to feature extraction, but over 30% of HCTSA operations were not able to yield good-quality features as most operations were designed for analysing longer time series. Therefore, 60-min periods were taken from hour 6-7 (mid-day) and hour 13-14 (early-night), and they labelled as ‘light’ and ‘dark’ accordingly. Since HCTSA only supports single-variable analysis, a HCTSA computation was done for each of the Mean velocity, X, Phi and Area variables, producing four different feature matrices. Three different classifiers were used: support vector machine (SVM), decision tree, and K-nearest neighbours (kNN)

#### <p class="hide-title">T1. Classifcation rates</p>
<center><table style="border:none;">
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
        <td>Mean velocity</td>
        <td>73.91%</td>
        <td>68.15%</td>
        <td>69.53%</td>
    </tr>
    <tr>
        <td>X</td>
        <td>67.89%</td>
        <td>62.86%</td>
        <td>59.21%</td>
    </tr>
    <tr>
        <td>Phi</td>
        <td>60.91%</td>
        <td>57.97%</td>
        <td>57.35%</td>
    </tr>
    <tr>
        <td>Area</td>
        <td>74.86%</td>
        <td>71.97%</td>
        <td>67.48%</td>
    </tr>
  </tbody>
</table></center>







## 3.2 Sleep Data Curation

### 3.2.1 Identifying Sleep Sessions

#### <p class="hide-title">F4. Time Series plot</p>
<iframe src="../graph/plotTS_24.html" class="pts"></iframe>

## 3.3 Classifying Sleep at Different Parts of the Day 

### 3.3.1 Two-class classification
#### <p class="hide-title">F5. PCA & T-SNE</p>
=== "PCA"
    <iframe src="../graph/plotPCA_24.html" class="plow"></iframe>
=== "T-SNE"
    <iframe src="../graph/plotTSNE_24.html" class="plow"></iframe>

#### <p class="hide-title">F6. Top Features</p>
![pic](img/plotTopFeatures_24.jpg)

### 3.3.2 Three-class classification

#### <p class="hide-title">F5. PCA & T-SNE</p>
=== "PCA"
    <iframe src="../graph/plotPCA_33.html" class="plow"></iframe>
=== "T-SNE"
    <iframe src="../graph/plotTSNE_33.html" class="plow"></iframe>


<iframe src="../graph/plotSingle17_33.html" height="400" width="500" frameBorder="0">
</iframe>


[^9]: van Alphen B, Yap MHW, Kirszenblat L, Kottler B, van Swinderen B. A Dynamic Deep Sleep Stage in Drosophila. J Neurosci. 2013 Apr 17;33(16):6917–27. 
[^14]: Cao W, Edery I. Mid-day siesta in natural populations of D. melanogaster from Africa exhibits an altitudinal cline and is regulated by splicing of a thermosensitive intron in the period clock gene. BMC Evol Biol. 2017 Jan 23;17(1):32. 