# Brain-MRI

## Data Source

<b> Brain MRI segmentation </b> : Brain MRI images together with manual FLAIR abnormality segmentation masks
This dataset contains brain MR images together with manual FLAIR abnormality segmentation masks.
The images were obtained from The Cancer Imaging Archive (TCIA).
They correspond to 110 patients included in The Cancer Genome Atlas (TCGA) lower-grade glioma collection with at least fluid-attenuated inversion recovery (FLAIR) sequence and genomic cluster data available.

## Data
### MRI Scan

<img src="https://github.com/orion29/Brain-MRI/blob/main/Images/mri.png"/>

### Mask

<img src="https://github.com/orion29/Brain-MRI/blob/main/Images/mri_mask.png"/>

## Pre-processing steps
<ul>
<li> Both Scanned Images and Masks were converted from int tensor (0-255) to float tensor (0-1) </li>
<li> Transfroms to Images and mask : <ul>
   <li>    flip </li>
   <li>    rotate </li>
   <li>    zoom </li>
   <li>    warp </li>
  <li>    lighting effects </li></ul>

</li>  
<li> Both Scanned Images and Masks were  normalized using imagenet stats .</li></ul><br>




## Training

### Model: UNET with Resnet-34 (pertained on cifar-10 imagenet model) as a backbone.
The <b> U-Net </b> is convolutional network architecture for fast and precise segmentation of images. It is an encoder-decoder style network.<br>
Using a U-Net with a pretrained resnet encoder means that the encoder part of the U-Net will be replaced by the resnet pretrained weights. It's a concept of transfer learning, i.e we don't need to train the model from scratch.<br>
<img src="https://github.com/orion29/Satellite-Image-Segmentation-for-Flood-Damage-Analysis/blob/main/Images/unet.png" width="600">

### Optimizer: ADAM

<b> Adaptive Moment Estimation (Adam) </b> is  an optimizer that computes adaptive learning rates for each parameter. In addition to storing an exponentially decaying average of past squared gradients vt like RMSprop, Adam also keeps an exponentially decaying average of past gradients mt, similar to momentum.
<li> gt =  Gradient Calculated </li>
<li> mt =  Momentum </li>
<li> vt =  RMSprop </li><br>
<img src="https://github.com/orion29/Satellite-Image-Segmentation-for-Flood-Damage-Analysis/blob/main/Images/moment.png" width="300">

### Scheduler: One Cycle Policy

The 1cycle policy has three steps:
We progressively increase our learning rate from base_lr to lr_max and at the same time we progressively decrease our momentum from mom_max to mom_min.

We do the exact opposite: we progressively decrease our learning rate from lr_max to lr_max/div_factor and at the same time we progressively increase our momentum from mom_min to mom_max.

We further decrease our learning rate from lr_max/div_factor to lr_max/(div_factor x 100) and we keep momentum steady at mom_max.
              			
<img src="https://github.com/orion29/Satellite-Image-Segmentation-for-Flood-Damage-Analysis/blob/main/Images/onefit.png"/>

### Training :

#### Segmentation Training  

Validation Set Dice score : 86%

## Predictions
 

<img src="https://github.com/orion29/Brain-MRI/blob/main/Images/Unknown.png"/>
          

