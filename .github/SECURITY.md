# Security & Integrity Policy

This document describes how to responsibly report security vulnerabilities and **scientific-integrity issues** in the HULYAS / ZEQ OS reference framework (Zenodo DOI [10.5281/zenodo.16930428](https://doi.org/10.5281/zenodo.16930428)).

Because this project is an Open-Science computational physics framework, "security" here is interpreted broadly. It covers conventional software-security issues **and** the integrity of the mathematical contract the framework is built on.

---

## Supported versions

| Version | Status | Receives security & integrity fixes |
|---|---|---|
| `v1287` (this repository, Zenodo record of record) | **Current** | Yes |
| Prior Zenodo preprints / supporting documents | Reference only | No |

Only the canonical release published on Zenodo under DOI `10.5281/zenodo.16930428`, and the `main` branch of this repository, are actively maintained.

---

## What to report

Please report any of the following through the private channels below, **not** in a public issue:

### 1. Software security issues
- Arbitrary code execution paths (for example, unsafe evaluation of user-supplied prompts in `interpret_prompt_components` / `score_operators_from_prompt`).
- Unsafe network behaviour in the optional scrapers (`scrape_wikipedia`, `scrape_nist_constants`, `scrape_nasa`, `scrape_esa`, `multi_source_scrape`) — for example, server-side request forgery, injection via scraped HTML, or uncontrolled resource consumption.
- Dependency vulnerabilities that can be exploited through normal framework usage.
- Unsafe file / path handling or logging of sensitive data to `CKO_LOG`.

### 2. Scientific-integrity issues
- **Precision-gate regressions** — cases where `run_master_experiment_strict(...)` reports a pass but independent verification shows mean error above `ERROR_THRESHOLD_PCT = 0.1`.
- **Auto-tune drift** — cases where `autotune_until_pass(...)` converges to a result that does not actually satisfy the gate when re-evaluated against the analytic references (`_analytic_free_fall`, `_analytic_shm`, `_solve_reference`).
- **Resonance-lock failures** — silent loss of phase-lock between the 1.287 Hz carrier and the computation (issues in `initialize_phase_lock_detector`, `update_phase_lock`, or `adaptive_tensioner_control`).
- **Protected-constant violations** — any code path, downstream fork, or published derivative that alters, renames, abstracts, or obscures the defined constants of the framework: **HulyaPulse = 1.287 Hz** and **Zeqond = 0.777 s**. These constants are protected by the 1.287HZ Public License.
- **Fabricated KO operators** — entries in `KINEMATIC_OPERATORS` whose cited equation does not match the stated source, or which silently duplicate or shadow an existing operator.
- **Reproducibility failures** — cases where fixing `RNG_SEED = 1287` no longer yields bit-stable results across platforms for a given input.
- **Misattribution** — cases where this framework (or a near-identical fork) is published without the mandatory attribution and DOI citation required by the license.

---

## How to report

Please do **not** open a public GitHub issue for anything in the categories above until the maintainers have had a chance to respond.

Preferred private channels, in order:

1. **GitHub Security Advisories** — open a private advisory on this repository via the **Security** tab. This is the recommended channel for both software-security and scientific-integrity reports.
2. **Direct contact via the project website** — contact information is published at <https://hulyas.org>.
3. **Production platform** — if the issue also affects the Physics-as-a-Service deployment, it can be raised alongside at <https://zeq.dev>.

When you report, please include:

- A clear description of the issue and its category.
- The framework version (git commit SHA) and, if relevant, the Zenodo version.
- A minimal reproducing snippet (for software-security issues) or a reproducible experiment prompt plus the full `CKO_LOG` entry (for integrity issues).
- Your Python / `numpy` / `scipy` versions and OS.
- Whether the issue affects the 0.1 % precision gate, the protected constants, or reproducibility under `RNG_SEED = 1287`.
- Optionally, your suggested fix.

---

## What to expect

- Acknowledgement of your report as soon as reasonably possible after receipt.
- An initial assessment that classifies the issue (software-security, integrity, licensing, or out-of-scope).
- A coordinated disclosure timeline for software-security issues; a correction / retraction plan for integrity issues.
- Credit in the release notes (and, where appropriate, in the Zenodo record metadata) unless you prefer to remain anonymous.

We will not take legal action against researchers who:

- Report issues in good faith through the channels above.
- Avoid privacy violations, destruction of data, and interruption or degradation of services.
- Give the maintainers reasonable time to investigate and fix before any public disclosure.

---

## Out of scope

- Disagreements about scientific methodology that do not involve a concrete integrity violation are out of scope for this policy; please use **Discussions** or open a normal issue.
- Performance regressions that do not cross the 0.1 % precision gate are normal bug reports — please use the Bug template, not this policy.
- Requests to weaken the protected constants, the precision gate, or the reproducibility anchor are not security reports and will be declined (see `CONTRIBUTING.md`).

---

Thank you for helping keep HULYAS / ZEQ OS mathematically honest and safe to use.
