# Exploring-Food-Safety-AI-Data-and-Applications

## Overview
### Introduction
Aims are to develop deeper collaboration to build out AI infrastructure for

1. Food safety testing database to power AI applications in produce safety
2. Federated Learning for collaborative and privacy-preserving learning
3. Allocation strategies for improved supply change resilience against disastrous events

### Methods
#### Allocation Strategies for Limited Food Resources during Disastrous Events

To model food bank demand and improve supply chain resilience, we collected data from two key sources: the Capital Area Food Bank (CAFB) Hunger Estimates dataset [https://catalog.data.gov/dataset/capital-area-food-bank-hunger-estimates]  and the Mid-Ohio Foodbank's "Community Response to Hunger" (CRH) dataset [https://data.world/smartcolumbusos/21d29da9-537c-4703-97b8-9d044f2c4231].

The CAFB Hunger Estimates dataset includes detailed information on hunger and food insecurity across Census Tracts in the DMV (DC, Maryland, and Virginia) area. Compiled by the CAFB through internal tracking and shared with the DC government, the dataset provides insights into food insecurity trends for the years 2014 and 2015. It includes estimates of food insecurity rates, the number of food-insecure individuals, the pounds of food needed and distributed, and the unmet need for food assistance in each census tract.

For supply modeling, we utilized the CRH dataset from the Mid-Ohio Foodbank. This dataset, titled "Services received from Food Pantries 2016-2017," is part of a multi-year analysis to better understand the true level of need within the community. Covering the period from July 1, 2016, through June 30, 2017, the dataset includes approximately 490,000 service records. These records detail the date of service, place of service, and type of service for every visit made by approximately 86,000 families. The goal of this dataset and analysis is to foster constructive conversations and meaningful action with the support of the entire community around the issue of hunger.

By leveraging these datasets, we aim to develop effective allocation strategies for limited food resources during disastrous events, ensuring that resources are distributed efficiently and equitably to those in need.

To model food bank demand and improve supply chain resilience, we collected data from the Capital Area Food Bank (CAFB) Hunger Estimates dataset. This dataset includes detailed information on hunger and food insecurity across Census Tracts in the DMV (DC, Maryland, and Virginia) area. Compiled by the CAFB through internal tracking and shared with the DC government, the dataset provides insights into food insecurity trends for the years 2014 and 2015. It includes estimates of food insecurity rates, the number of food-insecure individuals, the pounds of food needed and distributed, and the unmet need for food assistance in each Census Tract. This comprehensive data is essential for developing effective allocation strategies for limited food resources during disastrous events, ensuring that resources are distributed efficiently and equitably to those in need.

We use linear programming and incorporate a uniform delay to optimize the allocation of food resources. This approach ensures that resources are distributed efficiently and equitably, even during challenging circumstances.

### Results
#### Allocation Strategies for Limited Food Resources during Disastrous Events
In this application of online resource allocation problem, we validated and provided a framework that can achieve a constant regret comparing to hindsight. [Figure here].

## Usage
### Setup
Mention the environment the code was run on during development and testing as well as any dependencies that are needed.

### Running
Explain in detailed steps how to run the code in order to reproduce the results shown above in the results section.

## Authors
You can view the list of authors in the [AUTHORS](/AUTHORS) file.

## Contact
Corresponding author: Matthew J. Stasiewicz<br>
103 Agricultural Bioprocess Lab<br>
1302 W. Pennsylvania<br>
Urbana, IL, 1361801<br>
USA<br>
+1-217-265-0963<br>
[mstasie@illinois.edu](mailto:mstasie@illinois.edu)

## Citation
Include citation here.

## License
This project's code is licensed under the GNU General Public License v3.0 and dataset is licensed the Creative Commons Attribution Share Alike 4.0 International license. Please see the [LICENSE.code](/LICENSE.code) and [LICENSE.dataset](/LICENSE.dataset) files for details.

## Acknowledgements

## Funding
Include the source of project funding here.
