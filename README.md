# MS Prodromal Prediction using Clinical Concepts

Project Overview
This project investigates the prediction of Multiple Sclerosis (MS) diagnosis during the prodromal phase using unstructured clinical data from electronic health records (EHR). The prodromal phase of MS is characterized by increased healthcare utilization and early signs of neurodegeneration 5-10 years before formal diagnosis. While structured EHR data has been used for MS prediction, the utilization of unstructured clinical notes remains largely unexplored.

# Objectives:

- Extract and analyze clinical concepts from unstructured EHR notes
- Develop predictive models for MS diagnosis at 1, 3, and 5-year intervals
- Evaluate the impact of SPOKE knowledge graph embeddings on prediction accuracy
- Compare performance of different feature selection and modeling approaches

# Requirements

- Python 3.13.1
- Jupyter Notebook
- Key Python Libraries:
    - DuckDB for efficient database operations
    - Pandas and NumPy for data manipulation
    - Scikit-learn for machine learning
    - Matplotlib and Seaborn for visualization
    - Requests for API interactions
    - tqdm for progress tracking
- Access to UCSF’s Information Commons (IC) data
- BioPortal API key for concept mapping
- SPOKE knowledge graph data and embeddings

# Repository Structure

## Notebooks (in order of execution):

s1_OMOP_Query_MS.ipynb

    Identifies MS patients using OMOP diagnostic codes
    Extracts clinical notes and encounters
    Implements inclusion/exclusion criteria
    Creates initial MS cohort with demographic information

s2_OMOP_Query_Control.ipynb

    Identifies potential control patients
    Applies matching inclusion/exclusion criteria
    Creates initial control cohort
    Handles duplicate patient records

s3_PSM.ipynb

    Implements propensity score matching
    Balances cohorts based on demographics and healthcare utilization
    Provides matching quality assessment
    Creates final matched cohorts for analysis

s4_Cohort_Concepts.ipynb

    Extracts clinical concepts using cTAKES
    Processes and filters concept occurrences
    Creates concept frequency matrices
    Handles temporal alignment of concepts

s5_Mapping.ipynb

    Maps clinical concepts to SPOKE entities
    Generates Patient Specific Entity Vectors (PSEVs)
    Implements BioPortal API integration
    Creates concept embeddings for modeling

s6_Modeling.ipynb

    Implements multiple modeling approaches:
        Basic logistic regression with all concepts
        Feature-selected logistic regression
        Scaled and normalized models
        SPOKE-enhanced prediction models
    Provides comprehensive model evaluation
    Generates visualization of results

## Additional Files:

spoke_mappings.json: Pre-computed mappings between clinical concepts and SPOKE entities


## Additional Data Structures
The notebooks expect data to be accessible via UCSF Information Commons:

/path/to/ic/data/

├── DEID_OMOP/

└── DEID_CDW/

/path/to/scratch/

# Usage Instructions

Environment Setup:

    Ensure access to UCSF IC data
    Configure paths in notebooks to point to correct data locations
    Install required Python packages
    Obtain necessary API keys

Notebook Execution:

    Run notebooks in sequential order (s1 through s6)
    Each notebook contains detailed markdown cells explaining the process
    Intermediate outputs are saved to prevent recomputation
    Monitor execution progress through provided status indicators

Data Handling:

    Large datasets are processed using DuckDB for memory efficiency
    Intermediate results are saved in parquet format
    SPOKE mappings are cached to prevent redundant API calls

## Model Evaluation

The repository includes comprehensive evaluation metrics:

- ROC AUC scores for all prediction windows
- Feature importance analysis
- Comparison of different modeling approaches
- Visualization of results

# Notes

- Some processes require significant computational resources
- API rate limits may affect concept mapping speed
- Large memory requirements for SPOKE embedding generation

# Future Improvements

- Integration of additional knowledge sources
- Enhanced feature selection methods
- Improved temporal modeling

# Contact
For questions about the codebase or collaboration opportunities, please contact: noah.baker@ucsf.edu
