# Stablecoin Liquidity as a Crypto-Native Regime Signal

### State-Dependent Density Forecasts for BTC, ETH, and SOL

A replication-ready research repository for testing whether stablecoin liquidity acts as a crypto-native signal for latent return regimes in Bitcoin, Ether, and Solana.

![Article type](https://img.shields.io/badge/article-research%20paper-111827)
![Assets](https://img.shields.io/badge/assets-BTC%20%7C%20ETH%20%7C%20SOL-f59e0b)
![Models](https://img.shields.io/badge/models-HHM%20%7C%20NHHM-7c3aed)
![Sample](https://img.shields.io/badge/sample-2020--04--15_to_2026--03--17-0f766e)
![Python](https://img.shields.io/badge/python-3.x-3776AB?logo=python&logoColor=white)
[![ORCID](https://img.shields.io/badge/ORCID-0000--0002--1670--8033-A6CE39?logo=orcid&logoColor=white)](https://orcid.org/0000-0002-1670-8033)
![Zenodo DOI](https://img.shields.io/badge/Zenodo%20DOI-TBA-lightgrey)](https://doi.org/10.5281/zenodo.20180030)

</div>

---

## The idea in one picture

```text
Stablecoin balance-sheet + usage signals
        |
        v
Crypto-native liquidity and activity predictors
        |
        v
Bayesian latent-regime models
        |
        +--> HHM: fixed transition probabilities
        |
        +--> NHHM: covariate-driven transition probabilities
        |
        v
State-dependent predictive densities for BTC, ETH, and SOL returns
        |
        v
Forecast contest: log score, CRPS, and MSFE
```

This repository accompanies the research paper:

> **Stablecoin Liquidity as a Crypto-Native Regime Signal: State-Dependent Density Forecasts for BTC, ETH, and SOL**  
> **Article classification:** Research Paper  
> **Author:** Veliota Drakopoulou  
> **Affiliations:** Higher Colleges of Technology; Embry-Riddle Aeronautical University  
> **ORCID:** [0000-0002-1670-8033](https://orcid.org/0000-0002-1670-8033)  
> **Correspondence:** <vdrakopoulou@gmail.com>  
> **GitHub repository:** https://github.com/vdrakopoulou/stablecoin-liquidity-regime-forecasts
> 
> **Zenodo replication package DOI:**  https://doi.org/10.5281/zenodo.20180030

---

## Why this paper exists

Crypto markets have their own liquidity plumbing. Stablecoins are central to that plumbing: they move across exchanges, DeFi venues, payment rails, and market-making channels. This paper asks whether stablecoin liquidity and activity contain information about the **state** of major crypto-asset return distributions.

The empirical design treats stablecoin variables as **crypto-native regime signals** and evaluates whether they improve one-step-ahead density forecasts for:

| Asset | Ticker | Role in the study |
|---|---:|---|
| Bitcoin | BTC | Benchmark crypto reserve asset |
| Ether | ETH | Smart-contract and settlement asset |
| Solana | SOL | High-throughput alternative L1 asset |

The target is not only the conditional mean. The focus is the **full predictive density**: where returns are expected to land, how uncertain the distribution is, and how that uncertainty changes across latent regimes.

---

## Repository highlights

- **Daily sample:** 2020-04-15 to 2026-03-17.
- **Assets:** BTC, ETH, and SOL.
- **Stablecoin signals:** USDT and USDC market capitalization, spot volume, transaction count, and active-address growth.
- **Network controls:** BTC/ETH fee pressure and transaction pressure.
- **Macro controls:** S&P 500 return, VIX growth, and 10-year Treasury yield changes.
- **Models:** Bayesian Gaussian hidden Markov models and non-homogeneous hidden Markov models.
- **Forecast evaluation:** average log score, CRPS, MSFE, benchmark comparisons, and Diebold-Mariano style loss comparisons.
- **Replication-first design:** raw snapshots, processed data, configs, scripts, final outputs, diagnostics, and robustness outputs are bundled together.

---

## Main frozen result set

The final evidentiary set is frozen in `outputs/final_model_freeze/`.

| Asset | Frozen preferred model | Avg. log score | Avg. CRPS | MSFE | Holdout obs. | Primary takeaway |
|---|---:|---:|---:|---:|---:|---|
| BTC | NHHM(3) | -2.2155 | 1.2497 | 5.6371 | 433 | Covariate-driven transitions are retained for BTC. |
| ETH | HHM(3) | -2.7390 | 2.1186 | 15.9983 | 433 | A three-state homogeneous regime model is retained. |
| SOL | HHM(3) | -2.9307 | 2.4439 | 18.4588 | 339 | A three-state homogeneous regime model is retained under thinner SOL coverage. |

Primary density criteria are **average log score** and **CRPS**. MSFE is reported as a point-forecast diagnostic, but the paper's forecasting emphasis is on predictive densities.

Authoritative files:

```text
outputs/final_model_freeze/frozen_preferred_models.csv
outputs/final_model_freeze/final_forecast_summary.csv
outputs/final_model_freeze/table_6_final_forecast_contest.csv
outputs/final_model_freeze/FINAL_MODEL_FREEZE_NOTE.md
```

---

## Project structure

```text
.
|-- config/                         # JSON configs for main, quickstart, forecast, and robustness runs
|-- data/
|   |-- raw/                        # Bundled public-source raw snapshots
|   |-- processed/                  # Full-sample model-ready data
|   |-- processed_train_80/         # Training split for forecast evaluation
|   `-- processed_matched_sol/      # Matched-sample robustness inputs
|-- examples/                       # Minimal usage notes
|-- outputs/
|   |-- BTC/ ETH/ SOL/              # Asset-level model outputs
|   |-- forecast_eval/              # Holdout forecast scores and benchmark comparisons
|   |-- final_model_freeze/         # Frozen preferred-model decision
|   |-- statecount_robustness/      # K = 4 robustness evidence
|   |-- matched_sample_robustness/  # BTC/ETH/SOL matched-sample evidence
|   |-- mechanism_robustness/       # BTC predictor-block mechanism checks
|   `-- publication_*/              # Diagnostic and convergence evidence
|-- scripts/                        # End-to-end replication scripts
|-- src/                            # Data processing, metrics, models, export utilities
|-- FINAL_SUBMISSION_MANIFEST.csv   # Submission inventory
|-- LIST_OF_TABLES_AND_FIGURES.md   # Paper table/figure inventory
|-- PACKAGE_STATUS_FINAL.md         # Authoritative status and exclusions
|-- REPLICATION_APPENDIX.md         # Replication appendix
`-- requirements.txt                # Python package requirements
```

---

## Quick start

Clone or unzip the repository, then run from the project root.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Run a synthetic smoke test first:

```bash
python scripts/00_smoke_test.py
```

Run the short quickstart bundle:

```bash
bash scripts/run_quickstart_bundle.sh
```

Run the main full-sample rebuild using the bundled raw snapshots:

```bash
bash scripts/run_full_sample_bundle.sh
```

Run the retained robustness bundle:

```bash
bash scripts/run_updated_robustness_bundle.sh
```

The precomputed results are already included, so reviewers can inspect the evidence without rerunning estimation.

---

## Replication modes

| Mode | Command | Purpose |
|---|---|---|
| Smoke test | `python scripts/00_smoke_test.py` | Checks model code on synthetic data. |
| Quickstart | `bash scripts/run_quickstart_bundle.sh` | Runs a shorter sample for fast inspection. |
| Main full sample | `bash scripts/run_full_sample_bundle.sh` | Rebuilds the main HHM/NHHM grid for BTC, ETH, and SOL. |
| Robustness suite | `bash scripts/run_updated_robustness_bundle.sh` | Rebuilds state-count, matched-sample, mechanism, and forecast-evaluation evidence. |
| Manual pipeline | `python scripts/run_all.py --config config/quickstart.json` | Runs download, processing, estimation, export, and manifest generation through one driver. |

To refresh public-source raw data before processing, use:

```bash
python scripts/01_download_data.py --config config/full_sample_2026.json --force
```

Use this only when you intentionally want a refreshed public-source snapshot rather than the frozen submitted data.

---

## Data construction

The modeling files are produced from daily crypto and macro series.

| Variable | Meaning | Construction summary |
|---|---|---|
| `ret` | Target asset return | `100 * [log(P_t) - log(P_{t-1})]` |
| `lag_ret` | Own-return lag | `ret_{t-1}` |
| `SCAPG` | Stablecoin capitalization growth | Lagged growth in aggregate USDT + USDC market cap |
| `SVOLG` | Stablecoin spot-volume growth | Lagged growth in aggregate USDT + USDC spot volume |
| `STXG` | Stablecoin transaction-count growth | Lagged growth in aggregate USDT + USDC transaction count |
| `SADDRG` | Stablecoin active-address growth | Lagged growth in aggregate USDT + USDC active addresses |
| `FEEG` | BTC/ETH fee-pressure growth | Lagged growth in aggregate BTC + ETH fees |
| `BTXG` | BTC/ETH transaction-pressure growth | Lagged growth in aggregate BTC + ETH transaction counts |
| `SPXRET` | Equity-market control | Lagged S&P 500 log return |
| `VIXG` | Volatility-stress control | Lagged VIX log growth |
| `TY10` | Rate-shock control | Lagged daily change in 10-year Treasury yield |

The exported variable dictionary is here:

```text
data/processed/variable_dictionary.csv
```

Important design choices:

- Crypto and macro series are merged by calendar date.
- Macro variables are forward-filled over non-trading days to align with seven-day crypto trading.
- Predictors are lagged before estimation.
- BTC and ETH have 2,163 usable full-sample daily observations.
- SOL has 1,695 usable full-sample daily observations because free daily SOL price coverage is thinner over the full window.

---

## Model family

The repository estimates two closely related Bayesian latent-state models.

### HHM: homogeneous hidden Markov model

The HHM assumes fixed latent-regime transition probabilities:

```text
Pr(s_t = j | s_{t-1} = i) = P_ij
```

### NHHM: non-homogeneous hidden Markov model

The NHHM lets transition probabilities vary with lagged predictors:

```text
Pr(s_t = j | s_{t-1} = i, z_{t-1}) = softmax_j(gamma_ij' z_{t-1})
```

Both models allow the conditional return equation to vary by latent state:

```text
ret_t = x_{t-1}' beta_{s_t} + epsilon_t,    epsilon_t ~ Normal(0, sigma^2_{s_t})
```

The forecast object is a predictive density, evaluated using log score and CRPS.

---

## Output guide for reviewers

Start here:

```text
FINAL_SUBMISSION_MANIFEST.csv
PACKAGE_STATUS_FINAL.md
REPLICATION_APPENDIX.md
LIST_OF_TABLES_AND_FIGURES.md
```

Then inspect the evidence blocks:

| Evidence block | Location |
|---|---|
| Frozen preferred models and final forecast contest | `outputs/final_model_freeze/` |
| Initial forecast evaluation | `outputs/forecast_eval/` |
| Asset-level model summaries | `outputs/BTC/`, `outputs/ETH/`, `outputs/SOL/` |
| State-count robustness | `outputs/statecount_robustness/` |
| Matched-sample robustness | `outputs/matched_sample_robustness/` |
| BTC mechanism robustness | `outputs/mechanism_robustness/` |
| Multi-chain convergence diagnostics | `outputs/publication_diagnostics/` |
| ETH/SOL deeper diagnostics | `outputs/publication_ethsol_deeper_v2/`, `outputs/publication_sol_deeper_v3/` |
| BTC regularized and small-core diagnostics | `outputs/publication_final_regularized/`, `outputs/publication_final_btc_smallcore_rerun/` |

---

## Final evidence boundary

The final submission bundle intentionally excludes invalid Student-t robustness outputs. Earlier `publication_student_t_frozen_v2` results should **not** be cited as valid robustness evidence because the package did not confirm that Student-t emissions actually activated.

The retained final evidence set is documented in:

```text
PACKAGE_STATUS_FINAL.md
FINAL_SUBMISSION_MANIFEST.csv
```

---

## Reproducibility checklist

- [x] Raw public-source snapshots bundled.
- [x] Processed model-ready data bundled.
- [x] Main configs bundled.
- [x] Estimation scripts bundled.
- [x] Forecast-evaluation scripts bundled.
- [x] Final tables and figures bundled.
- [x] Robustness outputs bundled.
- [x] Final preferred-model freeze documented.
- [ ] GitHub repository URL added.
- [ ] Zenodo replication package DOI added.
- [ ] License file added before public release.

---

## How to cite

Update the DOI and repository URL once the public release is minted.

```bibtex
@article{drakopoulou2026stablecoin_regime_signal,
  title   = {Stablecoin Liquidity as a Crypto-Native Regime Signal: State-Dependent Density Forecasts for BTC, ETH, and SOL},
  author  = {Drakopoulou, Veliota},
  year    = {2026},
  note    = {Research paper},
  url     = {<GITHUB_REPOSITORY_URL>}
}
```

```bibtex
@dataset{drakopoulou2026stablecoin_regime_replication,
  title     = {Replication Package for Stablecoin Liquidity as a Crypto-Native Regime Signal},
  author    = {Drakopoulou, Veliota},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {<ZENODO_REPLICATION_PACKAGE_DOI>},
  url       = {<ZENODO_RECORD_URL>}
}
```

---

## Acknowledgments and data sources

This replication package uses bundled public-source snapshots, including Coin Metrics community data for crypto variables and public macro/market snapshots for SP500, VIXCLS, and DGS10-style controls. See the source manifest for exact bundled-source notes:

```text
data/raw/bundled_source_manifest.json
```

---

## License and reuse

No license file is included in the submitted bundle. Add a `LICENSE` file before public release so that code, text, figures, and data reuse terms are explicit. Also confirm that downstream redistribution terms are compatible with the bundled public data sources.

---

## Contact

**Veliota Drakopoulou**  
Higher Colleges of Technology; Embry-Riddle Aeronautical University  
ORCID: [0000-0002-1670-8033](https://orcid.org/0000-0002-1670-8033)  
Email: <vdrakopoulou@gmail.com>

---

<div align="center">

**Stablecoin liquidity is not just a balance-sheet variable. In this paper, it is treated as a regime signal.**
