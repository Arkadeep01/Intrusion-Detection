# **Network Intrusion Detection System (NIDS) – Development Report**

## **1. Introduction**

With the rapid evolution of cyber threats, traditional signature-based security systems are no longer sufficient to detect sophisticated and zero-day attacks. This project focuses on designing and implementing a **machine learning-based Network Intrusion Detection System (NIDS)** capable of real-time detection, high accuracy, and explainability.

The system leverages a **hybrid detection approach**, combining supervised and unsupervised models to ensure both known and unknown threats are effectively identified.

---

## **2. Problem Statement**

Traditional intrusion detection systems suffer from the following limitations:

* Dependence on **predefined attack signatures**
* Inability to detect **zero-day or unknown attacks**
* Reactive rather than proactive detection
* Limited adaptability to evolving attack patterns

This project addresses these challenges by introducing a **data-driven, adaptive, and real-time detection mechanism**.

---

## **3. Proposed System Overview**

The proposed system operates as a **real-time hybrid intrusion detection engine** with the following workflow:

1. **Data Ingestion**

   * Network flow data is received and processed in real-time.

2. **Preprocessing Pipeline**

   * Data cleaning, normalization, and feature scaling
   * Handling missing, infinite, and inconsistent values
   * Removal of duplicate and redundant records

3. **Model Architecture**

   * **XGBoost Classifier (Supervised Model)**

     * Detects known attack patterns with high precision
   * **Isolation Forest (Unsupervised Model)**

     * Identifies anomalous behavior (potential unknown threats)

4. **Detection Mechanism**

   * The system classifies traffic into:

     * Normal traffic
     * Malicious activity

5. **Explainability**

   * Feature importance is extracted to explain model decisions

6. **Output**

   * Results are stored and made available for dashboard visualization

---

## **4. Data Processing and Preparation**

The dataset was processed using the following steps:

* Chunk-based loading to handle large-scale data efficiently
* Conversion of all features to numeric format
* Removal of:

  * NaN and infinite values
  * Duplicate records
  * Constant (non-informative) features
* Outlier handling using percentile clipping
* Final dataset:

  * **Samples:** ~785,000
  * **Features:** 65

---

## **5. Model Training Pipeline**

### **5.1 Data Split**

* Training: 70%
* Testing: 30%
* Stratified sampling to preserve class distribution

### **5.2 Class Imbalance Handling**

* Applied **SMOTE (Synthetic Minority Oversampling Technique)**
* Balanced dataset:

  * Before: Highly skewed
  * After: Equal representation of classes

### **5.3 Feature Scaling**

* StandardScaler applied for normalization

---

## **6. Model Implementation**

### **6.1 XGBoost Classifier**

* Parameters:

  * n_estimators = 300
  * max_depth = 8
  * learning_rate = 0.05
* Role:

  * Primary detection model
  * Handles complex feature interactions

### **6.2 Isolation Forest**

* Used for anomaly detection
* Detects unusual traffic patterns beyond labeled data

---

## **7. Performance Evaluation**

### **7.1 Key Metrics**

| Metric    | Value  |
| --------- | ------ |
| Accuracy  | 99.90% |
| Precision | 0.9952 |
| Recall    | 0.9993 |
| F1 Score  | 0.9973 |

---

### **7.2 Confusion Matrix**

|               | Pred Normal | Pred Attack |
| ------------- | ----------- | ----------- |
| Actual Normal | 193,975     | 200         |
| Actual Attack | 28          | 41,581      |

**Observation:**

* Extremely low false negatives (critical for security)
* Very high detection reliability

---

### **7.3 ROC & PR Analysis**

* **ROC-AUC:** ~1.0000
* **PR-AUC:** ~0.9999

This indicates near-perfect classification capability.

---

## **8. Feature Importance Insights**

Top contributing features include:

* Average Packet Size
* Bwd Packet Length Std
* Packet Length Variance
* Max Packet Length
* Header Length metrics

These features significantly influence intrusion detection decisions.

---

## **9. System Strengths**

### **Hybrid Detection**

* Combines strengths of supervised and unsupervised learning

### **High Accuracy**

* Achieves near-perfect detection rates

### **Real-Time Capability**

* Designed for live network traffic monitoring

### **Explainability**

* Provides insight into why a flow is flagged as malicious

### **Scalability**

* Handles large datasets efficiently

---

## **10. Limitations and Considerations**

* Requires periodic retraining for evolving threats
* Performance depends on feature quality
* Real-time deployment requires optimized infrastructure

---

## **11. Conclusion**

The developed NIDS demonstrates **high accuracy, robustness, and scalability**, making it suitable for deployment in modern network environments.

The system is now **technically complete on the backend**, and the next logical step is to build a **user-facing web interface** to enable monitoring, visualization, and operational use.

---
