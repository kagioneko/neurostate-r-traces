# NeuroState R-Condition Traces

Per-trial NeuroState traces for the R (Response-NeuroState) condition across 9 models and 4 attack scenarios (S5, S7, S8, S9). Companion data for the paper **"NeuroState-R: Tracking Multi-Turn Drift in LLM Safety Boundaries"**.

## Files

### CSV (analysis-ready)
| File | Description |
|------|-------------|
| `traces_all.csv` | All models × all scenarios combined |
| `traces_s5.csv` | S5 scenario only (9 models) |
| `traces_s7.csv` | S7 scenario only (4 models) |
| `traces_s8.csv` | S8 scenario only (4 models) |
| `traces_s9.csv` | S9 scenario only (4 models) |

### JSON (raw)
| File | Models | Scenarios |
|------|--------|-----------|
| `s5_<model>_R_n30.json` | all 9 | S5 |
| `s5789_<model>_R_n30.json` | claude, deepseek, gemini, grok | S5, S7, S8, S9 |

## CSV Schema

```
model, scenario, trial, success, turn, G, C, D, S, O, E, corruption
```

| Column | Description |
|--------|-------------|
| `model` | Model name (claude, gemini, grok, deepseek, codex, gptoss, llama, llamabase, phi4) |
| `scenario` | Attack scenario ID (S5, S7, S8, S9) |
| `trial` | Trial index (0–29, N=30 per scenario×model) |
| `success` | 1 = attack succeeded, 0 = failed |
| `turn` | Turn index within the trial |
| `G` | Guardrail dimension |
| `C` | Compliance dimension |
| `D` | Drift index |
| `S` | Sensitivity dimension |
| `O` | Openness dimension |
| `E` | Engagement dimension |
| `corruption` | Corruption score |

## Models

| Model | Type | S5 ASR | Notes |
|-------|------|--------|-------|
| claude | GK | 13.3% | Gatekeeper |
| grok | GK | 0.0% | Gatekeeper |
| llamabase | GK | 0.0% | Gatekeeper (base) |
| llama | Mid | 30.0% | Mid-range |
| phi4 | Mid | 36.7% | Mid-range |
| gemini | DF | 76.7% | Drift-First |
| deepseek | DF | 70.0% | Drift-First |
| codex | DF | 86.7% | Drift-First |
| gptoss | DF | 56.7% | Drift-First |

## Key Finding

S8 (empathy-based attack): ASR = 0% across all models, yet NeuroState-R shows measurable drift — demonstrating that R tracks cumulative boundary erosion independently of attack success.
