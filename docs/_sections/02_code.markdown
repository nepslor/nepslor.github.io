---
layout: post
title:  "Code"
date:   2020-10-10 14:54:14 +0200
categories: jekyll update
---

### 2020 [Multivariate Boosted TRee](https://github.com/supsi-dacd-isaac/mbtr)                
MBTR is a python package for multivariate boosted tree regressors trained in parameter space. The code is described in the accompaning paper {% cite nespoli2020multivariate%}. The package can handle arbitrary multivariate losses, as long as their gradient and Hessian are known. Gradient boosted trees are competition-winning, general-purpose, non-parametric regressors, which exploit sequential model fitting and gradient descent to minimize a specific loss function. The most popular implementations are tailored to univariate regression and classification tasks, precluding the possibility of capturing multivariate target cross-correlations and applying conditional penalties to the predictions. This package allows to arbitrarily regularize the predictions, so that properties like smoothness, consistency and functional relations can be enforced. The python code is available [here](https://github.com/supsi-dacd-isaac/mbtr).
<p align="center">
    <img src="/figs/code/mbtr.svg " alt="drawing" width="100"/>
</p>



### 2019 [Scenario reduction for stochastic control](https://gitlab.com/supsi-dacd-isaac/scenred)
Code for optimal scenario tree reduction for multivariate data.
The code reduces a set of scenarios (obtained from sampling a multivariate distribution, or from historical data) to a scenario tree, in which each node has an associate probability, such as at each point in time, the sum of the probabilities in all the branches of the tree is equal to 1. The algorithm implemented is based on the one described in {% cite Growe-Kuska2003 %}, which rely on a greedy strategy to optimally reduce the scenarios, based on the Kantorovich distance.
The code, available [here](https://gitlab.com/supsi-dacd-isaac/scenred), is implemented both in Matlab and in Python. The python verision also includes the retrieval of the graph representation of the scenrio tree. The graph is encoded in a networkx graph object. 

<img src="/figs/code/scenred_scenarios.png" alt="drawing" width="300"/>
<img src="/figs/code/scenred_tree.png" alt="drawing" width="400"/>

### 2017 [Global Horizontal Irradiance Estimator](https://gitlab.com/supsi-dacd-isaac/GHIEstimator)
This code estimates the global horizontal irradiance (GHI) from the power measurements of one or more photovoltaic (PV) systems located in the same neighborhood, as described in the accompaning paper {% cite nespoli2017unsupervised%}. The method is completely unsupervised and is based on a physical model of a PV plant. It can estimate the nominal power and orientation of multiple PV fields, using only the aggregated power signal from their PV power plant. Moreover, if more than one PV power plant is available, the different signals are reconciled using outliers detection and assessing shading patterns for each PV plant. The matlab code is available [here](https://gitlab.com/supsi-dacd-isaac/GHIEstimator).
<p align="center">
<img src="/figs/code/GHI.png" alt="drawing" width="300"/>
</p>


{% bibliography  --cited%}

