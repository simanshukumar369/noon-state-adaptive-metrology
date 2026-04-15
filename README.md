# Quantum-Enhanced Single-Parameter Phase Estimation with Adaptive NOON States

**Authors:** Simanshu Kumar¹,² and Nandan S. Bisht¹  

**Affiliations:**  
¹ Department of Physics, DSB Campus, Kumaun University, Nainital, Uttarakhand, India – 263001  
² Applied Optics & Spectroscopy Laboratory, Department of Physics, SSJ University Campus, Almora, Uttarakhand, India – 263601  

**Corresponding authors:**  
bisht.nandan@gmail.com  
simanshukumar@gmail.com
---

## Overview

This repository contains all simulation codes for the paper:

> *Quantum-Enhanced Single-Parameter Phase Estimation with Adaptive NOON States*  
> Simanshu Kumar and Nandan S Bisht  
**Preprint:** [arXiv:2604.12323](https://arxiv.org/abs/2604.12323) [quant-ph]

We present an end-to-end differentiable photonic circuit that learns optimal
parameters for NOON-state generation by maximising the classical Fisher
information (CFI) across coincidence channels for N = 2, 3, 4, 5.

**Key results:**
- Raw CFI improvements: +153% (N=2) to +1775% (N=5)
- Post-selection rates: 1.5× to 33× improvement
- Probe quality: 82% of Heisenberg limit at N=2, 58% at N=5
- Useful measurement events per pulse: 8× to 133× improvement

---

## Repository Contents

- `noon-qfi.pdf` — Full preprint (25 pages)
- `noon-main.ipynb` — Complete Jupyter notebook containing:
  - All forward-model validation
  - Gradient-flow checks
  - Full Adam optimisation (N=2,3,4,5)
  - QFI & measurement-efficiency calculations
  - Figure generation (`fig_qfi.pdf/png`, fringe gallery, Wigner functions)
  - `requirements.txt` — pip dependencies
  - environment.yml -- conda environment (optional)
 ---

## Installation

### Option 1: pip (recommended – fastest)

```bash
conda create -n noon-sim python=3.10
conda activate noon-sim
pip install -r requirements.txt

### Verify installation
```bash
python -c "import strawberryfields; import tensorflow; print('OK')"
```
---

## Output files

After running `python run_all.py`, the following files are created:

| File | Description |
|------|-------------|
| `all_results.pkl` | Trained circuit parameters and training history |
| `qfi_results.pkl` | QFI and measurement efficiency for all N |
| `fig1_circuit.pdf` | Circuit schematic (Fig. 1) | However in main text we use Latex quantikz circuit |
| `fig2_fringe_gallery.pdf` | Fringe gallery Afek vs Opt (Fig. 3) |
| `fig3_scaling_summary.pdf` | Scaling of improvements with N (Fig. 9) |
| `fig4_pareto.pdf` | Pareto trade-off plot (Fig. 4) |
| `fig5_convergence.pdf` | Training convergence (Fig. 10) |
| `fig6_param_drift.pdf` | Parameter drift from Afek init (Fig. 11) |
| `fig7_photon_dist.pdf` | Photon-number distributions (Fig. 12) |
| `fig8_fim_bars.pdf` | Raw CFI bar chart (Fig. 2) |
| `figW1_gallery.pdf` | Wigner function gallery (Fig. 5) |
| `figW2_negativity.pdf` | Wigner negativity comparison (Fig. 6) |
| `figW3_portrait.pdf` | Phase-space portrait N=2 (Fig. 7) |
| `figW4_evolution.pdf` | State evolution through circuit (Fig. 8) |
| `fig_qfi.pdf` | QFI analysis figure (Fig. 13) |

---

## Hardware and timing

Tested on:
- Intel Core i5 13th Gen
- NVIDIA GeForce RTX 3050 (6 GB VRAM)
- 16 GB RAM, Arch Linux

Typical runtimes:

| Step | Time |
|------|------|
| Training (all N, 100 steps) | ~15–20 min |
| Wigner figures | ~3 min |
| QFI calculation (all N) | ~10–15 min |
| All figures | ~5 min |
| **Total** | **~35 min** |

---

## Circuit architecture

```
Mode 0: |α⟩ → R(d_c) ─┐
                        ├─ BS(θ₁,φ₁) → R(φ_est) → BS(θ₂,φ₂) → N₁
Mode 1: |r⟩ → R(d_s) ─┘                                     → N₂
```s

**8 trainable parameters:** r, log γ, d_c, d_s, θ₁, φ₁, θ₂, φ₂  
**Fixed:** φ_est (scanned to produce coincidence fringes)  
**Detection:** coincidence patterns (N₁, N₂) with N₁+N₂ = N

---

## Citation

If you use this code or the paper, please cite:

```bibtex
@article{kumar2026adaptive,
  title   = {Quantum-Enhanced Single-Parameter Phase Estimation 
             with Adaptive NOON States},
  author  = {Kumar, Simanshu and Bisht, Nandan S},
  journal = {Preprint},
  year    = {2026},
  note    = {arXiv:2604.12323 [quant-ph]}
}
```

---

## Licence

MIT Licence — see `LICENSE` file.

---

## Acknowledgements

Simulations use [Strawberry Fields](https://strawberryfields.ai) by
Xanadu Quantum Technologies and [TensorFlow](https://tensorflow.org).
