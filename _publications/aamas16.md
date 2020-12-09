---
title: "Using abstractions to solve opportunistic crime security games at scale."
collection: publications
permalink: /publications/aamas16
venue: 16th Conference on Autonomous Agents and MultiAgent Systems (AAMAS 2017)
---

[[PDF]](https://ayanmukhopadhyay.github.io/files/gamesec16.pdf)

## Abstract
In this paper, we aim to deter urban crime by recommending optimal police patrol strategies against opportunistic criminals in large scale urban problems. While previous work has tried to learn criminals' behavior from real world data and generate patrol strategies against opportunistic crimes, it cannot scale up to large-scale urban problems. Our first contribution is a game abstraction framework that can handle opportunistic crimes in large-scale urban areas. In this game abstraction framework, we model the interaction between officers and opportunistic criminals as a game with discrete targets. By merging similar targets, we obtain an abstract game with fewer total targets. We use real world data to learn and plan against opportunistic criminals in this abstract game, and then propagate the results of this abstract game back to the original game. Our second contribution is the layer-generating algorithm used to merge targets as described in the framework above. This algorithm applies a mixed integer linear program (MILP) to merge similar and geographically neighboring targets in the large scale problem. As our third contribution, we propose a planning algorithm that recommends a mixed strategy against opportunistic criminals. Finally, our fourth contribution is a heuristic propagation model to handle the problem of limited data we occasionally encounter in largescale problems. As part of our collaboration with local police departments, we apply our model in two large scale urban problems: a university campus and a city. Our approach provides high prediction accuracy in the real datasets; furthermore, we project significant crime rate reduction using our planning strategy compared to current police strategy.
