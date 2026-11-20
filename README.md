# AI-Based Phishing Website Detection

A Machine Learning and Deep Learning project that detects phishing websites by evaluating and comparing **10 classification algorithms** across 30 URL, domain, and HTML-based features.

## Overview
Phishing websites mimic legitimate platforms to steal sensitive user credentials. This project preprocesses a real-world phishing dataset, resolves duplicate/conflicting records, trains 10 distinct classifiers (from traditional ML models to a 1D Convolutional Neural Network and Soft Voting Ensemble), and exports the top-performing model for deployment.

## Dataset & Preprocessing
* **Format:** ARFF (`Training Dataset.arff`) containing **11,055 records** and **30 input features** (`having_IP_Address`, `URL_Length`, `SSLfinal_State`, `URL_of_Anchor`, `web_traffic`, etc.).
* **Data Cleaning:** Removed **5,206 exact duplicates** and **64 feature combinations with conflicting labels**, resulting in a clean, leak-free dataset of **5,721 unique records** (2,955 Phishing, 2,766 Legitimate).
* **Splitting & Scaling:** 80/20 stratified train-test split (4,576 training / 1,145 testing samples) scaled using `StandardScaler`.

## Model Performance Comparison
All 10 models were evaluated on the unseen test set (1,145 samples) and ranked by **F1-Score**:

| Rank | Algorithm | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| 1 | **Gradient Boosting** | **95.28%** | 96.05% | 94.75% | **95.40%** | 0.9903 |
| 2 | **Ensemble Learning (Soft Voting)** | 95.20% | 96.05% | 94.59% | 95.31% | 0.9912 |
| 3 | **Random Forest** | 95.20% | 96.69% | 93.91% | 95.28% | 0.9903 |
| 4 | **1D CNN (TensorFlow/Keras)** | 95.20% | **97.02%** | 93.57% | 95.26% | **0.9922** |
| 5 | **Decision Tree** | 93.97% | 94.24% | 94.08% | 94.16% | 0.9460 |
| 6 | **Support Vector Machine (SVM)** | 93.97% | 95.31% | 92.89% | 94.09% | 0.9860 |
| 7 | **Artificial Neural Network (MLP)** | 93.45% | 94.03% | 93.23% | 93.63% | 0.9868 |
| 8 | **K-Nearest Neighbors (KNN)** | 92.40% | 91.72% | 93.74% | 92.72% | 0.9765 |
| 9 | **Logistic Regression** | 91.27% | 91.82% | 91.20% | 91.51% | 0.9771 |
| 10 | **Naive Bayes (Gaussian)** | 64.98% | 59.58% | **100.00%** | 74.67% | 0.9673 |

### Key Takeaways
* **Best Overall Model:** **Gradient Boosting** achieved the highest F1-Score (**95.40%**) and Accuracy (**95.28%**), and was exported (`best_phishing_detection_model.pkl`) alongside `standard_scaler.pkl`.
* **Best Discrimination & Precision:** The **1D CNN** achieved the highest ROC-AUC (**0.9922**) and Precision (**97.02%**), minimizing false alarms on legitimate websites.

## Repository Structure
```text
├── AI_Phishing_Website_Detection.ipynb   # Main Google Colab notebook with EDA, training & plots
├── Training Dataset.arff                 # Raw dataset (11,055 samples, 30 features)
├── best_phishing_detection_model.pkl     # Saved Gradient Boosting model
├── standard_scaler.pkl                   # Saved StandardScaler for inference preprocessing
├── requirements.txt                      # Python dependencies
└── README.md                             # Project documentation
