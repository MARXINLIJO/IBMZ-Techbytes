# IBMZ-Techbytes

## Abstract :
The problem we are attempting to solve is unexpected machine failures in industrial settings, which lead to costly downtime, expensive repairs, and decreased productivity. In many industries, machines are critical to continuous production, and unplanned failures can halt operations, causing significant financial losses. Traditional maintenance strategies, such as scheduled or reactive maintenance, are inefficient—either leading to over-maintenance or delayed repairs.

## Algorithm :

### Step 1:
``` Import Matplotlib
Import the matplotlib.pyplot module using the alias plt.
```
### Step 2:
```
Define a Function to Get Marks Define a Python function get_marks(domain) that takes the name of a domain as an argument.
Inside the function, prompt the user to enter marks for the specified domain.
Convert the user input to an integer using int().
Return the entered marks.
```
### Step 3:
```
Define a List of Domains Create a list called domains to store the names of the domains for which you want to collect marks (e.g., "Computer Science," "ECE," "Graphic Design," and "Aerospace").
```
### Step 4: 
```
Initialize a Dictionary for Marks Initialize an empty dictionary called marks_dict. This dictionary will be used to store domain names as keys and the corresponding marks as values.
``` 

### Step 5:
```
Get Marks for Each Domain Use a for loop to iterate through each domain in the domains list.
Inside the loop, call the get_marks function for each domain to collect the user's input for marks.
Store the entered marks in the marks_dict dictionary with the domain name as the key.
```
### Step 6: 
```
Calculate Total Marks and Percentages Calculate the total marks by summing all the marks in the marks_dict.
Initialize an empty dictionary called percentage_dict to store domain names as keys and their respective percentages as values. Use a loop to calculate the percentage of marks for each domain:
For each domain, divide the marks in that domain by the total marks.Multiply the result by 100 to get the percentage. Store the domain name and its percentage in the percentage_dict dictionary.
```
### Step 7: 
```
Plot the Results
Use the matplotlib library to create a bar graph to display the results.
Set the figure size for the graph.
Create a bar graph with domain names on the x-axis and corresponding percentages on the y-axis.
Add labels for the x-axis, y-axis, and a title to the graph.Set the y-axis limits to ensure that the percentages are displayed in the range of 0 to 100.
```
### Step 8: 
```
Display the Graph Call plt.show() to display the graph with the entered marks and their percentages in each domain.
The user will see a bar graph showing the results based on the percentages of marks in different domains
```

#

### Import Package :

```
pip install matplotlib
```
Matplotlib is a widely used Python library for creating static, animated, and interactive visualizations in a variety of formats, including line charts, bar charts, scatter plots, and more. It provides a flexible and user-friendly way to generate high-quality plots and graphs for data visualization and scientific illustration. With its rich set of features and customization options, Matplotlib is a powerful tool for researchers, data scientists, and engineers to convey data insights and present results in a clear and visually appealing manner. You can easily install Matplotlib using pip install matplotlib to get started with creating informative and aesthetically pleasing plots in your Python projects.

#

### Program:
```
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, confusion_matrix, accuracy_score
# Import the necessary library for one-hot encoding
from sklearn.preprocessing import OneHotEncoder

# Step 1: Load the dataset
df = pd.read_csv('ai4i2020.csv')

# ... (Rest of your code for EDA and data preprocessing) ...

# Step 3: Data Preprocessing (with One-Hot Encoding)
# ... (handle missing values if needed) ...

# Define features (sensor data) and target (failure)
# Replace 'failure' and 'timestamp' with the actual column names from the output above
X = df.drop(columns=['UDI', 'Product ID', 'Machine failure'])  # All columns except target and id columns
y = df['Machine failure']  # Target variable # Changed 'Target' to 'Machine failure'

# Perform One-Hot Encoding for the 'Type' column
# 1. Create a OneHotEncoder object
encoder = OneHotEncoder(sparse_output=False, handle_unknown='ignore') # sparse=False for compatibility with RandomForest

# 2. Fit the encoder on the 'Type' column and transform it
encoded_type = encoder.fit_transform(X[['Type']]) 

# 3. Create a DataFrame from the encoded data
encoded_type_df = pd.DataFrame(encoded_type, columns=encoder.get_feature_names_out(['Type']))

# 4. Drop the original 'Type' column and concatenate the encoded columns
X = X.drop(columns=['Type'])
X = pd.concat([X, encoded_type_df], axis=1)

# Split the data into training and testing sets (80% train, 20% test)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ... (Rest of your code for model training and evaluation) ...
# Step 4: Model Training
# Initialize the Random Forest Classifier
model = RandomForestClassifier(n_estimators=100, random_state=42)

# Train the model
model.fit(X_train, y_train)

# Step 5: Model Evaluation
# Predict the results on the test set
y_pred = model.predict(X_test)

# Check the accuracy and classification report
print("Accuracy Score:", accuracy_score(y_test, y_pred))
print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
print("Classification Report:\n", classification_report(y_test, y_pred))

# Plot the Confusion Matrix for better visualization
plt.figure(figsize=(6,4))
sns.heatmap(confusion_matrix(y_test, y_pred), annot=True, fmt='d', cmap='Blues')
plt.title('Confusion Matrix')
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.show()

# Feature Importance
importances = model.feature_importances_
indices = np.argsort(importances)[::-1]

plt.figure(figsize=(10,6))
plt.title("Feature Importances")
plt.bar(range(X.shape[1]), importances[indices], align="center")
plt.xticks(range(X.shape[1]), X.columns[indices], rotation=90)
plt.tight_layout()
plt.show()

# ... (Your previous code) ...

# Step 6: Use the model for future predictions
# Assuming the new data point is of 'Type_L'
# Replace with actual sensor values and adjust the number of features, including one-hot encoded 'Type'

# The values for 'Type' should be one-hot encoded and added in the same order as during training
# For 'Type_L', the encoding is [0, 1, 0] (Type_H, Type_L, Type_M)
# So, new_sensor_data should have 13 elements (10 original + 3 encoded type)
new_sensor_data = [[55, 300, 80, 75, 90, 10, 70, 80, 95, 10, 0, 1, 0]]  # Replace with actual sensor values, removing the extra values
# Create the DataFrame with all column names except the target variable
new_sensor_data_df = pd.DataFrame(new_sensor_data, columns=X.columns) # Use all columns of X as column names

# Now use the data for prediction
prediction = model.predict(new_sensor_data_df)  
print("Predicted Failure Status (1 = Fail, 0 = No Fail):", prediction)
```

### Sample Result 1 :
![Screenshot 2024-10-20 001716](https://github.com/user-attachments/assets/f8760ee6-3a77-45ea-b3dc-7278b0fb0fe1)

### Sample Result 2 :
![Screenshot 2024-10-20 001758](https://github.com/user-attachments/assets/ee3536de-80f2-4132-b786-44610ddda79c)



