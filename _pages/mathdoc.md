---
title: "Statistical Methods"
permalink: /mathdoc/
author_profile: true
mathjax: true
---

This page is an explanation of the mathematical models that are used in the tool. 


<b>Data</b>

We assume the availability of a set of samples (possibly noisy) of historical incidents, which we refer to as $D$, and can be represented as a vector of tuples $\\{(s_1,t_1,k_1,w_1),(s_2,t_2,k_2,w_2),\dots,(s_n,t_n,k_n,w_n)\\}$, where $s_i$, $t_i$ and $k_i$ denote the location, time of occurrence, and reported severity of the $i$th incident, respectively, and $w \in \mathbb{R}^m$ represents a vector of features associated with the incident. These features can be spatial, temporal, or spatio-temporal. The features capture covariates that potentially affect incident occurrence. For example, $w$ typically includes features such as weather, population density, and time of the day. The most general form of incident prediction can then be stated as learning a function $f(X \mid w,\theta)$, where the random variable $X$ represents a measure of incident occurrence, and $\theta \in \mathbb{R}^m$ denotes the model parameters. For example, $X$ can measure the <em>count</em> of incidents (the number of incidents in $S$ during a specific time period), or <em>time</em> between successive incidents. The decision-maker seeks to find the <em>optimal</em> parameters $\theta^*$ that best describe $D$. This can be formulated as a maximum likelihood estimation (MLE) problem or an equivalent empirical risk minimization (ERM) problem.


<b>Forecasting</b>

The following forecasting models are currently supported by StatResp --

<ul>
<li><b>Poisson Regression</b>: In Poisson regression, the random variable of interest is the count of incidents in a region in a given time frame. The count follows a Poisson distribution, such that 
        
    $$
        f(X= x) = \frac{\lambda^x e^{-\lambda}}{x!}
    $$
    where $\lambda$ is the mean of the distribution. The regression model assumes that the expected value of the mean, conditional on the set of features $w$ can be modeled as 
    
    $$
        \mathbb{E}(\lambda|w) = e^{\sum_{i=1}^{m} \theta_i w_i}
    $$
    
    where $\theta \in \mathbb{R}^m$ is the set of regression coefficients.
</li>

<li><b>Zero-inflated Poisson Regression</b>: Many spatio-temporal processes like crashes and accidents are known to contain an excess of zeros, which can be challenging to deal with standard regression models. The zero-inflated Poisson models addresses this by considering two separate processes, one for observations with zero counts and one otherwise. The probability mass function (pmf) of the model takes the following form -- 
    
    $$
    f(x)= 
        \begin{cases}
            \phi + (1 - \phi)e^{-\lambda}& \text{if } x = 0\\ \\
            (1 - \phi)\frac{\lambda^x e^{-\lambda}}{x!},              & \text{otherwise}
        \end{cases}
    $$
    where $\lambda$ is the mean of the distribution, and $\phi$ represents the a measure of the proportion of zero counts in the data. A simple way of estimating $\phi$ is to calculate the empirical frequency of zeros in the data, such that 
    
    $$
        \phi = \frac{\sum_{i=1}^{n} \mathbb{I}(x_i = 0)}{n}
    $$
    
    It is also common to learn a model for $\phi$, conditional on the set of spatial-temporal features. StatResp estimates this by transforming $X$ into a binary random variable such that all non-zero counts in the data are marked as $1$. Then, a logistic regression model is learned to over $\phi$.
</li>


<li><b>Negative Binomial Regression</b> -- A well-known issue with using Poisson Regression on crash data is that its inability to handle dispersion. The Poisson distribution's mean equals its variance (both being equal to $\lambda$). Crash data is typically over-dispersed, meaning that the variance exceeds the mean of the distribution. The negative-binomial models (also known as the Poisson Gamma model) has been known to be a better predictor of such data. 
    
    The negative-binomial model has the following expression for the variance $\sigma$ in terms of the mean $\lambda$ as
    
    \[
        \sigma = \lambda + \alpha \lambda^{p}
    \]
    where $\alpha$ is an exogenous parameter and $p$ represents the order of the model. The setting with $p=1$ forms the <em>NB-1</em> model and the one with $p=2$ forms the <em>NB-2</em> model. Note that the setting where $p=0$ reduces to the standard Poisson model. StatResp uses the NB-2 model.
    
    The value of alpha is determined through auxiliary OLS regression~\cite{cameron2013regression}, using $\lambda$ from a standard Poisson model.
</li>

<li><b>Parametric Survival Model</b> A parametric survival model over incident arrival can be represented as  $f(X \mid \gamma(w))$, where
$f$ is the probability distribution for a continuous random variable $X$ (typically representing the inter-arrival time between incidents), which depends on
covariates $w$ via the link function $\gamma$. The link function is usually logarithmic. Formally, for a specific time-interval $x$, and associated feature vector $w$, this relationship is represented as

$$ log(x) = \sum_{i=1}^{m} \theta_i w_i + \epsilon $$

where, $\theta \in \mathbb{R}^{m}$ represents the regression coefficients and $\epsilon$ is the error term, distributed according to the distribution $h$. The specific distribution of $f$ is decided by how the error $y$ is modeled. RespStats models $X$ by an exponential distribution, which results from choosing the distribution of $\epsilon$ to be an extreme value distribution. Thus, in our incident prediction model, we assume that $h$ takes the following form
$$
    h(\epsilon = k) =e^{k - e^{k}} 
$$
</li></ul>


<b>Outlier Detection</b>

StatResp also supports the detection of outliers among clusters. Spatial clustering is done in StatResp on the basis of a set of <em>static</em> features specified by the user. Static features can be thought of as covariates that stay relatively constant over time. For example, the number of lanes on a roadway segment does not usually change. See the section on clustering to know how static features are used to cluster different spatial units together. However, despite exhibiting similar static features, units can have different arrival distributions for incidents. StatResp has a module for outlier detection, that aims to detect outliers within clusters. 

There are different methods to detect outliers given the distribution $f$ and data $D$. The simplest approach is to create an empirical distribution using $X$ (observed counts, for example), and then select units that are some predefined distance away from the mean. However, this ignores the feature space entirely. As a result, the following procedure is adopted to detect outliers. 

<ul>
    <li> A distribution $f$ and a clustering algorithm $A$ is specified by the user.</li>
    <li> The feature set is divided into static and dynamic features, represented by $w_s$ and $w_d$ respectively. The categorization is given by the user.</li>
    <li> Spatial units are clustered into $q$ clusters (say) by $A$. Let the $j$th cluster be denoted by $C_j$.</li>
    <li> For a given cluster $C_i$, we look at each each unit $u_k \in C_i$, and calculate the mean density (or probabilistic mass) resulting from each observation from the said unit. This can be calculated as
    $$
    m(u_{ik}) = \frac{\sum_{j=i}^{n}\unicode{x1D7D9}(x_j \in u_k)f(x_j|w)}{\sum_{j=i}^{n}\unicode{x1D7D9}(x_j \in u_k)(x_j)} 
    $$
    </li>
    <li> We then run the generalized extreme studentized deviate (ESD) test, which can be used to detect one or more outliers in a univariate data set that follows an approximately normal distribution. Note that for each cluster $C_i$, the elements of the vector $\{m(u_{i1}), m(u_{i2}) \dots\}$ follow a normal distribution in the limit since each observation is essentially the mean of a set of samples drawn from $f$.</li>
</ul>
