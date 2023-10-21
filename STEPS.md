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

### Import Package :

```
pip install matplotlib
```
Matplotlib is a widely used Python library for creating static, animated, and interactive visualizations in a variety of formats, including line charts, bar charts, scatter plots, and more. It provides a flexible and user-friendly way to generate high-quality plots and graphs for data visualization and scientific illustration. With its rich set of features and customization options, Matplotlib is a powerful tool for researchers, data scientists, and engineers to convey data insights and present results in a clear and visually appealing manner. You can easily install Matplotlib using pip install matplotlib to get started with creating informative and aesthetically pleasing plots in your Python projects.

### Program:
```python
import matplotlib.pyplot as plt

# Function to get marks from the user for each domain
def get_marks(domain):
    marks = int(input(f"Enter marks for {domain}: "))
    return marks

# List of domains
domains = ["Computer Science", "ECE", "Graphic Design", "Aerospace"]

# Initialize a dictionary to store domain names and marks
marks_dict = {}

# Get marks for each domain
for domain in domains:
    marks = get_marks(domain)
    marks_dict[domain] = marks

# Calculate percentages
total_marks = sum(marks_dict.values())
percentage_dict = {domain: (marks / total_marks) * 100 for domain, marks in marks_dict.items()}

# Plot the results
plt.figure(figsize=(8, 6))
plt.bar(percentage_dict.keys(), percentage_dict.values())
plt.xlabel("Domains")
plt.ylabel("Percentage")
plt.title("Results Based on Marks")
plt.ylim(0, 100)

# Display the graph
plt.show()

```
### Sample Input 1 :
```
Enter marks for Computer Science: 5
Enter marks for ECE: 8
Enter marks for Graphic Design: 5
Enter marks for Aerospace: 9
```
### Sample Result 1 :
![Sample](/sample.png)

### Sample Input 2 :
```
Enter marks for Computer Science: 5
Enter marks for ECE: 8
Enter marks for Graphic Design: 5
Enter marks for Aerospace: 9
```

### Sample Result 2 :
![Sample](/sample2.png)
