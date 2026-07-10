# AI Evaluation and Cheating Detection System

A production-grade AI system for evaluating AI-generated content and detecting cheating in educational and professional assessments.

---

## Project Overview

This system implements a dual-purpose AI platform:

1. **AI Evaluation Engine** — Evaluates quality, correctness, and alignment of AI-generated responses using calibrated LLM judges, semantic similarity, and human-aligned rubrics.
2. **Cheating Detection System** — Detects unauthorized AI assistance, collusion, and contract cheating through stylometric analysis, behavioral biometrics, watermark detection, and adversarially robust classifiers.

Built with production ML practices: evaluation-driven development, calibrated probabilities, ensemble diversity, adversarial evaluation in CI, human-in-the-loop active learning, and GitOps deployment.

---

## Objectives

| Objective | Description |
|-----------|-------------|
| **Reliable AI Evaluation** | Calibrated LLM judges with constitutional principles, pairwise Elo ratings, and conformal prediction for valid confidence intervals |
| **Robust Cheating Detection** | Multi-modal ensemble (stylometry + behavioral biometrics + watermark detection + classifier ensemble) with certified adversarial robustness |
| **Production MLOps** | Reproducible pipelines, model monitoring, automated retraining, canary deployments, full lineage tracking |
| **Human-in-the-Loop** | Active learning loop with expert review queue, continuous calibration updates, bias/fairness auditing |

---

## Challenges

| Challenge | Description |
|-----------|-------------|
| **Challenge 1: Calibrated LLM Evaluation** | LLMs are poorly calibrated judges. We implement temperature scaling ensembles, Bayesian neural network calibrators, and conformal prediction to produce statistically valid confidence sets. |
| **Challenge 2: Adversarial Cheating Detection** | Adversaries use paraphrasing, translation, and prompt injection to evade detection. We deploy certified defenses (randomized smoothing), adversarial training with PGD/TextAttack, and ensemble diversity to raise attack cost. |
| **Challenge 3: Distribution Shift** | Student populations, prompt styles, and model generations shift over time. We implement covariate shift detection (KS-test, MMD), label shift correction (BBSE), and automated retraining triggers. |
| **Challenge 4: Fairness & Privacy** | Detection must not discriminate by native language, disability, or demographic. We enforce demographic parity constraints, differential privacy in training, and FERPA-compliant data handling. |

---

## Repository Structure

