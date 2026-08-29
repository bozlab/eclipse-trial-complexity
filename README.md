# Characterizing the Textual Complexity of Eligibility Criteria Across Disease Domains in Interventional Clinical Trials

This repository contains the code used to retrieve, process, and analyze ClinicalTrials.gov data for a study examining the textual complexity of clinical trial eligibility criteria across disease domains.

## Study overview

The study included interventional trials registered on ClinicalTrials.gov with study start dates between January 1, 2005 and December 31, 2025.

ClinicalTrials.gov data were retrieved on **August 27, 2026**, using API v2 with the following query:

`AREA[StudyType]INTERVENTIONAL AND AREA[StartDate]RANGE[2005-01-01, 2025-12-31]`

Eligibility criteria were characterized using listed-item count, total word count, mean sentence length, Flesch Reading Ease (FRE), and the presence of quantitative, temporal, negation, conditional, and exception expressions.

Trials were classified into six disease domains: neoplasms, nervous system diseases, cardiovascular diseases, metabolic diseases, respiratory tract diseases, and infections.

## Repository contents

The notebooks correspond to successive stages of the study workflow and should be run in the following order:

1. **`CT_data.ipynb`**  
   Retrieves trial records from ClinicalTrials.gov API v2 and performs retrieval-level validation and reconciliation.

2. **`raw_cohort.ipynb`**  
   Constructs the study cohort, extracts relevant trial characteristics and eligibility text, and applies eligibility-text availability and substantive-content checks.

3. **`disease_grouping.ipynb`**  
   Classifies trials into the six prespecified disease domains using condition MeSH information.

4. **`pre_processing.ipynb`**  
   Preprocesses eligibility text and derives the textual measures and expression-based features used in the analysis.

5. **`qc.ipynb`**  
   Performs quality-control and reconciliation checks on the processed analytic dataset.

6. **`analysis.ipynb`**  
   Produces the descriptive analyses of eligibility criteria overall and across disease domains.

## Disease-domain classification

Trials were classified using Medical Subject Headings (MeSH) information provided by ClinicalTrials.gov. Both direct condition MeSH identifiers and their ancestor identifiers were considered.

The six disease domains and corresponding MeSH identifiers were:

| Disease domain | MeSH ID |
|---|---|
| Neoplasms | D009369 |
| Nervous System Diseases | D009422 |
| Cardiovascular Diseases | D002318 |
| Metabolic Diseases | D008659 |
| Respiratory Tract Diseases | D012140 |
| Infections | D007239 |

Because conditions may map to more than one disease domain within the MeSH hierarchy, trials could be assigned to multiple domains. Trials that did not map to any of the six selected domains were not included in the disease-domain analyses.

## Eligibility-criteria processing

Eligibility criteria were processed at the study level using the complete eligibility text. Text was normalized, and inclusion and exclusion section headings were identified. Because analyses were conducted on the complete eligibility field rather than separately by inclusion and exclusion sections, studies without identifiable section headings were retained.

Generic introductory phrases at the beginning of recognized inclusion and exclusion sections were removed. For text-based analyses, section headings and list markers were removed.

The number of listed eligibility items was determined from bullet, numeric, alphabetic, and Roman numeral lists, with sub-items excluded from the count. Sentence-like units were identified using line breaks, sentence-ending punctuation, and list formatting. Mean sentence length was calculated by dividing the total word count by the number of sentence-like units.

Flesch Reading Ease was used to assess readability, with higher scores indicating more readable text. Quantitative, temporal, negation, conditional, and exception expressions were identified using predefined regular expressions. An expression was considered present for a study when at least one occurrence was detected in its eligibility text.

## Data and generated files

Large raw, intermediate, and derived data files are not included in this repository because of their size. The source trial data are publicly available from ClinicalTrials.gov.

The data used for the reported analyses were retrieved on **August 27, 2026**. ClinicalTrials.gov is continuously updated, and trial records may be added or modified over time. Therefore, rerunning the retrieval code at a later date may produce a dataset that differs from the dataset used in the study.

The computational workflow can be reproduced by running the notebooks sequentially, beginning with `CT_data.ipynb`. The notebooks generate the required intermediate and output files as the workflow progresses.

## Quality control

Quality-control and reconciliation procedures are incorporated throughout the workflow. These include checks of study identifiers, record counts, expected variables, disease-domain assignments, preprocessing outputs, generated files, and consistency between successive stages of the pipeline.

The dedicated `qc.ipynb` notebook performs final quality-control and reconciliation checks before analysis.

## Data source

ClinicalTrials.gov  
https://clinicaltrials.gov/

ClinicalTrials.gov API v2 documentation  
https://clinicaltrials.gov/data-api/api

## Citation

Citation information will be added following publication of the associated study.

## License

License information will be added before public release.
