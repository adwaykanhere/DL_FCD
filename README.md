[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1uJLONcGv5o2HQ24yVefU0GFJIFeijSCy?usp=sharing)

# Automatic segmentation of Focal Cortical Dysplasia(FCD) using deep convolutional neural network.

Focal Cortical Dysplasia (FCD) is a common congenital malformation of brain development. 

Moreover, it is a frequent effector for intractable seizures and medically refractory epilepsy, hence many patients are treated with surgery to remove the affected lesion.

 - While 65 million people suffer from epilepsy around the world, a third of them have drug-resistant epilepsy and thus still experience seizures while under medication. 
Effective treatment is only resective surgery of the area that causes seizures. 
- This treatment technique requires clear identification of the seizure areas with minimal risk to the patient.It is thus important to accurately locate the seizure onset for efficient pre-surgical planning using a non-invasive approach
- As such, the most common modality to assess patients with FCD is Magnetic Resonance (MR) imaging. 
Using MRI, we derive surface-based and volume-based features to develop an algorithm using convolutional neural networks (CNN) to predict the region of onset.
- On MRI, FCD is displayed as cortical thickening, T2/FLAIR hyperintensity, and blurring of grey matter junction although significant overlapping features are observed. 
- Correct identification of the FCD areas on the brain with good accuracy is thus of primal importance

**Dataset**: MRI Dataset of 20 patients with FCD was collected with T1 & T2-FLAIR images of the head of the patients.

**Pre-Processing**: Both the T1w and T2/FLAIR modalities were skull stripped to focus only on the brain region. Next, they were co-registered using the affine transform method. 
- Augmentation: 
  - To represent the clinical features of FCD such as blurring of grey-white matter junction and FLAIR grey/white matter hyperintensity, the T1w and T2/FLAIR MR data was used. 
  - To better differentiate the cortical thickening, we calculate interhemispheric asymmetry maps from the corresponding regions of the head. This calculates the relative change in asymmetry within the hemispheres, which has shown to be an important predictor of FCD

**Models used**: 
- Pretrained U-Net model
- Custom model (Refer file): 
  - This model consists of two independent CNNs which are optimized separately.
  - The first network learns to classify whether every voxel contains a region of the lesion and generates an initial estimate of the regions of FCD.
  - The output of the first network is then limited by a threshold of 0.2 to discard the regions having a low probability of lesional tissue. 
    The output of the first network is then used as a sampling prior for the second network. The second network is trained to reduce the probability of occurrence of false positives predicted by the first network.



