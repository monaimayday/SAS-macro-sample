# SAS-macro-sample
SAS macro sample
Author: Xue Jia

# Introduction
This SAS macro is used for a simulation of selecting stratification factors in a clinical trial;

# Question: 
In a phase III oncology study with overall survival (OS) as the primary endpoint, we have 5 binary baseline prognostic factors (X1-X5), each of them have two levels. Randomization with these important variables as stratification factors can improve study power. However, too much stratified factors may cause over-stratification problem. If we already defined 4 stratified factors, should we add the 5th stratification factor in the randomization?

# Assumption:  
Stratification factors	Percentage of level 1	Percentage of level 2	Median OS of level 1 (mons)	Median OS of level 2 (mons)	HR	β
X1	24.50%	75.50%	8.5	4.5	1.89	0.63
X2	37.75%	62.25%	6.6	4	1.65	0.52
X3	41.70%	58.30%	4.6	6.7	0.69	-0.39
X4	37.60%	62.40%	4.5	4.2	1.07	0.07
X5	35%	65%	6	8	0.75	-0.29

Sample size 468 (α=0.05, β=0.1, HR=0.71)
Stratified blocked randomization with block size=4; Randomized ratio 1:1

# Method:
1.	Let Xi be the baseline prognostic variables, as well as potential stratification factors in the randomization, each factor has two levels.
2.	Simulated a study sample, in which each subject would be given a value in each Xi, based on the percentage of two levels of each Xi. These percentages are got from historical data.
3.	Repeated the simulations to get 1000 study samples;
4.	Generated a randomization scheme with block size=4 and arm=0,1;
5.	Assigned the study samples with arms: using the randomization scheme in each strata formed by different stratification combinations;
6.	According to the hazard function for the cox proportional hazard model, we used βi got from ln(HR) to calculate each patient’s hazard λ and survival time T;
7.	Defined censor C;
8.	For each study sample, performed Cox regression analysis of survival data in two arms to get P value;
9.	Calculated power;
10.	Compared the power with different stratification combinations, e.g. using X1-X4, or X1-X5 as stratification factors in the randomization
