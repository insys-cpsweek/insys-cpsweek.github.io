---
title: "Research"
permalink: /research/
author_profile: true
---

<p>The key components of an ERM pipeline are:</p>
<ul>
<li>Incident Forecasting: creating models to understand where and when incidents occur, and with what severity.</li>
<li>Long-term resource allocation: creating algorithmic approaches to station resources in the anticipation of future incidents.</li>
<li>Short-term dynamic allocation: updating responder allocation to adjust to the changing dynamics of urban areas.</li>
<li>Dispatch: creating principled approaches to dispatching responders</li>
</ul>
<p>Designing ERM pipelines is challenging. Despite the dynamic and uncertain environments in which ERM systems work, response is expected to be efficient and effective. Our research has spanned all the four components in the last few years. Below, we present a short summary of most commonly used models in ERM.</p>


1. Forecasting Methods -- Understanding <i>where</i> and <i>when</i> incidents like accidents occur is the most fundamental step in the emergency response pipeline. Both discrete time and continuous-time models have been used to learn distributions over incidents arrival. Poisson regression, negative binomial regression, zero-inflated poisson regression and parametric survival analysis are the most widely used models in this regard.

2. Allocation Methods -- Allocations models seek to optimize two targets: a) the spatial distribution of depots (fixed entities like fire stations), and b) the distribution of responders with the depots. The key idea is to frame an optimization problem that optimizes a specific metric like expected response time or coverage. 

3. Dispatch Methods -- Principled methods of dispatch involve optimizing over which responder should be dispatched once an incident has occurred, and also how the distribution of responders can be changed dynamically. Typically, a decision-theoretic model is created with an appropriate reward structure, and the expected sum of rewards is maximized to design the optimal model for dispatch.

4. Congestion Analysis Methods - Traffic congestion is a critical concern for emergency responders. As such good congestion prediction models and analyzing how congestion affects motor vehicle incidents and the response is important. Typically, recurrent neural networks and graph neural networks have performed well for this task. 

<!-- The problem is challenging because the correct answer may not only depend upon just sending the nearest emergency responder, but sometimes it may also require proactively placing emergency vehicles in regions with higher incident likelihood. Sending the nearest available responder by euclidean distance ignores road networks and their congestion, as well as where the resources are stationed. Greedily assigning resources to incidents can lead to resources being pulled away from their stations, increasing response times if an incident occurs in the future in the area where responder should be positioned. The goal of this project is to enable an ERM pipeline that solves these problem strategically.  -->

