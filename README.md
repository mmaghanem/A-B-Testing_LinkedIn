# LinkedIn Profile Picture Impact on Connection Acceptance Rate

Welcome to the repository for our research project on the impact of LinkedIn profile pictures on connection acceptance rates. This project investigates whether having a profile picture on LinkedIn increases the likelihood of connection requests being accepted. 

## Table of Contents

1. [Introduction](#introduction)
2. [Research Design](#research-design)
3. [Methods and Techniques](#methods-and-techniques)
4. [Skills and Technologies Applied](#skills-and-technologies-applied)
5. [Benefits of the Project](#benefits-of-the-project)



## Introduction

In the age of digital networking, LinkedIn serves as a critical platform for professional connections. Our study explores how visual elements, specifically profile pictures, influence the acceptance rate of connection requests. This README provides a detailed explanation of the research design and the R programming skills used to develop and analyze this project.

## Research Design

Our research aimed to answer the following question: **Does having a LinkedIn profile picture increase the acceptance rate of connection invitations?**

### Experimental Design

- **Treatment and Control Groups**: We created 10 LinkedIn profiles, divided into two groups: 5 with profile pictures (treatment) and 5 without (control). Each profile had identical professional details, differing only in the presence of a profile picture and the first name to avoid identification as fake accounts.

- **Randomization**: LinkedIn users were randomly assigned to receive connection requests from either the treatment or control profiles. This randomization helps eliminate selection bias and ensures a fair comparison between the groups.

- **Measurement**: The primary outcome was whether the recipient accepted the connection request. We measured this outcome using a binary indicator where 1 represents an accepted request and 0 represents a non-accepted request.

### Data Collection

- **Sampling**: We targeted members of the "Analytics and Data Science Career" LinkedIn group, scraping the most recent 2,828 members due to LinkedIn's restrictions on accessing full group membership lists.
- **Covariates**: Additional data such as recipient's activity status and the duration since the invitation was sent were collected to enhance the analysis.

### Power Analysis

We conducted a power analysis to determine the necessary sample size for detecting significant effects. Our analysis indicated that approximately 2,400 subjects were needed to achieve 80% power at a 5% significance level. 

## Methods and Techniques

### Data Cleaning and Preprocessing

We used R to clean and preprocess the data. This step involved removing duplicates, handling missing values, and preparing the data for analysis.

```r
# Load required libraries
library(dplyr)
library(lubridate)

# Read the data
data <- read.csv("final_project_data.csv")

# Data cleaning
data <- data %>%
  filter(!is.na(invite_sent)) %>%
  mutate(invite_accepted = ifelse(is.na(invite_accepted), 0, 1),
         invite_duration = as.numeric(difftime(Sys.Date(), as.Date(invite_sent), units = "days")))
```

### Statistical Analysis
We performed regression analysis to understand the relationship between having a profile picture and the acceptance rate of connection requests.
```r
# Logistic regression model
model <- glm(invite_accepted ~ has_picture + is_male + invite_duration, data = data, family = binomial)

# Summary of the model
summary(model)

```

### Data Visualization
We visualized the results to make them easier to understand and interpret.
```r
library(ggplot2)

# Plot acceptance rates
ggplot(data, aes(x = has_picture, fill = invite_accepted)) +
  geom_bar(position = "fill") +
  labs(title = "Connection Acceptance Rate by Profile Picture",
       x = "Profile Picture",
       y = "Acceptance Rate") +
  theme_minimal()
```

### Interaction Effects
We examined the interaction effects between having a profile picture and other factors such as gender.
```r
# Interaction model
interaction_model <- glm(invite_accepted ~ has_picture * is_male, data = data, family = binomial)

# Summary of the interaction model
summary(interaction_model)
```

## Skills and Technologies Applied
### R Programming
   - **Data Cleaning:** Used dplyr for efficient data manipulation and lubridate for handling date-time data.
   - **Statistical Analysis:** Applied regression models using glm to analyze binary outcomes and interaction effects.
   - **Data Visualization:** Created informative plots with ggplot2 to visualize acceptance rates and interaction effects.

### Research and Study Design
   - **Experimental Design:** Designed a robust experiment with treatment and control groups to test our hypothesis.
   - **Randomization:** Implemented random assignment to reduce bias and ensure valid results.
   - **Covariate Analysis:** Included relevant covariates to control for potential confounders and improve precision.

## Benefits of the Project
1. **Improved Understanding of Networking Dynamics:**
   - Provides insights into how visual elements, such as profile pictures, influence professional networking success on LinkedIn.
2. **Application of Advanced R Skills:**
   - Demonstrates the practical application of R in handling real-world data, performing statistical analysis, and visualizing results.
3. **Robust Research Methodology:**
   - Highlights the use of well-structured experimental designs and statistical techniques to answer important data science questions.
