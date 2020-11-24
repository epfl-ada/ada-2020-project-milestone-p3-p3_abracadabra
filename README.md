# "Good Cops"/"Bad Cops" Profiling

## Abstract

> A 150 word description of the project idea, goals, datasets used. What's the motivation behind your project? How do you propose to extend the analysis from the paper? What story would you like to tell, and why?

The original paper studies the bias made by police officers against minorities, specifically against hispanic and black drivers.

In this project, we would like to go a step back, and to understand what are the characteristics of the police officers in that study.

The goal would be to unearth patterns that could help us understand what are the "typical profiles" of police officers that are
more likely to be biased, and to help the authorities do additional trainings to avoid the aforementioned biases against minorities.

By proposing a systematic, data-driven approach, we believe this extension to the original paper would help address
the root cause of racial issues, by allowing the concerned authorities to understand what are officers likely to make
an error of judgement in the line of duty.

## Research Questions

> A list of research questions you would like to address during the project.

* When it comes to racial biases, what is the profile of a "good cop"?
* When it comes to racial biases, what is the profile of a "bad cop"?
* In which states can we find the "best" and "worst" cops, when it comes to racial biases?
* Are we able to predict if an officier will be a "bad" / "good" cop using his profil?

## Proposed dataset

> List the dataset(s) you want to use, and some ideas on how you expect to get, manage, process, and enrich it/them. Show us that you've read the docs and some examples, and that you have a clear idea on what to expect. Discuss data size and format if relevant. It is your responsibility to check that what you propose is feasible given the datasets at hand.

As seen in [the README of the GitHub project for the paper](https://github.com/stanford-policylab/opp/blob/master/data_readme.md), we have a description of the fields that are present in the paper's dataset.

We were thinking about using at least the following fields:

* officer_id: Officer badge number or other form of identification provided by the department.
* officer_id_hash: A unique hash of the officer id used to identify individual officers within a location. This is usually just a hash of the provided officer ID or badge number.
* officer_age: The age of the stopped officer. When date of birth is given, we calculate the age based on the stop date. Values outside the range of 10-100 are coerced to NA.
* officer_dob: The date of birth of the stopped officer.
* officer_race: The race of the stopped officer. Values are standardized to white, black, hispanic, asian/pacific islander, and other/unknown
* officer_sex: The recorded sex of the stopped officer.
* officer_first_name: First name of the officer when provided.
* officer_last_name: Last name of the officer when provided.
* officer_years_of_service: Number of years officer has been with the police department.
* officer_assignment: Department or subdivision to which officer has been assigned.
* department_id: ID of department or subdivision to which officer has been assigned.
* department_name: Name of department or subdivision to which officer has been assigned.
* unit: Unit to which officer has been assigned.

## Methods

> When it comes to racial biases, what is the profile of a "good cop"?
  When it comes to racial biases, what is the profile of a "bad cop"?
  
### Racial bias coefficient
  
To capture the level of racial bias of each officier, we will create a racial bias coefficient which measure this level. Higher is the coefficient, higher is the level of racial bias of an officier. To compute this coefficient, we will use the "veil of darkness" method developed by Grogger and Ridgeway. So, for each officier, we will take a look on the two ratios $frac{# of black drivers stopped before sunset / 1 million of black persons}{# of white drivers stopped before sunset / 1 million of white persons}$ and $frac{# of black drivers stopped after sunset / 1 million of black persons}{# of white drivers stopped after sunset / 1 million of white persons}$. Thus, if a ratio is higher than the other, it highlights the fact that an officier is subject to a racial bias. Our coefficient will reflect this difference of ratio.

TO DO: See if we also include hispannic drivers
TO DO: See if we do unique coefficient or if we do one coefficient bias against black drivers and another for white drivers and see if we can improve this coefficient.

### Simple modelization of the racial bias coefficient of an officier

To understant the profil of a "bad" / "good" cop, we will fit a simple model with characteristic of officier as features and our racial bias coefficient as label. This model will be simple for the reason that it needs to be analyzable. After this, we will explore the parameters of the model to understand which characteristics increase the level of racial bias and which decrease it.

In this part, we want to give recommendations to agencies to make them enable to focus on some profils, with for example prevention day for these cops.

TO DO: Define if we use linear regression or logistic (if log coeff need to be between 0 and 1)
TO DO: Define if we build a global model or a model for each state (maybe focus on 5/6 states)

> In which states can we find the "best" and "worst" cops, when it comes to racial biases?

### Statistical exploration of the racial bias coefficient

In this part, we will take a statistical look on our racial bias coefficient to understand the distribution of "bad" / "good" cop accross different states.

TO DO: Define stat to use (maybe hard without a first look on the coefficient)

> Are we able to predict if an officier will be a "bad" / "good" cop using his profil?

### Complex modelization of the racial bias coefficient of an officier

In this part, we will use a more complex model using an extended features space from the original characteristic of officier to label the racial bias coefficient. The goal is to obtain good predictions to be able to predict the level of racial bias of an officier.

TO DO: Define model (linear regression, logistic, NN ...)

## Proposed timeline

1. Have a notebook working with the original datasets
2. Getting the arrests numbers for one specific officer
3. Generalize for all officers in a state (or maybe a department/unit first)
4. Given the data in previous steps, think about attributes for the "good cop"/"bad cop" profiles
5. Make the profiles more precise
6. Do a summary and visualizations about those profiles

## Organization within the team

> A list of internal milestones up until project milestone P4. Add here a sketch of your planning for the next project milestone.

Basically, separate the steps above in between the team members. 1 and 2 should be done as early as possible, possibly with the whole team.

All of the other tasks could then be parallelized.

## Questions for TAs (optional)

> Add here any questions you have for us related to the proposed project.

* Does this sound realistic given the timeframe we have?
* The opposite of the question above: does this sound too simple given the timeframe we have? Should we do more?
