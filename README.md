# How Politicians Change the Way They Talk

Computational analysis of parliamentary discourse in Austria, Croatia, and Great Britain using embeddings, topic modeling, and LIWC-22 linguistic features.

## Overview

This project analyzes ~1.4 million parliamentary speeches (1996-2022) to understand how political language varies across topics, parties, and time using:

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
│   ├── 01_segmentation.ipynb          # Agenda episode detection
│   ├── 02_embeddings.ipynb            # BGE-m3 speech & segment embeddings
│   ├── 03_clustering_cap.ipynb        # UMAP + GMM + CAP mapping
│   ├── 04_liwc_profiling.ipynb        # LIWC-22 scoring & z-scores
│   └── 05_visualization.ipynb         # Generate all figures
├── data/
│   ├── raw/                           # ParlaMint v5 (not in repo; download separately)
│   └── processed/                     # Intermediate outputs (.pkl, .csv)
├── figures/                           # Generated visualizations
│   ├── pipeline.png
│   ├── confusion_matrix_hr.png
│   ├── confusion_matrix_at.png
│   ├── confusion_matrix_gb.png
│   ├── liwc_difference_macro_health.png
│   ├── liwc_coalition_opposition.png
│   └── temporal_topics_comparison.png
├── outputs/                           # Final tables & statistics
└── README.md
```

---

## Reproducing Results

### 1. Setup

**Install dependencies**:
```bash
pip install pandas numpy torch sentence-transformers scikit-learn
pip install bertopic umap-learn hdbscan openai python-dotenv tqdm
pip install matplotlib seaborn openpyxl
```

**Download data**:
- Get ParlaMint v5.0 from [CLARIN.si](https://www.clarin.si/repository/xmlui/handle/11356/2006)
- Download: `ParlaMint-{AT,HR,GB}` + `ParlaMint-{AT,HR}-en.ana` (English MT)
- Place in `data/raw/`

**Configure**:
- Set `OPENAI_API_KEY` in `.env` (for CAP mapping)
- Update paths in each notebook (`BASE_DATA_DIR`, `OUTPUT_DIR`)

### 2. Run Pipeline

Execute notebooks in order:

| Step | Notebook | Runtime | Output |
|------|----------|---------|--------|
| 1. Segmentation | `01_segmentation.ipynb` | ~2–4h per country | `{AT,HR,GB}_segments.pkl` |
| 2. Embeddings | `02_embeddings.ipynb` | ~6–8h per country | `{AT,HR,GB}_embeddings.pkl` |
| 3. Clustering + CAP | `03_clustering_cap.ipynb` | ~1–2h per country | `{AT,HR,GB}_topics_cap.pkl` |
| 4. LIWC Profiling | `04_liwc_profiling.ipynb` | ~30min per country | `{AT,HR,GB}_liwc_zscores.pkl` |
| 5. Visualization | `05_visualization.ipynb` | ~30min | `figures/*.png` |

### 3. Generated Figures

| Figure | Script | Output Path |
|--------|--------|-------------|
| Pipeline diagram | Manual (thesis) | `figures/pipeline.png` |
| Confusion matrices | `05_visualization.ipynb` | `figures/confusion_matrix_{at,hr,gb}.png` |
| LIWC focal topics | `05_visualization.ipynb` | `figures/liwc_difference_macro_health.png` |
| Institutional roles | `05_visualization.ipynb` | `figures/liwc_coalition_opposition.png` |
| Temporal dynamics | `05_visualization.ipynb` | `figures/temporal_topics_comparison.png` |
| Cross-lingual consistency | `05_visualization.ipynb` | `figures/crosslingual_embedding_similarity.png` |

---

## Requirements

- **Python**: 3.8+
- **GPU**: Recommended (16GB+ VRAM for embeddings)
- **Memory**: 32GB+ RAM (for large segment clustering)
- **LIWC-22**: Separate license required ([liwc.app](https://www.liwc.app))
- **OpenAI API**: For CAP domain mapping (GPT-4o-mini)

---

## Data Access

- **ParlaMint v5.0**: External corpus; download from [CLARIN.si](https://www.clarin.si/repository/xmlui/handle/11356/2006)
- **Repository**: Stores code and processing artifacts, not raw corpus
- **Processed outputs**: Available on request (contact author)

---

## Notes

- **Sequence matters**: Episode-level coherence is key for monitoring tasks
- **Cross-country comparability**: Multilingual embeddings + CAP standardization
- **Interpretability**: c-TF–IDF keywords + conservative LLM mapping + LIWC style profiles
- **Limitations**: Human test sets are context-blind; episode-aware evaluation remains challenging

---

**Author**: Pavle Savkovic  
**Year**: 2026

---

## License

[Specify license, e.g., MIT, CC-BY-4.0]


