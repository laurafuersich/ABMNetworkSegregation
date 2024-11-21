## How Do Social Network Features Shape Segregation? A Simulation Study.
## Author: Laura Fürsich, Mansueto Institute for Urban Innovation & Urban Science Laboratory, University of Chicago


## Funding: 
This research was supported by the Swedish Research Council (Dnr 2016-01987). The computations were enabled by resources provided by the National Academic Infrastructure for Supercomputing in Sweden (NAISS) and the Swedish National Infrastructure for Computing (SNIC) at Linköping University partially funded by the Swedish Research Council through grant agreements no. 2022-06725 and no. 2018-05973.

## Abstract:
This paper provides an analytical exploration of how network characteristics influence residential segregation. Building upon the foundational Schelling model, I develop an Agent-based simulation wherein agents are embedded within a social network structure. This approach allows for the experimental manipulation of network features such as homophily, clustering, and degree, enabling the assessment of their individual and combined impacts on segregation levels, patterns, and the stability of the socio-spatial system. I find that certain configurations of these network features can exacerbate residential sorting to levels exceeding those predicted by the original Schelling model. These outcomes underscore the critical role of social network dynamics, particularly the significance of weak ties, in driving a system toward a segregated state. The results contribute to the broader sociological discourse on social networks, highlighting the complex interplay between network structure and social phenomena, and offering new insights into the mechanisms underlying residential segregation.

This project is coded in Python and Anaconda building largely on the AgentPy (Foramitti, 2021) and NetworkX (Hagberg et al., 2008) libraries.

Foramitti, J. (2021). AgentPy: A package for agent-based modeling in Python. , 6 (62), 3065.
Hagberg, A. A., Schult, D. A., & Swart, P. J. (2008). Exploring Network Structure, Dynamics, and Function using NetworkX. In G. Varoquaux, T. Vaught, & J. Millman (Eds.), Proceedings of the 7th Python in Science Conference (pp. 11 – 15). Pasadena, CA USA.



## Installation 
To set up the environment for running this ABM, follow these steps:


1. **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/your-repo-name.git
    cd your-repo-name
    ```

2. **Install the required dependencies using Anaconda:**
    ```bash
    pip install -r requirements.txt
    ```




## Usage

Run the scripts in the following sequence:

1. run     ```setup_networks ``` 
    This script creates network setups based on the parameters defined in the parameter section of the model:
            parameters = {
            'n_groups': 2, # Number of groups (green/grey)
            'size': 30, # Height and length of the grid
            'steps': 1,  # Maximum number of steps
            'size_cliques':10 , # # how large are cliques
            'steps_rewire': 1,  # Rewiring iterations
            'n':800, # population size
            'want_ties':0.3, # preference thereshold for residential mobility
            'n_ties_outgroup':0,  # defines homophily
            'n_edges_drop':0,
            'clustering_threshold': 1, # defines clustering 
            'distance':30 # distance range for calculating segregation as H index 
        }
    
    ** Output **
    For each network configuration, this script creates an attributes and edgelist file in /network_files. It also stores a 
    sociogram for each network in /network_plots.
    The script stores reporters separately for each clique size c as reporters_networkcreate{c}.csv and plots the number of steps required for each combination of homophily, clustering threshold, and clique size. 

2. run   ```simulation ``` 
    In this file we conduct a multi-run experiment. To do so, first prepare a parameter sample that mirrors the parameters of networks previously created (if 'create_networks':False). Set the sampling factor (e.g., 5) using ```sample = ap.Sample(parameters_multi, n=5)```. Then run n iterations of the experiment separately for each clique size using ```exp = ap.Experiment(SegregationModel, sample, iterations=n)```

    The results of each model get saved in ap_output\SegregationModel_{#}. 
    Each folder contains:
        > info.json
        > parameters_constant.json
        > parameter_sample.csv
        > reporters.csv

    Additional reporting saved in
        3_simulation/t_seg: This folder contains information on the level of segregation and the number of unhappy agents at each time step. 

3. run   ```analysis_m{#} ``` 
    Copy this file into each ap_output\SegregationModel_{#} folder. This file creates plots for each experiment's spatial autocorrelation (measured as Moran's I) and segregation curves (measured as H-index over distances). 



## License
This project is licensed under the MIT License.

## Acknowledgments
I thank Benjamin F. Jarvis, Carl Nordlund, Martin Arvidsson, the SFI GWCSS 2022 participants, and instructors John Miller and Scott E Page for their helpful comments and suggestions.
