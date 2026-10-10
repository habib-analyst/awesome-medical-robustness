# Awesome Medical-AI Robustness [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of benchmarks, methods, tools, and papers for **robust medical AI** — because a model that works in the lab and breaks in the clinic is not a model at all.

Robustness is where medical AI meets reality: corrupted scanners, shifting patient populations, contaminated benchmarks, silent model drift. This list collects the benchmarks that measure it, the methods that fix it, and the tools that monitor it.

## Contents

- [Robustness Benchmarks](#robustness-benchmarks)
- [Test-Time Adaptation](#test-time-adaptation)
- [Uncertainty & Calibration](#uncertainty--calibration)
- [Contamination & Integrity](#contamination--integrity)
- [Distribution Shift](#distribution-shift)
- [Adversarial Robustness](#adversarial-robustness)
- [Deployment Monitoring](#deployment-monitoring)
- [Key Papers](#key-papers)
- [Community & Related Resources](#community--related-resources)
- [Contributing](#contributing)

---

## Robustness Benchmarks

Benchmarks that measure how models hold up under corruption, shift, and subpopulation change.

- [MedMNIST v2](https://github.com/MedMNIST/MedMNIST) — Lightweight 2D/3D biomedical image classification benchmark (12 2D + 6 3D datasets); the standard smoke-test for medical robustness work.
- [WILDS](https://github.com/p-lambda/wilds) — In-the-wild distribution-shift benchmark suite, including Camelyon17 (histopathology) and other real shift tasks.
- [ImageNet-C/R/A](https://github.com/hendrycks/robustness) — The classic corruption/robustness benchmark suite (noise, blur, weather, renditions); methodology transfers directly to medical corruptions.
- [BraTS Evaluation](https://github.com/brats/brats_evaluation) — Official evaluation package of the BraTS brain-tumor segmentation challenges; the multi-institutional MRI benchmark behind most medical segmentation robustness work.
- [fastMRI](https://github.com/facebookresearch/fastMRI) — Accelerated MRI reconstruction benchmark; pairs naturally with reconstruction-uncertainty methods.
- [CheXpert](https://stanfordmlgroup.github.io/competitions/chexpert/) — Large chest X-ray competition with uncertainty labels; a robustness staple.
- [MIMIC-CXR](https://physionet.org/content/mimic-cxr/2.0.0/) — 377k chest radiographs; the go-to real-world chest dataset for shift and calibration studies.
- [DomainBed](https://github.com/facebookresearch/DomainBed) — Testbed for domain generalization across vision benchmarks.
- [BREEDS](https://github.com/MadryLab/BREEDS-Benchmarks) — Subpopulation shift benchmarks built from ImageNet hierarchy structure.
- [SubpopBench](https://github.com/YyzHarry/SubpopBench) — Unified benchmark of subpopulation-shift algorithms and model selection.
- [synsync-bench](https://github.com/habib-analyst/synsync-bench) — Benchmark for multimodal synchronization-failure detection; cross-family fusion AUC drops expose brittle fusion pipelines.
- [robocorrupt-bench](https://github.com/habib-analyst/robocorrupt-bench) — Visual corruption robustness benchmark for vision-based robotic control (CPU, PyBullet).

## Test-Time Adaptation

Adapt the model at inference time when the test distribution shifts — no labels needed.

- [TENT](https://github.com/DequanWang/tent) — Fully test-time adaptation by entropy minimization; the baseline every TTA paper compares against.
- [CoTTA](https://github.com/qinenergy/cotta) — Continual test-time adaptation with weight-averaged teacher; handles long streams of shifting domains.
- [SHOT](https://github.com/tim-learn/SHOT) — Source-free domain adaptation via information maximization; no source data at adaptation time.
- [TTAB](https://github.com/yuejiangliu/ttab) — Official benchmark for "On Pitfalls of Test-Time Adaptation" (ICML 2023); standardized evaluation across TTA methods and shifts.
- [TTT (CIFAR release)](https://github.com/yueatsprograms/ttt_cifar_release) — Official code for test-time training with self-supervision (Sun et al., ICML 2020); adapts per test sample via a rotation-prediction auxiliary task.
- [tta-calib](https://github.com/habib-analyst/tta-calib) — Shift-aware test-time adaptation with calibrated referral for medical classifiers: adapts under shift, refers when uncertain.

## Uncertainty & Calibration

From softmax scores to guarantees: calibration, conformal prediction, and risk-controlled referral.

- [MAPIE](https://github.com/scikit-learn-contrib/MAPIE) — Conformal prediction for regression and classification in scikit-learn style.
- [Fortuna](https://github.com/awslabs/fortuna) — Bayesian uncertainty quantification for JAX/Flax and PyTorch models (AWS Labs).
- [TorchUncertainty](https://github.com/ENSTA-U2IS/torch-uncertainty) — Deep uncertainty estimation methods as drop-in PyTorch baselines.
- [netcal](https://github.com/fabiankueppers/calibration-framework) — Calibration framework: ECE, reliability diagrams, temperature scaling and more.
- [conformal-med](https://github.com/habib-analyst/conformal-med) — Conformal prediction toolkit for medical imaging: split/Mondrian/RCPS with measured coverage gaps under shift.
- [TaskUQ](https://github.com/jwen307/TaskUQ) — Task-driven uncertainty quantification for imaging inverse problems via conformal prediction (ECCV 2024).
- [Conformalized learning for medical imaging classification](https://arxiv.org/abs/2408.05037) — Instance-adaptive conformal thresholds for medical classifiers with smaller prediction sets (ISBI 2024).
- [A Gentle Introduction to Conformal Prediction and Distribution-Free Uncertainty Quantification](https://arxiv.org/abs/2107.07511) — The canonical tutorial (Angelopoulos & Bates); start here.

## Contamination & Integrity

Is the leaderboard lying? Train/test overlap, benchmark gaming, and integrity auditing.

- [benchshield](https://github.com/habib-analyst/benchshield) — Benchmark integrity toolkit: seed-instability scoring, contamination probes (dHash/canary), scaffold-sensitivity — one-command audit of any leaderboard.
- [SWE-bench](https://github.com/SWE-bench/SWE-bench) — The agentic coding benchmark whose verified split was retired over contamination concerns; the cautionary tale.
- [Min-K% Prob](https://github.com/swj0419/detect-pretrain-code) — Reference-free pretraining-data detection via token-probability statistics.
- [LiveCodeBench](https://github.com/LiveCodeBench/LiveCodeBench) — Continuously refreshed coding benchmark designed to resist contamination.
- [Detecting Benchmark Contamination Through Watermarking](https://arxiv.org/abs/2502.17259) — Watermark benchmarks before release, detect "radioactivity" in trained models (Meta FAIR, 2025).
- [How Much are LLMs Contaminated? (LLMSanitize)](https://arxiv.org/abs/2404.00699) — Comprehensive survey of contamination detection plus the LLMSanitize library.

## Distribution Shift

Papers that defined how we measure generalization under shift.

- [Do ImageNet Classifiers Generalize to ImageNet?](https://arxiv.org/abs/1902.10811) — Recht et al.: recreating ImageNet drops accuracy 11–14pp; the shift-replication wake-up call.
- [Accuracy on the Line](https://arxiv.org/abs/2107.02803) — Miller et al.: in-vs-out-of-distribution accuracy follows a predictable line — until it doesn't.
- [Measuring Robustness to Natural Distribution Shifts in Image Classification](https://arxiv.org/abs/2007.00644) — Taori et al.: synthetic robustness ≠ natural-shift robustness.
- [The Many Faces of Robustness](https://arxiv.org/abs/2006.16241) — Hendrycks et al.: a unified study across adversarial, corruption, and shift robustness.
- [WILDS: A Benchmark of In-the-Wild Distribution Shifts](https://arxiv.org/abs/2012.07421) — Koh et al.: real-world shifts including Camelyon17 pathology.

## Adversarial Robustness

Worst-case perturbations — with medical imaging's particular stakes.

- [RobustBench](https://github.com/RobustBench/robustbench) — Standardized adversarial robustness leaderboard (AutoAttack-verified).
- [Foolbox](https://github.com/bethgelab/foolbox) — Adversarial attack library (PyTorch/TF/JAX) with 40+ attacks.
- [CleverHans](https://github.com/cleverhans-lab/cleverhans) — The original adversarial-example library; still the reference implementation collection.
- [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) — IBM's comprehensive attack/defense/evasion/poisoning toolkit.
- [AutoAttack](https://github.com/fra31/auto-attack) — Parameter-free ensemble of attacks; the standard robustness evaluator.
- [Adversarial attacks on medical machine learning (Science, 2019)](https://pubmed.ncbi.nlm.nih.gov/30898923/) — Finlayson et al.: why medical ML is uniquely vulnerable to adversarial manipulation, from incentives to technical exposure.

## Deployment Monitoring

Detect drift, data-quality failures, and silent degradation in production.

- [Evidently](https://github.com/evidentlyai/evidently) — Open-source ML monitoring: drift detection, data-quality checks, interactive reports.
- [Alibi Detect](https://github.com/SeldonIO/alibi-detect) — Outlier, adversarial, and drift detection algorithms for tabular, image, text, and time series.
- [NannyML](https://github.com/NannyML/nannyml) — Estimate post-deployment performance without ground truth (CBPE).
- [TorchDrift](https://github.com/torchdrift/torchdrift) — PyTorch-native data/feature drift detection.
- [Deepchecks](https://github.com/deepchecks/deepchecks) — Continuous validation for ML models and data in CI and production.

## Key Papers

Foundational and field-defining papers on robustness, calibration, and medical-AI reliability.

- [MedMNIST v2: A Large-Scale Lightweight Benchmark for 2D and 3D Biomedical Image Classification](https://arxiv.org/abs/2110.14795) — Yang et al.: the 18-dataset medical benchmark behind most lightweight robustness studies.
- [Benchmarking Neural Network Robustness to Common Corruptions and Perturbations](https://arxiv.org/abs/1903.12261) — Hendrycks & Dietterich: ImageNet-C and the corruption-error metric.
- [Can You Trust Your Model's Uncertainty?](https://arxiv.org/abs/1905.13534) — Ovadia et al.: uncertainty degrades under shift; ensembles help but don't fix it.
- [On Calibration of Modern Neural Networks](https://arxiv.org/abs/1706.04599) — Guo et al.: modern nets are miscalibrated; temperature scaling as the baseline fix.
- [Task-Driven Uncertainty Quantification in Inverse Problems via Conformal Prediction (ECCV 2024)](https://github.com/jwen307/TaskUQ) — Wen et al.: conformal intervals on downstream task outputs from accelerated MRI.
- [CONReg: Uncertainty-Aware Medical Image Registration Using Conformal Prediction](https://doi.org/10.1007/s10278-026-01878-3) — Voxelwise conformalized registration uncertainty with 0.92–0.98 empirical coverage (J. Imaging Informatics in Medicine, 2026).

## Community & Related Resources

Ecosystems and hubs around medical imaging, robustness, and reliable ML.

- [MONAI](https://github.com/Project-MONAI/MONAI) — The medical-imaging deep learning framework; deployment and evaluation tooling.
- [TorchIO](https://github.com/TorchIO-project/torchIO) — Medical image preprocessing and augmentation for PyTorch, including artifact simulation.
- [nnU-Net](https://github.com/MIC-DKFZ/nnunet) — The self-configuring medical segmentation method; the baseline every medical robustness claim is measured against.
- [Papers With Code — Robustness](https://paperswithcode.com/area/robustness) — Living leaderboard of robustness benchmarks and SOTA results.
- [MICCAI](https://www.miccai.org) — The Medical Image Computing and Computer Assisted Intervention society; the field's main venue.

---

## Contributing

Contributions welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) first: entries must be on-topic (robustness of medical AI, broadly construed), actively maintained or field-defining, with a one-line description and a verified working link.

## License

[![CC0](https://img.shields.io/badge/license-CC0-blue.svg)](LICENSE) — To the extent possible under law, the curators have waived all rights to this list under [CC0](LICENSE). Linked projects keep their own licenses.
