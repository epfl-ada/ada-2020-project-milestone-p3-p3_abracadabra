# "Good Cops"/"Bad Cops" Profiling

NB: This ReadMe includes pictures of the repository https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img

## Abstract

> A 150-word description of the project idea, goals, datasets used. What's the motivation behind your project? How do you propose to extend the analysis from the paper? What story would you like to tell, and why?

The original paper studies the bias made by police officers against minorities, specifically against Hispanic and black drivers.

In this project, we would like to go a step back and to understand what are the characteristics of the police officers in that study.

The goal would be to unearth patterns that could help us understand what are the "typical profiles" of police officers that are
more likely to be biased, and to help the authorities do additional training to avoid the aforementioned biases against minorities.

By proposing a systematic, data-driven approach, we believe this extension to the original paper would help address
the root cause of racial issues, by allowing the concerned authorities to understand which officers are likely to make
an error of judgement in the line of duty.

## Research Questions

> A list of research questions you would like to address during the project.

* When it comes to racial biases, what is the profile of a "good cop"?
* When it comes to racial biases, what is the profile of a "bad cop"?
* In which states can we find the "best" and "worst" cops when it comes to racial biases?
* Are we able to predict if an officer will be a "bad" / "good" cop using his profile? 
* Can we find officers with a behaviour that deviate from the normal: officers who provoke an excessive amount of stop and arrests; officers which use an excessive amount of force.
* Are we able to draw a link between officers who are excessively violents and those that have a racial bias?
* Are officers with high responsability less violents than others? Do those officers have a past record indicating that?

## Proposed dataset

> List the dataset(s) you want to use, and some ideas on how you expect to get, manage, process, and enrich it/them. Show us that you've read the docs and some examples and that you have a clear idea on what to expect. Discuss data size and format if relevant. It is your responsibility to check that what you propose is feasible given the datasets at hand.

As seen in [the README of the GitHub project for the paper](https://github.com/stanford-policylab/opp/blob/master/data_readme.md), we have a description of the fields that are present in the paper's dataset.

We were thinking about using at least the following fields:

* officer_id: Officer badge number or other forms of identification provided by the department.
* officer_id_hash: A unique hash of the officer id used to identify individual officers within a location. This is usually just a hash of the provided officer ID or badge number.
* officer_age: The age of the stopped officer. When the date of birth is given, we calculate the age based on the stop date. Values outside the range of 10-100 are coerced to NA.
* officer_dob: The date of birth of the stopped officer.
* officer_race: The race of the stopped officer. Values are standardized to white, black, Hispanic, Asian/pacific islander, and other/unknown
* officer_sex: The recorded sex of the stopped officer.
* officer_first_name: First name of the officer when provided.
* officer_last_name: Last name of the officer when provided.
* officer_years_of_service: Number of years officer has been with the police department.
* officer_assignment: Department or subdivision to which officer has been assigned.
* department_id: ID of department or subdivision to which officer has been assigned.
* department_name: Name of department or subdivision to which officer has been assigned.
* unit: Unit to which officer has been assigned.

In order to measure the behaviour of an officer we could use the following fields:

##### Search and arrest:
* search_basis 	This provides the reason for the search where provided and is categorized into k9, plain view, consent, probable cause, and other...
* reason_for_arrest 	A freeform text field indicating the reason for arrest where provided. 	
* reason_for_frisk 	A freeform text field indicating the reason for frisk where provided. 	
* reason_for_search 	A freeform text field indicating the reason for search where provided. 	
* reason_for_stop 	A freeform text field indicating the reason for the stop where provided.
##### use of force:
* use_of_force_description 	A freeform text field describing the use of force. 	"handcuffed"
* use_of_force_reason 	A freeform text field describing the reason for the use of force.
##### Fields which indicate if a search and stop was conclusive
* contraband_found 	Indicates whether contraband was found. When search_conducted is NA, this is coerced to NA under the assumption that contraband_found shouldn't be discovered when no search occurred and likely represents a data error. 	
* contraband_drugs 	Indicates whether drugs were found. This is only defined when contraband_found is true. 	
* contraband_weapons 	Indicates whether weapons were found. This is only defined when contraband_found is true. 	
*  contraband_other 	Indicates whether contraband other than drugs and weapons were found. This is only defined when contraband_found is true.

## Methods

### Creating statistics: Determining if an officer deviates from the normal
In one of our research questions we wondered if we could find officers with an excessively violent behaviour.
We could try to find officers which provoke a number of stops arrests, that deviate from the normal. This could indicate policemen who are looking for action. We could then check if officers which use force more often than other police officers are linked to those who stop people excessively or to officers that have a racial bias. 
#### Finding excessive violence
We could try to enumerate the number of times an officer used force. We could then compare this number to the median use of force by officers in his department, unit or in the US. From that we could qualify if an officer's behaviour deviates from the normal. We could do some refinement and even create statistics telling whether or not an officer is excessively violent towards a certain race. 
#### Finding excessive arrests.
We could do something analogous to the analysis of the use of force.
#### Qualifying whether or not arrest are unjustified:
Per officer we could determine the ratio of (arrest and search which are conclusive) / (arrest and searches). We could then compare this value to the national, department, unit medians. By conclusive we mean that either one of the fields in "Fields which indicate if a search and stop was conclusive" is indicating something positive indicating the search led to some finding.

### Racial bias coefficient

To capture the level of racial bias of each officier, we will create a racial bias coefficient <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/delta.PNG"> which measures this level. Higher is the coefficient, higher is the level of racial bias of an officer. To compute this coefficient, we will use the "veil of darkness" method developed by Grogger and Ridgeway.

Let <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/alpha.PNG"> be the number of race r drivers stopped at time t

Where r can be:
* b: black
* h: hispanic
* w: white

And t can be:
* b: before sunset
* a: after sunset

We define <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/beta.PNG"> the proportion of race r drivers stopped at time t:

<img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/formulae_beta.PNG">

Let's condider <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/sigma.PNG"> the ratio of the proportion of race r drivers stopped before sunset over the proportion of the race r drivers stopped after sunset:

<img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/formulae_sigma.PNG">

Now, let's define <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/lambda.PNG"> the absolute value of the previous ratio over all races, centered:

<img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/formulae_lambda.PNG">

where <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/N.PNG"> is the number of different races in the studies (here we have <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/N_3.PNG">)

