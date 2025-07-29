---
title: "Research"
draft: false
---
### 1. Using Bayesian Inference and Flowpipe Construction to Bound Predictions of Biogas Production at Wastewater Treatment Plants  
- *Advisor: [Sriram Sankaranarayanan](https://home.cs.colorado.edu/~srirams/)* | *Feb 2025 - Jul 2025*  

- #### Overview  
    - Developed a **formal verification framework** to predict guaranteed bounds on biogas production in wastewater treatment plants (WWTPs) under uncertainty. Combines:  
        - **Bayesian inference** (probabilistic programming) to estimate uncertain parameters from noisy data  
        - **Reachability analysis** (formal methods) to propagate uncertainties through differential equations  

- **Key Achievements:**  
    - ✔ **100% ground-truth containment** in predicted bounds at 99% confidence  
    - ✔ **40× faster** than standard sampling approaches (3s vs 114s for 5-day predictions)  
    - ✔ Implemented in Julia using Turing.jl for inference and custom reachability solver  

```python
# Pseudocode of core approach
def predict_bounds(data, γ):
    # 1. Bayesian parameter estimation
    posterior = MCMC(model, data, samples=25000)  
    θ_lo, θ_hi = credible_intervals(posterior, γ)
    
    # 2. Flowpipe construction
    bounds = reachability(ODE_model, θ_lo, θ_hi) 
    return bounds
