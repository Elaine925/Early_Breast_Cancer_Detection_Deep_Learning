# Early Breast Cancer Detection Deep Learning



## Problem Statement

Utilizing low-dose X-rays of the breast, known as [mammograms](https://www.ucsfhealth.org/programs/screening-mammogram), can detect subtle abnormalities in breast tissue long before they become perceptible. Regular screening mammograms are essential for most women as they offer the most reliable means of early breast cancer detection, significantly improving treatment outcomes. Despite advancements, breast cancer remains a significant threat, with approximately [42,250](https://www.cancer.org/cancer/types/breast-cancer/about/how-common-is-breast-cancer.html) women projected to succumb to it in the United States in 2024. To mitigate the risk of incorrect interpretations and missed cases, diverse deep learning techniques are being employed to develop systems capable of detecting breast cancer in mammograms. These systems aim to assist physicians in achieving early detection and prompt intervention.



## Data Dictionary

| Field Name       | Description                                               |  Type |
|------------------|--------------------------------|-----------|
| Patient_ID       | Unique identifier for each patient               | String    | 
| Breast_density   | The amount of fibrous and glandular tissue in a woman’s breasts compared with the amount of fatty tissue in the breasts, as seen on a mammogram| Integer   |
| mass_shape       | Shape of the mass                                | String    | 
| mass_margins     | Margins of the mass                              | String    | 
| assessment       | Breast Imaging Reporting and Data System result category| String    | 
| pathology        | Pathology results of the lump                    | String    |
| image_file_path  | Full mammography images path  | String    | 



## Executive Summary


### Project objective
The project aims to develop a computer-aided detection (CADe) and diagnosis (CADx) system to aid radiologists in interpreting mammograms [source](https://www.nature.com/articles/sdata2017177). Although CADx systems for mammography are not currently approved for clinical use, this study seeks to reduce false-positive rates and facilitate the evaluation of decision support systems.
 

### Methodology  

The methodology involves several steps:   

1. Images Path Redirect:
    * Implement Hashmap to manage full image paths, cropped image paths, and ROI mask image paths.
    * Path updates are systematically applied to both Mass and Calcification description tables, ensuring seamless data integration.
2. Data Cleaning:
    * Streamline the management of full image, cropped image, and ROI mask image local pathways within Mass and Calcification tables/CSV.
    * Handling NULL values involves employing the next valid observation to fill gaps, optimizing data integrity.
3. Exploratory Data Analysis (EDA):
    * In-depth analysis delves into the distribution of Malignant, Benign, and Benign without callback cases, providing crucial insights into pathology occurrences.
    * Detailed examination of BI-RADS assessment, Breast Density, and Mass Shape/Calcification Type across all pathology results for Mass and Calcification tables informs subsequent decision-making processes. and Calcification tables. tables
4. Restructure Image folder files:
    * Undertaking a meticulous restructuring of the original image folder layout to enhance organizational efficiency.
    * The restructured framework categorizes images into Train (for model training) and Test (for evaluation), with further subdivisions based on Mass and Calcification categories.
5. Preprocess images:
    * Standardizing image sizes through reshaping enhances computational efficiency and ensures consistency in subsequent analyses.
    * Binary labeling (Benign/Malignant) facilitates streamlined classification tasks, optimizing model performance.
6. Train-Validation Split:
    * Data segmentation into distinct training and validation sets enables rigorous assessment of model performance across Mass and Calcification images, ensuring robust generalization capabilities.
7. Model Selection:
    * Approach involves the selection and evaluation of various Convolutional Neural Network (CNN) models.
    * Models include a basic CNN, augmented with data augmentation techniques, as well as pretrained architectures such as ResNet50 and VGG16, enabling comprehensive exploration of diverse methodologies.
8. Model Evaluation:
    * Training each CNN model on the designated training data and evaluating against validation datasets provides crucial performance metrics.
    * Assessment metrics, including accuracy, offer quantitative insights into the efficacy of each model variant.
9. Test Image Prediction:
    * Leveraging the best-performing model, conduct predictions on test images to validate performance.
10. Prediction Result Evaluation:
    * Rigorous evaluation of model performance on test images employs established metrics such as confusion matrices and F1 scores, providing a comprehensive assessment of diagnostic efficacy.




### Key Findings

After extensive model training and evaluation on both Mass and Calcification datasets, the following performance metrics were obtained:

|   Image Category  |    Model   |   Training Images Accuracy   |   Validation Images Accuracy  |
|-------------------|------------|------------------------------|-------------------------------|
|   Mass            |  Basic CNN |  0.584           |0.595     |
| | CNN with data augmentation|0.530|0.557|
| | ResNet50 pretrained architecture|0.512|0.518|
| | VGG16 pretrained architecture|0.514|0.580|
|   Calcification   |  Basic CNN |  0.763           |0.606     |
| | CNN with data augmentation|0.601| 0.607|
| | ResNet50 pretrained architecture|0.618|0.610|
| | VGG16 pretrained architecture|0.605|0.614|


These findings provide insights into the performance of different models across Mass and Calcification datasets, highlighting variations in training and test accuracies. Further analysis and fine-tuning may be required to optimize model performance and enhance diagnostic capabilities.




## Conclusion and Improvement

In this study, an extensive examination of mammogram data and images is conducted, utilizing a variety of deep learning models to mass and calcification mammography images for cancer detection. The investigation unveiled discrepancies in model performance between the training, validation and later on testify on testing images.

While certain models exhibited promising performance during the training phase, the CNN model demonstrated moderate accuracy, displaying slightly superior results in overall cancer detection across both calcification and mass images. However, the task was challenging due to the high resolution of the images, with dimensions exceeding 4000 pixels by 4000 pixels. Initially, preprocessing involved resizing the images to *224x224*, which led to a decrease in accuracy due to pixel loss. Subsequently, adjustments were made to reshape the images to *512x512*, resulting in a modest improvement in accuracy, albeit not significantly.

Furthermore, when applying this model to testing images,  an F1 score of 0.416 for mass cases and 0.4 for calcification cases were achieved. While these results fall short of ideal for breast cancer detection, additional efforts were made to enhance images through the use of CLAHE (Contrast Limited Adaptive Histogram Equalization) for preprocessing. This technique effectively increased the contrast of the images, potentially improving the model's ability to detect abnormalities.

Future improvement should prioritize the enhancement of mammography images to improve diagnostic accuracy and enable early detection of breast cancer. This can be achieved by implementing advanced image processing techniques such as Contrast Limited Adaptive Histogram Equalization (CLAHE), Gamma correction, and other methods that enhance image contrast and clarity. Simultaneously, fine-tuning the parameters of Convolutional Neural Network (CNN) models is crucial, and leveraging pretrained models such as MobileNet can offer significant advantages. By integrating these approaches, future research can achieve substantial improvements in overall accuracy and facilitate earlier detection of breast cancer.





#### **Citations**

Data Citation: Sawyer-Lee, R., Gimenez, F., Hoogi, A., & Rubin, D. (2016). Curated Breast Imaging Subset of Digital Database for Screening Mammography (CBIS-DDSM) [Data set]. The Cancer Imaging Archive. https://doi.org/10.7937/K9/TCIA.2016.7O02S9CY

Screening Mammography Images: [Source](https://www.cancerimagingarchive.net/collection/cbis-ddsm/)  
Mass-Train-Description.csv: [Source](https://www.cancerimagingarchive.net/collection/cbis-ddsm/)  
Calc-Training-Description.csv: [Source](https://www.cancerimagingarchive.net/collection/cbis-ddsm/)  
Mass-Test-Description.csv: [Source](https://www.cancerimagingarchive.net/collection/cbis-ddsm/)  
Calc-Test-Description.csv: [Source](https://www.cancerimagingarchive.net/collection/cbis-ddsm/)  
DICOM-info.csv

Publication Citation:  
Rebecca Sawyer Lee, Francisco Gimenez, Assaf Hoogi, Kanae Kawai Miyake, Mia Gorovoy & Daniel L. Rubin. (2017) **A curated mammography data set for use in computer-aided detection and diagnosis research**. Scientific Data volume 4, Article number: 170177 DOI: https://doi.org/10.1038/sdata.2017.177


TCIA Citation:   
Clark K, Vendt B, Smith K, Freymann J, Kirby J, Koppel P, Moore S, Phillips S, Maffitt D, Pringle M, Tarbox L, Prior F. The Cancer Imaging Archive (TCIA): Maintaining and Operating a Public Information Repository, Journal of Digital Imaging, Volume 26, Number 6, December, 2013, pp 1045-1057. DOI: https://doi.org/10.1007/s10278-013-9622-7*
