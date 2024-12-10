# nnUNet_MRI_arm_muscles
This repository contains weights for pretrained nnUNet models for upper limb muscle segmentation of T1 in phase MR images.

## Training data
nnUNets were trained on in phase images of **A)** the shoulder and upper arm (n=38, age 25-83 [1-3]) and **B)** the forearm (n=20, age 25-60 [1,2]) of healthy adult subjects.

Images were obtained with 1T MRI instruments; shoulder/arm images used a body coil, forearm images used a longbone coil. Specific scanner and sequence parameters can be found in source articles:
1. K. R. S. Holzbaur, W. M. Murray, G. E. Gold, and S. L. Delp, “Upper limb muscle volumes in adult subjects,” Journal of Biomechanics, vol. 40, no. 4, pp. 742–749, Jan. 2007, doi: 10.1016/j.jbiomech.2006.11.011.
2. K. R. Saul, M. E. Vidt, G. E. Gold, and W. M. Murray, “Upper Limb Strength and Muscle Volume in Healthy Middle-Aged Adults,” J Appl Biomech, vol. 31, no. 6, pp. 484–491, Dec. 2015, doi: 10.1123/jab.2014-0177.
3. M. E. Vidt, M. Daly, M. E. Miller, C. C. Davis, A. P. Marsh, and K. R. Saul, “Characterizing upper limb muscle volume and strength in older adults: a comparison with young adults,” J Biomech, vol. 45, no. 2, pp. 334–341, Jan. 2012, doi: 10.1016/j.jbiomech.2011.10.007.

## nnUNet settings
Default nnUNet settings were used for training (trained Aug '24). The weights are the result of training 3D models with 5 fold cross validation. Separate models were trained for the shoulder/upper arm and forearm regions due to imaging coil and resolution differences.

The models were trained on and output labels for the following muscles.

**A) Shoulder and Upper Arm**
1. Biceps brachii
2. Brachialis
3. Coracobrachialis
4. Deltoid
5. Infraspinatus
6. Latissimus dorsi
7. Pectoralis major
8. Subscapularis
9. Supraspinatus
10. Teres major
11. Teres minor
12. Triceps brachii

**B) Forearm**
1. Anconeus
2. Brachioradialis
3. Flexor carpi radialis
4. Flexor carpi ulnaris
5. Pronator quadratus
6. Pronator teres
7. Supinator

## How to use the model to segment new MR images
1. Install nnUNet: https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/installation_instructions.md
2. Download the zip file in this repository containing the trained model weights (created using the nnUNetv1_export_model_to_zip command).
3. Import the trained model using the command ```nnUNetv2_install_pretrained_model_from_zip PATH_TO_ZIP```
