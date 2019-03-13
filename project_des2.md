# Model Proposal for Temporal Dynamics of Network Attractor Memories

Bolaji Eniwaye

* Course ID: CMPLXSYS 530,
* Course Title: Computer Modeling of Complex Systems
* Term: Winter, 2019



&nbsp; 

### Goal 
*****
 
_Provide a short, 1-3 sentence description of the goal of your model_

I will be modeling a network of neurons and introducing spiking attractors that represent memory formation. I will then look at the temporal dynamics of the attractors in response to different initialization.

&nbsp;  
### Justification
****
_Short explanation on why you are using ABM_

Because neural networks consist of many different interacting units, neurons, agent based techniques are natural for the analysis of neural networks.

&nbsp; 
### Main Micro-level Processes and Macro-level Dynamics of Interest
****

_Short overview of the key processes and/or relationships you are interested in using your model to explore. Will likely be something regarding emergent behavior that arises from individual interactions_

The two important qualities of neurons are that they spike(have drastic changes in membraine potential) and that they connect with other neurons. Although the spiking dynamics of each individual neuron can be analyzed the more interesting behavior is the pattern of spiking of neuron groups that occurs as the result of the connections between neurons.. In this case we will be looking at the localization of spiking groups. 

&nbsp; 


## Model Outline
****

I will be using a modified version of the Hodgekin Huxley equations that govern neuron dyanmics where the modification is an ion current that inhibits a neuron the more it fires. I will then introduce two classes of neurons, inhibitory and excitatory, where inhibitory neurons inhibit their neighbors spike rate and excitatory neurons promote their neighbors spike rate. Each inbitotry neuron will be connected to every other neuron in the network while the excitatory neurons will be connected only to its neighbors within a certain radius. I will then introduce attractors by increasing the synaptic strength of neurons within a specific region. I will implement a learning rule tha leads to the destabilization of attractors over time. 


&nbsp; 
### 1) Environment
_Description of the environment in your model. Things to specify *if they apply*:_

* _Boundary conditions (e.g. wrapping, infinite, etc.)_
* _Dimensionality (e.g. 1D, 2D, etc.)_
* _List of environment-owned variables (e.g. resources, states, roughness)_
* _List of environment-owned methods/procedures (e.g. resource production, state change, etc.)_


The environment will be the two lattices of excitatory neurons and inhibitory neurons where I will have roughly 1000 excitatory neurons and 250 inhibitory neurons. The map will be a square grid consisting of both populations. The dimensionaliity with therefore be two dimensional with wrapped boundary conditions. The envirosment will consist of localized current inputs such that neurons in certain regions are exposed to different amounts of external input. 
```
# Include first pass of the code you are thinking of using to construct your environment
# This may be a set of "patches-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any patch methods/procedures you have. Filling in with pseudocode is ok! 
# NOTE: If using Netlogo, remove "python" from the markdown at the top of this section to get a generic code block

#THIS CODE IS PROTOTYPED IN C++ AND WILL BE TRANSCRIBED TO PYTHON FOR THE FINAL RESULT

//set up of neuron location
if(i!=0){if( (radius_connect_ee[i-1][1]-floor((i)/ (sqrt(nexc))) ) !=0  ){x_coor_counter=0; }} // so this is to basically set where the neuron is in the column, so this line of code resets if move to the next row to start in the zero column
	radius_connect_ee[i][0]= x_coor_counter;//i%( (int) round(sqrt(nexc)));

	radius_connect_ee[i][1]= floor((i)/ (sqrt(nexc)));

	radius_con_ee_text<< radius_connect_ee[i][0];	
	radius_con_ee_text << " ";

	radius_con_ee_text<< radius_connect_ee[i][1];
	radius_con_ee_text<<endl;
x_coor_counter++;
}

//////////////////////////////////////////
//set up of connections between neurons
bool rewire;
double distance_prob;
double distance_prob_2;
int preconnectivityee[nexc][nexc];
	for(int i=0;i<nexc;i++)
	{
		for(int j=0;j<nexc;j++)
		{
			//cout<< randee<<endl;
			randee=((double)rand()/(RAND_MAX));
			
		// distance_prob=gaus_prob_2D(radius_connect_ee[i][0],radius_connect_ee[i][1],radius_connect_ee[j][0],radius_connect_ee[j][1], sqrt(nexc)/3 ); //(xcoor_self,ycoor_self,xcoor_neighbor,ycoor_neighbor, max_size); // so this is for a gussian 
                 distance_prob=radius_prob_2D(radius_connect_ee[i][0],radius_connect_ee[i][1],radius_connect_ee[j][0],radius_connect_ee[j][1], nexc,nexc,16);
                  //radius_prob_2D(int xcoor_self, int ycoor_self,int xcoor_neighbor, int ycoor_neighbor, nexc ,n_neigh,kxx)         
		if(j>1200)//j%100==0)
		{// cout<< j <<" " << radius_connect_ee[i][0]<<" " << radius_connect_ee[i][1] <<" " << radius_connect_ee[j][0] <<" " << radius_connect_ee[j][1] << " " << distance_prob << endl;
		}


			//rewire=randee<pconee;
			rewire=randee<distance_prob;
			
			if ((rewire))
			{


				preconnectivityee[i][j]=1;


			}else
			{
				preconnectivityee[i][j]=0;
			}

		}
	}




//int connectivityee[nexc][nexc];

int **connectivityee = new int*[nexc];

for(int i=0; i<nexc; i++)
{
connectivityee[i]= new int[nexc];
}


	for(int i=0; i<nexc;i++)
	{
		for(int j=0; j<nexc;j++)
		{
			//cout<<preconnectivityee[j][i]<<"hi"<<endl;
			connectivityee[i][j]= preconnectivityee[j][i];
			connectivityeetext<<connectivityee[i][j];
			connectivityeetext<< " ";
		}
		connectivityeetext<<endl;
	}


	for(int i=0; i<nexc; i++) // I just did this on july 26, because excitatory  cant go down
	{
		for (int j=0; j<nexc; j++ )
		{
			if(connectivityee[i][j]){
			w[i][j]=gsynee;}

		}

	}


```

