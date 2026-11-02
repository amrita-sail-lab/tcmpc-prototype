# Predatory Comment Detector

A Streamlit prototype that flags potentially predatory comments written in **Tamil, Tanglish (romanised Tamil) and English**, with an optional per-comment explanation of *why* the model made its call.

![Python](https://img.shields.io/badge/python-3.x-blue) ![Streamlit](https://img.shields.io/badge/built%20with-Streamlit-FF4B4B) ![License: MIT](https://img.shields.io/badge/code-MIT-green)

## Overview

- **Model:** [MuRIL](https://huggingface.co/google/muril-base-cased) fine-tuned for binary classification (`predatory` vs `non_predatory`) on Tamil code-mixed comments.
- **Explainability:** a concise [LIME](https://github.com/marcotcr/lime) explanation highlights the tokens that pushed a single prediction towards or away from the predatory class.
- **Interface:** paste one comment, get a label and (optionally) the explanation.

## Performance

Held-out test set of 188 comments (94 predatory, 94 non-predatory), from the accompanying research repository:

| Metric | Score |
|---|---|
| Accuracy | 95.21% |
| Macro F1 | 0.952 |
| Predatory recall | 95.74% |

The training corpus contains 5,530 labelled comments, balanced 50/50 across the two classes.

## Run locally

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
streamlit run app.py
```

## Repository layout

| File | Purpose |
|---|---|
| `app.py` | Streamlit user interface |
| `predictor.py` | Loads the fine-tuned model and returns predictions |
| `explainer.py` | LIME explanation for a single comment |
| `best_model.pkl` | Trained classifier artefact |
| `requirements.txt` | Python dependencies |

## Responsible use

This is a research prototype, **not** a moderation system. It can make mistakes, especially on slang, sarcasm and spellings it has not seen, and should never be the only basis for action against a person. Outputs should be reviewed by a human. `best_model.pkl` is a pickle file, so only load models from sources you trust.

## Related work

Training code, datasets and full experiment results (MuRIL, MuRIL + XGBoost, TF-IDF + SentenceBERT, LIME figures) live in the companion research repository `amrita-sail-lab/tcmpc`, which is private until the accompanying paper is released.

## License

Code is released under the [MIT License](LICENSE).
