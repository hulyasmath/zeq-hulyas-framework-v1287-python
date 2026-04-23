# Contributing to HULYAS / ZEQ OS

Thank you for your interest in contributing to the **HULYAS / ZEQ OS — Synchronised Computational Physics Framework for Instant Verification** (Zenodo DOI [10.5281/zenodo.16930428](https://doi.org/10.5281/zenodo.16930428)).

This repository is the reference Python implementation of the 1.287 Hz / 0.777 s protocol. Contributions are welcomed, and the primary currency of contribution is **independently-verified, reproducible results**.

Please read the [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md) before participating.

---

## What contributions we welcome

1. **Reproducibility runs** — run the strict validation suite (`run_100_random_strict`) on your own hardware and publish the numbers, with your Python version, OS, and package versions. Open an Issue with the tag `reproducibility` and attach the `CKO_LOG` output.
2. **New Kinematic Operator (KO) proposals** — proposals to extend the canonical `KINEMATIC_OPERATORS` table. A proposal must include: a formal name and citation of the underlying established physics, the LaTeX equation, a proposed KO id and symbol, and at least one reference experiment that passes the 0.1 % precision gate with the proposed operator included.
3. **Bug reports** — deterministic regressions, numerical instabilities, failures of the auto-tune loop (`autotune_until_pass`) to converge within `MAX_TUNE_ITERS`, scraper breakages, or any behaviour that contradicts the Golden Rules listed in the README.
4. **Documentation** — worked examples, clarifications of the architecture, corrections to the README, BibTeX and citation improvements, translations.
5. **Performance improvements** — faster solvers, better vectorisation, memory reductions — provided they preserve bit-stable, Golden-Rule-compliant behaviour under `RNG_SEED = 1287`.
6. **New worked examples** in the style of the quick-start snippets: orbital mechanics, signal processing, biological modelling, plasma dynamics, three-body problem, etc.

---

## What contributions we do NOT accept

The framework's integrity depends on a small number of hard constraints. The following PRs will be closed on sight:

- Changes to the **protected constants**: `HULYA_FREQ = 1.287`, the 0.777 s Zeqond interval, or any attempt to rename or abstract them away. These are defined by the 1.287HZ License.
- Relaxation of the **0.1 % precision gate** (`ERROR_THRESHOLD_PCT`). The gate may be probed or instrumented, but never silently softened.
- Silent bypasses of the validator (`VALIDATOR_STATE`, `_apply_validator_correction`).
- Removal of reproducibility anchors (`RNG_SEED = 1287`).
- Contributions whose only demonstrated effect is to "make the framework look like" something it is not — e.g. to dress it up as a new physics theory, or to strip out the HULYAS/ZEQ naming to rebrand it.
- Plagiarism, fabricated results, or uncited reuse of third-party code.

If in doubt, open a **Discussion** or an **Issue** before writing code.

---

## Development workflow

1. **Fork** this repository to your own account.
2. **Create a branch** from `main` named after your change (e.g. `feature/ko47-fluid-continuity`, `fix/autotune-convergence`, `docs/quickstart-three-body`).
3. **Keep changes focused.** One logical change per PR. Large refactors should be split.
4. **Run the strict suite locally** before opening a PR:
    ```python
    from hulyas_1_287hz_framework import run_100_random_strict
    print(run_100_random_strict())
    ```
    Your PR description must include the pass rate, mean error, and worst case.
5. **Open a Pull Request** against `main`. Fill in the template: what changed, why, which KOs/modules are affected, reproducibility numbers, and any relevant citations.

---

## Coding standards

- **Language:** Python 3.7+. Keep the reference module self-contained; do not introduce heavy dependencies beyond `numpy`, `scipy`, `matplotlib`, `requests`, `beautifulsoup4` without discussion.
- **Style:** PEP 8 for formatting, descriptive names, inline comments for non-obvious physics.
- **Determinism:** any stochastic step must respect `RNG_SEED`. Do not reseed globally.
- **Numerical safety:** honour the existing safety knobs (`BASELINE_K`, `BASELINE_DAMP`, `INIT_PERTURBATION`, `MIN_GRID_POINTS`, `NUM_NORM`). Document any change to them and justify it with a numerical experiment.
- **Docstrings:** every new public function needs a docstring stating inputs, outputs, and the physical regime it targets.
- **LaTeX for equations:** KO equations are stored as raw LaTeX strings; keep that convention.

---

## Proposing a new Kinematic Operator (KO)

A PR that adds a new KO must include **all** of the following:

1. A new entry in `KINEMATIC_OPERATORS` of the form `("<KOID>", r"<symbol>", "<Name (Author, Year)>", r"<LaTeX equation>")`.
2. A short rationale in the PR description: which established physics law or relation it represents, and a citation (book, paper, or authoritative source).
3. At least one reference experiment that uses the new KO and passes the 0.1 % precision gate.
4. Updated tests (or a new example) in the style of the existing quick-start snippets.
5. An entry in the README's KO section if the total operator count changes.

The maintainers will review for physical correctness, numerical stability under the tensioner, and non-redundancy with existing KOs.

---

## Reporting a bug

Open a new Issue using the Bug template. Please include:

- Framework version (git commit SHA) and Zenodo DOI version if relevant.
- Python version, OS, and `numpy` / `scipy` versions.
- A minimal reproducing snippet (prefer a `run_master_experiment(...)` call).
- The full `CKO_LOG` entry (if the experiment completed) or the full traceback.
- Expected vs. observed behaviour.
- Whether the Golden Rules (see README) are still satisfied in the failing case.

---

## Questions and discussion

- General questions about usage or interpretation of results: open a **Discussion**.
- Methodology, theoretical framing, or paper-level questions: see the Zenodo record and the cited preprint, then open a Discussion if still unresolved.
- Commercial / API questions: the production Physics-as-a-Service counterpart is hosted at <https://zeq.dev>.

---

## License of contributions

By submitting a Pull Request you agree that your contribution will be licensed under **THE 1.287 HULYAS ZEQ Public License (1.287HZ) v1.287** (see [`LICENSE`](../LICENSE)). You retain copyright in your contribution; you grant the project the rights required by that license, including the mandatory-attribution and protected-constant clauses.

Thank you for contributing. Independent verification is the heart of open science, and every verified experiment strengthens the framework.