&nbsp; 

### 2) Agents
 
 _Description of the "agents" in the system. Things to specify *if they apply*:_
 
* _List of agent-owned variables (e.g. age, heading, ID, etc.)_
* _List of agent-owned methods/procedures (e.g. move, consume, reproduce, die, etc.)_


```
# Include first pass of the code you are thinking of using to construct your agents
# This may be a set of "turtle-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any agent methods/procedures you have so far. Filling in with pseudocode is ok! 
# NOTE: If using Netlogo, remove "python" from the markdown at the top of this section to get a generic code block

//Set up of the agents and paramters
// Sim1 is analogous to turtles own
struct sim1 {
	double Vv;
	//double spiketimesdyn;
	double mv;
	double nv;
	double sv;
	//double zv;
	double hv;
	//double isyn;
};



//////////////////////
//Differential equations governing certain variables
double hinf(double V){
	double x;
	x=pow((1+exp((V+53.0)/(7.0) )),(-1));
	return x;
};

double tauh(double V){
	double x;
		x= 0.37 + 2.78*pow((1 + exp( (V+40.5)/(6.0) ) ),(-1));
		return x;
};

double ninf(double V) {
	double x;
	x=pow((1+exp( - (V+30.0)/10.0 )),(-1));
	return x;
};
double minf(double V ){
	double x;
	x=pow( (1+exp( ((-V-30.0)/9.5 ) )),(-1));
	return x;
}

//////////////////gausprob
double gaus_prob_2D(int xcoor_self, int ycoor_self,int xcoor_neighbor, int ycoor_neighbor, double std)
{
	double p;
	//(1/(2*pi))*(1/(pow(std,2)))*
	p=exp(    -(   (pow((xcoor_neighbor-xcoor_self),2))   / (2*(pow(std,2)))  )   - ( pow((ycoor_neighbor-ycoor_self),2)) / (2*(pow(std,2)))  ) ;     //);		
        return p;

}



double radius_prob_2D(int xcoor_self, int ycoor_self,int xcoor_neighbor, int ycoor_neighbor,int nexc , int n_neigh, int kxx)
{
	double p;
	//(1/(2*pi))*(1/(pow(std,2)))*
	if(     sqrt( pow((xcoor_neighbor-xcoor_self) , 2) + pow((ycoor_neighbor-ycoor_self),2) ) <= 1.01*sqrt( nexc*kxx/(n_neigh*pi) )   ){p=1 ;}
	else
        {p=0;}			
        return p;

}


////////////////////////





double taun(double V) {
	double x;
	x=0.37 + 1.85*pow((1 + exp( (V+27.0)/(15.0) ) ),(-1));
	return x;
};

double sinf(double V) {
	double x;
	x=pow((1+exp( - (V+39.0)/5.0 )),(-1));
	return x;
};

double taus(double V ){
	return 75.0;
}

double an (double V) {
	double x;
	x=0.01*(V+10.0)/(exp( (V+10.0)/10.0 ) -1);
	return x;
};

double bn (double V){

	double x;
	x= 0.125*exp(V/80.0);
	return x;
};

double am (double V){
	double x;
	x=0.1*(V+25.0)/(exp( (V+25.0)/10.0 ) -1);
	return x;
};

double bm (double V){
	double x;
	x=4*exp(V/18.0);
	return x;
};

double ah(double V){
	double x;
	x= 0.07*exp(V/20.0);
	return x;
};
double bh(double V){
	double x;
	x= 1/(exp((V+30.0)/10.0) +1);
	return x;
};

/////////////////////////////////////////////////////////////////////////////////////////////////


	double hd(double V,double hv){
		double x;
		x=(1.0/tauh(V))*(hinf(V)-hv);
		return x;
	}
	double nd(double V,double nv){
		double x;
		x=(1.0/taun(V))*(ninf(V)-nv);
		return x; }
	double sd(double V,double sv){
		double x;
		x=(1.0/taus(V))*(sinf(V)-sv);
		return x;
	}

	double md(double V,double mv){
		double x;
		x=0;
		return x;
	}
	double Vd(double V, double gna,double minf,double hv,double sv,double nv,double Vna,double Vk, double Vl, double gkdr,double gks,double gl,double Iext,double Isyn,double Id, double C){
		double Vout;
		Vout= (1.0/C)*(-gna*pow(minf,3)*hv*(V-Vna)-gkdr*pow(nv,4)*(V-Vk)-gks*sv*(V-Vk)-gl*(V-Vl)+Iext-Isyn +Id);
		return Vout;
	}

//gatingpm1 gatecomp;


sim1 V_integrate(double V1,double mv1, double nv1, double sv1, double hv1, double isyn1,double Iext,double Id,double dt,double gks){

	sim1 calcout;

	double C=1.0; // uF/cm^2
	double Is=0; //
	//double Id=2;

	double In=0;
	double Vna=55.0; //% mV
	double Vk= -90.0;// % mV
	double Vl=-60.0; //% mv
	double gkdr=3.0; //%mS/cm^2
	double gna= 24.0;// % mS/cm^2
	double gl=0.02; //% mS/cm^2


	double Vk1, hk1, nk1, sk1, halfdt, sixthdt;
	double Vk2, hk2, nk2, sk2;
	double Vk3, hk3, nk3, sk3;
	double Vk4, hk4, nk4, sk4;
	halfdt=(dt/2.0);
	sixthdt=(dt/6.0);


	//double dt=.05;


	Vk1=Vd(V1,gna,mv1,hv1,sv1,nv1,Vna,Vk,Vl,gkdr,gks,gl,Iext,isyn1,Id,C);
	hk1=hd(V1,hv1);
	nk1=nd(V1,nv1);
	sk1=sd(V1,sv1);


	Vk2=Vd(V1+halfdt*Vk1,gna,mv1,hv1+halfdt*hk1,sv1+halfdt*sk1,nv1+halfdt*nk1,Vna,Vk,Vl,gkdr,gks,gl,Iext,isyn1,Id,C);
	hk2=hd(V1+halfdt*Vk1,hv1+halfdt*hk1);
	nk2=nd(V1+halfdt*Vk1,nv1+halfdt*nk1);
	sk2=sd(V1+halfdt*Vk1,sv1+halfdt*sk1);

	Vk3=Vd(V1+halfdt*Vk2,gna,mv1,hv1+halfdt*hk2,sv1+halfdt*sk2,nv1+halfdt*nk2,Vna,Vk,Vl,gkdr,gks,gl,Iext,isyn1,Id,C);
	hk3=hd(V1+halfdt*Vk2,hv1+halfdt*hk2);
	nk3=nd(V1+halfdt*Vk2,nv1+halfdt*nk2);
	sk3=sd(V1+halfdt*Vk2,sv1+halfdt*sk2);

	Vk4=Vd(V1+dt*Vk3,gna,mv1,hv1+dt*hk3,sv1+dt*sk3,nv1+dt*nk3,Vna,Vk,Vl,gkdr,gks,gl,Iext,isyn1,Id,C);
	hk4=hd(V1+dt*Vk3,hv1+dt*hk3);
	nk4=nd(V1+dt*Vk3,nv1+dt*nk3);
	sk4=sd(V1+dt*Vk3,sv1+dt*sk3);


    //calcout = V_integrate(V[i],m[i],n[i],s[i],h[i],isyn[i],Iex );


	calcout.Vv= V1+ sixthdt*(Vk1 + 2.0*Vk2+2.0*Vk3+Vk4);
    calcout.hv=hv1+ sixthdt*(hk1 + 2.0*hk2+2.0*hk3+hk4);
    calcout.mv=minf(V1);//md(V1,mv1)*dt+mv1;
    calcout.nv=nv1+ sixthdt*(nk1 + 2.0*nk2+2.0*nk3+nk4);
    calcout.sv=sv1+ sixthdt*(sk1 + 2.0*sk2+2.0*sk3+sk4);
	return calcout;
}



```

