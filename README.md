# Biomass Moisture Prediction Using Machine Learning and NIR Spectroscopy

## 📌 Overview

This repository contains code and analysis for predicting **biomass moisture content** using **Near-Infrared (NIR) Spectroscopy** and **Machine Learning (ML)** models. Traditional moisture measurement methods are slow and costly, whereas **NIR combined with ML** provides a **fast, non-destructive, and cost-effective alternative**.

### 🔬 **Key Components**
- **Data Preprocessing:** Smoothing, scatter correction, and outlier removal.
- **Machine Learning Models:** Partial Least Squares Regression (PLS), Support Vector Regression (SVR), and Artificial Neural Networks (ANN).
- **Performance Evaluation:** R², RMSE, and bias for assessing predictive accuracy.

---

## Exploratory Data Analysis

![image](https://github.com/user-attachments/assets/887a5bf2-5907-47b4-b6a4-d53c1cadf195)

Key Observations from the EDA:

- A clear separation in moisture content levels was
  observed across different principal components,
  indicating that moisture content influences spectral
  variations significantly.

- PC1 showcased the highest correlation with the
  target variable, Moisture due to the clear upward
  trend.

- The presence of overlapping clusters suggests that
  while spectral data is useful for moisture prediction,
  some preprocessing and dimensionality reduction
  are necessary to enhance separation.

- Some spectra exhibited extreme deviations from the
  general trend, which warranted outlier detection
  and removal using PLS Q-residuals and
  Hotelling’s T-squared statistics.

---

## Data Preprocessing

### **Outlier Removal using PLS Regression**

![image](https://github.com/user-attachments/assets/c324d7f6-3596-41bb-ba9f-b865f4c5be3f)

- Outliers can distort the calibration and
prediction accuracy of machine-learning models. In this
study, Partial Least Squares (PLS) regression combined with
two key statistical measures—Q-residuals and Hotelling’s Tsquared—were used to systematically detect and remove
outliers. The outliers are detected using a 95% confidence
interval and a scatter Q-residuals VS Hotelling’s T-squared
was created which marks the position of the confidence level
in both axes.

**Savitzky-Golay (SV-GOL) Smoothing**

- The original absorbance value
distribution is noisy, and by applying different SV-Gol filters
with varying window sizes and polynomials, various degrees
of smoothness in data were achieved

  - The blue line is the original spectrum.
  - The red line shows a mild smoothing
  - The green line represents more aggressive
  smoothing
  - The magenta line is a more optimal choice of
  parameters.

- Therefore, by analyzing these variations, the optimal window
size and polynomial values were selected as 21 and 6
respectively to be applied in the SV-Gol smoothing filter

![image](https://github.com/user-attachments/assets/15377d1c-82f2-4d77-b0ee-083856318bad)


### **Scatter correction using SNV**

- SNV correction is particularly useful in
cases where scattering causes spectral variations unrelated to
moisture content. By standardizing spectra, SNV ensures that
any differences in absorbance are primarily due to chemical
composition rather than physical variations in the sample.

![image](https://github.com/user-attachments/assets/106635e0-b039-4fac-827a-e972b5425952)

### **Scatter correction using MSC**

- MSC is effective in reducing the impact
of sample heterogeneity on spectral data. By aligning spectra
to a common reference, it improves model performance by
ensuring that the differences observed are due to the analyte
of interest rather than external scattering effects.

![image](https://github.com/user-attachments/assets/feeee3a0-d680-491d-94ed-382bcaf3b212)

---
### **Data Modelling**

1. Partial Least Squares Regression (PLS)


- Projects spectral data onto a lowerdimensional space.
- Captures covariance between spectral
- Reduces dimensionality.
- Robust against noisy spectral data.

2. Support Vector Regression (SVR)
- Constructs a hyperplane that best fits the
data in a transformed feature space.
- Uses kernel functions (linear, RBF) for
nonlinear regression.
- Ideal for datasets where relationships are
nonlinear.
- Effective when the dataset has high
variance.
- Handles nonlinear relationships
effectively.
- Robust against overfitting, especially with
small datasets.

3. Artificial Neural Networks (ANN)

- ANN consists of multiple layers of neurons
to model complex relationships.
- Learns hierarchical representations from
spectral data.
- Best for large datasets with nonlinear
dependencies.
- High adaptability to complex spectral
patterns.

---
**Results**

- Model performance comparison before vs after different preprocessing techniques

![image](https://github.com/user-attachments/assets/daaa0154-3cc8-44db-86df-980b6113d7c3)

![image](https://github.com/user-attachments/assets/09ce05ac-febe-4042-8fe3-bc26d0dfb983)

![image](https://github.com/user-attachments/assets/88a2e935-3e08-4c51-814d-bb05cb0dc5a6)

![image](https://github.com/user-attachments/assets/95863d3f-fc2e-4876-8e7b-b88446b99fa5)

- Model performance Metrics Comparison

![image](https://github.com/user-attachments/assets/d490f9b7-48de-4329-8ce7-9e64f7c9db74)


- Basic preprocessing with Savitzky-Golay (SV-Gol)
smoothing and outlier removal using PLS
regression was essential in removing noise and
enhancing feature clarity.

- Advanced preprocessing techniques such as MSC
and SNV significantly improved model accuracy
by addressing scattering effects.

- PLS regression provided the best accuracy across
all models, as indicated by its highest R² of 0.965,
lowest RMSE of 2.523. While SVR also showed
competitive performance, PLS remained the most
robust and reliable choice for this dataset.

- Among the Advanced preprocessing techniques,
MSC Scatter Correction showed slightly better
results, with the lower bias, RMSE and higher R²
values. The potential reasons for this observation
could be as follows.
  - MSC aligns spectra to a chosen reference,
  which enhances the consistency of the data
  and improves correlation with true
  chemical concentrations.
  - By modeling and removing scattering
  effects through linear regression, MSC
  retains the original spectral characteristics
  better than SNV. In contrast, SNV
  normalizes each spectrum individually,
  which can distort spectral relationships and
  increase variability.






