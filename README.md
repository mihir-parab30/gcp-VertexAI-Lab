# Student Performance Prediction using Vertex AI AutoML

This project trains and deploys a machine learning model using Google Cloud Vertex AI AutoML Tables. The goal is to predict a student’s final grade (G3) based on demographic and academic attributes from the Student Performance Dataset published by the UCI Machine Learning Repository.

---

## Dataset

Source: UCI Student Performance Dataset  
Dataset link: https://archive.ics.uci.edu/static/public/320/student.zip

The experiment uses the `student-mat.csv` file, which includes:

- demographic details  
- family background  
- study habits  
- previous grades (G1 and G2)  
- absences  
- academic support indicators  

The target variable is **G3**, which represents the final grade.  
The dataset is already structured and clean, so no heavy preprocessing was required.

---

## Objective

The purpose of this lab is to complete a full training and deployment workflow using Google Cloud Vertex AI:

1. Import the tabular dataset  
2. Train a regression model using AutoML  
3. Deploy the model to a Vertex AI endpoint  
4. Run online predictions on the deployed model  

This demonstrates an end-to-end MLOps process using Vertex AI in a simple and practical way.

---

## Steps

### 1. Upload the Dataset to Vertex AI

1. Open the Google Cloud Console and go to **Vertex AI**  
2. Select **Datasets → Create Dataset → Tabular**  
3. Upload `student-mat.csv`  
4. Allow Vertex AI to automatically detect all column types  
5. Set **G3** as the target column  

The default schema detection works without any issues.

---

### 2. Train the AutoML Model

1. Choose **AutoML** as the training method  
2. Keep all column transformations on default  
3. Set the training budget (1 node-hour is sufficient for this dataset)  
4. Start the training job  

Vertex AI automatically handles:

- feature engineering  
- data encoding  
- model selection  
- hyperparameter tuning  

Training typically completes in 15 to 25 minutes.

---

### 3. Deploy the Model

1. Open the trained model in Vertex AI  
2. Select **Deploy to Endpoint**  
3. Create a new endpoint  
4. Choose a basic machine type, such as `n1-standard-2`  
5. Confirm deployment  

The model becomes available for online predictions once deployment is complete.

---

### 4. Test the Endpoint

Predictions can be tested directly in the Vertex AI console using JSON input.  
Example:

```json
{
  "instances": [
    {
      "school": "GP",
      "sex": "F",
      "age": 17,
      "studytime": 2,
      "absences": 4,
      "G1": 12,
      "G2": 13
    }
  ]
}
