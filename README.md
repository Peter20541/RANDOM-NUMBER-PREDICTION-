# RANDOM-NUMBER-PREDICTION-
Predicting Random Number With Machine Learning Algorithm 


import pandas
import numpy
import time
import random
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier


#Solvers(lbfgs', 'sgd' and 'adam'.)

#All Models
modelLR = LogisticRegression(max_iter=1000)

modelDT = DecisionTreeClassifier()


#My Data
data = {"r_val":[],"÷2":[],"÷3":[],"÷4":[]}

win = 0
played = 0

# Range Loop
for i in range(9999999):
	played +=1
	r_val = random.randint(1,20)
	data["r_val"].append(r_val)
	d2 = r_val / 2
	data["÷2"].append(d2)
	d3 = r_val / 3
	data["÷3"].append(d3)
	d4 = r_val / 4
	data["÷4"].append(d4)
	df = pandas.DataFrame(data)
	xx = 500
	if i >xx:
		X = df[["÷2","÷3","÷4"]].values
		y = df["r_val"].values
		
		

		#Train , Test And Split the data
		X_train,X_test,y_train,y_test = train_test_split(X,y,train_size = 0.8,random_state = 1)
		modelLR.fit(X_train,y_train)
		pre_y = modelLR.predict([[data["÷2"][-1],data["÷3"][-1],data["÷4"][-1] ]])
		print("	\nLOGISTIC REGRESSION PREDICTED RANDOM NUMBER IS :",pre_y)
		print("model score:",modelLR.score(X_test,y_test)*100)
		
		#Fiting the model
		modelDT.fit(X_train,y_train)
		pre_DT = modelDT.predict([[data["÷2"][-1],data["÷3"][-1],data["÷4"][-1] ]])
		print("	\nDECISION TREE PREDICTED RANDOM NUMBER IS :",pre_DT)
		print("model score:",modelDT.score(X_test,y_test)*100)
		
		
		#User input
		usr = int(input("\n	 GUESS THE RANDOM NUMNBER :"))
		if usr==r_val:
			win+=1
			print("\n	YOUR GOT IT CORRECTLY IN ",played-(xx+1),"TIMES PLAYED")
			print("\n	YOUR CURRENT WINS IS :",win)
		if usr!=r_val:
			print(usr," IS THE WRONG NUMBER,",r_val," IS THE CORRECT NUMBER")
			print("\n")
		time.sleep(3)
		


