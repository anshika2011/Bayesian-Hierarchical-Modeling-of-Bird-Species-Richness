# Bayesian-Hierarchical-Modeling-of-Bird-Species-Richness

Species richness, defined as the count of distinct bird species observed, is an important ecological indicator. Modeling species richness presents challenges due to its non-linear relationship with observational effort, regional variability, and seasonal effects. To address these complexities, this project employs a Bayesian hierarchical NegativeBinomial model to predict species richness across the United States. The primary goal is to estimate the relationship between species richness and multiple factors, including region, day of the year, and observational effort, while accounting for spatial and temporal variability. The model incorporates random effects for U.S. states and employs a Fourier basis to capture seasonal patterns. Gibbs sampling using JAGS is utilized to estimate the posterior distribution of model parameters. This analysis aims to investigate potential relationships between these factors and bird species richness while ensuring model convergence through diagnostic checks.

1. Introduction
Biodiversity assessment is crucial for understanding ecological health, and species richness serves as a key indicator in this context. Species richness, defined as the number of distinct species observed in a given area, helps ecologists monitor environmental changes and conservation efforts. However, accurately estimating species richness poses challenges due to the inherent variability in bird observations, influenced by geographical, temporal, and observational factors.
A common approach to modeling species richness involves treating it as a count variable and using a Poisson regression model. However, the simplistic assumption of a linear relationship between species counts and observational effort can lead to inaccuracies, as the relationship is often more complex. In particular, variations in observer effort, regional differences, and temporal patterns significantly impact the observed species richness.

To address these challenges, a hierarchical Bayesian approach is proposed, allowing for the inclusion of random effects to account for regional variability and temporal patterns. The model specifically incorporates random intercepts for U.S. states to capture spatial heterogeneity and employs a Fourier basis to model seasonal variations. Additionally, effort variables such as observation duration and the number of observers are carefully standardized to maintain consistency. Instead of a Poisson model, a Negative Binomial model is used to account for overdispersion.
In this project, we utilize Gibbs sampling through JAGS to estimate the posterior distri- bution of model parameters. By modeling the underlying relationship between species richness and these factors, we aim to gain a deeper understanding of the ecological dynamics influencing bird biodiversity across the United States.


2. Data Description
This project leverages data from the eBird database, which records bird observations across the United States. eBird is one of the world’s largest biodiversity-related science projects, managed by the Cornell Lab of Ornithology. It aggregates bird observation data contributed by birdwatchers globally, with more than 100 million bird sightings annually. The dataset contains detailed records of bird species observations, including species identification, location information, date, and observational effort.

2.1. Data Acquisition
The data was collected using the eBird API, which provides recent bird observation records for specific states in the U.S. The Python script used for data collection accessed data from the states of Illinois, Indiana, Missouri, Kentucky, and Iowa for the past 30 days. Each record includes the species observed, location (latitude and longitude), date, and effort metrics.

2.2. Data Characteristics
The raw dataset initially consisted of multiple columns, including: • Species Code, Common Name, Scientific Name
• Location ID, Location Name, Observation Date
• Count of Individuals Observed, Latitude, Longitude
• Validation Status, Review Status, Privacy Settings
• Submission ID, Region, Exotic Category
To focus on analyzing species richness effectively, the dataset was preprocessed to retain only the most relevant variables. The primary outcome variable, species richness, is quantified as the number of distinct species observed per site visit.

2.3. Predictors
The following predictors were incorporated into the analysis:
Region: Encodes the U.S. state where the observation was recorded, allowing for spatial variation.
Day: Represents the day of the year, derived from the observation date to capture seasonal trends.
Effort Variables:
– Duration: Standardized observation duration to account for variations in effort. 
– Effort: Standardized latitude as a proxy for regional effort variation.
– Observers: Standardized longitude, reflecting the number of observers involved.
