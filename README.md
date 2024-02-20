# Picking-Invest-Managers
This file provides instructions to replicate the key results from "Finding Fortune: How Do Institutional Investors Pick Asset Managers?" by Gregory Brown, Oleg Gredil, and Preetesh Kantak published in the Review of Financial Studies, vol 36, issue 8, 2023 -- https://academic.oup.com/rfs/article/36/8/3071/6900951. 
Please cite this paper if you use this code.

This repositary provides code that 

(1) Solves the equilbrium state space for our theoretical model 

	Run file: Equilibria.m (Matlab file)
	Description: Numerically solves Hamilton-Jacobi-Bellman equation from paper across different parameter values in Matlab. State spaces are saved in folder ".\data". The optimization routine uses (i) various freely available Matlab packages that can be manually downloaded when code is run, and (ii) various functions developed by the authors which are available in folder ".\function_calls". While the file should be self-contained to call these functions as needed, the authors have run the code and supplied the various equilbrium state spaces given a set of parameter values in the ".\data" folder. The structures are named vf_alpha_sigma, where "alpha" and "sigma" are parameters described in the main model.
	
(2) Outputs all graphs capturing the model's comparative statics

	Run file: CompStats.m (Matlab file)
	Description: Uses equilibrium values solved above to produce our illustrations of the intensity (Figure 3B), investment decision (Figure 3A), fund types (old and new, in Figure 3D), the near linear theoretical relationship between intensity and the spread between allocator and market subjective beliefs of manager quality (Figure 4A) and the comparative statistics across the two parameters alpha (Figure 3C) and sigma (Figure 3B). If value functions are available in the ".\data" folder code will run. The code will use freely available Matlab packages that can be manually downloaded when code is run. All figures are deposited into the ".\figures" folder.

(3) Generates figures from simulating our primary calibration 

	Run file: MainSimulation.m (Matlab file)
	Description: Uses primary calibration (described in paper) and run simulations via the Euler's method. One thousand funds are simulated for ten years. This allows us to produce the figure showing which parts of the state space are most active (heatmap, Figure 3C) and the two examples provided in the appendix of established (Figure A1B) and young investments (Figure A1A). The code also produces the model simulated moments, which are used to calibrate the model and provided in Table A1B. Finally, the code also produces the figure that illustrates the empirically relevant relationship between expected rates of return and intensity (Figure 2). If value functions are available in the ".\data" folder code will run. The code will use freely available Matlab packages that can be manually downloaded when code is run. All figures are deposited into the ".\figures" folder.

(4) Produces two datasets that allow one to run our regression specificaions on the data simulated from the model
	
	Run file: ReplicationSimulation.m (Matlab file)
	Description: Our primary analysis uses proprietary data that is protected by a non-disclosure aggreement (NDA) between the authors and the allocator. In order to replicate the regressions in our paper we thus simulate datasets that allow one to replicate the table in the paper having to do with predicting selection by the allocator (discrete logistic hazard model, Table 5) and the post selection return dynamics of selected versus unselected, matched managers (Table 6). The code produces datasets "hazard_sim.csv" and "post_select_sim.csv", respectively.

(5) Outputs the main results tables (Table 5 and Table 6) using the datasets produced in step (4)
	
	Run file: MainSTATAcode.do
	Description: The code must be run after step (4) unless the equivalents of "hazard_sim.csv" and "post_select_sim.csv" are obtained elsewhere (i.e. not simulated from our model; use lines 25 and 37 to specificy different names for the source files). Unsurprisingly the simulated data produces somewhat different coefficients than those obtianed from our proprietary data. Of especial note is the coefficients in Tables 5 and 6 on lagged AUM, which is (i) positive and significant in our paper, but positive and insignificant using simulated data for the hazard regression (Table 5) and (ii) absorbs all the time effect coefficient in the post-selection regression in our paper, but does not in our simulated data (Table 6). As discussed in the paper (see page 17 of main text), this is driven by two phenomenon that we are not fully addressing in our model, but present in reality: 
		
		(i) Our model ignores heterogeneity of ''informatedness" across allocators. In other words ther are likely other allocators that are actively learning about manager quality beyond only returns and their decisions are reflected in AUM, making the variable more informative of future returns than in our model.
		(ii) In our model we assume intensity if functionally a direct reflection of only the allocator's ability to better filter past excess returns (i.e., public information). In reality after the decision to meet the manager the allocator may also be acquiring informtion orthogonal to the public signal, once again making AUM more informative of future returns than implied by our model. 
		
(6) Conducts the LDA analysis of the text corpus. Per our NDA, we cannot provide the meeting minutes-notes. We therefore provide the code and its output instead. The packages needed are listed at the top of the LDAMain.py and LDAOutput.py. 
	(i) LDAMain.py runs the latent dirichlet allocation (LDA) algorithm on the textual data (notes plus segmented pitchbooks). On line 217 a file is created, "document_distribution.csv", which available to view in ".\data" folder. This file contains the allocation of the algorithm for each note across the 30 topics. This data is used to produce our empirical intensity measure as described in section 3.
	(ii) LDAOutput.py produces the coherence scores (CS) (see line 50) for the topics and also lists the top 10 words for each topic in "coherenceScore.csv" which is also available in the ".\data" folder. This output is used to create Table 4. 

Copyright 2023. Gregory Brown, Oleg Gredil, and Preetesh Kantak.
