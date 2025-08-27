# **Financial Fraud Detection Web Application**

## **Table of Contents**

* [Project Overview](https://www.google.com/search?q=%23project-overview)  
* [Key Features](https://www.google.com/search?q=%23key-features)  
* [Technology Stack](https://www.google.com/search?q=%23technology-stack)  
* [Project Structure](https://www.google.com/search?q=%23project-structure)  
* [Installation and Setup](https://www.google.com/search?q=%23installation-and-setup)  
* [Usage](https://www.google.com/search?q=%23usage)  
* [Model Details](https://www.google.com/search?q=%23model-details)  
* [Future Improvements](https://www.google.com/search?q=%23future-improvements)

## **Project Overview**

This project presents a machine learning-powered web application for detecting fraudulent financial transactions in real-time. The application provides a simple and intuitive user interface where users can input transaction details and receive an instant prediction on whether the transaction is likely to be fraudulent or legitimate.

The core of the application is a pre-trained scikit-learn pipeline that processes the input data and makes predictions using a Logistic Regression model. The entire application is built and served using Streamlit, demonstrating a complete end-to-end deployment of a machine learning model.

**Goal:** To provide a fast, accessible, and reliable tool for identifying potentially fraudulent activities, showcasing skills in machine learning, model deployment, and application development.

## **Key Features**

* **Interactive UI**: A clean and user-friendly web interface built with Streamlit for easy data entry.  
* **Real-Time Prediction**: Instant classification of transactions upon user submission.  
* **Pre-trained ML Pipeline**: Utilizes a joblib-serialized scikit-learn pipeline that handles data preprocessing and prediction seamlessly.  
* **Clear Feedback**: The application provides unambiguous results, highlighting potential fraud with a distinct error message and confirming legitimate transactions with a success message.

## **Technology Stack**

* **Programming Language**: Python 3.x  
* **Web Framework**: Streamlit  
* **Machine Learning**: Scikit-learn  
* **Data Manipulation**: Pandas  
* **Model Serialization**: Joblib

## **Project Structure**

.  
├── fraud\_detection.py             \# Main Streamlit application script  
├── fraud\_detection\_pipeline.pkl   \# Serialized pre-trained scikit-learn pipeline  
├── requirements.txt               \# Project dependencies  
└── README.md                      \# Project documentation

## **Installation and Setup**

To run this project on your local machine, please follow these steps.

**1\. Clone the Repository**

git clone \<repository-url\>  
cd \<repository-directory\>

2\. Create and Activate a Virtual Environment  
It is highly recommended to use a virtual environment to manage project dependencies.

* **For macOS/Linux:**  
  python3 \-m venv venv  
  source venv/bin/activate

* **For Windows:**  
  python \-m venv venv  
  .\\venv\\Scripts\\activate

3\. Install Dependencies  
Create a requirements.txt file with the following content:  
streamlit  
pandas  
scikit-learn==1.2.2  
joblib

Then, install the required packages using pip:

pip install \-r requirements.txt

## **Usage**

Once the setup is complete, you can run the application with a single command:

streamlit run fraud\_detection.py

This will start the Streamlit server and open the web application in your default browser.

**How to use the App:**

1. Navigate to the local URL provided by Streamlit (usually http://localhost:8501).  
2. Use the input widgets on the sidebar to enter the transaction details:  
   * **Transaction Type**: Select from the dropdown menu.  
   * **Amount**: Enter the transaction amount.  
   * **Old/New Balances**: Provide the sender and receiver balances before and after the transaction.  
3. Click the **"Predict"** button.  
4. The application will display the prediction result below the button.

## **Model Details**

The predictive power of this application comes from a scikit-learn pipeline, which ensures that the raw input data is processed in the exact same way as the data used for training.

* **Model Type**: LogisticRegression  
  * The classifier is a Logistic Regression model from scikit-learn. It was configured with class\_weight='balanced' to effectively handle the inherent class imbalance commonly found in fraud detection datasets.  
* **Preprocessing Pipeline**: ColumnTransformer  
  * The pipeline automatically applies different transformations to different types of columns.  
    * **Numerical Features**: The following features are scaled using StandardScaler to normalize their range and variance:  
      * amount  
      * oldbalanceOrg  
      * newbalanceOrig  
      * oldbalanceDest  
      * newbalanceDest  
    * **Categorical Features**: The type feature is converted into a numerical format using OneHotEncoder. The model was trained on the following categories: PAYMENT, TRANSFER, CASH\_OUT, DEBIT, CASH\_IN.  
* Input Features  
  The model expects the following six features for prediction:  
  * type (Categorical): Type of transaction.  
  * amount (Numerical): The value of the transaction.  
  * oldbalanceOrg (Numerical): Sender's balance before the transaction.  
  * newbalanceOrig (Numerical): Sender's balance after the transaction.  
  * oldbalanceDest (Numerical): Receiver's balance before the transaction.  
  * newbalanceDest (Numerical): Receiver's balance after the transaction.

## **Future Improvements**

While this application serves as a strong proof-of-concept, it can be extended in several ways:

* **Deployment**: Deploy the application to a cloud platform like Streamlit Community Cloud, Heroku, or AWS for public access.  
* **Advanced Models**: Experiment with more complex models such as XGBoost, LightGBM, or a simple neural network to potentially improve prediction accuracy.  
* **Explainable AI (XAI)**: Integrate libraries like SHAP or LIME to provide explanations for each prediction, helping users understand why a transaction was flagged as fraudulent.  
* **Batch Processing**: Add a feature to allow users to upload a CSV file with multiple transactions and receive predictions for the entire batch.  
* **CI/CD Pipeline**: Implement a CI/CD pipeline using tools like GitHub Actions to automate testing and deployment.  
* **Model Monitoring**: Set up a system to monitor the model's performance in production and trigger alerts for retraining when performance degrades (model drift).