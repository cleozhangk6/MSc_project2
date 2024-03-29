# Inferring Sleep Stages in *Drosophila Melanogaster* with Ethoscope Data and Machine Learning
<!-- **Meng Zhang** 
Supervisors: Giorgio Gilestro, Laurence Blackhurst -->

## Abstract
![pic](img/drosophila2.png){ width="250", align=right }
<!-- <p style="text-align:justify">  -->

Sleep in mammals is known to be a dynamic process with distinguishable stages. However, sleep in *Drosophila melanogaster* has often been assumed homogenous and is defined by a simple metric which is five minutes of immobility. There has been increasing evidence that *Drosophila* also adopts different sleep stages with varying internal states and external behaviours. Such internal change for a deeper sleep stage refers to reduced brain activity, measured by quantifying electrical signals produced in nervous tissue, while the external behavioural changes include increased arousal threshold and a stereotypical micromovement of the mouth organ. These measurements either require additional experimental conditions or are at a microscopic level. Therefore, this study investigates whether the sleep stages suggested by previous research can be inferred from more readily detectable behavioural data generated by the Ethoscope. Ethoscope employs machine vision algorithms to track single fly movement over time. The resulting time series data is then subjected to highly comparative time series analysis (HCTSA) to detect patterns that differentiate potential sleep stages. HCTSA performs massive feature extraction on time series data which allows subsequent machine learning techniques to cluster or classify the data. Here using HCTSA and other exploratory analysis, it is showed that the velocity of fly locomotion may be the most informative parameter for inferring sleep stages. It is also showed that deeper and lighter sleep stages could be differentiated by simple metrics such as the burstiness of movement over time. These provides interesting scope for uncovering more details of *Drosophila* sleeping behaviours, ultimately to further improve the capability of using *Drosophila* as a model for sleep studies. 
</br>
</br>
</br>

<!-- !!! example "Aims"
    1. Infer sleep stages
    2. different variables -->
    