&nbsp; 

### 3) Action and Interaction 
 
**_Interaction Topology_**

_Description of the topology of who interacts with whom in the system. Perfectly mixed? Spatial proximity? Along a network? CA neighborhood?_
As described in the model description The inhibitory and excitatory neurons will be distributed uniformly over the square lattice. Inhibitry neurons will be connected to every other neuron in the network while the excitatory neurons will be connected only to its neighbors within a certain radius. This means that the exciatory neurons will be connected to about 4 times as many excitatory neurons as inhibitory neurons. I will then introduce attractors by increasing the synaptic strength of  connections within a specific region.
 
**_Action Sequence_**

_What does an agent, cell, etc. do on a given turn? Provide a step-by-step description of what happens on a given turn for each part of your model_

1. Sum all input currents
2. calculate change in voltage/other parameters
3. add input to neightbors

&nbsp; 
### 4) Model Parameters and Initialization

_Describe and list any global parameters you will be applying in your model._

_Describe how your model will be initialized_

_Provide a high level, step-by-step description of your schedule during each "tick" of the model_

Global paramters
double dt=0.05; // ms
double runtime=2000;//500;// 2000.0; // ms
int ninh=250; // number of inhibitory neurons
int nexc=1000;// number of excitatory neurons


//initialization
At the first time step each parameter will be given a random value in the following range.
 Vi=-62+rand*40;
 ni=.2 +rand*.6;
 si=0.2+rand*.1;
 mi=0;
 hi=.2+rand*.6;
 Where rand is a random number between zero and one.
 
