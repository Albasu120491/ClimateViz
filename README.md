# 🌍 ClimateViz: A Benchmark for Statistical Reasoning and Fact Verification on Scientific Charts

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**ClimateViz** is the first large-scale benchmark for scientific fact-checking grounded in real-world, expert-curated climate charts. It challenges models to perform complex statistical reasoning over visual data, supporting structured explanation via knowledge graphs. The benchmark contains **49,862 claims** aligned with **2,896 scientific charts**, each annotated with a fact-checking label (`support`, `refute`, `not enough information`) and a structured explanation graph.

📄 If you use the ClimateViz dataset or benchmark in your research, please cite our paper:

> Su, R., Si, J., Guo, Z., & Pierrehumbert, J. (2025). *ClimateViz: A Benchmark for Statistical Reasoning and Fact Verification on Scientific Charts*. arXiv preprint [arXiv:2506.08700](https://arxiv.org/abs/2506.08700).


## 📌 Key Features

- **Real-World Climate Charts**: Sourced from institutions like NOAA, Met Office, and Copernicus.
- **Rich Claim Types**: Includes human-authored true claims and GPT-generated false and NEI (Not Enough Information) claims.
- **Structured Explanations**: Knowledge Graphs (KGs) of canonicalized (subject, relation, object) triplets.
- **High Annotation Quality**: Annotated via a Zooniverse campaign, verified by domain experts.
- **Multimodal Setup**: Supports both image-text and table-text reasoning tasks.

## 📊 Chart Sources

All charts included in the **ClimateViz** benchmark are sourced from publicly available, expert-curated scientific platforms. The dataset draws on high-quality climate visualizations from the following organizations:

- **🌐 NOAA (National Oceanic and Atmospheric Administration)**  
  [https://www.noaa.gov/](https://www.noaa.gov/)  
  Provides authoritative data on global and regional climate trends, including temperature anomalies, sea level, and CO₂.

- **🇬🇧 UK Met Office**  
  [https://www.metoffice.gov.uk/](https://www.metoffice.gov.uk/)  
  The UK’s national weather and climate service, offering historical climate records and projections.

- **🇪🇺 Copernicus Climate Change Service (C3S)**  
  [https://www.copernicus.eu/](https://www.copernicus.eu/)  
  Delivers open-access climate datasets, visual indicators, and reports as part of the European Union’s Earth observation program.

- **🛰️ NASA Earth Observatory**  
  [https://earthobservatory.nasa.gov/](https://earthobservatory.nasa.gov/)  
  Hosts satellite-based scientific visualizations and climate narratives covering cryosphere, ocean, and atmosphere data.

- **🌎 NOAA Climate.gov**  
  [https://www.climate.gov/](https://www.climate.gov/)  
  Educational and data-driven charts and maps used in public outreach and climate research.

- **🌡️ Climate Reanalyzer (University of Maine)**  
  [https://climatereanalyzer.org/](https://climatereanalyzer.org/)  
  Offers reanalysis-based climate visualizations including global weather anomalies and time series trends.

All charts were used under open-access conditions and manually verified by experts during dataset curation. No proprietary or sensitive content was included in the benchmark.


##  Dataset Overview

| Statistic               | Value         |
|------------------------|---------------|
| Supported claims       | 15,100        |
| Refuted claims         | 19,504        |
| NEI claims             | 15,258        |
| Total claims           | 49,862        |
| Avg. tokens per claim  | 19.0          |
| Avg. claims per chart  | 17.2          |

### Input Modalities

- **CT** (Chart + Text): Chart image + caption + claim
- **CTT** (Chart + Table + Text): Chart + DePlot-converted table + caption + claim

### Output Modes

- **Label-Only**: Predict `support`, `refute`, or `NEI`
- **Explanation-Augmented**: Generate knowledge graph triplets + label

## Tasks

1. **Claim Verification**: Does the claim match the chart data?
2. **Explanation Generation**: Generate structured (h, r, t) triplets to justify predictions.

## Reasoning Types Covered

- Temporal comparison, value extraction, anomaly detection
- Aggregation, spatial comparison, trend detection, uncertainty, and unit interpretation


## Baselines & Benchmarks

We evaluate:
- Open-source models: LLaMA-4, InternVL 2.5, Qwen 2.5
- Closed-source models: GPT-4o, Gemini 2.5, o3
- Chart-specific models: Matcha variants (ChartQA, PlotQA)

## Directory Structure

The `data/` folder contains the main dataset files for ClimateViz. It includes the full dataset as well as official training, development, and test splits. 
The `Code/` directory contains scripts for training, evaluation, and explanation generation over the ClimateViz dataset using state-of-the-art vision-language models.


```bash
Data/
├── ClimateViz.csv                # Full dataset with all claims and annotations
├── ClimateViz_train.csv          # Training split (70%)
├── ClimateViz_dev.csv            # Development/validation split (10%)
├── ClimateViz_test.csv           # Test split (20%)
├── annotated_reasoning.csv       # Manually labeled subset with reasoning types



Code/
├── matcha_finetune.py           # Fine-tune Matcha on ClimateViz fact-checking
├── zeroshot.py                  # Run zero-shot evaluation with multimodal LLMs
├── fewshot.py                   # Few-shot in-context prompting experiments
├── knowledge_graph.py           # Generate and canonicalize KG-based explanations
├── explanation_evaluation.py   # Evaluate generated triplets with BLEU, METEOR, etc.

