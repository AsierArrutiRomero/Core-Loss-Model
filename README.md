# Core-Loss-Model
This repository recolects informations, resources and advancements regarding core loss modelling.

## Composite Improved Generalised Steinmetz Equation
The Composite Improved Generalised Steinmetz Equation (ciGSE) is the main core loss model developed by Mondragon University. As the name suggest, the model combines two previous works:

1. The Composite Waveform Hypothesis (CWH) |REF|: main working principle for the model, responsible for the improved accuracy under different waveforms.
2. The Improved Generalised Steinmetz Equation (iGSE) |REF|: main mathematical foundation for the model, relating the model with other works from the Steinmetz Equation family of models.

Originally the model was presented with a heavier enphasis in the CWH by using high order polynomials to define the losses per segment |REF|, but further refinements and optimizations of the models made for the MagNet Challenge |REF| allow for a far simpler and accurate representation of the model.

According to the ciGSE, the losses are

$P=\Sigma[D·(P_{qs}+P_{mr})]$



Repositery with all relevant work regarding core loss modelling.

This repository is currently under work, and will be updated with:

a) all relevant information regarding the work published in APEC 2026 before the event, including  
   a.1) datasets used for the models  
   a.2) relevant results and model accuracies compared with original datasets  
   a.3) examples of application for different waveforms  
   a.4) shareable loss functions  

b) additional relevant information as the model is improved and updated

![til](./resources/GIF_triangular.gif)
