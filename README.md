# Smart-Agriculture: Tomato Disease Detection & Classification

### Motivation:
Pesticide sales alone account for over $400 million in annual control expenses and some bugs develop resistance to more than a hundred chemical compounds, making them the most resilient arthropods. Plant diseases can be detected automatically using image processing techniques, reducing the amount of surveillance needed on large plant farms and allowing for proper response in the early stages, such as when symptoms appear on plant leaves.

Detecting the symptoms in a timely manner can help evaluate the seriousness of the disease and in turn help in choosing the best approach in dealing with the disease.

### Project Overview
This project implements a **Hybrid Approach** for detecting and classifying diseases in Tomato leaves. It combines traditional Image Processing for segmentation with Machine Learning for classification.

**Target Diseases:**
1.  **Tomato Bacterial Spot**
2.  **Tomato Early Blight**
3.  **Tomato Late Blight**

### Methodology

#### 1. Image Segmentation
The goal is to isolate the disease lesion from the leaf background.
*   **Preprocessing:** Images are resized to a standard width (800px) and smoothed using Gaussian Blur.
*   **Color Thresholding:** The image is converted to the **LAB color space**. We assume disease spots often differ significantly in the red-green component. Otsu's thresholding is applied specifically to the **'a' channel** to separate the reddish/brown lesions from the green leaf tissues.
*   **Refinement:** Morphological operations (Closing and Opening) are used to remove noise and fill gaps in the mask.

#### 2. Feature Extraction
From each segmented lesion, a 27-dimensional feature vector is extracted:
*   **Shape:** Area, Perimeter, Circularity.
*   **Color:** Mean Color intensity (BGR) and HSV Histograms (Hue and Saturation bins).
*   **Texture:** Gray-Level Co-occurrence Matrix (GLCM) properties including Contrast, Dissimilarity, Homogeneity, Energy, and Correlation are computed on the quantized grayscale ROI.

#### 3. Classification
Two supervised learning models were trained and compared using the extracted features:
*   **Random Forest Classifier:** Optimized using GridSearchCV (tuning estimators, depth, split criteria).
*   **Support Vector Machine (SVM):** Used as a benchmark with an RBF kernel.

### Flowchart
![image](https://user-images.githubusercontent.com/64474195/124127556-7ef88600-da99-11eb-857e-132462b0066a.png)

### Results
The project compares the accuracy of Random Forest and SVM on a test set (20% split). Confusion matrices are generated to analyze misclassifications.

![image](https://user-images.githubusercontent.com/64474195/124126860-ba468500-da98-11eb-8600-314eeae62bcb.png)
