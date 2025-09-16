# How Politicians Change the Way They Talk

A computational analysis of Austrian parliamentary discourse using LIWC-22 (Linguistic Inquiry and Word Count).

## Project Overview

This project analyzes linguistic patterns in Austrian parliamentary speeches to understand how political discourse varies across topics, parties, and speakers.

## Key Features

- LIWC-22 linguistic analysis of parliamentary speeches
- Topic modeling and classification
- Statistical analysis with Holm's method for multiple comparison corrections
- Comprehensive visualization of linguistic patterns across different dimensions

## Project Structure

```
thesis/
├── notebooks/
│   └── liwc_visualization.ipynb    # Main analysis notebook
├── data/
│   ├── AT_LIWC.csv                # Austrian parliamentary data with LIWC features
│   ├── AT_with_topics.pkl         # Topic classifications
│   └── LIWC-22.Descriptive.Statistics-Test.Kitchen.xlsx
├── README.md
└── requirements.txt
```

## Analysis Components

1. **Topic-based Analysis**: Comparing "Tax and Budget Needs" vs other topics
2. **Party Comparisons**: Linguistic differences across political parties
3. **Temporal Analysis**: Evolution of discourse over time
4. **Speaker Role Analysis**: Language differences by parliamentary roles
5. **Coalition vs Opposition**: Rhetorical strategy differences
6. **Demographic Analysis**: Age and gender-based linguistic patterns

## Key Findings

- Statistical analysis using Holm's method for family-wise error rate control
- Significant linguistic differences identified across multiple LIWC dimensions
- Comprehensive visualization of political discourse patterns

## Requirements

- Python 3.8+
- Jupyter Notebook
- See `requirements.txt` for full package list

## Usage

1. Install required packages: `pip install -r requirements.txt`
2. Open and run `notebooks/liwc_visualization.ipynb`

## Methodology

- Independent t-tests for group comparisons
- Holm's method for multiple comparison correction (α = 0.01)
- LIWC-22 reference corpus for contextual comparison
- Comprehensive statistical visualization using seaborn and matplotlib

## Data

The analysis uses Austrian parliamentary speech data with:
- LIWC-22 linguistic features
- Speaker metadata (party, role, demographics)
- Topic classifications
- Temporal information

---

*This project is part of a thesis on computational political discourse analysis.*
