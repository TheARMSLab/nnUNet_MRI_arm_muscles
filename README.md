# nnUNet_MRI_arm_muscles [![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

Pretrained 3D nnU‑Net weights for segmentation of upper limb muscles from T1 in‑phase MRI.

## nnU-Net
* https://github.com/MIC-DKFZ/nnUNet
* Isensee, F., Jaeger, P. F., Kohl, S. A., Petersen, J., & Maier-Hein, K. H. (2021). nnU-Net: a self-configuring 
method for deep learning-based biomedical image segmentation. Nature methods, 18(2), 203-211.

## Datasets

Three previously published MRI datasets were used (healthy adults). Each dataset differs in anatomical coverage (forearm vs. shoulder/arm), number of muscles annotated, and coil type.

| Label | Source                 | Age ± SD (yrs) | Subjects (M/F) | Muscles | Total Segmentations | Coil Type    |
|------:|------------------------|----------------|----------------|--------:|---------------------:|--------------|
| A     | Holzbaur et al., 2007 | 28.6 ± 4.5     | 10 (5/5)       | 32      | 295                  | Arm & Body   |
| B     | Saul et al., 2015     | 53.2 ± 5.5     | 10 (5/5)       | 19      | 189                  | Arm & Body   |
| C     | Vidt et al., 2012     | 75.1 ± 4.3     | 19 (11/8)      | 12      | 222                  | Body         |

Specific scanner and sequence parameters can be found in source articles:

    A)  K. R. S. Holzbaur, W. M. Murray, G. E. Gold, and S. L. Delp, “Upper limb muscle volumes in adult subjects,” Journal of Biomechanics, vol. 40, no. 4, pp. 742–749, Jan. 2007, doi: 10.1016/j.jbiomech.2006.11.011.

    B)  K. R. Saul, M. E. Vidt, G. E. Gold, and W. M. Murray, “Upper Limb Strength and Muscle Volume in Healthy Middle-Aged Adults,” J Appl Biomech, vol. 31, no. 6, pp. 484–491, Dec. 2015, doi: 10.1123/jab.2014-0177.

    C)  M. E. Vidt, M. Daly, M. E. Miller, C. C. Davis, A. P. Marsh, and K. R. Saul, “Characterizing upper limb muscle volume and strength in older adults: a comparison with young adults,” J Biomech, vol. 45, no. 2, pp. 334–341, Jan. 2012, doi: 10.1016/j.jbiomech.2011.10.007.

## Model details

- Framework: **nnU‑Net** (3D full‑resolution), default settings
- Training: **5‑fold cross‑validation**
- **Three separate multiclass 3D nnU‑Net models** were trained to accommodate differences in muscle availability across datasets:
  - **Model 1** – Muscles present **only in Dataset A**  
  - **Model 2** – Muscles present in **Datasets A and B**  
  - **Model 3** – Muscles present in **Datasets A, B, and C**
> Although Model 1 predicts the full set of muscles contained in Model 2, it was trained only on Dataset A and therefore uses less training data for those shared muscles than Model 2

## Output muscle labels

**Model 1 (A only):**  
Forearm muscles
1. Anconeus (ANC)
2. Abductor pollicis longus (APL)  
3. Brachioradialis (BRD)
4. Extensor carpi radialis brevis (ECRB)
5. Extensor carpi radialis longus (ECRL)
6. Extensor carpi ulnaris (ECU)
7. Extensor digitorum communis (EDC)
8. Extensor digiti minimi (EDM)
9. Extensor indicis proprius (EIP)
10. Extensor pollicis brevis (EPB)
11. Extensor pollicis longus (EPL)  
12. Flexor carpi radialis (FCR)  
13. Flexor carpi ulnaris (FCU)
14. Flexor digitorum profundus (FDP)
15. Flexor digitorum superficialis (FDS)
16. Flexor pollicis longus (FPL)  
17. Pronator quadratus (PQ)  
18. Pronator teres (PT)  
19. Supinator (SUP)  

**Model 2 (AB — present in A and B):**  
Forearm muscles
1. Anconeus (ANC)  
2. Brachioradialis (BRD)  
3. Flexor carpi radialis (FCR)  
4. Flexor carpi ulnaris (FCU)  
5. Pronator quadratus (PQ)  
6. Pronator teres (PT)  
7. Supinator (SUP)  

**Model 3 (ABC — common to A, B, and C):**  
Shoulder & upper arm muscles
1. Biceps brachii (BIC)  
2. Brachialis (BRA)  
3. Coracobrachialis (COR)  
4. Deltoid (DELT)  
5. Infraspinatus (INFRA)  
6. Latissimus dorsi (LAT)  
7. Pectoralis major (PEC)  
8. Subscapularis (SUB)  
9. Supraspinatus (SUPRA)  
10. Teres major (TMAJ)  
11. Teres minor (TMIN)  
12. Triceps brachii (TRI)  

## Segmenting new MR images
1. **Install nnUNet**
    -  https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/installation_instructions.md
3. **Download the pretrained model(s)**
    -  The pretrained model zip files (one for each model, exported via nnUNetv1_export_model_to_zip) are contained in the releases associated with this repository.
    -  Click the releases link on the right side of the page and download the zip file(s) corresponding to the model(s) you want to use.
5. **Install the pretrained model(s)**
    -  Use this command for each model zip you downloaded (replace PATH_TO_ZIP):
    ######
        nnUNetv2_install_pretrained_model_from_zip PATH_TO_ZIP
4. **Prepare your MR images**:
    -  Convert your images to nifti file format (dataset_conversion.ipynb notebook in this repo helps with conversion from DICOM)
    -  Ensure filenames follow nnUNet's expected naming scheme: https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/dataset_format_inference.md
5. **Run inference with the desired model**
    -  Each model has its own inference instructions (see inference_instructions_model1/2/3.txt)

## Getting started
* Sample arm and body images are included in the releases page for testing your installation with correctly formatted images.

## Fine-tuning pre-trained models
* To use your own own segmentation data to fine-tune the performance of these pre-trained models, follow the instructions provided by nnUNet documentation:
* https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/pretraining_and_finetuning.md

## Recommendations
* If you are unfamiliar with/do not currently have Python installed, download the miniconda distribution (https://docs.anaconda.com/miniconda/install/) 
    * This enables you to create a virtual environment (https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html), activate it, then install the necessary packages (PyTorch, nnUNetv2)

## License
This project is licensed under the Apache License 2.0 — see [LICENSE](LICENSE) for details.

## Acknowledgments
The segmentation model is built on [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) (Apache License 2.0),
developed by the Division of Medical Image Computing, German Cancer Research Center (DKFZ).

> Isensee, F., Jaeger, P. F., Kohl, S. A., Petersen, J., & Maier-Hein, K. H. (2021).
> nnU-Net: a self-configuring method for deep learning-based biomedical image segmentation.
> *Nature Methods*, 18(2), 203-211.
