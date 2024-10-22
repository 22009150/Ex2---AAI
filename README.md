<H3>Enter Name : ARCHANA K</H3>
<H3>Enter Register No : 212222240011</H3>
<H3>Experiment 2</H3>
<H3>Date : 02-09-2024</H3>
<h1 align =center>Implementation of Exact Inference Method of Bayesian Network</h1>

## Aim :
To implement the inference Burglary P(B| j,⥗m) in alarm problem by using Variable Elimination method in Python.

## Algorithm :

### Step 1 :

Define the Bayesian Network structure for alarm problem with 5 random variables, Burglary,Earthquake,John Call,Mary Call and Alarm.<br>

 ### Step 2 :
 
Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class from the pgmpy library.<br>
 
### Step 3 :

Add the CPDs to the network.<br>

### Step 4 :

Initialize the inference engine using the VariableElimination class from the pgmpy library.<br>

### Step 5 :

Define the evidence (observed variables) and query variables.<br>

### Step 6 :

Perform exact inference using the defined evidence and query variables.<br>

### Step 7 :

Print the results.<br>

## Program :

### Import the Libraries :
```python
from pgmpy.models import BayesianNetwork
from pgmpy.inference import VariableElimination
```


### Define the network structure :
```python
alarm_model = BayesianNetwork(
    [
        ("Burglary", "Alarm"),
        ("Earthquake", "Alarm"),
        ("Alarm", "JohnCalls"),
        ("Alarm", "MaryCalls"),
    ]
)
```

### Define the Conditional Probability Distributions (CPDs) :
```python

from pgmpy.factors.discrete import TabularCPD

cpd_burglary = TabularCPD(
    variable="Burglary", variable_card=2, values=[[0.999], [0.001]]
)
cpd_earthquake = TabularCPD(
    variable="Earthquake", variable_card=2, values=[[0.998], [0.002]]
)
cpd_alarm = TabularCPD(
    variable="Alarm",
    variable_card=2,
    values=[[0.999, 0.71, 0.06, 0.05], [0.001, 0.29, 0.94, 0.95]],
    evidence=["Burglary", "Earthquake"],
    evidence_card=[2, 2],
)
cpd_johncalls = TabularCPD(
    variable="JohnCalls",
    variable_card=2,
    values=[[0.95, 0.1], [0.05, 0.9]],
    evidence=["Alarm"],
    evidence_card=[2],
)
cpd_marycalls = TabularCPD(
    variable="MaryCalls",
    variable_card=2,
    values=[[0.99, 0.3], [0.01, 0.7]],
    evidence=["Alarm"],
    evidence_card=[2],
)
```
###  Associating the parameters with the model structure :
```python
alarm_model.add_cpds(
    cpd_burglary, cpd_earthquake, cpd_alarm, cpd_johncalls, cpd_marycalls
)
```

```python
alarm_model.check_model()
```

### Initializethe inference :
```python
inference=VariableElimination(alarm_model)
```


### Perform inference :
```python

evidence={"JohnCalls":1,"MaryCalls":0}
evidence2={"JohnCalls":1,"MaryCalls":1}
query='Burglary'
```

### Print the final value :

```python
res=inference.query(variables=[query],evidence=evidence)
res2=inference.query(variables=[query],evidence=evidence2)
print(res)
print(res2)
```

## Output :

![Screenshot 2024-09-03 182803](https://github.com/user-attachments/assets/2091c3eb-b5cd-4d31-beaf-60ea3da32fdf)

![Screenshot 2024-09-03 182810](https://github.com/user-attachments/assets/7db2905d-2f94-4162-919a-31dc0c6fdd46)



## Result :

Thus, Bayesian Inference was successfully determined using Variable Elimination Method.

