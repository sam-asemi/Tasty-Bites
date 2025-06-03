# 🍽️ Tasty Bytes Recipe Site Traffic Analysis

This project analyzes recipe page performance for **Tasty Bytes**, a fictitious recipe website, using a combination of **data cleaning**, **exploratory analysis**, and **machine learning modeling** to predict whether a recipe will generate high or low traffic.

---

## 📊 Objective

To build a classification model that predicts whether a recipe will experience **high traffic** based on features such as category, calories, and other metadata—helping content teams prioritize and optimize recipes for user engagement.

---

## 🧹 Data Cleaning & Validation

- Set the **first row as column headers**, then removed it from the dataset
- Replaced missing values placeholders (`NA`, `N/A`, `NULL`, `-`, and `''`) with `NaN`
- Removed rows with **fewer than 5 non-null values**
- Filled missing values in the `high_traffic` column with `"Not High"` for consistency

---

## 📊 Exploratory Data Analysis

### 🔸 High Traffic Distribution

Most recipes received **high traffic**, suggesting a skew toward popular content on the site.

![High Traffic Histogram](https://github.com/user-attachments/assets/75994f49-153f-4120-bfa7-1b666b537b73)

---

### 🔸 Recipe Category Distribution

Recipe categories are fairly **evenly distributed**, indicating no single content type dominates the site.

![Category Pie Chart](https://github.com/user-attachments/assets/6c3cc47f-54b1-4fdf-9a01-10190cce949d)

---

### 🔸 High vs. Not High Traffic by Category

This stacked bar chart reveals which **recipe categories attract more traffic**, helping content teams identify high-performing segments.

![Traffic by Category](https://github.com/user-attachments/assets/490cac14-612e-43e0-ba90-f8493745e1e5)

---

### 🔸 Calories by Category

Shows which categories are typically **higher or lower in calories**, though **no strong correlation** with traffic volume was found.

![Calories by Category](https://github.com/user-attachments/assets/7a836e88-8f9c-4ef6-b275-4c8987cc4388)

---

## 🤖 Model Development

### 🧠 Problem Type
- **Binary Classification**: Predict whether a recipe is `high_traffic = 1` or `not_high = 0`

### 🔍 Models Evaluated
- **Logistic Regression**: Simple, interpretable baseline
- **Support Vector Machine (SVM)**: More flexible, capable of capturing non-linear relationships  
  *(Hyperparameters tuned using `GridSearchCV`)*

---

## 🧪 Model Performance Comparison

| Metric        | Logistic Regression | SVM      |
|---------------|---------------------|----------|
| Accuracy      | **77%**             | 59%      |
| Precision     | **0.79**            | 0.59     |
| Recall        | 0.68                | **1.00** |
| F1-Score      | **0.81**            | 0.74     |

📌 **Logistic Regression** outperformed SVM in most metrics, except for recall.

![Model Evaluation](https://github.com/user-attachments/assets/f22e6526-d9fa-42bf-9a81-30d1c089e3b2)

---

## 📈 Confusion Matrix Comparison

| Metric        | Logistic Regression | SVM      |
|---------------|---------------------|----------|
| False Positives | 18                | **0**    |
| False Negatives | **23**            | 73       |
| True Positives  | **50**            | 0        |
| True Negatives  | 88                | **106**  |

### 🔍 Key Insight:
- **SVM perfectly identified all low-traffic recipes**, but **failed to identify any high-traffic ones**, making it unsuitable unless recall is the sole concern.
- **Logistic Regression provided a balanced approach**, suitable for general deployment.

---

## ✅ Recommendations

### 🎯 Model Deployment
- Use **Logistic Regression** as the primary model due to its **balanced precision and recall**
- Consider SVM if the **cost of missing high-traffic recipes is extremely high**, but validate thoroughly due to its poor precision

### 📉 Business Impact
- **False Positives**: Promoting low-performing recipes may reduce site engagement
- **False Negatives**: Failing to highlight popular recipes could hurt traffic and revenue

### 🔄 Continuous Improvement
- Retrain the model regularly to avoid concept drift
- Integrate additional features (e.g., time on page, user ratings)
- Address class imbalance using resampling or custom loss functions

---

## 📬 Summary

This project highlights how **machine learning and data visualization** can provide real-time insights into **content performance**. With a well-balanced classification model, recipe websites can better allocate promotional efforts, improve user engagement, and optimize content strategy.

---

