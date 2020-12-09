---
title: "A Decision Theoretic Framework for Emergency Responder Dispatch"
collection: publications
permalink: /publications/aamas18
venue: 17th Conference on Autonomous Agents and MultiAgent Systems (AAMAS 2018)
---

[[PDF]](https://ayanmukhopadhyay.github.io/files/aamas18.pdf)

## Abstract
Efficient emergency response is a major concern in urban areas across the globe. The problem of predicting incidents and subsequently allocating responders spatially has been studied extensively. The problem of dynamically deploying responders, however, has received considerably less attention and has been noted as a difficult problem in prior literature due to inherent complexities in the environment in which such problems evolve. We formulate a decision-theoretic framework for the emergency responder problem, which effectively leverages state-of-the-art methods for continuous-time spatio-temporal incident forecasting. We formulate the responder dispatch problem as a Semi-Markov Decision Process (SMDP) that evolves in continuous time, and efficiently engineer its representation leveraging structural insights of the problem space. We then propose a novel approach to solve the problem based on policy iteration. First, we transform the SMDP into a discrete-time MDP (DTMDP). Then, we simulate our system to estimate value of states as well as learn the state transition probabilities of the transformed DTMDP. We also design heuristic policies with which our algorithm can be seeded. We validate the efficacy of our approach on real traffic and assault data from Nashville, USA, as well as synthetic data, and highlight that our approach outperforms the state of the art emergency responder dispatch system.