//timestep
Each neuron will follow the equations
dv/dt= (1.0/C)*(-gna*pow(minf,3)*hv*(V-Vna)-gkdr*pow(nv,4)*(V-Vk)-gks*sv*(V-Vk)-gl*(V-Vl)+Iext-Isyn +Id);
which will be based off of parameters that follow the equations
dh/dt=(1.0/tauh(V))*(hinf(V)-hv);
dn/dt=(1.0/taun(V))*(ninf(V)-nv);
ds/dt=(1.0/taus(V))*(sinf(V)-sv);
Where the derivative multiplied by the time step will be added to the to values of the variable at each time step.

Additionally, at each time set the sum of the inputs will be computed.


 

&nbsp; 

### 5) Assessment and Outcome Measures

_What quantitative metrics and/or qualitative features will you use to assess your model outcomes?_

The aim of the model is to analyze the stability of spiking attractors in response to different parameters such as the radius of connection and strength of connections. I will add learning rules between adjacent neurons and then look at the effect of intial instantiation of parameters and time evolution of the attractor. By time evolution I mean that I will look at the radial distribution of firing rate and see how the variance changes for time. I will expect that the initial radius of enconding and strength will have a signficant impact on the change in spiking distribution. 

&nbsp; 

### 6) Parameter Sweep

_What parameters are you most interested in sweeping through? What value ranges do you expect to look at for your analysis?_

For the parameter sweep I will run through the radius of effect for excitatory to inhibitory as well as excitatory to exciatory connections as  well as the strength of the initial synapse. I will also scan over the strength of the excitatory connection and look map the rate of change of the attractors. I hope that for certain combinations of parameters that there will be a linear relation ship between the change in the variance of the attraction radius and linear time. 
