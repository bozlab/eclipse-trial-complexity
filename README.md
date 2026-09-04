# How Representative are Eligibility Criteria Benchmarks? A Registry-Wide Complexity Analysis

This repository contains the code used to retrieve, process, and analyze ClinicalTrials.gov data for the study examining the representativeness of publicly available annotated clinical trial eligibility criteria corpora by comparing them with a reference cohort of trials from ClinicalTrials.gov. 

## Study overview

The reference cohort included interventional trials registered on ClinicalTrials.gov with study start dates between January 1, 2005 and December 31, 2025.

ClinicalTrials.gov data were retrieved on **August 27, 2026**, using API v2 with the following query:

`AREA[StudyType]INTERVENTIONAL AND AREA[StartDate]RANGE[2005-01-01, 2025-12-31]`

Trials represented in the CHIA and Leaf Clinical Trials (LCT) corpora were identified using their NCT identifiers. Eligibility criteria text for these trials was retrieved from ClinicalTrials.gov.

Eligibility criteria were characterized using listed-item count, total word count, mean sentence length, Flesch Reading Ease (FRE), and the presence of quantitative, temporal, negation, conditional, and exception expressions.

## Repository contents

The notebooks correspond to stages of the study workflow and should be run in the following order:

1. **`CT_data.ipynb`**  
   Retrieves interventional trial records from ClinicalTrials.gov API v2 and performs retrieval-level validation and reconciliation.

2. **`raw_cohort.ipynb`**  
   Constructs the ClinicalTrials.gov cohort, extracts relevant trial characteristics and eligibility text, and applies eligibility text availability and substantive-content checks.

3. **`chia_LCT.ipynb`**  
   Extracts the NCT identifiers of trials included in CHIA and LCT and retrieves the corresponding eligibility criteria text from ClinicalTrials.gov.

4. **`remove_overlaps.ipynb`**  
   Removes trials represented in CHIA or LCT from the ClinicalTrials.gov cohort to construct the final reference cohort.

5. **`pre_processing.ipynb`**  
   Applies the same preprocessing procedures to the reference, CHIA, and LCT cohorts and derives the textual measures and expression features used in the analysis.

6. **`analysis.ipynb`**  
   Produces the descriptive analyses of eligibility criteria characteristics across the reference, CHIA, and LCT cohorts.

## Data sources

ClinicalTrials.gov  
https://clinicaltrials.gov/

ClinicalTrials.gov API v2 documentation  
https://clinicaltrials.gov/data-api/api

CHIA:  
Kury F, Butler A, Yuan C, et al. *Chia, a large annotated corpus of clinical trial eligibility criteria.* Scientific Data. 2020;7:281.  
https://doi.org/10.1038/s41597-020-00620-0

Leaf Clinical Trials Corpus:  
Dobbins NJ, Mullen T, Uzuner Ö, Yetisgen M. *The Leaf Clinical Trials Corpus: a new resource for query generation from clinical trial eligibility criteria.* Scientific Data. 2022;9:490.  
https://doi.org/10.1038/s41597-022-01521-0

## Citation