```
ai-evaluation-cheating-detection/
├── configs/                    # YAML configuration files
│   ├── evaluation.yaml         # Evaluation engine config
│   ├── detection.yaml          # Detection ensemble config
│   ├── calibration.yaml        # Calibration methods config
│   └── deployment/             # K8s/Helm values per environment
├── docs/
│   ├── architecture/           # System design documents
│   │   ├── evaluation_system_design.md
│   │   ├── cheating_detection_architecture.md
│   │   ├── data_flow.md
│   │   └── deployment_architecture.md
│   ├── adr/                    # Architecture Decision Records
│   │   ├── 001-evaluation-driven-development.md
│   │   ├── 002-calibration-over-accuracy.md
│   │   └── 003-ensemble-diversity.md
│   └── api/                    # OpenAPI specs
├── kubernetes/
│   ├── base/                   # Kustomize base
│   ├── evaluation/             # Evaluation service manifests
│   ├── detection/              # Detection service manifests
│   └── monitoring/             # Prometheus/Grafana/Loki
├── scripts/
│   ├── setup_data.py           # Data download & preprocessing
│   ├── download_models.py      # Model weight downloads
│   ├── run_evaluation.py       # CLI for evaluation
│   ├── run_detection.py        # CLI for detection
│   └── benchmark.py            # Performance benchmarking
├── src/
│   ├── ai_evaluation/          # Evaluation engine package
│   │   ├── __init__.py
│   │   ├── config.py           # Pydantic config models
│   │   ├── judges/             # LLM judge implementations
│   │   │   ├── __init__.py
│   │   │   ├── base.py         # Abstract judge interface
│   │   │   ├── constitutional.py
│   │   │   ├── pairwise_elo.py
│   │   │   └── rubric_based.py
│   │   ├── calibration/        # Probability calibration
│   │   │   ├── __init__.py
│   │   │   ├── temperature_scaling.py
│   │   │   ├── bayesian_nn.py
│   │   │   └── conformal.py
│   │   ├── aggregation/        # Judge aggregation strategies
│   │   │   ├── __init__.py
│   │   │   ├── weighted_voting.py
│   │   │   ├── bayesian_model_averaging.py
│   │   │   └── conformal_aggregation.py
│   │   ├── metrics/            # Evaluation metrics
│   │   │   ├── __init__.py
│   │   │   ├── semantic_similarity.py
│   │   │   ├── factual_consistency.py
│   │   │   └── alignment_scores.py
│   │   ├── api/                # FastAPI routes
│   │   │   ├── __init__.py
│   │   │   ├── routes.py
│   │   │   └── schemas.py
│   │   └── pipeline.py         # Evaluation pipeline orchestration
│   ├── cheating_detection/     # Detection system package
│   │   ├── __init__.py
│   │   ├── config.py
│   │   ├── detectors/          # Individual detector modules
│   │   │   ├── __init__.py
│   │   │   ├── base.py
│   │   │   ├── stylometric.py
│   │   │   │   ├── __init__.py
│   │   │   │   ├── lexical.py
│   │   │   │   ├── syntactic.py
│   │   │   │   └── structural.py
│   │   │   ├── behavioral.py
│   │   │   │   ├── __init__.py
│   │   │   │   ├── keystroke.py
│   │   │   │   ├── mouse_dynamics.py
│   │   │   │   └── timing_patterns.py
│   │   │   ├── watermark.py
│   │   │   │   ├── __init__.py
│   │   │   │   ├── kgw.py
│   │   │   │   ├── Kirchenbauer.py
│   │   │   │   └── custom.py
│   │   │   └── classifier.py
│   │   │       ├── __init__.py
│   │   │       ├── deberta.py
│   │   │       ├── roberta.py
│   │   │       └── ensemble.py
│   │   ├── ensemble/           # Detection ensemble
│   │   │   ├── __init__.py
│   │   │   ├── stacking.py
│   │   │   ├── bayesian_fusion.py
│   │   │   └── conformal_ensemble.py
│   │   ├── adversarial/        # Adversarial robustness
│   │   │   ├── __init__.py
│   │   │   ├── attacks.py
│   │   │   ├── defenses.py
│   │   │   └── certified.py
│   │   ├── active_learning/    # Human-in-the-loop
│   │   │   ├── __init__.py
│   │   │   ├── query_strategies.py
│   │   │   ├── annotation_queue.py
│   │   │   └── calibration_update.py
│   │   ├── fairness/           # Fairness constraints
│   │   │   ├── __init__.py
│   │   │   ├── constraints.py
│   │   │   ├── auditing.py
│   │   │   └── mitigation.py
│   │   ├── api/
│   │   │   ├── __init__.py
│   │   │   ├── routes.py
│   │   │   └── schemas.py
│   │   └── pipeline.py
│   └── shared/                 # Shared utilities
│       ├── __init__.py
│       ├── logging.py
│       ├── metrics.py
│       ├── tracing.py
│       └── validation.py
├── tests/
│   ├── unit/
│   │   ├── ai_evaluation/
│   │   │   ├── test_judges.py
│   │   │   ├── test_calibration.py
│   │   │   └── test_aggregation.py
│   │   └── cheating_detection/
│   │       ├── test_detectors.py
│   │       ├── test_ensemble.py
│   │       └── test_adversarial.py
│   ├── integration/
│   │   ├── test_evaluation_pipeline.py
│   │   ├── test_detection_pipeline.py
│   │   └── test_api_endpoints.py
│   ├── adversarial/
│   │   ├── test_paraphrase_attacks.py
│   │   ├── test_translation_attacks.py
│   │   └── test_prompt_injection.py
│   ├── fixtures/
│   │   ├── sample_responses.json
│   │   ├── golden_sets/
│   │   └── adversarial_examples/
│   └── conftest.py
├── docker/
│   ├── Dockerfile.evaluation
│   ├── Dockerfile.detection
│   ├── Dockerfile.api
│   └── docker-compose.yml
├── .github/
│   └── workflows/
│       ├── ci.yml
│       ├── cd.yml
│       ├── adversarial_eval.yml
│       └── drift_detection.yml
├── .pre-commit-config.yaml
├── pyproject.toml
├── poetry.lock
├── Makefile
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── LICENSE
└── README.md
```

