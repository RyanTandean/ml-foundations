# ML Foundations Plan

**Context:** Already have UW coursework math (probability, stats, linear algebra) — this plan is
about applying those concepts to ML, not relearning math. Sequenced for early return: front-loaded
phases are the ones to never skip, even if Honda work interrupts progress later. Long-term interest
is computer vision, but time-series/forecasting fundamentals take priority for now given current
Honda relevance — CV work is deferred to Phase 5.

---

## Phase 1 — Classic ML From Scratch (2–3 weeks)
**Goal:** bias-variance, regularization, overfitting stop being memorized words and become things
you've watched happen in code you wrote yourself.

- [ ] Linear regression from scratch (NumPy only) — implement gradient descent by hand
- [ ] Logistic regression from scratch — same approach, understand sigmoid + cross-entropy loss
- [ ] Regularization (L1/L2) — implement, observe effect on overfitting with a toy dataset
- [ ] Redo each with scikit-learn — compare, confirm you get the same behavior, see what the library abstracts away
- [ ] A decision tree from scratch (simplified — just the split logic) — optional but high value

**Deliverable:** a small repo/notebook set showing linear regression, logistic regression, and
regularization, all implemented manually and validated against sklearn.

**Sources:**
- Andrew Ng's CS229 (Stanford, free lecture notes + problem sets online) — the rigorous version, not the popular Coursera intro
- "Hands-On Machine Learning" by Aurélien Géron — good applied companion, has a from-scratch flavor in early chapters
- Udemy: generally weak for "from scratch" rigor at this phase — most Udemy ML courses teach library-calling, not derivation. Skip Udemy here.

**Never skip this phase**, even under time pressure — highest return of the whole plan.

---

## Phase 2 — Evaluation & Model Selection (1–2 weeks)
**Goal:** precision/recall/F1/ROC-AUC become things you can rederive from a confusion matrix on the
spot, not memorized terms. You're already ahead here from the forecasting project's calibration work.

- [ ] Confusion matrix → precision/recall/F1 → derive relationships yourself, don't just memorize formulas
- [ ] ROC-AUC — what it means, when it misleads (e.g. imbalanced classes)
- [ ] Cross-validation — k-fold, stratified k-fold, and why time series needs a different approach (ties into Phase 4)
- [ ] Overfitting diagnostics — learning curves, train/val gap interpretation
- [ ] Calibration — you've already done this for quantile forecasts; connect it to classification calibration (reliability diagrams) for the fuller picture

**Deliverable:** a short write-up/notebook applying all these metrics to a toy classification dataset,
in your own words explaining what each one tells you.

**Sources:**
- StatQuest (YouTube) — genuinely excellent for building intuition on every metric here, free
- CS229 notes again cover the theory side

**Natural pause point #1** — if Honda pulls you away here, you already have durable fundamentals + evaluation literacy, the two most transferable pieces.

---

## Phase 3 — Tree Ensembles: LightGBM/XGBoost, Properly (2–3 weeks)
**Goal:** understand boosting vs. bagging, real hyperparameter tuning, feature importance and its
pitfalls — not just calling `.fit()`. Directly deepens the model you started in the forecasting practice project.

- [ ] Bagging vs. boosting — conceptual difference, why boosting tends to win on tabular data
- [ ] Random Forest — implement or closely study one, understand variance reduction
- [ ] Gradient boosting mechanics — how each tree corrects the previous ensemble's residuals
- [ ] LightGBM/XGBoost/CatBoost — practical usage, key hyperparameters (learning rate, depth, regularization terms) and what each actually controls
- [ ] Feature importance — types (gain vs. split vs. permutation), and why default importances can mislead
- [ ] Real hyperparameter tuning — grid/random search, and ideally Bayesian optimization (Optuna) — not manual guessing

**Deliverable:** apply this directly to your parts-forecasting practice project's LightGBM step.

**Sources:**
- Udemy: **"Feature Engineering and Ensemble Learning"**-type courses are decent here — tree ensembles are one area where Udemy's practical, library-focused approach is actually well-suited, since the theory is simpler than deep learning and the practical tuning knowledge has real value
- Official LightGBM/XGBoost docs — genuinely well-written, worth reading directly
- Kaggle competition writeups/notebooks for real-world tuning patterns

