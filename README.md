# Mendalian Randomization 
Mendelian Randomization (MR) is a statistical method that uses genetic variants as natural instruments to infer the causal effect of a modifiable exposure (like a lifestyle factor) on a health outcome, 
such as a disease. By exploiting the principle that genetic inheritance is random and independent of other lifestyle choices or confounding factors, 
MR allows researchers to overcome biases found in traditional observational studies, providing stronger evidence for cause-and-effect relationships. 
## How it Works
 ### 1. Genetic Variants as Instruments:
 - MR uses genetic variants, such as single-nucleotide polymorphisms (SNPs), as "instruments". These variants are associated with a particular exposure (e.g., a gene that influences smoking habits). An instrumental variable is a special type of independent variable used to address issues like endogeneity and estimate causal relationships when other variables are correlated with the error term.
 - A **confounder** is a third variable that distorts the true relationship between an exposure and an outcome by influencing both. An **instrumental variable (IV)** is a third variable that is independent of the outcome and unobserved confounders, but it affects the exposure, allowing researchers to estimate a causal effect that is free from confounding. The key difference is that a confounder introduces bias, while an IV is a tool used to remove or control for that bias, particularly unmeasured confounding.  
 ### 2. Random Inheritance:
 Because genes are inherited randomly from parents, the distribution of these genetic variants in the population is independent of other factors that could confound the relationship between an exposure and an outcome (like age, socioeconomic status, or lifestyle choices). 
 ### 3. Inferring Causality:
 By observing how genetic variants that are known to influence a specific exposure also influence the outcome, researchers can estimate the causal impact of the exposure on the disease. 
## Key Advantages
 ### Reduces Confounding:
 Genetic variants are generally not associated with lifestyle or environmental factors that could otherwise distort the observed relationship between an exposure and outcome. 
 ### Avoids Reverse Causation:
 Random genetic inheritance also helps avoid reverse causation, where the outcome might influence the exposure (e.g., a disease causing someone to adopt an unhealthy lifestyle), as genes are established before exposure. 
## Applications
  ### Identifying Risk Factors:
  MR can provide supportive evidence for whether a risk factor, such as high cholesterol or a specific behavior, is a true cause of a disease. 
  ### Informing Drug Development:
  It can help identify and prioritize potential drug targets by understanding the causal role of biological pathways in disease. 
## Limitations
 ### Relies on Assumptions:
 The validity of MR studies depends on several key assumptions, such as the genetic variant only affecting the outcome through the specified exposure. These assumptions must be carefully assessed in each study. 
 ### Focus on Onset:
 MR is often more effective at identifying factors that influence the onset of a disease rather than its progression or treatment once developed. 
## Apply to mineralocorticoid receptor antagonists (MRAs) on human health outcomes of Aortic Aneurysm/Dissection (AAD)
Mendelian Randomisation (MR) using UK Biobank data is a powerful way to infer causal relationships between risk factors (exposures) and health outcomes, leveraging genetic variants as instrumental variables (IVs). Here’s a step-by-step guide that outlines both the conceptual and practical workflow.
1. **Conceptual overview**
Mendelian Randomisation (MR) uses the random allocation of alleles at conception as a “natural experiment” to test whether an exposure causally affects an outcome.
It relies on three key assumptions:

  - *Relevance*: Genetic variants (instruments) are associated with the exposure.
  - *Independence*: Instruments are independent of confounders.
  - *Exclusion Restriction*: Instruments affect the outcome only through the exposure.
- **Workflow for UK Biobank data**
 a. Define your exposure and outcome
    - Exposure: LDL cholesterol levels, BMI, alcohol intake.
    - Outcome: AAD treatment.
    Both should be measurable (directly or via summary statistics) in UK Biobank or from external GWAS consortia.

 b. Choose or derive your genetic instruments
    You need SNPs associated with your exposure at genome-wide significance (typically p<5×10−8).
    **Options:**
     - Use published GWAS summary statistics for your exposure (e.g., from GWAS Catalog, OpenGWAS).
     - Or perform your own GWAS within UK Biobank using tools like PLINK, BOLT-LMM, or regenie.
    **Make sure to:**
     - LD-clump your SNPs to ensure independence (e.g., r² < 0.001, 10,000 kb window).
     - Record SNP, effect allele, beta, SE, and p-value.
  c. Obtain genetic associations for the outcome
     You’ll need corresponding SNP-outcome associations.

If using individual-level data in UK Biobank:

Run regression of the outcome on each SNP, adjusting for covariates (age, sex, principal components, etc.).

If using summary-level data:

Extract associations from published GWAS or UK Biobank’s Pan-UKB project.

4. Harmonise exposure and outcome data

Align alleles so that the effect of each SNP corresponds to the same allele in both datasets.
This can be done automatically using R packages like TwoSampleMR.

5. Perform the MR analysis

You can use:

R package: TwoSampleMR (for summary data)

R package: MendelianRandomization (for individual-level data)

Python package: pymr

Typical methods include:

Inverse-Variance Weighted (IVW) (main analysis)

MR-Egger (checks for directional pleiotropy)

Weighted Median / Mode

Leave-one-out analysis (robustness)