---

## AI Concepts Covered

| Category | Techniques Implemented |
|----------|------------------------|
| **LLM Evaluation** | Constitutional AI judges, pairwise comparison with Bradley-Terry/Elo, rubric-based scoring, self-consistency, chain-of-thought verification |
| **Probability Calibration** | Temperature scaling (single/multi-class), Bayesian neural network calibration, conformal prediction (split/APS/RAPS), Venn-ABERS |
| **Ensemble Methods** | Stacking with meta-learner, Bayesian model averaging, conformalized ensembles, diversity-aware weighting (KL-divergence, disagreement) |
| **Stylometric Analysis** | Lexical (TTR, MTLD, zipfian), syntactic (PCFG, dependency depth), structural (paragraph/sentence/discourse), cross-lingual |
| **Behavioral Biometrics** | Keystroke dynamics (dwell/flight, n-graphs), mouse dynamics (velocity, acceleration, curvature), timing patterns (pause distributions) |
| **Watermark Detection** | KGW (Gumbel-max), Kirchenbauer (green/red lists), Christ/MarkLLM, distortion-robust detection, z-score / p-value calibration |
| **Classifier Ensembles** | DeBERTa-v3-large, RoBERTa-large, CodeBERT, GraphCodeBERT, LoRA-adapted Llama-3 classifiers |
| **Adversarial Robustness** | PGD/TextFooler/BAE attacks, randomized smoothing certification, adversarial training (TRADES, MART), input purification |
| **Active Learning** | BALD, Core-Set, BADGE, margin sampling, batch active learning with diversity, cost-sensitive querying |
| **Fairness & Privacy** | Demographic parity / equalized odds constraints, counterfactual fairness, DP-SGD, PATE, FERPA-compliant data handling |
| **MLOps** | MLflow/DVC tracking, Evidently/WhyLabs monitoring, Feast feature store, ArgoCD GitOps, canary/blue-green deployment |

---

## Future Improvements

| Area | Planned Enhancements |
|------|---------------------|
| **Evaluation** | Constitutional AI judges from preference data; pairwise Elo with Bayesian inference; rubric induction from expert annotations; process-based supervision |
| **Calibration** | Ensemble temperature scaling; Dirichlet calibration; conformal risk control; selective classification with AUC guarantees |
| **Detection** | Multilingual detection (mDeBERTa, XLM-R); code-specific watermarking (CodeBERT watermark); cross-platform behavioral biometrics (mobile, tablet) |
| **Adversarial** | Universal adversarial triggers; certified L∞ robustness via interval bound propagation; adaptive attack evaluation suite |
| **Active Learning** | Batch active learning with determinantal point processes; human-AI collaborative labeling interface; continuous calibration drift correction |
| **Explainability** | Natural language explanations via LLM; counterfactual generation; interactive SHAP dashboard; detection rationale reports |
| **MLOps** | Feast feature store integration; Evidently/WhyLabs automated monitoring; automated retraining triggers on drift/performance drop |
| **Scalability** | vLLM/TGI for high-throughput inference; Ray for distributed evaluation; Kafka event streaming for async processing |
| **Governance** | Model cards & data cards; bias/fairness audit reports; EU AI Act compliance artifacts; FERPA/COPPA compliance tooling |
| **Research** | LLM self-consistency evaluation; process-based supervision; mechanistic interpretability for detectors; watermark distillation |

---

## Author

**Aditya Rai**

- GitHub: [@AdityaRai](https://github.com/AdityaRai)
- Email: aditya.rai@example.com

---

*Built with production-grade ML engineering practices inspired by OpenAI, Anthropic, Google DeepMind, and leading ML platforms.*