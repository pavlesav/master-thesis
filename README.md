# How Politicians Change the Way They Talk

A computational analysis of parliamentary discourse across multiple countries using modern NLP techniques, topic modeling, and LIWC-22 (Linguistic Inquiry and Word Count) linguistic analysis.

## Project Overview

This project analyzes linguistic patterns in parliamentary speeches from multiple European countries to understand how political discourse varies across topics, parties, speakers, and countries. The analysis pipeline includes:

- Semantic segmentation of parliamentary sessions into agenda items
- Embedding-based topic modeling with BERTopic
- Comparison with ParlaCAP benchmark labels
- LIWC-22 linguistic feature analysis
- Statistical analysis with multiple comparison corrections
- Cross-country comparative analysis

## Key Features

- **Automated Agenda Segmentation**: Semantic boundary detection within parliamentary sessions
- **Multi-language Support**: Handles original language and machine-translated English
- **Advanced Topic Modeling**: BERTopic with custom embeddings for fine-grained topic detection
- **LIWC-22 Analysis**: Comprehensive linguistic feature extraction
- **Statistical Rigor**: Holm's method for multiple comparison corrections
- **Benchmark Comparison**: Validation against ParlaCAP standard labels

## Data Sources

Parliamentary data is sourced from the **ParlaMint corpus** available at [CLARIN.si](https://www.clarin.si/repository/xmlui/handle/11356/1432).

### Supported Countries
- Austria (AT)
- Belgium (BE)
- Bosnia and Herzegovina (BA)
- Additional countries can be added following the same pipeline

## Project Structure

```
master-thesis/
├── notebooks/
│   ├── 1_data_preparation.ipynb           # Data loading and preprocessing
│   ├── 2_embedding_generation.ipynb       # Generate embeddings for speeches
│   ├── 3_agenda_segmentation.ipynb        # Detect agenda boundaries
│   ├── 4_topic_modeling.ipynb             # BERTopic analysis
│   ├── 5_parlacap_comparison.ipynb        # Benchmark validation
│   ├── 6_liwc_analysis.ipynb              # LIWC-22 feature analysis
│   └── 7_visualization.ipynb              # Results visualization
├── data/
│   ├── raw/                               # Raw ParlaMint data (not in repo)
│   ├── processed/                         # Processed datasets
│   ├── embeddings/                        # Generated embeddings
│   ├── topics/                            # Topic modeling results
│   └── liwc/                              # LIWC analysis outputs
├── src/
│   ├── preprocessing.py                   # Data preprocessing utilities
│   ├── segmentation.py                    # Agenda boundary detection
│   ├── topic_modeling.py                  # BERTopic wrapper functions
│   └── statistical_analysis.py            # Statistical testing utilities
├── results/
│   ├── figures/                           # Generated visualizations
│   └── tables/                            # Statistical tables
├── README.md
└── requirements.txt
```

## Installation & Setup

### Prerequisites

- Python 3.8 or higher
- 16GB+ RAM recommended for embedding generation
- GPU recommended (but not required) for faster processing

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/master-thesis.git
cd master-thesis
```

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 3: Download Parliamentary Data

1. Visit [CLARIN.si ParlaMint repository](https://www.clarin.si/repository/xmlui/handle/11356/1432)
2. Download the ParlaMint corpus for desired countries (e.g., ParlaMint-AT, ParlaMint-BE)
3. Extract the downloaded files to `data/raw/`

**Directory structure after download:**
```
data/raw/
├── ParlaMint-AT/
│   ├── ParlaMint-AT.xml
│   └── ...
├── ParlaMint-BE/
│   ├── ParlaMint-BE.xml
│   └── ...
└── ...
```

### Step 4: Download LIWC-22 Dictionary (Optional)

For LIWC analysis, you'll need access to the LIWC-22 dictionary:
1. Purchase or obtain access to LIWC-22 from [LIWC.app](https://www.liwc.app/)
2. Place the dictionary file in `data/liwc/LIWC-22.dic`

## Usage Workflow

### 1. Data Preparation

Run the data preparation notebook to parse and structure the parliamentary data:

```bash
jupyter notebook notebooks/1_data_preparation.ipynb
```

This notebook will:
- Parse ParlaMint XML files
- Extract speeches with metadata (speaker, party, date, etc.)
- Create structured datasets for analysis

### 2. Generate Embeddings

Generate semantic embeddings for speeches:

```bash
jupyter notebook notebooks/2_embedding_generation.ipynb
```

Options:
- **Original language embeddings**: Using multilingual models
- **Machine-translated English embeddings**: For cross-country comparison

### 3. Agenda Segmentation

Detect semantic boundaries within parliamentary sessions:

```bash
jupyter notebook notebooks/3_agenda_segmentation.ipynb
```

Methods:
- Cosine similarity dips between consecutive speeches
- Chairperson agenda mentions
- Manual annotation comparison
- Sensitivity analysis for parameters

### 4. Topic Modeling

Run BERTopic to identify fine-grained topics:

```bash
jupyter notebook notebooks/4_topic_modeling.ipynb
```

Features:
- Custom embeddings from step 2
- Guided topic modeling with KeyBERTInspired
- Clustering with HDBSCAN or K-means
- Mapping to 22 ParlaCAP categories using GPT

### 5. Benchmark Validation

Compare results with ParlaCAP labels:

```bash
jupyter notebook notebooks/5_parlacap_comparison.ipynb
```

Validation metrics:
- Label agreement rates
- Confusion matrices
- Category-level precision/recall

### 6. LIWC-22 Analysis

Extract and analyze linguistic features:

```bash
jupyter notebook notebooks/6_liwc_analysis.ipynb
```

Analysis dimensions:
- Topic-based linguistic patterns
- Party comparisons
- Temporal evolution
- Speaker role analysis
- Coalition vs. opposition rhetoric
- Demographic patterns (age, gender)

### 7. Visualization

Generate comprehensive visualizations:

```bash
jupyter notebook notebooks/7_visualization.ipynb
```

Outputs saved to `results/figures/`

## Statistical Methodology

- **Independent t-tests** for group comparisons
- **Holm's method** for family-wise error rate control (α = 0.01)
- **Effect size calculations** (Cohen's d)
- **LIWC-22 reference corpus** for contextual comparison

## Key Findings

Results include:
- Agenda segmentation accuracy vs. manual annotations
- Topic model performance vs. ParlaCAP benchmark
- Significant linguistic differences across:
  - Topics
  - Political parties
  - Speaker roles
  - Countries
- Cross-country discourse pattern comparison

## Reproducibility

All analyses are fully reproducible:
1. Notebooks contain detailed comments and explanations
2. Random seeds are fixed where applicable
3. Data preprocessing steps are documented
4. Statistical methods are transparently reported

## Output Files

After running the complete pipeline, you'll have:
- `data/processed/`: Cleaned and structured speech datasets
- `data/embeddings/`: Speech embeddings in multiple languages
- `data/topics/`: Topic assignments and labels
- `results/figures/`: Publication-ready visualizations
- `results/tables/`: Statistical test results

## Contributing

This is a research project. For questions or collaborations, please open an issue or contact the author.

## Citation

If you use this code or methodology, please cite:

```
[Your thesis citation information]
```

## Acknowledgments

- **ParlaMint Corpus**: European parliamentary data
- **CLARIN.si**: Data hosting and infrastructure
- **LIWC-22**: Linguistic analysis framework
- **BERTopic**: Topic modeling library

## License

[Your chosen license]

---

*This project is part of a master's thesis on computational political discourse analysis.*

