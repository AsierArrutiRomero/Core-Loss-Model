# Core-Loss-Model
This repository recolects informations, resources and advancements regarding core loss modelling.

## Composite Improved Generalised Steinmetz Equation
![til](./resources/GIF_triangular.gif)

### Description of the ciGSE

The Composite Improved Generalised Steinmetz Equation (ciGSE) is the main core loss model developed by Mondragon University. As the name suggest, the model combines two previous works:

1. The Composite Waveform Hypothesis (CWH) |CWH|: main working principle for the model, responsible for the improved accuracy under different waveforms.
2. The Improved Generalised Steinmetz Equation (iGSE) |iGSE|: main mathematical foundation for the model, relating the model with other works from the Steinmetz Equation family of models.

According to the CWH, the per cycle energy losses $E$ in a magnetization waveform is the summation of the energy loss contributions $E_{i}$ of its different segments

$E=\sum_{i}E_{i}$

or rewritten for power losses $P_{i}$ instead of energy

$P=\sum_{i}D_{i}·P_{i}$

where $D_{i}$ are the duration factors of the different segments, thus $\sum_{i}[D_{i}]=1$. The CWH was demonstrated to be accurate along a wide data range |ciGSE_poly|, so the key to generate an accurate an usable model is to define the power loss function for $P_{i}$. Initially high order polynomials |ciGSE_poly| where proposed, but this results in a high number of parameters required and high error when extrapolation is used.

During the MagNet Challenge 2023 |MagNet_Challenge1| a dual-plane approach that closer resembles the iGSE |ciGSE_MagNet| was proposed.

$\ln(P_{1})=k_1+{a_1}·\ln({|\Delta B/\Delta t|})+{b_1}·\ln(B_{pp})$

$\ln(P_{2})=k_2+{a_2}·\ln({|\Delta B/\Delta t|})+{b_2}·\ln(B_{pp})$

$P=P_{1}+P_{2}=\exp(k_1)·{|\Delta B/\Delta t|}^{a_1}·B_{pp}^{b_1}+\exp(k_2)·{|\Delta B/\Delta t|}^{a_2}·B_{pp}^{b_2}$

The factors $k_1$, $a_1$, $b_1$, $k_2$, $a_2$, and $b_2$ are parametrized from datasets available at the MagNet database. Due to its similarity with the iGSE, which also models losses as functions of $|\Delta B/\Delta t|$ and $B_{pp}$, these parameters can be related with the iGSE Steinmetz parameters

$a = \alpha$, $b = \beta$, $\exp(k)=k_{i}$

When evaluating the results, some correlation between the different materials are found out for these parameters

$\alpha_1 \approx 1$, $\alpha_2 \approx 2$, $\beta_2 \approx 2$

These values demonstrate a direct correlation with the dual plane approach and the hysteresis/eddy loss separation proposed by Charles Proteus Steinmetz on 1984, where the losses should take the form

$P=\eta_{hyst}·f^1·B^{\beta}+\eta_{eddy}·f^2·B^2$

Due to this, the dual plane approach is redefined, so that the power losses of each segment are the contribution of two different sources,

1. The quasi-static losses dominant at low frequencies, analogue to Steinmetz's hysteresis losses. $P_1=\exp(k_1)·{|\Delta B/\Delta t|}^{a_1}·B_{pp}^{b_1}$ → $P_{qs}=\exp(k_{qs})·{|\Delta B/\Delta t|}^{a_{qs}}·B_{pp}^{b_{qs}}$
2. The magnetization-rate losses dominant at high frequencies, analogue to Steinmetz's eddy losses. $P_2=\exp(k_2)·{|\Delta B/\Delta t|}^{a_2}·B_{pp}^{b_2}$ → $P_{mr}=\exp(k_{mr})·{|\Delta B/\Delta t|}^{a_{mr}}·B_{pp}^{b_{mr}}$

The complete ciGSE equation is thus:

$P=\sum_{i}D_{i}·[\exp(k_{qs})·{|\Delta B/\Delta t|}^{a_{qs}}·B_{pp}^{b_{qs}}+\exp(k_{mr})·{|\Delta B/\Delta t|}^{a_{mr}}·B_{pp}^{b_{mr}}]$

### Accuracy of the model
#### Triangular waveforms
The relative error distributions for the different materials are as following:

| Material | Temperature | $E_{RMS}$ | $E_{P_{5%}}$ | $E_{P}_{95%}$ |
| --- | --- | --- | --- | --- |
| N87 | 25 ºC | X | X | X |
| N87 | 50 ºC | Y | Y | Y |

### ciGSE parameters obtained from the MagNet database
The parameters fitted from the MagNet database are classified per tempaerature and DC bias. 

## Relaxation aware ciGSE

## DC magnetization aware ciGSE




Repositery with all relevant work regarding core loss modelling.

This repository is currently under work, and will be updated with:

a) all relevant information regarding the work published in APEC 2026 before the event, including  
   a.1) datasets used for the models  
   a.2) relevant results and model accuracies compared with original datasets  
   a.3) examples of application for different waveforms  
   a.4) shareable loss functions  

b) additional relevant information as the model is improved and updated

![til](./resources/GIF_triangular.gif)
