# Final_Capstone_Project
Final Capstone Project

Capstone Project: Estimate Product Power

UC Berkeley: Professional Certificate in Machine Learning and Artificial Intelligence

Author: Michael King

Date: September 2025


Executive Summary

This project addresses a critical lack of centralized power information for products within Cisco, which has led to significant data gaps. To overcome this, we developed a multi-stage supervised learning framework that leverages Bill of Materials (BOM) and product classification data to estimate product power.

Key Results:

* Product Classification (Model 1): A Gradient Boosting model achieved a strong 94% accuracy and F1-score, significantly outperforming a 45% dummy baseline. This ensures reliable identification of critical product types (MECH, MOD, PWR).

* Product Weight Prediction (Model 2): A Random Forest model achieved the lowest RMSE of 1.93, outperforming a dummy classifier's RMSE of 4.78 for products under 20 kg.

* Product Power Prediction (Model 3): A Random Forest model achieved the lowest RMSE of 116.50, significantly better than a dummy classifier's RMSE of 241.43.


Impact: This project establishes a robust, data-driven framework for estimating product power, directly addressing a major data gap and providing a foundation for more accurate greenhouse gas emissions reporting, as electricity consumption is Cisco's largest source of these emissions.


1. Problem Statement & Goal

Problem: Power consumption information for many Cisco products has not been collected and managed in a centralized manner, resulting in significant data gaps. This lack of data hinders efforts to understand and manage the environmental impact of products.

Goal: The primary objective of this project is to create a reliable model that can estimate the typical power consumption of Cisco's products. This is crucial because the electricity consumed by Cisco's products represents its largest source of greenhouse gas emissions.


2. Data Acquisition & Pre-processing

Data Sources: Data was extracted from Cisco's product lifecycle management tool and product creation tool. The dataset includes Bill of Materials (BOM) information (e.g., component types) and product classification details.

Initial Data Exploration:

* The raw dataset initially contained 93,449 rows and 94 columns, with various data types (int64, object, float64).

* Through collaboration with Subject Matter Experts (SMEs), the number of columns was consolidated and refined to 25 (21 int64, 4 object) to focus on relevant features.

* Rows with missing data were removed, as there was no viable method to fill these gaps, resulting in a final cleaned dataset of 41,279 rows.


Key Data Insights (EDA):

Skewed Distributions: Initial analysis of key numerical features (e.g., total_comp, IC, elec, mech) revealed distributions heavily skewed towards lower values. This meant most observations were in lower numerical ranges, with fewer observations as values increased.

Log Transformation: To address the skewness and improve model performance, a log function was applied to these features. This successfully corrected the skew, yielding more balanced distributions, many of which appeared bimodal or multimodal, suggesting distinct groups within the data.



3. Modeling Approach: A Multi-Stage Supervised Learning Framework

A multi-stage supervised learning framework was developed, consisting of three sequential models:

* Product Classification (Model 1): Classifies products into types (e.g., MECH, MOD, PWR) based on BOM and categorical data.

* Product Weight Prediction (Model 2): Predicts product weight using BOM information.

* Product Power Prediction (Model 3): Predicts product power consumption using the enriched dataset, including classified product types and predicted weights.



4. Model 1: Product Classification

Goal: Develop a supervised learning model to accurately predict product type (MECH, MOD, PWR) based on Bill of Materials (BOM) information and other categorical data.

Target Variable: MOD (Modular), PWR (Power), MECH (Mechanical).

Key Results:

* The model significantly outperformed the dummy baseline accuracy of 45% (where 'MOD' was the majority class).

* Best Model: Gradient Boosting was selected as the most effective approach.

* Performance: Achieved a test accuracy of approximately 94% and an F1-score of approximately 94%.

* Reliability: This high accuracy ensures reliable identification of critical product types, reducing the risk of misclassification.



5. Model 2: Product Weight Prediction

Goal: Develop a supervised learning model to predict product weight (in kilograms), leveraging the relationship between weight and BOM information.

Target Variable: Product net_weight in kilograms.

Key Results:

* Initial modeling struggled due to outliers. A significant improvement was made by focusing the model on products with net_weight less than 20 kg, as outliers were heavily affecting results.

* The dummy classifier produced a test RMSE of 4.78.

* Best Model: Random Forest achieved the lowest RMSE of 1.93.

* Performance: The Random Forest model significantly improved prediction accuracy compared to the baseline.

* Metric: Root Mean Squared Error (RMSE) was chosen as the evaluation metric due to its ability to penalize large prediction errors and provide a consistent basis for model comparison.



6. Model 3: Product Power Prediction

Goal: Train a new supervised learning model to predict power consumption (in Watts) for products that currently lack this data, using the completed dataset (including classified product types and predicted weights).

Target Variable: Product power in Watts.

Key Results:

* The distribution of power across products showed that the majority of products consume less than 50 Watts, with a long tail extending to higher values.

* The dummy classifier produced a test RMSE of 241.43.

* Best Model: Random Forest achieved the lowest RMSE of 116.50.

* Performance: The Random Forest model demonstrated a substantial improvement in predicting product power compared to the baseline.

* Metric: RMSE was again chosen for its effectiveness in penalizing large errors and facilitating fair comparison. This model is critical for estimating the greenhouse gas emissions associated with Cisco’s products.



Conclusion

This project successfully developed a robust, multi-stage machine learning framework to estimate the typical power consumption of Cisco products. By addressing the critical data gap in power information, we have created a reliable system that can classify products, predict their weight, and ultimately predict their power usage. This directly supports Cisco's efforts to understand and reduce its largest source of greenhouse gas emissions, contributing to sustainable growth and environmental responsibility.


Next Steps

To further enhance and operationalize this project, the following steps are recommended:

* Integrate Models into Existing Systems: Automate the classification, weight, and power prediction processes directly within Cisco's product lifecycle and creation tools. This will ensure new products automatically receive estimated data, preventing future data gaps.

* Expand Data Collection for Outliers: Investigate the nature of products exceeding 20 kg that were excluded from the weight prediction model. Develop targeted data collection strategies or specialized models for these larger products to achieve comprehensive weight prediction.

* Continuous Model Monitoring and Retraining: Implement a system for ongoing monitoring of model performance (accuracy, RMSE) against new product data. Regularly retrain models with updated datasets to maintain accuracy and adapt to evolving product designs or component changes.

* Explore Advanced Feature Engineering: Investigate additional features or more complex transformations from the extensive Bill of Materials (BOM) information that could further enhance the predictive power of all three models.

* Quantify Prediction Uncertainty: For the weight and power prediction models, consider providing prediction intervals or confidence scores alongside point estimates. This would give users a better understanding of the reliability of each prediction.

* Operationalize Emissions Reporting: Clearly define how the estimated power data will be used in the company's greenhouse gas emissions reporting and reduction strategies, directly linking this technical solution to business impact.



