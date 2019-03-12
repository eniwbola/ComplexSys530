# Model Proposal for Temporal Dynamics of Network Attractor Memories

Bolaji Eniwaye

* Course ID: CMPLXSYS 530,
* Course Title: Computer Modeling of Complex Systems
* Term: Winter, 2019



&nbsp; 

### Goal 
*****
 
_Provide a short, 1-3 sentence description of the goal of your model_
I will be modelling a network of neurons and introducing spiking attractors that represent memory formation. I will then look at the temporal dynamics of the attractors.

&nbsp;  
### Justification
****
_Short explanation on why you are using ABM_
 Because neural networks consist of many different interacting units, neurons, agent based techniques are natural for the analysis of neural networks.

&nbsp; 
### Main Micro-level Processes and Macro-level Dynamics of Interest
****

_Short overview of the key processes and/or relationships you are interested in using your model to explore. Will likely be something regarding emergent behavior that arises from individual interactions_
The two important qualities of neurons are that they spike(have drastic changes in membraine potential) and that they connect with other neurons. Although the spiking dynamics of each individual neuron can be analyzed the more interesting behavior is the pattern of spiking of neuron groups that occurs as the result of the connections between neurons which causes connected neurons of to be primed to spike if their neighbor previously spikes. In this case we will be looking at the localization of spiking groups. 

&nbsp; 


## Model Outline
****

I will be using a modified version of the hodgekin huxley equations that govern neuron dyanmics where the modiffication is an ion current that inhibits a neuron the more it fires. I will then introduce two classes of neurons, inhibitory and excitatory, where inhibitory neurons inhibit their neighbors spike rate and excitatory neurons promote their neighbors spike rate.  The each inbitotry neruons will be connected to every other neuron in the network while the excitatory neurons will be connected only to its neighbors within a certain radius. I will then introduce attractors by increasing the synaptic strength of neurons within a specific region. 


&nbsp; 
### 1) Environment
_Description of the environment in your model. Things to specify *if they apply*:_

* _Boundary conditions (e.g. wrapping, infinite, etc.)_
* _Dimensionality (e.g. 1D, 2D, etc.)_
* _List of environment-owned variables (e.g. resources, states, roughness)_
* _List of environment-owned methods/procedures (e.g. resource production, state change, etc.)_


The environment with tbe the two lattices of excitatory neurons and inhibitory neurons where I will have roughly 1000 excitatory neurons and 250 inhibitory neurons. Such that the map will be and a grid consisting of both populations. The dimensionaliity with therefore be two dimensional will wrapped bounday condtions. The envirosment with will consist of localized current inputs such that neurons in certain regions are exposed to different amounts of external input. 
```python
# Include first pass of the code you are thinking of using to construct your environment
# This may be a set of "patches-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any patch methods/procedures you have. Filling in with pseudocode is ok! 
# NOTE: If using Netlogo, remove "python" from the markdown at the top of this section to get a generic code block
```

&nbsp; 

### 2) Agents
 
 _Description of the "agents" in the system. Things to specify *if they apply*:_
 
* _List of agent-owned variables (e.g. age, heading, ID, etc.)_
* _List of agent-owned methods/procedures (e.g. move, consume, reproduce, die, etc.)_


```python
# Include first pass of the code you are thinking of using to construct your agents
# This may be a set of "turtle-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any agent methods/procedures you have so far. Filling in with pseudocode is ok! 
# NOTE: If using Netlogo, remove "python" from the markdown at the top of this section to get a generic code block
```

&nbsp; 

### 3) Action and Interaction 
 
**_Interaction Topology_**

_Description of the topology of who interacts with whom in the system. Perfectly mixed? Spatial proximity? Along a network? CA neighborhood?_
 
**_Action Sequence_**

_What does an agent, cell, etc. do on a given turn? Provide a step-by-step description of what happens on a given turn for each part of your model_

1. Step 1
2. Step 2
3. Etc...

&nbsp; 
### 4) Model Parameters and Initialization

_Describe and list any global parameters you will be applying in your model._

_Describe how your model will be initialized_

_Provide a high level, step-by-step description of your schedule during each "tick" of the model_

&nbsp; 

### 5) Assessment and Outcome Measures

_What quantitative metrics and/or qualitative features will you use to assess your model outcomes?_

&nbsp; 

### 6) Parameter Sweep

_What parameters are you most interested in sweeping through? What value ranges do you expect to look at for your analysis?_
