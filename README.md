# Core-Loss-Model
This repository recolects informations, resources and advancements regarding core loss modelling.

## Composite Improved Generalised Steinmetz Equation
![til](./resources/GIF_triangular.gif)

### Description of the ciGSE

The Composite Improved Generalised Steinmetz Equation (ciGSE) is the main core loss model developed by Mondragon University. As the name suggest, the model combines two previous works:

1. The Composite Waveform Hypothesis (CWH) |CWH|: main working principle for the model, responsible for the improved accuracy under different waveforms.
2. The Improved Generalised Steinmetz Equation (iGSE) |iGSE|: main mathematical foundation for the model, relating the model with other works from the Steinmetz Equation family of models.

According to the CWH, the per cycle energy losses $E$ in a magnetization waveform is the summation of the energy loss contributions $E_{i}$ of its different segments

$$E=\sum_{i}E_{i}$$

or rewritten for power losses $P_{i}$ instead of energy

$$P=\sum_{i}D_{i}·P_{i}$$

where $D_{i}$ are the duration factors of the different segments, thus $\sum_{i}[D_{i}]=1$. The CWH was demonstrated to be accurate along a wide data range |ciGSE_poly|, so the key to generate an accurate an usable model is to define the power loss function for $P_{i}$. Initially high order polynomials |ciGSE_poly| where proposed, but this results in a high number of parameters required and high error when extrapolation is used.

During the MagNet Challenge 2023 |MagNet_Challenge1| a dual-plane approach that closer resembles the iGSE |ciGSE_MagNet| was proposed.

$$\ln(P_{1})=k_1+{a_1}·\ln{\left|\frac{\Delta B}{\Delta t}\right|}+{b_1}·\ln(B_{pp})$$

$$\ln(P_{2})=k_2+{a_2}·\ln{\left|\frac{\Delta B}{\Delta t}\right|}+{b_2}·\ln(B_{pp})$$

$$P=P_{1}+P_{2}=\exp(k_1)·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_1}·B_{pp}^{b_1}+\exp(k_2)·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_2}·B_{pp}^{b_2}$$

The factors $k_1$, $a_1$, $b_1$, $k_2$, $a_2$, and $b_2$ are parametrized from datasets available at the MagNet database. Due to its similarity with the iGSE, which also models losses as functions of $|\Delta B/\Delta t|$ and $B_{pp}$, these parameters can be related with the iGSE Steinmetz parameters

$a = \alpha$, $b = \beta-\alpha$, $\exp(k)=k_{i}$

When evaluating the results, some correlation between the different materials are found out for these parameters

$\alpha_1 \approx 1$, $\alpha_2 \approx 2$, $\beta_2 \approx 2$

These values demonstrate a direct correlation with the dual plane approach and the hysteresis/eddy loss separation proposed by Charles Proteus Steinmetz on 1984, where the losses should take the form

$$P=\eta_{hyst}·f^1·B^{\beta}+\eta_{eddy}·f^2·B^2$$

Due to this, the dual plane approach is redefined, so that the power losses of each segment are the contribution of two different sources,

1. The quasi-static losses dominant at low frequencies, analogue to Steinmetz's hysteresis losses. $P_1=\exp(k_1)·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_1}·B_{pp}^{b_1}$ → $P_{qs}=\exp(k_{qs})·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_{qs}}·B_{pp}^{b_{qs}}$
2. The magnetization-rate losses dominant at high frequencies, analogue to Steinmetz's eddy losses. $P_2=\exp(k_2)·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_2}·B_{pp}^{b_2}$ → $P_{mr}=\exp(k_{mr})·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_{mr}}·B_{pp}^{b_{mr}}$

The complete ciGSE equation is thus:

$$P=\sum_{i}D_{i}·[\exp(k_{qs})·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_{qs}}·B_{pp}^{b_{qs}}+\exp(k_{mr})·{\left|\frac{\Delta B}{\Delta t}\right|}^{a_{mr}}·B_{pp}^{b_{mr}}]$$

### Accuracy of the model
#### Triangular waveforms
The relative error distributions for the different materials are as following:

| Material | Temperature [ºC] | $H_{DC}$ [A/m] | $E_{RMS}$ [%] | $E_{P5}$ [%] | $E_{P95}$ [%] | $E_{worst}$ [%] |
| ---      | ---              | ---            | ---           | ---              | ---               | ---             |
| N87      | 25               | 0              | 6.06          | -8.24            | +10.9             | -27.6           |
| N87      | 50               | 0              | 5.40          | -7.74            | +8.07             | -21.3           |
| N87      | 70               | 0              | 5.78          | -10.3            | +8.77             | -20.2           |
| N87      | 90               | 0              | 6.93          | -11.9            | +10.5             | -20.6           |

### ciGSE parameters obtained from the MagNet database
The parameters fitted from the MagNet database are classified per tempaerature and DC bias. 
| Material | Temperature [ºC] | $H_{DC}$ [A/m] | $k_{qs}$ | $a_{qs}$ | $b_{qs}$ | $k_{qs}$ | $a_{qs}$ | $b_{qs}$ |
| ---      | ---              | ---            | ---      | ---      | ---      | ---      | ---      | ---      |
| N87 | 25 | 0 | 5.4672 | 0.8237 | 1.6226 | -15.6965 | 2.4333 | 0.0252 |
| N87 | 50 | 0 | 2.8063 | 1.0411 | 1.6025 | -17.3231 | 2.5099 | -0.2492 |
| N87 | 70 | 0 | 1.6620 | 1.1377 | 1.7312 | -16.9025 | 2.4634 | -0.3003 |
| N87 | 90 | 0 | 0.4493 | 1.2472 | 1.8876 | -16.2839 | 2.4133 | -0.3230 |
| N49 | 25 | 0 | 2.6408 | 1.1209 | 2.0333 | -23.8149 | 2.8417 | -0.5868 |
| N49 | 50 | 0 | 1.9322 | 1.1897 | 2.1696 | -25.3756 | 2.9400 | -0.7468 |
| N49 | 70 | 0 | 1.8411 | 1.2054 | 2.1254 | -24.8325 | 2.9072 | -0.7336 |
| N49 | 90 | 0 | 2.1401 | 1.1879 | 2.0091 | -23.6194 | 2.8471 | -0.6186 |
| 3C94 | 25 | 0 | 2.5831 | 1.0273 | 1.4527 | -16.1004 | 2.4004 | -0.1329 |
| 3C94 | 50 | 0 | 0.9304 | 1.1520 | 1.6510 | -15.2556 | 2.3203 | -0.1948 |
| 3C94 | 70 | 0 | -0.2713 | 1.2543 | 1.9247 | -14.4659 | 2.2540 | -0.1876 |
| 3C94 | 90 | 0 | -1.7937 | 1.3946 | 2.1164 | -14.4882 | 2.2492 | -0.2146 |
| 3C90 | 25 | 0 | 3.5829 | 0.9707 | 1.5885 | -17.5029 | 2.5039 | -0.1798 |
| 3C90 | 50 | 0 | 2.1718 | 1.0836 | 1.7513 | -17.3730 | 2.4717 | -0.3133 |
| 3C90 | 70 | 0 | 1.4292 | 1.1529 | 1.9996 | -16.8907 | 2.4300 | -0.3263 |
| 3C90 | 90 | 0 | 0.4158 | 1.2518 | 2.1776 | -16.5997 | 2.4065 | -0.3306 |


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
