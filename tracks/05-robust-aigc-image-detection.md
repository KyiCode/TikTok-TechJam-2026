# Track 5 — Robust detection of AI-generated images under real-world transformations

**Official objective:** build an image-level prototype that distinguishes AI-generated from authentic images and retains useful accuracy after realistic post-processing. The point is robustness, not clean-data accuracy alone.

Workshop: **28 August 2026, 5:00–5:45pm SGT**.

## Track summary and example products

Build a program that takes images and gives each one a confidence score for “this was AI-generated.” The difficult part is that an image can be compressed by a social platform, cropped for a profile, blurred, resized, or colour-adjusted before it reaches the detector. Your project must show that it still works reasonably after those changes—not only on untouched images.

The required practical interface is simple: provide a script that receives a folder of images and writes a JSON file containing each `image_path` and its prediction (`pred`). The required scientific evidence is less simple: compare clean-image results with transformed-image results, then explain false alarms (real images predicted as AI) and misses (AI images predicted as real).

Example product directions: a compact AIGC classifier trained with transformation augmentation; a calibrated detector that flags uncertain predictions; or an ensemble combining visual and forensic features. The team needs Python/CV capability for model inference/training and careful data separation.

### What success looks like

- The inference script handles a directory and produces the specified JSON output.
- You can show a clean-versus-transformed comparison, not just a single accuracy number.
- The model is below the 2B-parameter limit and validation images prohibited for training are kept out of training.
- You understand and communicate when the detector should not be trusted.

## Official robustness target

The organizer may evaluate a subset of these transformations:

| Transformation | Parameters in brief | Real-world analogue |
| --- | --- | --- |
| JPEG compression | quality 90, 70, 50, 30 | Social/media re-encoding |
| Gaussian blur | σ 0.5, 1.0, 2.0 | Out-of-focus images |
| Resize then upscale | 0.5× or 0.25× | Thumbnails |
| Gaussian noise | σ 0.02, 0.05, 0.10 | Low-light noise |
| Color jitter | brightness/contrast/saturation ±20% | Filters/auto-enhance |
| Center crop | 80% crop | Profile/framing crop |

## Constraints

- In scope: image-level AIGC detection, robust features/models/evaluation, error analysis, and explainability ideas.
- Out of scope: production moderation systems and video/audio/non-image modalities.
- Use models **smaller than 2B parameters**.
- Optimise for a hackathon proof of concept under limited compute; no production/internal systems are expected.
- Public or properly licensed datasets and self-created transformations are allowed, provided assumptions are stated.

Suggested sources in the brief are SID_Set, CIFAKE, and WildFake. The cited WildFake/COCO val2017 + DALL·E Advanced validation subset (4,998 non-AIGC; 8,843 AIGC) is for demonstration/iteration only and **must not be used for training**. It does not contribute to final score.

## Required deliverables

In addition to Devpost description, public repo/README, and public YouTube demo:

- Include a runnable script that accepts an image directory and writes JSON predictions. Each output record must contain `image_path` and `pred`, where `pred` is the AIGC confidence.
- Include a compact table or visual comparing clean versus transformed performance.
- Include an error-analysis note covering representative false positives, false negatives, and trade-offs.

The judging split is Technical Execution 35%, Innovation & Problem Insight 20%, Impact & Relevance 20%, Feasibility & Practicality 15%, and Presentation 10%.

## Recommended experimental design

Use a held-out, source-disjoint evaluation protocol where feasible, then produce a transformation matrix by transform/severity. Report an operating threshold and classwise metrics (at least precision/recall or false-positive/false-negative rates) beside aggregate accuracy; false positives are especially important for a detector that could affect authentic content.

Start with a reproducible compact baseline, then make robustness interventions one at a time: augmentation policy, frequency/forensic feature branch, ensembling, calibration, or transform-aware consistency. Keep all train/validation/test provenance and transformation seeds in a manifest. Do not use the demonstration validation subset during training.

## Definition of done

- [ ] Model size is under 2B parameters and data licensing/provenance are documented.
- [ ] Directory-to-JSON inference script produces `image_path` and `pred` for every input.
- [ ] Clean and transformed results are shown side-by-side, including severity where practical.
- [ ] Error analysis includes real false-positive and false-negative examples with explanation.
- [ ] Setup, exact checkpoint/configuration, reproduction steps, limitations, and demo are complete.