Finally, we can define <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/delta.PNG"> our racial bias coefficient:

<img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/formulae_delta.PNG">

We have designed this coefficient on three principal ideas:
* If there are some little differences between <img src="https://github.com/epfl-ada/ada-2020-project-milestone-p3-p3_abracadabra/blob/master/img/sigma_b_h_w.PNG">, we want to not penalize the racial bias coefficient since these differences can be due of a noise (we are looking stop for each officier so we do not have the same amount of data than for each state).
* If there are big differences, we want to penalize a lot.
* If an officier harshly focus a race, we want to penalize a lot.

> When it comes to racial biases, what is the profile of a "good cop"?

> When it comes to racial biases, what is the profile of a "bad cop"?

### Simple modelization of the racial bias coefficient of an officer

To understand the profile of a "bad" / "good" cop, we will fit a simple model with the characteristics of officers as features and our racial bias coefficient as the label. This model will be simple for the reason that it needs to be analyzable. After this, we will explore the parameters of the model to understand which characteristics increase the level of racial bias and which decrease it.

In this part, we want to give recommendations to agencies to enable them to focus on some profiles, with for example prevention day for these cops.


> In which states can we find the "best" and "worst" cops when it comes to racial biases?


### Statistical exploration of the racial bias coefficient

In this part, we will take a statistical look at our racial bias coefficient to understand the distribution of "bad" / "good" cop across different states.

> Are we able to predict if an officer will be a "bad" / "good" cop using his profile?

### Complex modelization of the racial bias coefficient of an officer

In this part, we will use a more complex model using an extended features space from the original characteristic of an officer to label the racial bias coefficient. The goal is to obtain good predictions to be able to predict the level of the racial bias of an officer.

## Proposed timeline

1. Have a notebook working with the original datasets
2. Getting the arrests numbers for one specific officer
3. Generalize for all officers in a state (or maybe a department/unit first)
4. Given the data in previous steps, think about attributes for the "good cop"/"bad cop" profiles
5. Make the profiles more precise
6. Do a summary and visualizations about those profiles

## Organization within the team

> A list of internal milestones up until project milestone P4. Add here a sketch of your planning for the next project milestone.

Separate the steps above in between the team members. 1 and 2 should be done as early as possible, possibly with the whole team.

All of the other tasks could then be parallelized.

## Questions for TAs (optional)

> Add here any questions you have for us related to the proposed project.

* Does this sound realistic given the timeframe we have?
* The opposite of the question above: does this sound too simple given the timeframe we have? Should we do more?

## Contributions

RBC: racial bias coefficient

### Kevin

* Part compute RBC and model officer RBC
* import and preprocess data + analyze (figure and pearson)
* Write the corresponding part on the website (question 2)

### David

* Setting up the website + basic text in there
* Questions 1 and 5 in the website + notebook

### Simon

* Part of Question 2
* Question 3
* 
