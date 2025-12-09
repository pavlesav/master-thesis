# How Politicians Change the Way They Talk

Computational analysis of parliamentary discourse in Austria, Croatia, and Great Britain using embeddings, topic modeling, and LIWC-22 linguistic features.

## Overview

This project analyzes ~650,000 parliamentary speeches (1996-2022) to understand how political language varies across topics, parties, and time using:

- **Semantic segmentation** of sessions into agenda items
- **BERTopic + GPT-4** for topic classification (23 policy categories)
- **LIWC-22 analysis** of 37 linguistic dimensions
- **Temporal tracking** of discourse patterns

## Quick Start

### 1. Install Dependencies

```bash
pip install pandas numpy torch sentence-transformers scikit-learn bertopic umap-learn
pip install openai python-dotenv tqdm matplotlib seaborn openpyxl
```

### 2. Download Data

Get ParlaMint 5.0 from [CLARIN.si](https://www.clarin.si/repository/xmlui/handle/11356/2006):
- ParlaMint-AT + ParlaMint-AT-en.ana (Austria, bilingual)
- ParlaMint-HR + ParlaMint-HR-en.ana (Croatia, bilingual)
- ParlaMint-GB (Great Britain, English)

Organize as:
```
data/
├── AT/ParlaMint-AT/ParlaMint-AT.txt/[year folders]
├── AT/ParlaMint5.0-AT-en.ana/ParlaMint-AT-en.txt/[year folders]
├── HR/[same structure]
└── GB/ParlaMint-GB/ParlaMint-GB.txt/[year folders]
```

### 3. Run Analysis Pipeline

**Notebook 1: `data_preprocessing.ipynb`** (~8 hours per country)
- Loads speeches, generates BGE-m3 embeddings
- Detects segment boundaries using similarity + keywords
- Outputs: `{AT,HR,GB}_speeches_processed.pkl`

**Notebook 2: `topic_modelling.ipynb`** (~1-2 hours)
- Runs BERTopic with GMM clustering (150-250 topics)
- Classifies topics with GPT-4o-mini into CAP categories
- Merges LIWC-22 results and human labels
- Outputs: `{AT,HR,GB}_final.pkl`

**Notebook 3: `visualization.ipynb`** (~30 mins)
- Generates confusion matrices, z-score heatmaps
- Creates temporal plots with event markers
- Outputs 30+ figures to `figures/` subfolders

### 4. Configure Paths

Update these variables in each notebook:
- `data_preprocessing.ipynb`: `LOCAL_DATA_DIR` or `COLAB_DATA_DIR`
- `topic_modelling.ipynb`: `BASE_DATA_DIR` 
- `visualization.ipynb`: `BASE_DATA_DIR`, `base_output_dir`

Set OpenAI API key in `.env`:
```
OPENAI_API_KEY=your_key_here
```

## Project Structure

```
master-thesis/
├── code/
│   ├── data_preprocessing.ipynb    # Embeddings + segmentation
│   ├── topic_modelling.ipynb       # BERTopic + GPT + LIWC
│   └── visualization.ipynb         # All figures
├── data/                           # Raw + processed data
├── figures/                        # Generated visualizations
└── README.md
```

## Key Methods

- **Embeddings**: BAAI/bge-m3 (1024-dim, multilingual)
- **Segmentation**: Cosine similarity (95th percentile) + chairperson keywords
- **Topic Modeling**: BERTopic → GMM (150-250 clusters) → GPT-4o-mini classification
- **LIWC**: Z-scores vs population norms, Holm's correction (α=0.01)

## Requirements

- Python 3.8+
- GPU and at least 16GB or RAM recommended
- OpenAI API key
- LIWC-22 software

## Citation

```
[Add your thesis citation]
```


