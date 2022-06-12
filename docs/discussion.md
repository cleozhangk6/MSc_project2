## 4.1 Multivariable Ethoscope Data Follows a Circadian Cycle

Results from [section 3.1.1](results.md) have shown that all Ethoscope variables follow a circadian cycle. The `mean velocity` variable directly relates to the activity level (or mobility), and flies with `mean velocity` below a certain threshold is generally considered as asleep.  It is hence found that *Drosophila* typically sleep during mid-day and the first few hours of the night. Sleep during the day has also been seen in previous fly studies and is known as the mid-day siesta [^15], which is thought to be an adaptive response to minimize exposure to heat  [^16] [^17] [^18]. Flies also exhibit sleep behaviours during late-night (around hour 20-22) followed by a few hours of low-level activities. 

Using the `mean velocity` as a reference, it is seen that `x` and `phi` also follow a similar pattern. Flies tend to be located at `x` positions around 0.2-0.3 during mid-day siesta and early-night sleep, which is roughly where the food is placed. It is likely because sleep happens after feeding, as food consumption has been thought to induce sleepiness [^19]. The `phi` angle is also generally lower (i.e., closer to horizontal) during sleep and consistently higher when active, which is likely due to increased turning when walking back and forth in the tube. Size-related variables including `w`, `h` and `area` all have slightly decreased values during mid-day siesta. Shrinking in size due to fly crouching down when resting has also been observed by previous research [^20]. However, these measures during the night are less reliable for interpretation in this study as the oval masks are not well assigned in dim lights. 

Although the `x` and `phi` variables may be useful in distinguishing sleep and awake states, they seem to be less discriminable when trying to identify deep and light sleep stages according to the classification results in [section 3.1.2](results.md). This study therefore focused on univariate analysis of the `mean velocity` variable to explore potential indicators of sleep stages. 

## 4.2 Sleep Depth and Burstiness of Activity

In this study, a different way of identifying sleep was developed which allows short bursts of activity during sleep. This is to potentially include more light sleep, that has higher activity levels, into our time series data for analysis. Sleep sessions are extracted from different parts of the day using this method, and results from [section 3.3.2](results.md) showed that sleep can be relatively well-differentiated between mid-day, early-night and late-night. Time series for mid-day and early-night sleep are generally organised into single clusters, while late-night sleep data is more distributed with a range of characteristics. The hypothesis is that the majority of sleep during early-night is at a deeper stage and the majority for mid-day is at a lighter stage, and both stages can occur during late-night. 

Investigation of the time series features in [section 3.3.2](results.md) revealed that differences between the three classes may be explained by a small amount of simple, location- and spread-dependent features. These top features are also highly correlated and can be narrowed down to a single representative feature: burstiness. Burstiness describes the intermittent short timeframes of activity following long periods of inactivity [^21]. It is often measured by the Fano factor which is a ratio between the variance and mean of burst counts. The orginal burstiness statistics is proposed by Goh and Barabasi [^22] and is defined as

$$
\Delta \equiv \frac{\operatorname{sgn}\left(\sigma_{\tau}-m_{\tau}\right)}{2} \int_{0}^{\infty}\left|P(\tau)-P_{\mathrm{P}}(\tau)\right| d \tau
$$

where $\Delta$ is the burstiness parameter, $\operatorname{sgn}$ is a function that extracts the sign of a number, $m_{T}$ and $\sigma_{T}$ are the mean and standard deviation of $P(\tau)$, $P(\tau)$ is the given time series, and $P_{\mathrm{P}}(\tau)$ is a random, time-independent series that follows an exponential distribution. This equation is adapted by Fulcher and Jones (12) and incorporated into HCTSA with equation

$$
B=\frac{\sigma_{\tau}-m_{\tau}}{\sigma_{\tau}+m_{\tau}}
$$

where $B$ is the burstiness parameter, $m_{T}$ and $\sigma_{T}$ are the mean and standard deviation of the time series. For the three classes, late-night sleep yields the highest mean burstiness, and early-night sleep yields the lowest. This suggests that early-night sleep time series have fewer significantly enhanced activity levels, which corresponds to the reduced mobility known for deep sleep [^9] [^10]. In addition, sleep has also been associated to increased arousal thresholds (or decreased sensory responsiveness) [^20] [^23], and previous work by the Gilestro Lab Group has shown that late-night sleep exhibits the greatest response to stimuli compared to mid-day siesta and early-night sleep [^24]. This is concordant to the fact that late-night sleep has the highest burstiness. However, responsiveness of early-night sleep seems to be greater than siesta, which contradicts the order of their burstiness values. More work needs to be carried out to determine whether the arousal threshold is correlated to burstiness of activity during sleep. Overall, burstiness may serve as a possible indicator for sleep depth and help to distinguish sleep stages. 

