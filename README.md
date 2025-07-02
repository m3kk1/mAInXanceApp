# mAInXanceApp

Capstone Project for Predicting Technician Actions from Work Order Descriptions

Objective
Train a model to analyze historical work order data and predict the likely technician response based on a short issue description. This project lays the groundwork for building an app to assist in future troubleshooting by mapping problem descriptions to technician solutions.

Dataset
Source: Internal company spreadsheet

Total Records: Originally 70,000+ cleaned to 40,000+

Fields Used:


Description: Short note about the problem

Text: Free-text technician notes after job is completed


Data Cleaning & Preparation
Dropped empty or irrelevant rows

Removed invalid WO numbers

Cleaned and standardized strings

Created two clean columns:

Description_cleaned

Text_cleaned

Flagged technician names and filler words for future cleaning (not used in this version this cut training accuracy in half, while still showing up in the dataset. Will debug and update in the latest version).


Clustering the Notes
KMeans on Technician Notes
Used TfidfVectorizer on Text_cleaned and applied KMeans to group similar actions into behavior-based clusters.
Tuned cluster size using silhouette scores (k=2 to 9)


Final model used k=5 for balanced behavior clusters


New column created: Note_Cluster


Model Training
Description → Note Cluster Prediction
Input (X): Description_cleaned


Output (y): Note_Cluster


Model: Pipeline([TF-IDF, Logistic Regression])


Train/Test Split: 80/20


Accuracy: 0.74


Weighted F1: 0.67

Confusion matrix and classification report provided to evaluate per-cluster precision and recall.
Similarity Search Tool
Built a cosine similarity function using TfidfVectorizer to return the top 5 most similar past work orders based on input description.
Deliverables
Final Notebook: CapStoneProjMAInXanceApp.ipynb


Summary Report: Capstone Deliverable.docx


Future Work
Clean technician names and filler terms (e.g., “completed”, “done”)


Replace TF-IDF with contextual embeddings (e.g., MiniLM)


Use true labels instead of unsupervised clusters


Deploy as part of a troubleshooting maintenance assistant app
