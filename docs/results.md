
<!-- !!! pied-piper "Figure X. Mean Velocity Over Time" -->

## 3.1 Variables Averaged over Time

#### <p class="hide-title">Figure 3. Variables over time</p>
=== "Mean velocity"
    <iframe src="../graph/mean_velocity_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3A. Mean Velocity Over Time</p>
=== "X"
    <iframe src="../graph/x_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3B. Mean Velocity Over Time</p>
=== "Phi"
    <iframe src="../graph/Phi_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3C. Mean Velocity Over Time</p>
=== "W"
    <iframe src="../graph/w_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3D. Mean Velocity Over Time</p>
=== "H"
    <iframe src="../graph/h_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3E. Mean Velocity Over Time</p>
=== "Area"
    <iframe src="../graph/area_overtime.html" class="pvot"></iframe>
    <p class="fig-cap">Figure 3F. Mean Velocity Over Time</p>


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
        <th>KNN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td>mean_velocity</td>
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

### Plot Time Series
<iframe src="../graph/plotTS_24.html" class="pts"></iframe>

### 24 Plot low 
=== "PCA"
    <iframe src="../graph/plotPCA_24.html" class="plow"></iframe>
=== "T-SNE"
    <iframe src="../graph/plotTSNE_24.html" class="plow"></iframe>

### Plot Top Featues
![pic](img/plotTopFeatures_24.jpg)

### 33
=== "PCA"
    <iframe src="../graph/plotPCA_33.html" class="plow"></iframe>
=== "T-SNE"
    <iframe src="../graph/plotTSNE_33.html" class="plow"></iframe>


<iframe src="../graph/plotSingle17_33.html" height="400" width="500" frameBorder="0">
</iframe>