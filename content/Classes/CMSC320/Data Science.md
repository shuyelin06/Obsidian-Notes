---
title: Data Science
tags:
- cmsc320
- wip
---

# Data Science
**Data Science** refers to the application of computational and statistical techniques to address or gain insight into some problem in the real world. Here, we discuss some fundamental concepts to Data Science. 

## Big Data
Data Science has risen significantly in importance over the last 20 years, due to the emergence of **big data**, data that is high in volume, variety, and velocity. Each of these properties is defined below.
- **Volume**: Describes the quantity of data generated or collected.
- **Velocity**: Describes the speed in which data is generated and processed.
- **Variety**: Describes the wide number of differnt forms data can take on and be represented.

As more companies and organizations use big data, demand for Data Science only continues to increase.

## The Data Lifecycle
In Data Science, data will go through (approximately) the following 5 stages, which are known as the **data lifecycle**. Each of these stages will be described more in depth below.

```mermaid
graph LR
      1[Collection];
      2[Processing];
      3[Exploratory Analysis];
      4[Analysis & Model Building];
      5[Insight & Decisions];

      1 -.-> 2 -.-> 3 -.-> 4 -.-> 5;   
```
> While one stage roughly moves to the next, **Data Science is not a linear science**; it's always possible to move from one stage to another, and even move backwards!

We describe each of the stages more in depth below.

### Data Collection
Suppose we have some problem. To determine what to do next, we first need to **collect data**, which refers to any systematic approach to gathering relevant information from a variety of sources.

Sources of data can be widely distributed, and don't even have to be collected by the data scientist. There are 2 forms of data collection: **primary** and **secondary** data collection.
- **Primary data collection** refers to employing methods to collect the data yourself, whether through surveys, interviews, or monitors.
- **Secondary data collection** refers to the collection of data readily available, or already collected by someone else, whether through the internet, news, or the census.

The field of [[Experimental Design]] is often used to collect effective data.

### Data Processing
After collecting our data, we then need to **process the data**, which refers to the cleaning (scrubbing) of data to ensure the quality of data. This is necessary as misleading information is often unavoidable, and need to be accounted for to avoid inaccurate results.

This can be done, for example, by replacing invalid data with neutral values that don't influence the results, or by correcting the data values.

### Exploratory Analysis
While collecting and processing our data, we will want to perform **exploratory analysis** on it to extract insights for patterns, which may be useful for later model building or decision making. Such analysis is not deep, and aims to find correlations to give the scientist a better idea of what to do next.

Exploratory analysis often goes hand-in-hand with **data visualization**, as such visualizations of data often can yield interesting results.

### Analysis & Model Building
We can then **analyze our data**, which refers to the building of a model which uses the data, and makes predictions about hypothetical scenarios. With a good dataset, such models can serve as effective predictors which can guide decision making.

### Insights & Decisions
Finally, equipped with a model we will **interpret** our data, using the models to derive useful insights and make policy decisions. A model is often useful when working with non-technical people, as it provides a more streamlined way to convey meaningful inforomation to them.