## 4.3 Limitations and Aspects for Improvements

The use of HCTSA for time series analysis has greatly facilitated our exploration for nuances in sleep. However, it also posed many restrictions to the analysis, particularly during the data curation process. First, most HCTSA operations prefers longer time series as inputs, and so sleep sessions are taken in windows of 60 minutes using the more forgiving sleep metric. This excludes shorter sleep periods which may be more typical for *Drosophila* sleep. One solution is to obtain per-second data from the Ethoscope database but its downloading and analysis would be more time-consuming and not suitable for this short exploratory project.  Secondly, it is known for mammals that sleep stages exists in cycles and have varying lengths [^1] [^2], but HCTSA operations return single statistical values for a given time series which may overlook such details. Lastly, HCTSA only allows single-variate analysis, and multivariable analysis that includes other Ethoscope parameters could potentially improve the classification rate. 



[^15]: Cao W, Edery I. Mid-day siesta in natural populations of D. melanogaster from Africa exhibits an altitudinal cline and is regulated by splicing of a thermosensitive intron in the period clock gene. BMC Evol Biol. 2017 Jan 23;17(1):32.
[^16]: Majercak J, Sidote D, Hardin PE, Edery I. How a circadian clock adapts to seasonal decreases in temperature and day length. Neuron. 1999 Sep;24(1):219–30.
[^17]: Rensing L, Ruoff P. Temperature effect on entrainment, phase shifting, and amplitude of circadian clocks and its molecular bases. Chronobiol Int. 2002 Sep;19(5):807–64. 
[^18]: Sweeney BM, Hastings JW. Effects of temperature upon diurnal rhythms. Cold Spring Harb Symp Quant Biol. 1960;25:87–104. 
[^19]: Murphy KR, Deshpande SA, Yurgel ME, Quinn JP, Weissbach JL, Keene AC, et al. Postprandial sleep mechanics in Drosophila. Scott K, editor. eLife. 2016 Nov 22;5:e19334.
[^20]: Hendricks JC, Finn SM, Panckeri KA, Chavkin J, Williams JA, Sehgal A, et al. Rest in Drosophila Is a Sleep-like State. Neuron. 2000 Jan;25(1):129–38. 
[^21]: Lambiotte R, Tabourier L, Delvenne JC. Burstiness and spreading on temporal networks. Eur Phys J B. 2013 Jul 15;86(7):320. 
[^22]: Goh KI, Barabási AL. Burstiness and memory in complex systems. EPL Europhys Lett. 2008 Jan;81(4):48002. 
[^9]: van Alphen B, Yap MHW, Kirszenblat L, Kottler B, van Swinderen B. A Dynamic Deep Sleep Stage in Drosophila. J Neurosci. 2013 Apr 17;33(16):6917–27. 
[^10]: van Alphen B, Semenza ER, Yap M, van Swinderen B, Allada R. A deep sleep stage in Drosophila with a functional role in waste clearance. Sci Adv. 2021 Jan 20;7(4):eabc2999. 
[^20]: Hendricks JC, Finn SM, Panckeri KA, Chavkin J, Williams JA, Sehgal A, et al. Rest in Drosophila Is a Sleep-like State. Neuron. 2000 Jan;25(1):129–38. 
[^23]: Shaw PJ, Cirelli C, Greenspan RJ, Tononi G. Correlates of sleep and waking in Drosophila melanogaster. Science. 2000 Mar 10;287(5459):1834–7. 
[^24]: French AS, Geissmann Q, Beckwith EJ, Gilestro GF. Sensory processing during sleep in Drosophila melanogaster. Nature. 2021 Oct;598(7881):479–82. 
[^1]: Blake H, Gerard RW. Brain potentials during sleep. Am J Physiol-Leg Content. 1937 Jul 31;119(4):692–703. 
[^2]: Wolpert EA. A Manual of Standardized Terminology, Techniques and Scoring System for Sleep Stages of Human Subjects. Arch Gen Psychiatry. 1969 Feb 1;20(2):246–7.