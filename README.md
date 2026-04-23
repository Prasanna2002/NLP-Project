# 🧬 Clinical Biomarker Extraction & Negation Analysis

An automated pipeline for extracting clinical biomarkers, therapy combinations, and clinical metadata from National Cancer Institute (NCI) drug labels. This project utilizes specialized Biomedical NLP models and Deep Learning to transform unstructured medical text into structured data.

## 🚀 Overview

This repository implements a 4-stage pipeline designed to scale medical data extraction while maintaining high linguistic precision. It specifically addresses the challenge of **Negation** (e.g., distinguishing between "indicated for" vs "not indicated for") in oncology drug labeling.

### 🏗️ The 4-Stage Pipeline

1.  **Stage 1: Data Acquisition**
    * Crawls the NCI Drug Dictionary.
    * Extracts drug names, NDC codes, and raw clinical descriptions.
    * Generates a structured "skeleton" dataset.

2.  **Stage 2: Biological NER**
    * Uses **scispaCy** (`en_ner_bionlp13cg_md`) to identify biological entities.
    * Extracts Genes, Proteins, and Cancer types.
    * Implements GPU acceleration for high-throughput processing.

3.  **Stage 3: Deep Linguistic Analysis**
    * **Hybrid Classification:** Uses Dependency Parsing and Proximity analysis to identify binary clinical flags (Metastatic, First-line, Accelerated Approval).
    * **Negation Modeling:** Integrates **NegBERT** (Cue & Scope models) to verify the context of identified biomarkers.
    * **Dependency Parsing:** Extracts complex therapy combinations via subtree analysis.

4.  **Stage 4: Sanitization & Export**
    * Performs data cleaning, deduplication, and re-indexing.
    * Exports the final clinical report as a structured CSV.

## 🛠️ Technical Stack

* **Language:** Python 3.12+
* **Data Handling:** Pandas, NumPy
* **Utilities:** BeautifulSoup4, Requests, tqdm, PyTorch

## 📦 Installation & Setup

```bash
# Install core dependencies
pip install spacy==3.7.2 scispacy==0.5.4
pip install pandas requests beautifulsoup4 tqdm torch

# Install specialized scispaCy model
pip install [https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.1/en_ner_bionlp13cg_md-0.5.1.tar.gz](https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.1/en_ner_bionlp13cg_md-0.5.1.tar.gz)
