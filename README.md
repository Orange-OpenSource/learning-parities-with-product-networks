# Learning High-Dimensional Parity Functions with Product Networks

**Guillaume Larue · Louis-Adrien Dufrène · Quentin Lampin · Hadi Ghauch · Ghaya Rekaya**

This repository contains the complete source code to reproduce the experimental results reported in the paper [Learning High-Dimensional Parity Functions with Product Networks using Gradient Descent](https://arxiv.org/abs/2605.28612) accepted at ICML 2026.

---

## Abstract

Parity functions are fundamental Boolean operations with critical applications across machine learning, cryptography, and error correction.
Yet, learning high-dimensional parity functions poses significant challenges: in a general setting, standard neural network architectures typically require exponential sample complexity, making gradient-based optimization intractable for large number of inputs $N$.
We demonstrate that compact product-based neural architectures combined with stochastic data sparsity (Bernoulli inputs with $p_e \leq 1/N$) and appropriate hyperparameter choice enable efficient parity learning, with theoretical guarantees of convergence.
Experiments validate our theory across dimensions up to $N = 100{,}000$, with empirical evidence showing optimal hyperparameter choices for $p_e$ and learning rate $\alpha$, as well as polynomial complexity scaling laws.
This work establishes fundamental connections between architectural inductive bias and data sparsity, opening new possibilities for neural arithmetic, structured reasoning, binary neural networks, and machine learning applied to automated protocol discovery.

**Keywords:** Parity Learning, Product Neural Networks, Data Sparsity, Boolean Functions, Sample Complexity

---

## Citation

```bibtex
@article{larue2025parity,
  title   = {{L}earning {H}igh-{D}imensional {P}arity {F}unctions with {P}roduct {N}etworks using {G}radient {D}escent},
  author  = {Larue, Guillaume and Dufrène, Louis-Adrien and Lampin, Quentin and Ghauch, Hadi and Rekaya, Ghaya},
  year    = {2026},
  url={https://arxiv.org/abs/2605.28612}
}
```

---

## Installation

Requires **Python 3.12**.

```bash
git clone https://github.com/Orange-OpenSource/learning-parities-with-product-networks.git
cd learning-parities-with-product-networks
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## Reproducing the results

Each study in the paper corresponds to a script in `studies/` and a visualisation notebook in `notebooks/`.
Pre-computed results are stored under `studies/results/` and loaded automatically by the notebooks.

### Run a single study

```bash
python studies/run_study_A.py   # replace A with any label below
```

### Run all studies

```bash
python studies/run_all_studies.py
```

Running all studies takes around 8h to run on 3 NVidia L40S GPUs. To speed up the simulations one can reduce the maximum number of steps, experiments granularity, number of parallel nodes, etc. depending on their needs.

### Study overview

| Study | Script | Description |
|-------|--------|-------------|
| **A** | `run_study_A.py` | Impact of $p_e$ on convergence — sweeps $p_e \in [0.001,\, 0.1]$ for $N=100$ |
| **B** | `run_study_B.py` | Optimal $p_e^*$ vs $N$ — locates the best $p_e$ for each $N \in [10, 1000]$ |
| **C** | `run_study_C.py` | Impact of $\alpha$ — sweeps $\alpha \in [0.01, 100]$ for $N=100$ |
| **D** | `run_study_D.py` | Optimal $\alpha^*$ vs $N$ — locates the best $\alpha$ for each $N \in [10, 1000]$ |
| **E** | `run_study_E.py` | Impact of $p_e$ under large batch — reproduces Study A at higher batch size |
| **F** | `run_study_F.py` | Weight distribution dynamics — records weight statistics throughout training |
| **G** | `run_study_G.py` | Joint $\alpha / p_e$ / batch sweep — maps convergence across all three hyperparameters |
| **H** | `run_study_H.py` | Comparison of generalisation capabilities of the product node vs std. MLP |

Companion Jupyter notebooks (`notebooks/plot_study_*.ipynb`) load the saved results and reproduce every figure from the paper.

---

## Project structure

```
models/       – XOR node and product network definitions
training/     – training loop and SGD utilities
plotting/     – shared plotting helpers
studies/      – experiment scripts (run_study_A.py … run_study_H.py)
  results/    – pre-computed .npy result arrays
notebooks/    – figure notebooks (plot_study_A.ipynb … plot_study_H.ipynb)
docs/         – Sphinx documentation sources
```

---

## Documentation

Full API reference, study descriptions, and interactive figure notebooks are available in the [online documentation](https://orange-opensource.github.io/learning-parities-with-product-networks/).
Build it locally with:

```bash
sudo apt-get install -y pandoc 
cd docs
make html
cd _build/html && python -m http.server
```

---

## License

See [LICENSE](https://opensource.org/licenses/MIT) for details.
