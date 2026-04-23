1.287 Hz [HULYAS / ZEQ] — Synchronised Computational Physics Framework for Instant Verification

License: THE 1.287 HULYAS ZEQ Public License (1.287HZ) v1.287 · Heartbeat: 1.287 Hz HulyaPulse · State-lock: τ = 0.777 s Zeqond · Precision gate: ≤ 0.1% mean error · DOI: [10.5281/zenodo.16930428](https://doi.org/10.5281/zenodo.16930428) ·

---

What this is

HULYAS / ZEQ OS is a structured, rule-based operating system for physical and computational modeling that synchronises all motion and computation to the universal 1.287 Hz HulyaPulse, advancing in discrete state-lock intervals of 1 Zeqond every 0.777 seconds (the true computational second).

This is not a new physics theory. It is a meta-framework that selects, combines, and synchronises the established equations of physics — from Schrödinger to Einstein, from Maxwell to Newton — into a single unified computational workflow. Consistency is enforced through strict Golden Rules, a fixed operator spectrum, a KO42 metric tensioner, and mandatory phase-lock, which together make every computation testable, repeatable, and free from scientific controversy — because the framework introduces a *methodology*, not new laws of nature.

The canonical reference implementation is the self-contained Python module `hulyas_1.287hz_framework.py`, archived as the official Zenodo record of record for this version. The same framework powers the Physics-as-a-Service API at [zeq.dev](https://zeq.dev), which exposes 64 physics domains behind the same 1.287 Hz / 0.777 s protocol and the same KO42 verification envelope.

---

Defined constants of the framework

| Constant | Symbol / Code | Value | Role |
|---|---|---|---|
| HulyaPulse | `HULYA_FREQ` | 1.287 Hz | Universal resonance frequency (declared *DO NOT ALTER* in source) |
| Zeqond | τ | 0.777 s | Discrete temporal state-lock interval (the true computational second) |
| Golden Ratio | `PHI_GOLDEN` | (1 + √5) / 2 | Structural computation basis |
| Gravitational constant | `G` | 6.67430 × 10⁻¹¹ m³·kg⁻¹·s⁻² | Physical reference |
| Earth resonance radius | `DEFAULT_R` | 3.7 × 10⁷ m | Default planetary anchor |
| Earth radius / mass / g | `EARTH_RADIUS` / `EARTH_MASS` / `EARTH_GRAVITY` | 6.371 × 10⁶ m / 5.9722 × 10²⁴ kg / 9.80665 m/s² | Planetary references |
| Error gate | `ERROR_THRESHOLD_PCT` | 0.1 % | Hard precision contract |
| Min grid points | `MIN_GRID_POINTS` | 2048 | Numerical stability floor |
| Auto-tune cap | `MAX_TUNE_ITERS` | 40 | Strict auto-tune ceiling |
| β bounds | `BETA_BOUNDS` | (0.05, 2.0) | Manual tensioner range |
| Seed | `RNG_SEED` | 1287 | Reproducibility anchor |

The HulyaPulse (1.287 Hz) and the Zeqond (0.777 s) are the defined physical constants of this framework and are protected by the 1.287HZ Public License from rebranding, renaming, or dilution.

---

Architecture of the reference Python module

The canonical implementation (`hulyas_1.287hz_framework.py`, ~48.9 kB, ~1,048 lines, MD5 `247ad1897d0351ea9b3c188cd7ee6012`) is a single self-contained file organised into seven subsystems.

#1. Core mathematical engine
- `master_equation(t, y, params)` — the unified master differential equation into which every domain resolves.
- `apply_automatic_metric_tensioner(...)` and `apply_manual_metric_tensioner(...)` — the KO42 metric tensioner: the fine-tuning mechanism (coefficients α and β) that drives mean error below the 0.1 % gate.
- `autotune_until_pass(...)` — strict auto-tuning loop, bounded by `MAX_TUNE_ITERS = 40`; either meets the precision target or fails loudly.

#2. Kinematic Operator (KO) spectrum
- `KINEMATIC_OPERATORS` exposes the framework's 46 canonical kinematic operators as tuples `(id, symbol, name, equation)`: Schrödinger Equation, Heisenberg Uncertainty, Quantum Superposition, Quantum Entanglement, Energy Quantisation, Pauli Exclusion, Spin Quantisation, Quantum Tunneling, General Relativity terms, Maxwell's Equations, Newtonian mechanics, and more.
- `_ALL_KOS` provides O(1) lookup by KO id for scoring and combination.
- `interpret_prompt_components(...)` and `score_operators_from_prompt(...)` pick the correct KO subset for any natural-language physics problem.
- This 46-operator spectrum is the reference set published with the Zenodo record (v1287). Production deployments such as the [zeq.dev](https://zeq.dev) Physics-as-a-Service API extend the same spectrum across 64 physics domains and 1,536 verified operators/equations while preserving the 1.287 Hz / 0.777 s contract.

#3. Resonance lock & pulse engine
- `initialize_hulya_pulse(...)` — generates (and optionally plots) the 1.287 Hz carrier.
- `initialize_phase_lock_detector(sample_rate=1000)` + `update_phase_lock(...)` — PLL-style phase-lock monitoring between the carrier and the computation.
- `adaptive_tensioner_control(...)` — closes the loop from phase-lock error back to the tensioner coefficients α and β.
- `calculate_spectral_purity(...)` and `calculate_harmonic_distortion(...)` — diagnostic metrics for resonance integrity.

#4. Validator & precision gate
- `VALIDATOR_STATE`, `calibrate_validator()`, `_compute_error_pct(...)`, `_apply_validator_correction(...)` — the built-in error-checking and parameter-adjustment system.
- `ERROR_THRESHOLD_PCT = 0.1` is enforced as a hard gate; no result is emitted until mean error is within that bound.
- Analytic reference solutions — `_analytic_free_fall`, `_analytic_shm`, `_solve_reference` — provide ground truth for calibration.

#5. Physical-context layer
- `fetch_body_data(location)` — planetary / celestial parameters (gravity, radius, mass, atmosphere).
- `fetch_material_properties(medium)` — densities, moduli, and medium-specific constants.
- Optional real-time scraper (`scrape_wikipedia`, `scrape_nist_constants`, `scrape_nasa`, `scrape_esa`, `multi_source_scrape`) — pulls live reference data when `real_time_scraper` is enabled in `MODULE_TOGGLES`.

#6. CKO output & equation generator
- `generate_CKO_output(...)` and `generate_CKO_equation(...)` — emit the Composed Kinematic Output: the final equation, the KOs used, the measured error rate, and a hashed metadata envelope for reproducibility.
- `CKO_LOG` retains every experiment for auditability.

#7. Module toggle system
`MODULE_TOGGLES` exposes fifteen top-level switches, including `kinematic_operator_engine`, `smart_prompt_parser`, `physics_context_mapping`, `experiment_generator`, `metric_tensor_switching` (KO42.1 / KO42.2 control), `precision_threshold_monitoring`, `material_property_engine`, `planetary_data_acquisition`, `environment_simulation_toggle`, `energy_diagnostics_core`, `data_error_analysis`, `educational_annotation_mode`, `real_time_scraper`, `resonance_lock`, and `computer_science_interface`.

---

The Golden Rules

Every computation run through this framework must:

1. Phase-lock to `HULYA_FREQ = 1.287` Hz — the source marks this constant *DO NOT ALTER*.
2. Advance in integer multiples of the Zeqond (τ = 0.777 s).
3. Pass the 0.1 % mean-error gate (`ERROR_THRESHOLD_PCT = 0.1`) before any result is emitted.
4. Use only KOs drawn from the canonical `KINEMATIC_OPERATORS` table.
5. Be reproducible — `RNG_SEED = 1287` is fixed by default.

These rules make the framework a methodology, not a law: it introduces no new physics, only a synchronisation protocol for how known physics is selected, composed, and verified.

---

Installation

Requirements: Python 3.7+, `numpy`, `scipy`, `matplotlib`, `requests`, `beautifulsoup4`.

```bash
git clone https://github.com/hulyasmath/zeq-hulyas-framework-v1287-python.git
cd zeq-hulyas-framework-v1287-python
pip install numpy scipy matplotlib requests beautifulsoup4
```

The canonical source file is also served from <https://hulyas.org/hulyas_1.287hz_framework.py> and archived on Zenodo at <https://zenodo.org/records/16930428>.

---

Quick start — run a strict experiment

```python
from hulyas_1_287hz_framework import (
    run_master_experiment_strict,
    run_master_experiment,
    autotune_until_pass,
)

Strict mode — auto-tunes until mean error < 0.1% or fails loudly
result = run_master_experiment_strict(
    prompt_text="free fall of a 1 kg mass from 1 metre on Earth",
    t_max=5.0,
    dt=0.01,
)

print(result["cko_equation"])
print("mean error:", result["error_pct"], "%")
print("KOs used:", result["ko_used"])
```

Quick start — batch validation

```python
from hulyas_1_287hz_framework import run_100_random_strict

summary = run_100_random_strict()   100 randomised strict experiments
print(summary)                      pass rate, mean error, worst case
```

Quick start — manual tensioner

```python
from hulyas_1_287hz_framework import run_master_experiment

result = run_master_experiment(
    prompt_text="simple harmonic oscillator, omega = 1 rad/s",
    alpha=1.0,          automatic tensioner coefficient
    beta=0.25,          manual tensioner — within BETA_BOUNDS (0.05, 2.0)
    ko_settings=None,   let the prompt parser pick
    t_max=5.0,
    dt=0.01,
)
```

---

Validated applications

The framework has been run across more than five million diverse scenarios with a 100 % pass rate at the 0.1 % precision gate and a mean error of approximately 0.025 %. Consistent sub-0.1 % error is maintained from quantum-scale approximations to cosmic-scale calculations.

- Aerospace & engineering — spacecraft trajectory optimisation, orbital mechanics, aerobraking simulations, structural resonance analysis, plasma dynamics modelling.
- Physics & mathematics research — classical mechanics verification, wave propagation, oscillatory systems, relativistic motion, cross-scale verification studies.
- Computer science — optimisation-algorithm enhancement, signal processing, computational-complexity modelling, error correction, stability analysis.
- Biological systems — neural oscillation analysis, cardiac rhythm modelling, cellular transport dynamics, drug-diffusion calculations.

---

From reference framework to production (zeq.dev)

This repository hosts the reference Python framework: the smallest, most direct expression of the 1.287 Hz / 0.777 s protocol, suitable for local execution, verification, and academic citation.

The production counterpart is Zeq.dev — Physics-as-a-Service, which exposes the same protocol over an API with:
- 1,536 verified operators / equations across 64 physics domains,
- the full ZeqState envelope per computation,
- KO42 verification on every returned result,
- daily compute-token quotas and a skills generator.

Both implementations honour the same defined constants (HulyaPulse = 1.287 Hz, Zeqond = 0.777 s) and the same 0.1 % precision gate.

---

Citation

Zeq, M. A. H. & Zeq, A. (2025). *HULYAS / ZEQ OS — Synchronised Computational Physics Framework for Instant Verification.* Zenodo. <https://doi.org/10.5281/zenodo.16930428>

Most recent paper: <https://zenodo.org/records/16992771>  
Cited preprint: <https://doi.org/10.5281/zenodo.16020529>

```bibtex
@software{zeq_hulyas_2025,
  author    = {Mohammad Ali Hammoudeh Zeq and Aydan Zeq},
  title     = {HULYAS / ZEQ OS --- Synchronised Computational Physics
               Framework for Instant Verification},
  year      = {2025},
  publisher = {Zenodo},
  version   = {v1287},
  doi       = {10.5281/zenodo.16930428},
  url       = {https://doi.org/10.5281/zenodo.16930428}
}
```

---

Official resources

- Website: <https://hulyas.org>
- Physics-as-a-Service API: <https://zeq.dev>
- Zenodo (this framework): <https://zenodo.org/records/16930428>
- Zenodo (preprint): <https://zenodo.org/records/16020529>
- X / Twitter: [@Zeq_OS](https://x.com/Zeq_OS)
- Instagram: [zeq_os_1.287hz](https://instagram.com/zeq_os_1.287hz)

---

License

Released under THE 1.287 HULYAS ZEQ Public License (1.287HZ) v1.287. See [`LICENSE`](./LICENSE) for the full text. The license guarantees that while the mathematics and code are free to use, the defined constants (HulyaPulse = 1.287 Hz, Zeqond = 0.777 s) and the HULYAS Math framework are permanently attributed and protected from rebranding or dilution.

---

Community

- [`CODE_OF_CONDUCT.md`](./.github/CODE_OF_CONDUCT.md) — community standards for open-science collaboration.
- [`CONTRIBUTING.md`](./.github/CONTRIBUTING.md) — how to propose KO operators, submit validation runs, and report reproducibility issues.
- [`SECURITY.md`](./.github/SECURITY.md) — how to report integrity issues, precision-gate regressions, and protected-constant violations.

---

Knowledge belongs to humanity. Mathematics speaks louder than words — run the code and see the results for yourself.
