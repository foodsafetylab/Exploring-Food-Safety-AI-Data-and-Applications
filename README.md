# Exploring-Food-Safety-AI-Data-and-Applications

## Overview
### Introduction
Aims are to develop deeper collaboration to build out AI infrastructure for

1. Food safety testing database to power AI applications in produce safety
2. Federated Learning for collaborative and privacy-preserving learning
3. Inventory strategies for improved supply change resilience against disastrous events

### Methods
#### Aim 1
#### Allocation Strategies for Limited Food Resources during Disastrous Events
To model food bank demand for improving supply chain resilience, we collected data from two key sources: the [Capital Area Food Bank (CAFB) Hunger Estimates dataset](https://catalog.data.gov/dataset/capital-area-food-bank-hunger-estimates) and the [Mid-Ohio Foodbank's "Community Response to Hunger" (CRH) dataset](https://data.world/smartcolumbusos/21d29da9-537c-4703-97b8-9d044f2c4231).

The CAFB Hunger Estimates dataset includes detailed information on hunger and food insecurity across Census Tracts in the DMV (DC, Maryland, and Virginia) area. Compiled by the CAFB through internal tracking and shared with the DC government, the dataset contains a rich set of records of 2014 and 2015 that provides important insights about trajectories of food insecurity. For each census tract, the database includes estimates of the size of the population without secured food supply, both in numbers and as a fraction of the entire population. It also keeps records of the amounts of food needed and the amounts distributed, based on which the extent of food shortage can be estimated. 

To model food supply, we have used the CRH dataset from the Mid-Ohio Foodbank. This dataset, titled "Services received from Food Pantries 2016-2017," is part of a multi-year analysis to better understand the true level of need for food within the community. Covering the period from July 1, 2016, through June 30, 2017, the dataset includes approximately 490,000 service records. These records detail the date of service, place of service, and type of service for every visit made by approximately 86,000 families. As is stated by its developers, “The goal of this dataset and analysis is to foster constructive conversations and meaningful action with the support of the entire community around the issue of hunger.” 

Exploring these datasets, we are in the process of developing effective allocation strategies when the supply of food is limited, especially during occurrences disastrous events.

We use linear programming and incorporate a uniform delay to optimize the allocation of food resources. This approach ensures that resources are distributed efficiently and equitably, even during challenging circumstances.

### Results
#### Aim 1
##### Produce Sampling Data De-siloing and Standardization
Some produce sample testing is conducted that does not fall under private data ownership, such as FDA sampling assignments or data collected under academic research for publication. Typically, the resulting data is isolated within databases that are not immediately easily accessed for public use. Furthermore, each of these databases will not overlap with others, may use different standards, and may contain different supplementary data in addition to the sampling result (i.e., "data silos"). 

Through discussions with Western Growers and Crème, we have started to establish a potential standard baseline for produce sampling data. Western Growers have also offered to help mediate contact between UIUC and government organizations (e.g., the Food and Drug Administration) for access to larger datasets. This unified produce sample database would operate using the aforementioned standard baseline, with the aim of pulling data from multiple "siloed" databases into a single location (Figure 1). The specific hosting platform of this database has not been finalized yet; however, potential options include hosting at UIUC, hosting by the Center for Produce Safety (CPS), or the extension of Crème's Greenlink private produce sample database to also feature public-facing database.

Figure 1. Schematic of database development framework
![Figure 1](https://github.com/foodsafetylab/Exploring-Food-Safety-AI-Data-and-Applications/blob/main/README%20Figures/Figure%201.jpg)

##### Database Seeding
A potential source of initial produce sample testing data to seed the database with has been identified under the CPS' project list. As of May 1st 2023, the CPS listed a total of 207 projects (CPS, 2023), 40 (19%) of which are estimated to be likely sources of pre-harvest data. These would have to be individually requested from each project author and added to the database, but may set a precedence for future CPS projects requiring the publication of datasets through this database as a requirement of their funding.

##### Geographically-Informed Risk Factors
Multiple geographical and weather-related risk factors have been identified in relation to various foodborne pathogens (Bergholz & Wiedmann, 2016), as well as specifically to _Listeria_ spp. (Liao et al., 2021), Non-LM _Listeria_ spp. (Weller, Belias, et al., 2020), _Listeria monocytogenes_ (Strawn et al., 2013, Weller, Brassill, et al., 2020), _Salmonella_, and _Escherichia coli_ (Strawn et al., 2013, Weller, Brassill, et al., 2020, Weller, Brassill, et al., 2020). While a limited amount of this information can be accurately determined retroactively for existing data, an additional component under consideration is the creation of a "black box" data processing step that uses the exact position of a user to determine local weather and geographically-related risk factors. Calculated outputs based on local risk may then be added to the new data while exact location is discarded, preserving privacy and anonymity of the data while enriching it with supplementary information for risk-based analysis.

#### Aim 2
##### FL framework and codebase:
We have developed a codebase and testbed for FL using the federated averaging (FedAvg) algorithm for smart manufacturing applications (Mehta & Shao, 2022), which can be leveraged for case studies in the agri-food sector. The steps involved in the FedAvg algorithm are as follows.
-	The central server initializes the global neural network and sends its parameters to all factories participating in the data federation.
-	Each factory downloads the parameters as its initialization and trains the local neural network on its private dataset for a small number of local epochs. 
-	Each factory uploads the updated parameters of its local model back to the central server.
-	The server computes a weighted average of the parameters received from all factories to update the global model. The parameters from each factory are given weights proportional to the size of its local dataset.

Figure 2. The schematic of the FL framework. The codebase and algorithmic framework can be easily integrated for specific applications with distributed data across several entities, for instance, for the de-siloed produce database proposed in Aim 1.
![Figure 2](https://github.com/foodsafetylab/Exploring-Food-Safety-AI-Data-and-Applications/blob/main/README%20Figures/Figure%202.jpg)

##### Dealing with data heterogeneity:
Big data collected by entities in the agri-food sector is inherently multi-source and heterogeneous. Another bottleneck particular to food safety data is the issue of imbalance where most samples fall in the negative class and very limited positive samples are available. Recent studies have shown that the quality of the global FL model deteriorates in the presence of non-IID (independent and identically distributed) and class-imbalanced data. To remedy this, we developed a novel client clustering algorithm called Federated Learning via Agglomerative Client Clustering (FLACC) (Mehta & Shao, 2023). FLACC greedily agglomerates clients or groups of clients based on their gradient updates while learning the global FL model. Once the clustering is complete, each cluster is separated into its own federation, allowing clients with similar underlying distributions to train together. We show that FLACC can enable clients with significantly different data distributions to train personalized FL models under the FedAvg framework without deteriorating performance. This framework can be further tested on data collected from Aim 1 to improve performance over vanilla FL.

##### Next steps:
The FL framework developed for smart manufacturing applications can be fine-tuned for food safety data collected under Aim 1. Our groups are currently brainstorming concrete requirements to create a collaborative, privacy-preserving deep learning framework for food safety data. Some important considerations are highlighted below.
-	Incentive mechanisms: In conventional FL, all firms participating in the data federation learn a single global model irrespective of the quantity and quality of their individual data. This may lead to the free-rider problem, where factories with less valuable data unfairly benefit from others in the federation. To remedy this, future research will consider sustainable incentive mechanisms to encourage participation in FL.
-	Privacy guarantees: FedAvg provides a rudimentary notion of privacy due to data minimization. When many firms participate in FL, formal privacy guarantees are often required (Qian et al., 2022). Firms in FL are susceptible to adversarial attacks (data poisoning, model evasion, model update poisoning from a participating client). Cross-silo systems also need protection against data inference attacks, where a malicious firm or the central server tries to infer information about data from other firms. Future work can focus on methods to protect client data by enhancing privacy like differential privacy, homomorphic encryption, secure multiparty computation, and blockchain technology.
-	System design: In real federations, a more concrete fill-stack pipeline from data to model that addresses communication cost, central server design, built-in privacy mechanisms, and regulatory implications is required. A system design allows seamless addition of new data sources, learning models on the fly, and integrations across the food supply chain.

#### Aim 3
Ze-Xuan Liu and Qiong Wang developed two test problems: one is investigating the optimal food bank dispatching policy, the other is investigating the demand shift when disruption occurs at the supply side.

##### Food bank dispatching policy:
Considering catastrophic events such as hurricanes and pandemics, food banks emerge as indispensable entities in mitigating food insecurity. Notwithstanding, constrained by limited inventory and catering to a clientele characterized by unpredictability and diverse nutritional requisites, these institutions confront formidable challenges in distributing food efficiently within a week to ensure its freshness. The profound ethical ramifications of potentially denying sustenance due to suboptimal allocation accentuate the imperative for a refined dispatching strategy. Such a strategy ought to be attuned to real-time demands and encompass a spectrum of nutritional prerequisites, thereby augmenting both operational efficacy and equitable distribution of food.

We have conceptualized the problem with an objective to optimize the total number of individuals satiated, given a predetermined inventory of food. Considering the disparate demands of distinct customer categories, the decision-maker is tasked with ascertaining whether to allocate food to the incoming populace and, consequentially, determining the appropriate provisions based on extant inventory and the residual decision-making horizon. Our policy has consistently exhibited an upper bound of regret when juxtaposed with the hindsight optimal. This benchmark delineates the optimal outcome that would be attainable if we possessed a priori knowledge of the entire customer arrival sequence. Such findings underscore the robustness of our policy, suggesting its alignment with near-optimal outcomes, even devoid of anticipatory knowledge regarding customer arrivals.

For future work, we are developing an inter-institutional collaboration with Prof. Xin Liu from UC Davis who is helping link us to other food bank projects in AIFS where there may be data we can use to test our algorithm. 

##### Demand Shift after Disruption:
Structural demand shifts were commonly observed in food supply chains during the pandemics. As schools, restaurants, and hotels are closed and foods are mostly prepared and stockpiled at homes, demands for products processed and packaged for foodservice industry vanished and demands for products sold in grocery stores skyrocketed. As a result, food waste and shortage happened simultaneously: farmers dispose milks and abandon crops that cannot find their ways to service facilities and cafeteria tables at the same time when grocers were struggling to find supplies to stock their shelves (Ellison & Kalaitzandonakes, 2020; Mulvey et al., 2020). A case in point is the onion market, where there was a pronounced shift in demand from eateries to household cooking (Miguel-Ángel et al., 2022). Refer to Figures 3A,3B, where the orange and yellow arrows depict existing supply-demand relationships. In scenarios with a direct one-to-one match, any disruption leads to lost demand. However, in a networked structure, this demand simply reroutes to another segment of the supply chain. It has also been shown, by experience in New Jersey (MacFall et al., 2015), that instead of relying on a few large, centralized processors, dairy supply chains that operate with many vertical-integrated and horizontal-cooperative small farmers were far more resilient to COVID-induced demand changes. The implied message is that supply chain structure does make difference in robustness against disruption. We will model such systems and analyze their advantage of adapting to random, disruptive events.

Figure 3. Figure 3A. One to One supply chain
![Figure 3A](https://github.com/foodsafetylab/Exploring-Food-Safety-AI-Data-and-Applications/blob/main/README%20Figures/Figure%203A.jpg)

Figure 3B. Network shape supply chain
![Figure 3B](https://github.com/foodsafetylab/Exploring-Food-Safety-AI-Data-and-Applications/blob/main/README%20Figures/Figure%203B.jpg)

There is a large body of supply chain literature on the flexibility design (Wang et al., 2021). The goal is to inject an adequate level of adaptivity into the supply side to facilitate timely responses to demand changes. An important subject is robust flexibility design, which focuses on the performance in the worst-case scenario (Wang et al., 2022). Our modeling and analytical efforts will be carried out under this framework.

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

## Citations
Mehta, M., & Shao, C. H. (2022). Federated learning-based semantic segmentation for pixel-wise defect detection in additive manufacturing. _Journal of Manufacturing Systems, 64_, 197-210. https://doi.org/10.1016/j.jmsy.2022.06.010 

Mehta, M., & Shao, C. (2023). A Greedy Agglomerative Framework for Clustered Federated Learning. _IEEE Transactions on Industrial Informatics, 19_(12), 11856-11867. https://doi.org/10.1109/tii.2023.3252599

## License
This project's code is licensed under the GNU General Public License v3.0 and dataset is licensed the Creative Commons Attribution Share Alike 4.0 International license. Please see the [LICENSE.code](/LICENSE.code) and [LICENSE.dataset](/LICENSE.dataset) files for details.

## Acknowledgements

## Funding
Include the source of project funding here.