---

## Phase 4 — Time Series Specifics (2 weeks)
**Goal:** the extra rules layered on top of general ML for sequential data — most of this should feel
like "oh, this is just ML with a few extra constraints," not a separate universe, given your forecasting project head start.

- [ ] Why random train/test splits leak information in time series — walk-forward / rolling-origin validation instead
- [ ] Autocorrelation and partial autocorrelation — what ACF/PACF plots tell you
- [ ] Stationarity — what it means, why ARIMA needs it, differencing to achieve it
- [ ] Classical models: exponential smoothing, ARIMA/SARIMA — you've touched these already, go one level deeper
- [ ] Adapting tree ensembles for forecasting — lag features, rolling stats, the approach you already built in `data_loader.py`/`features.py`
- [ ] Quantile/probabilistic forecasting — pinball loss, calibration (you've already built strong intuition here)

**Deliverable:** finish the M5 practice project — Tier 1 baseline vs. Tier 2 LightGBM, full eval pipeline (pinball loss + calibration).

**Sources:**
- "Forecasting: Principles and Practice" (Hyndman & Athanasopoulos) — free online, the standard reference, very readable
- Udemy: **"Time Series Analysis, Forecasting, and Machine Learning in Python"** (Lazy Programmer) is generally well-regarded and covers both classical + ML approaches — reasonable pick if you want a structured Udemy option here

**Natural pause point #2** — solid classic ML + tabular/time-series competence. Enough to be a real practitioner on most business ML work.

---

## Phase 5 — Neural Networks & Deep Learning, CV-Oriented (4–6 weeks, later/deferred)
**Goal:** this is the phase to revisit when Phases 1–4 are solid and Honda work has settled down.
Restructured toward computer vision specifically, since that's the long-term interest — lighter on
generic breadth (e.g. NLP/transformers-for-text), more direct toward CV.

- [ ] Neural network fundamentals from scratch — backprop by hand, build a tiny autograd engine
- [ ] CNNs specifically — convolutions, pooling, why they suit image data; build a basic image classifier near-scratch (not just calling a pretrained model)
- [ ] Classic CV architecture evolution — LeNet → AlexNet → ResNet → Vision Transformers, understanding *why* each innovation mattered
- [ ] Transfer learning done properly — when/how to fine-tune vs. train from scratch, understanding why it works
- [ ] Classic (non-deep-learning) CV — edge detection, filters, basic OpenCV — builds intuition for what a CNN automates
- [ ] Object detection/segmentation basics, if going beyond classification

**Deliverable:** the bird feeder classifier project (real data, real mess — lighting, angles, false positives) as the capstone.

**Sources:**
- Karpathy's "Neural Networks: Zero to Hero" (YouTube, free) — builds backprop and an autograd engine from scratch, excellent
- Stanford CS231n (Convolutional Neural Networks for Visual Recognition) — free lecture notes/videos, the standard CV foundation course
- Udemy: mixed here — avoid generic "Deep Learning A-Z" style courses (too shallow); if choosing Udemy for this phase, look specifically for PyTorch-based CV courses with hands-on CNN-from-scratch content rather than pretrained-model tutorials

*Not detailed further for now — revisit and expand this phase's plan once you actually reach it.*

---

## Phase 6 — Applied Depth / Specialization (ongoing)
Open-ended. Once Phases 1–5 are solid, branch based on what you gravitate toward — likely deeper CV
specialization, but could shift. This phase never really ends.

---

## Notes on note-taking (see chat for full discussion)
Recommended split: Jupyter notebooks for anything with code/output (Phases 1, 3, 4, 5 exercises) since
seeing results inline matters for building intuition; a separate lightweight written notes file
(markdown in the same repo, or Notion/Obsidian) for concept summaries and "explain it in your own
words" write-ups, since re-deriving a concept in plain text is a different and complementary exercise
from writing code. Avoid paper for anything you'll want to search back through later.
