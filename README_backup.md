Emergency response management (ERM) is a critical problem faced by communities across the globe. First-responders are constrained by limited resources, and must attend to different types of incidents like traffic accidents, fires, crime, and distress calls. In prior art, as well as practice, incident forecasting and response are typically siloed by category and department, reducing effectiveness of prediction and precluding efficient coordination of resources. Further, most of these approaches are offline and fail to capture the dynamically changing environments under which critical emergency response occurs. As a consequence, statistical and algorithmic approaches to emergency response have received significant attention in the last few decades. Governments in urban areas are increasingly adopting methods that enable Smart Statistical Emergency Response, which are a combination of forecasting models and visualization tools to understand where and when incidents occur, and optimization approaches to allocate and dispatch responders. 

The problem is challenging because the correct answer may not only depend upon just sending the nearest emergency responder, but sometimes it may also require proactively placing emergency vehicles in regions with higher incident likelihood. Sending the nearest available responder by euclidean distance ignores road networks and their congestion, as well as where the resources are stationed. Greedily assigning resources to incidents can lead to resources being pulled away from their stations, increasing response times if an incident occurs in the future in the area where responder should be positioned. The goal of this project is to enable an ERM pipeline that solves these problem strategically. 

The key components of our approach to the ERM pipeline are: (1) *Incident forecasting* -- understanding where and when incidents occur , (2) *Long-term
 resource allocation* -- strategic decisions on long-term resource
 place- ment, such as how many stations and vehicles to acquire and
 where to build said stations , (3) *Dynamic resource allocation* --
 short term operational decisions such as rebalancing vehicle
 allocations based on current demands , and (4) *Dispatching* -- policy
 for deploying responders when an incident is reported.
 
 With our collaborators at Tennessee Department of Transportation (focusing on incident response on state highways) and Nashville fire department (focusing on incident response in urban communities) this project is developing an online incident forecasting and algorithmic approaches to  decentralized multi-agent response that focuses on resource allocation and dispatching policies.
 
To understand our methodology please refer to the following [overview paper](overview.pdf). Technical details of individual components of the pipeline can be obtained from the following technical papers.

## Incident Prediction Models.
 - *Batch Prediction Models* : A. Mukhopadhyay, Y. Vorobeychik, A. Dubey, and G. Biswas, [Prioritized Allocation of Emergency Responders based on a Continuous-Time Incident Prediction Model](https://scope-lab.org/files/Mukhopadhyay2017.pdf), in Proceedings of the 16th Conference on Autonomous Agents and MultiAgent Systems, AAMAS 2017, São Paulo, Brazil, May 8-12, 2017, 2017, pp. 168–177.
 - *Updating the forecasting Models Online*: A. Mukhopadhyay, G. Pettet, C. Samal, A. Dubey, and Y. Vorobeychik, [An online decision-theoretic pipeline for responder dispatch](https://scope-lab.org/files/Mukhopadhyay2019.pdf), in Proceedings of the 10th ACM/IEEE International Conference on Cyber-Physical Systems, ICCPS 2019, Montreal, QC, Canada, 2019, pp. 185–196.
 - Bayesian and Clustering Based Methods: G. Pettet, S. Nannapaneni, B. Stadnick, A. Dubey, and G. Biswas, [Incident analysis and prediction using clustering and Bayesian network](https://scope-lab.org/files/Pettet2017.pdf), in 2017 IEEE SmartWorld, 2017, pp. 1–8.
 
## Dispatch Response Methods
- *Theoretical Formulation*: Ayan Mukhopadhyay, Zilin Wang, and Yevgeniy Vorobeychik. 2018. [A Decision Theoretic Framework for Emergency Responder Dispatch](https://dl.acm.org/doi/10.5555/3237383.3237471). In Proceedings of the 17th International Conference on Autonomous Agents and MultiAgent Systems (AAMAS ’18). International Foundation for Autonomous Agents and Multiagent Systems, Richland, SC, 588–596.
- *Heuristic Based Online Decision Making*: A. Mukhopadhyay, G. Pettet, C. Samal, A. Dubey, and Y. Vorobeychik, [An online decision-theoretic pipeline for responder dispatch](https://scope-lab.org/files/Mukhopadhyay2019.pdf), in Proceedings of the 10th ACM/IEEE International Conference on Cyber-Physical Systems, ICCPS 2019, Montreal, QC, Canada, 2019, pp. 185–196.

## Stationing and Rebalaning Methods
- *Online Stationing and Rebalancing Using Decentralized Methods*: G. Pettet, A. Mukhopadhyay, M. Kochenderfer, Y. Vorobeychik, and A. Dubey, [On Algorithmic Decision Procedures in Emergency Response Systems in Smart and Connected Communities](https://scope-lab.org/files/Pettet2020.pdf), in Proceedings of the 19th Conference on Autonomous Agents and MultiAgent Systems, AAMAS 2020, Auckland, New Zealand, 2020.
 



 
 
