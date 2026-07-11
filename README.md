# Deep Learning 2026 — Colab-Ready Notebooks Collection

[![GitHub](https://img.shields.io/badge/GitHub-JamshaidBasit01-blue)](https://github.com/JamshaidBasit01)
[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-red)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-CC0%201.0-lightgrey)](deep-learning-2026/LICENSE)

A unified, **Google Colab-ready** collection of two major Deep Learning teaching repositories — reviewed, patched, and validated for seamless **Run All** execution.

| Collection | Source | Notebooks | Focus |
|------------|--------|-----------|-------|
| **Deep-Learning-Workshop-2026** | [MiRL-IITM](https://github.com/MiRL-IITM/Deep-Learning-Workshop-2026) | 19 | PyTorch → CNN → RNN → Seq2Seq (IITM Certificate Course) |
| **deep-learning-2026** | [NTU DL Bootcamp](https://github.com/ntu-dl-bootcamp/deep-learning-2026) | 20 | 5-session bootcamp: ML basics → PyTorch → Vision → NLP → RL |

**Total: 39 notebooks** | **All training & solution notebooks run end-to-end on Colab**

---

## Table of Contents

- [Quick Start](#quick-start)
- [Repository Structure](#repository-structure)
- [Workshop 2026 — Notebooks & Fixes](#workshop-2026--notebooks--fixes)
- [NTU Bootcamp 2026 — Notebooks & Fixes](#ntu-bootcamp-2026--notebooks--fixes)
- [Universal Fix Patterns](#universal-fix-patterns)
- [Colab Runtime Guide](#colab-runtime-guide)
- [Student vs Solution Notebooks](#student-vs-solution-notebooks)
- [Credits & Acknowledgments](#credits--acknowledgments)
- [Detailed Fix Logs](#detailed-fix-logs)

---

## Quick Start

### 1. Clone this repository

```bash
git clone https://github.com/JamshaidBasit01/Deep-Learning-Colab-Ready.git
cd Deep-Learning-Colab-Ready
```

### 2. Open in Google Colab

1. Go to [colab.research.google.com](https://colab.research.google.com/)
2. **File → Upload notebook** (or open from GitHub)
3. Navigate to the notebook you want in either folder
4. **Runtime → Change runtime type → GPU** (recommended for CNN, RNN, NLP, RL sessions)
5. **Runtime → Run all**

### 3. Install dependencies (optional — most notebooks self-install)

```bash
pip install -r deep-learning-2026/requirements-colab.txt
```

---

## Repository Structure

```
Deep-Learning-Colab-Ready/
│
├── README.md                          ← You are here
├── .gitignore
│
├── Deep-Learning-Workshop-2026/       ← IITM Workshop (MiRL-IITM)
│   ├── NOTEBOOK_FIXES.md              ← Detailed fix log for this collection
│   ├── README.md
│   ├── Pre-requisites/
│   │   ├── 00_python_programming.ipynb
│   │   ├── 01_self_test_solutions.md
│   │   └── 02_google_colab.md
│   ├── S0 - Pytorch/
│   │   ├── 01_pytorch_fundamentals.ipynb
│   │   ├── 02_pytorch_workflow.ipynb
│   │   ├── E1.ipynb / E1_Solution.ipynb
│   │   └── E2.ipynb / E2_Solution.ipynb
│   ├── S1 - CNN/
│   │   ├── 03_image_classification.ipynb
│   │   └── E3.ipynb / E3_Solution.ipynb
│   ├── S2 - RNN (Sequence Modelling)/
│   │   ├── 04_sequence_modelling.ipynb
│   │   ├── sales_dataset.csv
│   │   └── E4.ipynb / E4_Solution.ipynb
│   ├── S3 - RNN (Sentiment Analysis)/
│   │   ├── 05_sentiment_analysis.ipynb
│   │   ├── IMDB Dataset.csv
│   │   └── E5.ipynb / E5_Solution.ipynb
│   └── S4 - RNN (Encoder Decoder Models)/
│       ├── 06_encoder_decoder.ipynb
│       └── E6.ipynb / E6_Solution.ipynb
│
└── deep-learning-2026/                ← NTU Bootcamp
    ├── NOTEBOOK_FIXES_DOCUMENTATION.md ← Detailed fix log for this collection
    ├── requirements-colab.txt
    ├── README.md
    ├── LICENSE
    ├── SESSION1/  … SESSION5/
    └── (Jekyll website files, slides, datasets)
```

---

## Workshop 2026 — Notebooks & Fixes

> Full fix details: [`Deep-Learning-Workshop-2026/NOTEBOOK_FIXES.md`](Deep-Learning-Workshop-2026/NOTEBOOK_FIXES.md)

### Pre-requisites

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `00_python_programming.ipynb` | Python self-test: lists, functions, OOP, NumPy, Matplotlib | Intentional student stubs (`answer = 0`) | **No change** — stubs are by design; cells run without error |

### S0 — PyTorch Fundamentals

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `01_pytorch_fundamentals.ipynb` | Tensors, shapes, GPU, NumPy interop, common errors | `x.mean()` on int tensor crashes Run All; shape/dtype mismatch demos crash; hardcoded `cuda` fails on CPU | Wrapped intentional error demos in `try/except`; added `torch.cuda.is_available()` guards |
| `02_pytorch_workflow.ipynb` | End-to-end linear regression: train, predict, save/load | `!ls -l` Unix-only command fails on Windows | Replaced with `os.path.getsize()`; added `weights_only=True` on `torch.load` |
| `E1.ipynb` | Student exercise: 10 tensor/GPU questions | No Colab setup | Exercise stubs preserved (student work) |
| `E1_Solution.ipynb` | Complete E1 solutions | — | Fully runnable reference |
| `E2.ipynb` | Student exercise: linear regression pipeline | No Colab setup | Exercise stubs preserved |
| `E2_Solution.ipynb` | Complete E2 solutions | — | Fully runnable reference |

### S1 — Convolutional Neural Networks

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `03_image_classification.ipynb` | FashionMNIST: baseline → ReLU → CNN (TinyVGG) | `model_0` on CPU but `eval_model()` sends batches to GPU → **RuntimeError**; accuracy printed as `0.85%` instead of `85%` | `model_0.to("cpu")` + `device="cpu"` in eval; multiply accuracy by 100; quiet pip install |
| `E3.ipynb` | Student exercise: MNIST CNN, confusion matrix | Missing `torchmetrics`/`mlxtend` install | Exercise stubs preserved; install added in `E3_Solution.ipynb` |
| `E3_Solution.ipynb` | Complete E3 with `MNIST_model` CNN | — | Pip install + full implementation |

### S2 — RNN Sequence Modelling

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `04_sequence_modelling.ipynb` | Sales forecasting with RNN, LSTM, GRU | `pd.read_csv("sales_dataset.csv")` fails when Colab CWD is wrong; hidden states use global `device` | Added `setup_notebook_dir(['sales_dataset.csv'])`; changed `.to(device)` → `.to(x.device)` for `h0`/`c0` |
| `E4.ipynb` | Student exercise: reimplement sales pipeline | CSV path not resolved | Exercise stubs preserved; fix in `E4_Solution.ipynb` |
| `E4_Solution.ipynb` | Complete E4 solutions | — | `setup_notebook_dir` + full models |

**Dataset:** `sales_dataset.csv` — 222 rows, daily sales (2018)

### S3 — RNN Sentiment Analysis

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `05_sentiment_analysis.ipynb` | IMDB 50k reviews: RNN vs LSTM sentiment | CSV path fails on Colab; `display()` missing import; `torch.load` security warning in PyTorch 2.x | `setup_notebook_dir`; `from IPython.display import display`; `weights_only=True` |
| `E5.ipynb` | Student exercise: full IMDB pipeline | CSV path not resolved | Exercise stubs preserved; fix in `E5_Solution.ipynb` |
| `E5_Solution.ipynb` | Complete E5 solutions | — | Full pipeline with `SentimentRNN`, `SentimentLSTM` |

**Dataset:** `IMDB Dataset.csv` — 50,000 movie reviews (positive/negative)

### S4 — Encoder-Decoder (Seq2Seq)

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `06_encoder_decoder.ipynb` | Hindi→English Neural Machine Translation | Missing `datasets` package; text said "German→English"; `NUM_LAYERS=1` + `DROPOUT=0.4` ineffective; `num_workers=4` crashes Colab; downloads entire 1.6M dataset | `pip install datasets`; corrected markdown; `NUM_LAYERS=2`, `DROPOUT=0.1`; `num_workers=0`; **streaming** subset (10k train / 2k val) |
| `E6.ipynb` | Student exercise: build Encoder, Decoder, Seq2Seq | Missing `datasets` package | Exercise stubs preserved; fix in `E6_Solution.ipynb` |
| `E6_Solution.ipynb` | Complete E6 solutions | — | Full Seq2Seq with streaming load |

---

## NTU Bootcamp 2026 — Notebooks & Fixes

> Full fix details: [`deep-learning-2026/NOTEBOOK_FIXES_DOCUMENTATION.md`](deep-learning-2026/NOTEBOOK_FIXES_DOCUMENTATION.md)

### SESSION 1 — Deep Learning Essentials

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `session1_p1_student.ipynb` | Python, NumPy, Matplotlib, intro linear regression | `ipywidgets` not pre-installed; remote matplotlib style URL fails offline | `%pip install -q ipywidgets`; `seaborn-v0_8-whitegrid` fallback |
| `session1_p1_answers.ipynb` | Full p1 solutions | Same as student | Same fixes; **validated on Colab** |
| `session1_p2.ipynb` | Bias-variance, Decision Trees, Random Forest on California Housing | `input()` hangs on Colab "Run all" | `try/except EOFError` with defaults (`max_depth=5`) |
| `session1_p3_student.ipynb` | House price EDA + sklearn/PyTorch regression | `!rm` and `!wget` fail on Windows | Replaced with `urllib.request.urlretrieve()` |
| `session1_p3_answers.ipynb` | Full p3 solutions with PyTorch `nn.Linear` | Same wget issue | `urllib` download; **validated locally** |

**Dataset:** `home_data.csv` — King County house sales (~21,613 rows)

### SESSION 2 — PyTorch Regression & Classification

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `session2_part1.ipynb` | PyTorch tensors, GPU operations | None | No changes needed |
| `solutions/session2_part1.ipynb` | Part 1 exercise solutions | — | **Validated locally** |
| `session2_part2.ipynb` | MNIST classification, `NeuralNetwork`, save/load | Mini-challenge redefines `class NeuralNetwork`, **breaking entire pipeline** on Run All; `torch.load` security warning | Renamed to `ChallengeNeuralNetwork`; `weights_only=True` |
| `session2_part3.ipynb` | Student challenge: California Housing with PyTorch | `...` placeholders throughout | Intentional student exercise |
| `solutions/session2_part3.ipynb` | Complete housing challenge | Class typo `HousingNueralNetwork` | Renamed to `HousingNeuralNetwork`; **validated locally** |

### SESSION 3 — Deep Learning for Images

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `session3_part1_student.ipynb` | Convolutions, edge filters, coloured MNIST CNN | TODO conv layer placeholders | Intentional student exercise |
| `session3_part1_instructor.ipynb` | Complete LeNet on coloured MNIST | — | **Validated** (~98%+ MNIST accuracy) |
| `session3_part2_student.ipynb` | LeNet classification, U-Net segmentation, DDPM diffusion | Hardcoded `/content/` paths; Kaggle creds fragile; `medpy` missing `scikit-image`; shell unzip fails | `get_colab_base_dir()`; Colab `userdata` Kaggle secrets; Python `subprocess` + `zipfile` download |
| `session3_part2_instructor.ipynb` | Complete part 2 solutions | 8000+ lines of bloated outputs | Cleared embedded outputs; same infrastructure fixes |

> **SESSION3 Part 2 requires Kaggle API credentials** in Colab Secrets: `KAGGLE_USERNAME`, `KAGGLE_KEY`

### SESSION 4 — Natural Language Processing

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `Session4_part1.ipynb` | RNN, LSTM, Word2Vec, BERT, BBC text classification | `!wget` fails; wrong CSV filename; missing `nltk`/`pandas`; student `translator = ...` stub crashes next cell | `urllib.request` + Dropbox `dl=1`; added packages; demo lambda stub |
| `Session4_part2.ipynb` | TinyLlama prompt engineering, DistilBERT fine-tuning, RAG | Inconsistent pip install | Standardized `%pip install -q` |
| `BERT_for_Polymer_Informatics_...ipynb` | polyBERT embeddings, RDKit, polymer SMILES | Colab badge pointed to 2025 repo; `rdkit-pypi` fails on some Python versions | Updated badge to 2026; `rdkit` fallback |

### SESSION 5 — Reinforcement Learning

| Notebook | What It Covers | Original Issues | Fixes Applied |
|----------|----------------|-----------------|---------------|
| `session5_grid.ipynb` | GridWorld 5×5 with DQN and PPO (easy) | Missing `shimmy>=2.0` for gymnasium + SB3 | Consolidated `%pip install` with shimmy |
| `session5a_grid_solution.ipynb` | Complete DQN + PPO solution | **Wrong Colab badge** (linked to SESSION1); bloated plot outputs (>5 MB) | Fixed badge URL; cleared outputs; merged pip cells |
| `session5b_flappy_bird_studentversion.ipynb` | Custom Flappy Bird env + DQN (hard) | Missing pygame/imageio/ipywidgets; manual Google Drive sprite upload; hardcoded `/content/sprites.zip` | Added packages; auto-download via `gdown`; dynamic `BASE_DIR` + `zipfile` |

---

## Universal Fix Patterns

These patterns were applied across both collections to ensure Colab compatibility:

| Pattern | Purpose | Used In |
|---------|---------|---------|
| `setup_notebook_dir(['file.csv'])` | Auto-find correct working directory after git clone | Workshop S2, S3 |
| `device = "cuda" if torch.cuda.is_available() else "cpu"` | Device-agnostic code | Both collections |
| `.to(x.device)` instead of `.to(device)` | Hidden states follow input tensor device | Workshop S2 |
| `try/except` on intentional error demos | Run All completes without crashing | Workshop S0 |
| `urllib.request.urlretrieve()` | Cross-platform file downloads | Bootcamp S1, S4 |
| `weights_only=True` in `torch.load()` | PyTorch 2.4+ security compliance | Both collections |
| `%pip install -q ...` | Quiet, Colab-safe package installs | Both collections |
| `get_colab_base_dir()` / `get_base_dir()` | Dynamic `/content` vs local path | Bootcamp S3, S5 |
| Streaming HuggingFace datasets | Avoid downloading full 1.6M-row dataset | Workshop S4 |
| `try/except EOFError` on `input()` | Non-interactive Run All with defaults | Bootcamp S1 |

---

## Colab Runtime Guide

| Collection / Session | Recommended Runtime | Notes |
|----------------------|---------------------|-------|
| Workshop — Pre-requisites, S0 | CPU or GPU | Either works |
| Workshop — S1 CNN | **GPU** | FashionMNIST training slow on CPU |
| Workshop — S2 Sequence | **GPU** | Faster epoch loops |
| Workshop — S3 Sentiment | **GPU** | 50k reviews |
| Workshop — S4 Seq2Seq | **GPU** | Seq2Seq training |
| Bootcamp — SESSION 1 | CPU | sklearn / basic PyTorch |
| Bootcamp — SESSION 2 | GPU (optional) | MNIST faster on GPU |
| Bootcamp — SESSION 3 | **GPU** | CNN training + Kaggle data |
| Bootcamp — SESSION 4 | **GPU** | TinyLlama needs ~6 GB RAM |
| Bootcamp — SESSION 5 | **GPU** | DQN/PPO training |

### Quick Validation Checklist

- [ ] Workshop: `03_image_classification.ipynb` → Run all → 3 models train, ~86% CNN accuracy
- [ ] Workshop: `05_sentiment_analysis.ipynb` → Run all → RNN + LSTM train on IMDB
- [ ] Workshop: `06_encoder_decoder.ipynb` → Run all → Hindi→English translation works
- [ ] Bootcamp: `session1_p3_answers.ipynb` → Run all → PyTorch model trains
- [ ] Bootcamp: `solutions/session2_part3.ipynb` → Run all → 5-epoch housing training
- [ ] Bootcamp: `session3_part1_instructor.ipynb` → Run all → ~98% MNIST accuracy
- [ ] Bootcamp: `session5a_grid_solution.ipynb` → Run all → DQN + PPO reward plots

---

## Student vs Solution Notebooks

Both collections follow a **learn → practice → verify** pattern:

| Type | Naming | Runnable? | Purpose |
|------|--------|-----------|---------|
| **Training / Demo** | `01_...`, `03_...`, `session2_part2.ipynb` | ✅ Yes | Instructor-led demonstrations |
| **Student Exercise** | `E*.ipynb`, `*_student.ipynb`, `session2_part3.ipynb` | ⚠️ Partial | `# Your code here`, `NotImplementedError`, `TODO` stubs |
| **Solution / Instructor** | `*_Solution.ipynb`, `*_answers.ipynb`, `*_instructor.ipynb` | ✅ Yes | Complete reference implementations |

> Student exercise stubs are **intentionally incomplete** — students must fill them in. Use the corresponding solution notebook to verify your answers.

---

## Credits & Acknowledgments

### Original Repositories

| Collection | Institution | Repository |
|------------|-------------|------------|
| Deep Learning Workshop 2026 | IITM — MiRL Lab | [MiRL-IITM/Deep-Learning-Workshop-2026](https://github.com/MiRL-IITM/Deep-Learning-Workshop-2026) |
| Deep Learning Bootcamp 2026 | NTU Singapore | [ntu-dl-bootcamp/deep-learning-2026](https://github.com/ntu-dl-bootcamp/deep-learning-2026) |

### Workshop References

- Bourke, D. (2024). [Learn PyTorch for Deep Learning](https://www.learnpytorch.io/) — PyTorch fundamentals & workflow
- Wang, Z. J. et al. (2020). [CNN Explainer](https://poloclub.github.io/cnn-explainer/) — Interactive CNN visualization

### This Collection

- **Maintained by:** [JamshaidBasit01](https://github.com/JamshaidBasit01)
- **Work:** Colab compatibility review, bug fixes, validation, unified documentation
- **License:** CC0 1.0 (from NTU Bootcamp); original workshop materials retain their respective licenses

---

## Detailed Fix Logs

For exhaustive per-cell fix documentation, see the dedicated logs inside each folder:

| File | Covers |
|------|--------|
| [`Deep-Learning-Workshop-2026/NOTEBOOK_FIXES.md`](Deep-Learning-Workshop-2026/NOTEBOOK_FIXES.md) | All 13 Workshop training + exercise notebooks |
| [`deep-learning-2026/NOTEBOOK_FIXES_DOCUMENTATION.md`](deep-learning-2026/NOTEBOOK_FIXES_DOCUMENTATION.md) | All 20 Bootcamp notebooks |

---

<p align="center">
  <strong>39 notebooks · 2 collections · 1 repo · 0 broken Run Alls</strong><br>
  <sub>Last updated: July 2026</sub>
</p>
