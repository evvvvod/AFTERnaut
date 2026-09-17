AFTERnaut (Embodied Interaction with AFTER)
========

AFTERnaut is an interactive interface for exploration and embodied mapping of complex neural synthesis latent spaces. 
It combines latent space exploration, multimodal sensor data input, and interactive machine learning in a single, easy-to-navigate GUI.

[Link to paper](https://zenodo.org/records/22250842).

***Dependencies***

* [nn~](https://github.com/acids-ircam/nn_tilde/releases/tag/v1.6.0)
* [AFTER](https://github.com/acids-ircam/AFTER)
* [FluCoMa](https://github.com/flucoma) for datasets and machine learning
* [BBDMI](https://gitlab.huma-num.fr/bbdmi) for EMG input
* [PiPo](https://github.com/ircam-ismm/pipo) for Bayes filter

![Alt text](https://github.com/evvvvod/AFTERnaut/blob/main/AFTERnaut_v1_screenshot.png)

***Instructions***

Turn on DSP and activate the model in upper left of the patch.

Main Inputs: 

Select input source to use with the AFTER model:
* The audio player, where you can use preloaded files or drag and drop your own.
* The input oscillator, which sends either sine waves of square wave pulses at an adjustable frequency.
* External input to use a microphone or other external source.

Activate your chosen input, preview the raw sound if you wish. 
The AFTER model has a 2-3 second latency, after which you will hear its interpretation of the input.

Structure:

Bias or scale eight exposed latent dimensions of the model by moving the sliders or dials.
From the source dropdown you can also select Modulation, Sensors, or ML Model.
* Modulation: Uses the bank of oscillators in the modulation section of the patch to modulate the latent biasers and scalers. Each oscillator can be adjusted independently. 
* Sensors: Biasers and scalers follow sensor data readings (routed in the sensor section of the patch)
* ML Model: Biasers and scalers follow outputs from regression models trained on gesture data (described below)

Timbre:

Functions similarly to structure, but with only audio player input. 
By selecting Direct Set, users can also set latent dimensions manually using the biasers, and further scale those readings with scalers.

Diffusion Bias:

Performs a similar function to the biasers on the diffusion layer, but via a 2D interface, and only on a limited number of dimensions.

Modulators:

A bank of eight oscillators with adjustable frequency which can be routed to any bank of biasers or scalers.

Sensor Inputs:

Receives input from the [EAVI board](https://doi.org/10.13140/RG.2.2.36173.28646), taking electromyogram (EMG) readings, and [Mugic](https://www.mugicmotion.com/) IMU unit, sending gyroscope (x y z), accelerometer (x y z) and quaternions (w x y z).
EMG input is routed through the BBDMI library, offering a Bayesian filter for smoothing, and a calibration module.
We welcome others to modify the patch to use other types of sensor inputs.

Route Sensor Data:

Choose any combination of sensor data streams, route to an eight-value list. 
This in turn can be routed to any bank of eight biasers or scalers.
This also becomes an eight point vector for interactive machine learning.

Presets and Datasets:

Once you identify sounds you like from the blue sections of the patch, you can save these as presets via the pattr system and give them a numerical label.
You can then recall these and build three-part datasets, consisting of a label (the preset number), sensor data (eight point vector from sensor routing), and biasers and scalers (32 point vector of current slider and dial readings).
We recommend starting by demonstrating fixed gestural positions while using the sensors and taking snapshots, recalling a preset, and clicking Add Example.
You can save or load these presets and datasets as JSON files through the interface.

Machine Learning:

Classification models are trained on preset labels and sensor data, and predict presets for new sensor input.
Regression models are trained on sensor data and biaser scaler values, and output new biaser scaler values for new sensor input.
Train by clicking the button until the loss function is acceptable.
Save and load models as JSON.
