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

No particular method in mind, apart from a lot of exploration and visualization about the data.

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
