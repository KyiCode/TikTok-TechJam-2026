# Track 3 — Implement a GPU Kernel for a Transformer Layer

**Official objective:** implement one or more optimized GPU kernels/layer implementations for the supplied Transformer benchmark, improving runtime while staying numerically close to the PyTorch or TensorFlow reference.

Workshop: **28 August 2026, 3:00–3:45pm SGT**.

## What must work

Download and use either the Torch benchmark (`torch_transformer_benchmark.py`) or TensorFlow benchmark (`tensorflow_transformer_benchmark.py`). You may alter the layer implementation and select different kernels/fusion strategies for different supplied shapes. Tests will include varying batch sizes, sequence lengths, and hidden dimensions; supplied test cases compare against the framework reference.

Correctness tolerance is **relative error < 0.02** and **absolute error < 0.002**. Optimise and test on your own machine. The brief encourages AI tools and asks for a clear technical report; detailed AI-tool usage earns bonus points.

## Scope and technical strategy

In scope: AI-assisted code generation, profiling, kernel fusion, memory-layout work, lower precision, tensor-core utilisation, softmax optimisation, and custom CUDA/Triton/TensorFlow/PyTorch implementation. Production deployment is out of scope.

The official prompt permits shape-specialised dispatch. That makes a measured portfolio of kernels preferable to forcing one universal kernel:

- First establish a correctness harness for every official shape.
- Profile baseline to distinguish launch overhead, bandwidth, and compute bottlenecks.
- Focus fusion where intermediates are expensive (for example attention score → scaling/masking → softmax → value multiplication, when benchmark interface allows).
- Use safe dispatch predicates and a correct fallback. Never trade correctness on a less-common shape for a headline speedup.
- Benchmark warm-up and repeated timing consistently; report more than a single best timing.

## Required artifacts

- Devpost description: approach, tools, APIs, libraries/frameworks, and assets/datasets.
- Public repository with structured/commented code, project overview, setup, reproduction instructions, limitations/next steps, and team contributions.
- Public YouTube demo linked from Devpost. A backend/performance walkthrough is acceptable if no UI is relevant.
- Technical report describing CPU, GPU, disk/environment, optimisation techniques, final test results, and AI skills/tools used.

The standard judging rubric is Technical Execution 35%, Innovation & Problem Insight 20%, Impact & Relevance 20%, Feasibility & Practicality 15%, and Presentation 10%.

## Recommended report table

Use one row per shape or dispatch class: shape/dtype, reference latency, optimized latency, speedup, relative error, absolute error, warm-up/repetitions, and selected kernel. Add profiler evidence and explain any variance, memory trade-off, or unsupported optimisation.

## Definition of done

- [ ] One benchmark path runs reproducibly on the declared GPU/software environment.
- [ ] Every supplied shape passes the official numerical thresholds.
- [ ] Timings demonstrate the final implementation against the reference under a documented method.
- [ ] Dispatch/fallback logic is explicit and tested.
- [ ] Repository, environment report, results, and video reproduce the demonstrated outcome.
