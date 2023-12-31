# FETAL_HEALTH_CLASSIFICATION

import pandas as pd
data=pd.read_csv("/content/sample_data/fetal_health.csv")
data

data.duplicated()

data.drop_duplicates()

data.shape

data.info()

data.head()

data.tail()

data.describe()

data["baseline value"].value_counts()

data["accelerations"].value_counts()

# See the min, max, mean values
print('The highest accelerations was of:',data['accelerations'].max())
print('The lowest accelerations was of:',data['accelerations'].min())
print('The average accelerations in the data:',data['accelerations'].mean())

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_palette(palette='RdPu')
data.accelerations.hist()
plt.title('Accelerations');

data.fetal_movement.value_counts()

data.fetal_movement.hist()
plt.title('Fetal Movement');

data.severe_decelerations.value_counts()

data.abnormal_short_term_variability.hist()
plt.title('Abnormal Short-Term Variability');

data.histogram_width.describe()

data.histogram_min.describe()

data.histogram_max.describe()

# Line plot
plt.plot(data['histogram_tendency'])
plt.xlabel("histogram_tendency")
plt.ylabel("Levels")
plt.title("Line Plot")
plt.show()

import matplotlib.pyplot as plt
fig, (ax1, ax2, ax3) = plt.subplots(1, 3, figsize=(13, 5))

data_len_1 = data[data['fetal_health'] == 1]['fetal_health'].value_counts()
ax1.hist(data_len_1, color='red')
ax1.set_title('Normal')

data_len_2 = data[data['fetal_health'] == 2]['fetal_health'].value_counts()
ax2.hist(data_len_2, color='green')
ax2.set_title('Suspect')

data_len_3 = data[data['fetal_health'] == 3]['fetal_health'].value_counts()
ax3.hist(data_len_3, color='blue')
ax3.set_title('Pathological')

fig.suptitle('Fetal Health Levels')
plt.show()

data.isnull().sum()

data[1:5]

from sklearn import preprocessing
import pandas as pd

d = preprocessing.normalize(data.iloc[:,1:5], axis=0)
scaled_df = pd.DataFrame(d, columns=["fetal_movements", "uterine_contractions", "light_decelerations", "severe_declerations"])
scaled_df.head()

from sklearn.model_selection import train_test_split #training and testing data split
from sklearn import metrics #accuracy measure
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, classification_report #for confusion matrix
from sklearn.linear_model import LogisticRegression,LinearRegression #logistic regression

train,test=train_test_split(data,test_size=0.3,random_state=0,stratify=data['fetal_health'])
train_X=train[train.columns[:-1]]
train_Y=train[train.columns[-1:]]
test_X=test[test.columns[:-1]]
test_Y=test[test.columns[-1:]]
X=data[data.columns[:-1]]
Y=data['fetal_health']
len(train_X), len(train_Y), len(test_X), len(test_Y)

model = LogisticRegression()
model.fit(train_X,train_Y)
prediction3=model.predict(test_X)
print('The accuracy of the Logistic Regression is',metrics.accuracy_score(prediction3,test_Y))
report = classification_report(test_Y, prediction3)
print("Classification Report:\n", report)

# Create and fit the Linear Regression model
model = LinearRegression()
model.fit(train_X, train_Y)

# Make predictions on the test set
prediction = model.predict(test_X)

# Assuming 'test_Y' contains the true labels for the test set
# Calculate the accuracy
accuracy = accuracy_score(test_Y, prediction.round())

# Print the accuracy
print('The accuracy of Linear Regression is:', accuracy)
