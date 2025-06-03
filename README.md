Tasty Bytes Recipe Site Traffic
Data Validation
In the first step, we use the first row as column headers and remove it from the data to prevent duplication. Next, we replace missing value placeholders (e.g., NA, N/A, NULL, -, and '') with NaN using NumPy. To maintain data quality, we drop rows containing fewer than 5 non-null values.

Finally, we fill missing values in the high_traffic column with the label "Not High" to ensure consistency in the dataset.

Distribution of High Traffic Recipes
The histogram illustrates the distribution of website traffic across recipes, providing insights into whether most recipes experience high or low traffic. The chart reveals that a larger proportion of recipes receive high traffic compared to those with low traffic, indicating that popular recipes make up a significant portion of the website's content.
![image](https://github.com/user-attachments/assets/75994f49-153f-4120-bfa7-1b666b537b73)


Recipe Category Distribution
The pie chart displays the proportion of recipes by category, highlighting the dominant categories that may influence website traffic. The chart reveals a fairly even distribution across all categories, suggesting that no single category overwhelmingly dominates the recipe collection.
![image](https://github.com/user-attachments/assets/6c3cc47f-54b1-4fdf-9a01-10190cce949d)


High Vs Not High Traffic Based on Category
The stacked bar chart illustrates the distribution of high vs. not high traffic across recipe categories. Each bar represents a category, with two segments showing the proportion of high-traffic and not high-traffic recipes. The chart reveals which categories tend to attract more traffic, helping identify high-performing recipe types. Categories with a larger red segment (high traffic) indicate stronger user engagement, while those with a larger blue segment (not high traffic) may require optimization or promotion.
![image](https://github.com/user-attachments/assets/490cac14-612e-43e0-ba90-f8493745e1e5)


Calories per Recipe Category
The bar plot illustrates the relationship between recipe categories and their calorie content, allowing for a clear comparison of calorie variations across categories. It highlights which categories tend to feature higher-calorie recipes and which ones typically contain lower-calorie options, offering insights into the nutritional profile of different recipe types.Also, calorie content does not strongly correlate with high traffic, suggesting that users may be influenced by other factors.
![image](https://github.com/user-attachments/assets/7a836e88-8f9c-4ef6-b275-4c8987cc4388)


Model Development
a) Problem Type Statement

The task is a binary classification problem, where the goal is to predict whether a recipe will generate high traffic or low traffic based on various features (e.g., category, calories, etc.).

Target variable: high_traffic (binary: 1 for high, 0 for not high).

Features: All other columns, including category and calories.

b) Reason for Model Selection

Logistic Regression (Baseline Model): Chosen as the baseline due to its simplicity and interpretability. Suitable for binary classification problems. Provides probabilistic outputs, making it useful for threshold-based decisions.

Support Vector Machine (SVM): Chosen as a comparison model due to its ability to handle complex, non-linear relationships. Uses kernel tricks to separate classes in higher-dimensional spaces. GridSearchCV was used to tune hyperparameters, improving performance.

Key Insights from Model Evaluation
Accuracy: The Logistic Regression model achieved 77% accuracy, which is higher than the 59% accuracy of the SVM model. Accuracy alone is not always the best metric, especially when class imbalance is present.

Precision: Logistic Regression achieves a precision of 0.79, indicating that 79% of the recipes it labels as high-traffic are actually high-traffic. The SVM model has a significantly lower precision of 0.59, meaning 41% of the recipes it predicts as high-traffic are false positives. This could lead to less relevant recipes being promoted on the website, which may hurt customer experience.

Recall: The SVM model achieved a perfect recall (1.00), meaning it correctly identified all high-traffic recipes. However, the lower accuracy indicates it might be overfitting to the positive class.

F1-Score: Logistic Regression has a slightly higher F1-score (0.81) compared to SVM (0.74), suggesting a better balance between precision and recall.
![image](https://github.com/user-attachments/assets/f22e6526-d9fa-42bf-9a81-30d1c089e3b2)


Business Metrics and Comparison
False Positives (FP):
Recipes incorrectly classified as high traffic. This could result in displaying low-performing recipes on the homepage, reducing customer engagement.

Logistic Regression: 18 FP
SVM: 0 FP
False Negatives (FN):
Recipes incorrectly classified as low traffic. Missing out on promoting a high-performing recipe could reduce potential traffic and revenue.

Logistic Regression: 23 FN
SVM: 73 FN
True Positives (TP):
Recipes that are truly high traffic and correctly classified as high traffic.

Logistic Regression: 50 TP
SVM: 0 TP
True Negatives (TN):
Recipes that are truly low traffic and correctly classified as low traffic.

Logistic Regression: 88 TN
SVM: 106 TN
Key Insights:
The SVM model is overly biased toward predicting recipes as low traffic, leading to zero true positives and high false negatives (73).
The Logistic Regression model has a more balanced classification but still misclassifies some recipes.
SVM's behavior may be due to class imbalance or a poorly tuned model, which should be investigated further.
Summary
Logistic Regression: Higher overall accuracy (77%). Balanced recall and precision with a solid F1-score (81%). More reliable for general-purpose classification.

SVM with GridSearchCV: Perfect recall (100%) ensures no high-traffic recipes are missed. Lower accuracy, indicating overfitting or poor handling of class imbalance. Better for scenarios where missing a high-traffic recipe is costly.

Recommendations
Model Selection:

Based on the Precision, F1-score and accuracy, Logistic Regression is the better option for general performance. If recall (catching all high-traffic recipes) is the main priority, SVM might be preferable, but you should be cautious of its lower accuracy and potential false positives.

Business Actions:

Use the Logistic Regression model for production deployment due to its balanced performance.
Regularly retrain the model with new data to prevent concept drift.
Monitor recall and precision to avoid displaying low-performing recipes.
Collect additional features such as user engagement time or recipe reviews to improve model performance.
