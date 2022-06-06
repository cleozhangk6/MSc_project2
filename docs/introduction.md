# 1. Introducion

<!-- ??? example "Try Collapsible"
    === "try citation"
        This is a citation [^1].
    === "try html"
        <p style="color:green;"> trying html </p>
    === "try image"
        ![pic](img/drosophila.png)
            *figure: drosophila* -->


## 1.1. Sleep Behaviours in *Drosophila Melanogaster*

Sleep is an important yet complex physiological process that occurs in virtually every animal that has been studied so far, but its underpinnings and functions remain elusive despite the rapidly developing effort towards sleep analysis. Mammalian sleep is known to be a multistage process with varying sleep depth associated with changes in neuronal activity [^1][^2][^3]. In humans, for example, electroencephalographic (EEG) recordings can be used to identify the different sleep stages which circulate between wake, light sleep, deep sleep, and rapid eye movement (REM). It is believed that different sleep stages may serve distinct biological functions. For instance, evidence has shown that deep sleep contributes to bodily recovery and growth [^4], while REM sleep is essential to cognitive functions such as memory and learning [^5]. 

!!! info inline end "Definitions"
    === "EEG"
        Electroencephalography (EEG) is a method that measures electrical activity in the brain using small, metal discs (electrodes) attached to the scalp [(Wikipedia)](https://en.wikipedia.org/wiki/Electroencephalography).

    === "PE"
        A proboscis in insects refers to the tubular mouthpart used for feeding and sucking. Proboscis extension (PE) can either occur spontaneously or in response to antennal stimulation [(Wikipedia)](https://en.wikipedia.org/wiki/Proboscis). 

Over the last few decades, the fruit fly *Drosophila Melanogaster* has been an increasingly popular model organism to understand how sleep is controlled by internal and external stimuli and how it affects other biological functions. The simplicity, cost-effectiveness, rapid developmental time, and relevance to human genetics and physiology have made *Drosophila* an indispensable tool [^6]. In most current studies, the sleeping state in *Drosophila* is  defined by a simple metric: immobility for more than five minutes, and it is often assumed to be homogenous throughout. Nevertheless, there has been increasing evidence that sleep in *Drosophila* is also a dynamic process with differing sleep intensities [^7]. Methods including EEG recordings, arousal-testing, and Proboscis Extension (PE) measurements have been used together to show that Drosophila exhibits a deep sleep stage which is characterised by  1) reduced neural activity, 2) increased immobility, 3) increased arousal threshold, and 4) stereotypical PE movement, namely the periodic extensions and retractions of the proboscis  [^8][^9]. These studies also indicated that Drosophila sleep follows a circadian rhythm, where flies sleep the most during start of the night, and it is also under homeostatic control as sleep deprivation leads to increased sleep amount and reduced sleep latency [^9]. 

In this study, we turn to a novel method of measuring Drosophila behaviours using the Ethoscope, developed in the [Gilestro lab](https://lab.gilest.ro/), which can track the movement of a single fly housed in a glass tube [^10]. This provides a simple, non-invasive, and high-throughput measurement of the external behaviour of sleep. The aim is to try and identify patterns in *Drosophila* locomotive data that can infer distinct sleep stages as indicated in previous research. 

## 1.2. The Ethoscope
An ethoscope contains a hardware that video-records the fly in a longitudinal glass tube and a software to track its activity in real-time by applying an oval mask over the fly with machine vision algorithms (Figure 1).
![pic](img/ethoscope.png)
<p style="font-size:0.8em">Figure 1. Ethoscope</p>

## 1.3. Time Series Analysis

![pic](img/hctsa.png)
<p style="font-size:0.8em">Figure 1. Ethoscope</p>

*[EEG]: Electroencephalogram
*[REM]: Rapid Eye Movement
*[PE]: Proboscis Extension


[^1]: Blake H, Gerard RW. Brain potentials during sleep. Am J Physiol-Leg Content. 1937 Jul 31;119(4):692–703. 
[^2]: Wolpert EA. A Manual of Standardized Terminology, Techniques and Scoring System for Sleep Stages of Human Subjects. Arch Gen Psychiatry. 1969 Feb 1;20(2):246–7. 
[^3]: Webb WB, Agnew HW. Stage 4 sleep: influence of time course variables. Science. 1971 Dec 24;174(4016):1354–6. 
[^4]: Yordanova J, Kolev V, Wagner U, Verleger R. Differential associations of early- and late-night sleep with functional brain states promoting insight to abstract task regularity. PloS One. 2010 Feb 26;5(2):e9442. 
[^5]: Drago V, Foster PS, Heilman KM, Aricò D, Williamson J, Montagna P, et al. Cyclic alternating pattern in sleep and its relationship to creativity. Sleep Med. 2011 Apr;12(4):361–6. 
[^6]: Dissel S. Drosophila as a Model to Study the Relationship Between Sleep, Plasticity, and Memory. Front Physiol [Internet]. 2020 [cited 2022 Jun 6];11. Available from:[https://www.frontiersin.org/article/10.3389/fphys.2020.00533](https://www.frontiersin.org/article/10.3389/fphys.2020.00533)
[^7]: Tainton-Heap LAL, Kirszenblat LC, Notaras ET, Grabowska MJ, Jeans R, Feng K, et al. A Paradoxical Kind of Sleep in Drosophila melanogaster. Curr Biol CB. 2021 Feb 8;31(3):578-590.e6. 
[^8]: van Alphen B, Yap MHW, Kirszenblat L, Kottler B, van Swinderen B. A Dynamic Deep Sleep Stage in Drosophila. J Neurosci. 2013 Apr 17;33(16):6917–27. 
[^9]: van Alphen B, Semenza ER, Yap M, van Swinderen B, Allada R. A deep sleep stage in Drosophila with a functional role in waste clearance. Sci Adv. 2021 Jan 20;7(4):eabc2999. 
[^10]: Geissmann Q, Rodriguez LG, Beckwith EJ, French AS, Jamasb AR, Gilestro GF. Ethoscopes: An open platform for high-throughput ethomics. PLOS Biol. 2017 Oct 19;15(10):e2003026. 


