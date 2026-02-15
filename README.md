# Statistical Analysis of Rare Genetic Variants in the ATXN2 Gene

**Master's Thesis Project** | Simon Fraser University (2024)  
**Author:** Diksha Jethnani  
**Supervisor:** Dr. Jinko Graham  

[![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)](https://www.r-project.org/)
[![Statistics](https://img.shields.io/badge/Statistics-Bayesian%20%7C%20SKAT-blue)](https://github.com/yourusername/DJ)

---

## 🔬 Project Overview

This research investigates the association between rare genetic variants in the first exon of the **ATXN2 gene** and neurodegenerative diseases. Using advanced statistical methods on diagnostic exome sequencing data from 358 patients, we identified significant associations that could inform future clinical trials and treatment strategies.

### Key Finding
**Rare variants in exon 1 of ATXN2 are significantly associated with neurodegenerative disease status (p = 0.005-0.03)**, even after adjusting for age, sex, and technical confounders.

---

## 📊 Dataset

- **Sample Size:** 358 patients from diagnostic genome sequencing
- **Cases:** 134 with neurodegenerative diseases (primarily ALS)
- **Controls:** 161 with non-neurodegenerative diseases
- **Uncertain:** 63 with mixed symptoms
- **Variants Analyzed:** 19 rare genetic variants (frequency < 1% in gnomAD database)

### Diseases Studied
- Amyotrophic Lateral Sclerosis (ALS) - 74 cases
- Spinocerebellar Ataxia (SCA)
- Spastic Paraplegia
- Other neurodegenerative and control conditions

---

## 🧬 Background: Why ATXN2 Matters

The **ATXN2 gene** encodes a protein critical for:
- RNA translation and regulation
- Mitochondrial function
- Cell growth and endocytosis

**Clinical Significance:**
- Large polyglutamine (CAG) expansions → Spinocerebellar Ataxia Type 2 (SCA2)
- Intermediate expansions (27-34 repeats) → Risk factor for ALS
- Current clinical trial (NCT04494256) using ATXN2 antisense oligonucleotides

**Research Gap:** While PolyQ expansions are well-studied, the role of other rare variants in exon 1 remains unclear. This thesis addresses that gap.

---

## 🔍 Methodology

### 1. Exploratory Data Analysis
- **Univariate analysis:** Distribution of age, sex, disease types, enrichment kits
- **Bivariate analysis:** Association tests between categorical variables
- **Confounder identification:** Enrichment kit identified as a potential confounder
- **Visualization:** Age distribution, disease patterns, variant presence

**Tools Used:** R (ggplot2, dplyr), descriptive statistics, exact permutation tests

### 2. Statistical Modeling

#### Sequence Kernel Association Test (SKAT-O)
- **Method:** Rare-variant association testing using kernel regression framework
- **Advantages:** 
  - Accounts for varying effects across variants
  - Weights rare variants more heavily
  - Handles both protective and deleterious variants
  - Adjusts for familial relationships (kinship matrix)

#### Models Fitted
1. **Logistic Regression** (n=352 unrelated subjects)
   - Binary outcome: ND vs non-ND
   - Covariates: age, sex, enrichment kit
   - Result: **p = 0.03** (with "maybe ND" subjects included)
   - Result: **p = 0.005-0.008** (excluding "maybe ND" subjects)

2. **Gaussian Regression** (n=358 related subjects)
   - Accounted for familial relationships via kinship matrix
   - 4 parent-child trios, 1 father-son pair, 1 sibling pair
   - Result: **p = 0.02**

### 3. Data Preprocessing
- Calculated patient age from dates of birth and sampling
- Created genotype matrix (358 × 19) with variant copy numbers
- Imputed missing allele frequencies from gnomAD database
- Removed questionable variants through frequency thresholding
- Merged enrichment kit categories based on vendor specifications

### 4. Confounding Variable Adjustment
- **Age:** Significantly associated with ND status (older patients more likely to have ND)
- **Sex:** No significant association with ND status
- **Enrichment kits:** Significant confounder, adjusted in all models

---

## 📈 Key Results

### Main Findings

| Analysis | Sample Size | P-value | Interpretation |
|----------|-------------|---------|----------------|
| Logistic (with "maybe ND") | 352 | 0.03 | Significant association |
| Gaussian (with "maybe ND") | 358 | 0.02 | Significant association |
| Logistic (excluding "maybe ND") | 289 | 0.005-0.008 | **Strong association** |

### Effect Estimates (Logistic Regression)

| Variable | Estimate | P-value | Interpretation |
|----------|----------|---------|----------------|
| Age | +0.077 | <0.001 | Older age → higher ND risk |
| Sex (Male) | +0.079 | 0.78 | No significant sex difference |
| Enrichment Kit (TCE) | -0.846 | 0.01 | Technical confounder |

### Variant Characteristics
- **Most common functional consequence:** Frameshift variants (33/53 total)
- **Questionable variants excluded:** 3 variants with no gnomAD frequency data
- **Variant weights:** Based on gnomAD population allele frequencies

---

## 💻 Technical Implementation

### Technologies & Tools
- **Language:** R (version 4.x)
- **Key Packages:**
  - `SKAT` - Sequence Kernel Association Test
  - `ggplot2` - Data visualization
  - `dplyr` - Data manipulation
  - `readxl` - Excel data import
- **Statistical Methods:**
  - SKAT-O (optimized kernel association test)
  - Logistic regression with bootstrap testing (100,000-150,000 replicates)
  - Exact permutation tests
  - F-tests with parametric bootstrapping
  - Generalized additive models (GAM)

### Reproducibility
- All analysis code available in R scripts
- Data preprocessing documented step-by-step
- Bootstrap replicates ensure robust p-values
- Sensitivity analyses performed (with/without "maybe ND" subjects)

---

## 🎯 Impact & Implications

### Clinical Relevance
1. **Treatment Expansion:** Suggests ATXN2-targeted therapies (currently only for PolyQ expansions) might benefit patients with other exon 1 variants
2. **Diagnostic Value:** Rare variants in ATXN2 exon 1 could serve as genetic markers for ND risk assessment
3. **Future Research:** Recommends long-read sequencing for better resolution of repeat regions

### Statistical Contributions
- Demonstrated effective confounder adjustment in genetic association studies
- Showed robustness of SKAT-O across different modeling assumptions
- Handled familial relationships through kinship matrices
- Addressed missing data through principled imputation

---

## 📚 Repository Contents

```
DJ/
├── README.md                           # This file
├── Diksha_Jethnani_Msc_Thesis_Final.pdf   # Full thesis document
├── scripts/
│   ├── exploratory_analysis.R          # EDA and visualization
│   ├── preprocessing.R                 # Data cleaning and preparation
│   ├── skat_analysis.R                 # Main SKAT-O analysis
│   └── supplementary_tables.R          # Generate appendix tables
├── data/
│   ├── persons_data.xlsx               # Patient information (anonymized)
│   └── variants_data.xlsx              # Genetic variant details
└── results/
    ├── figures/                        # Plots and visualizations
    └── tables/                         # Summary statistics
```

---

## 🏆 Academic Achievements

- **Thesis Grade:** MSc in Statistics, Simon Fraser University (April 2024)
- **Fellowships:** 
  - Graduate Fellowship - $10,000 (2023)
  - Entrance Award - $5,500 (2022)
- **Committee:** 
  - Supervisor: Dr. Jinko Graham (Statistics & Actuarial Science)
  - Committee Member: Dr. Brad McNeney
  - Examiner: Dr. Joanna Lubieniecka

---

## 🔗 Related Work

This thesis is part of a collaborative effort with clinical genetics researchers at:
- **Ruhr University Bochum** (diagnostic genome-sequencing facility)
- **Simon Fraser University** (Statistical Genetics Lab)

**Coursework Supporting This Research:**
- Statistical Computing
- Applied Statistics
- Statistical Consulting
- Machine Learning
- Regression & Predictive Analytics

---

## 📖 How to Use This Repository

### For Researchers
1. Read the [full thesis PDF](./Diksha_Jethnani_Msc_Thesis_Final.pdf) for complete methodology
2. Explore R scripts in `/scripts` for implementation details
3. Examine `/results/figures` for visualizations

### For Recruiters
This project demonstrates:
- ✅ **Statistical Expertise:** SKAT-O, logistic regression, Bayesian methods, bootstrap testing
- ✅ **Programming Skills:** Advanced R, data manipulation, visualization
- ✅ **Domain Knowledge:** Genetics, genomics, neurodegenerative diseases
- ✅ **Communication:** Clear documentation, stakeholder-ready reports
- ✅ **Problem Solving:** Confounder identification, missing data handling, sensitivity analyses

---

## 📧 Contact

**Diksha Jethnani**  
📍 Surrey, BC, Canada  
📧 d.jethnani1999@gmail.com  
📱 778-325-5092  

---

## 📝 Citation

If you use this work, please cite:

```bibtex
@mastersthesis{jethnani2024atxn2,
  author  = {Diksha Jethnani},
  title   = {Statistical analysis of rare genetic variants in the first exon of the ataxin-2 gene in patients with neurodegenerative diseases},
  school  = {Simon Fraser University},
  year    = {2024},
  type    = {Master's Thesis},
  address = {Burnaby, BC, Canada}
}
```

---

## 🙏 Acknowledgments

Special thanks to:
- **Dr. Jinko Graham** for supervision and statistical guidance
- **Dr. Joanna Lubieniecka** for clinical genetics expertise and data provision
- **Dr. Brad McNeney** for committee feedback
- **Ruhr University Bochum** for diagnostic sequencing data
- **SFU Department of Statistics** for coursework and research support

---

## 📄 License

This thesis is copyright © 2024 Diksha Jethnani. All rights reserved.  
Code and analysis scripts are available for academic and educational purposes.

---

*Last Updated: February 2026*
