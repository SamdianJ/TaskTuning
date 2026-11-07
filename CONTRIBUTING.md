# Contributing to TaskTuning

The framework uses the `task_tuning` package and `task-tuning` CLI. Keep pull requests
focused and describe the behavior changed, its validation and any remaining limitations.

## Development

Use Python 3.11 or newer. The tested local cable runtime uses Python 3.12.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -e ".[cma,cable,dev]"
pre-commit install
pre-commit run --all-files
python -m task_tuning.tests
python -m examples.cable_calibration.verify
python -m build
```

Core tests and the archived cable verifier run on the CPU with NumPy. Install the
optional extras above to run CMA-ES checks and build packages.

Ruff owns formatting and import ordering through the shared Newton profile in
`ruff-newton.toml`, with a 120-column limit.
Use descriptive errors, explicit units and real behavioral tests. Do not bypass
`Tuning.run()` with a second calibration loop. Keep expensive Newton simulations separate
from the CPU checks and document the exact solver source, hardware and qualification scope.
Do not change historical acceptance statuses when reproducing old scores.

## Source and test conventions

The package lives in `task_tuning/`, with implementation under `task_tuning/_src/`
and `unittest.TestCase` tests under `task_tuning/tests/`. Import core objects from
`task_tuning` and run the suite with `python -m task_tuning.tests`. See
[CODING_GUIDELINES.rst](CODING_GUIDELINES.rst) for the public API conventions and
[REVIEW_GUIDELINES.rst](REVIEW_GUIDELINES.rst) for review guidance.

The adapters in `examples/cable_calibration/backends/` use NumPy arrays and share
common stage implementations. These adapters are excluded from Ruff. Keep new
maintained adapters outside this directory. If an existing adapter must change,
explain the change and rerun the relevant behavior checks. Git tracks source
revisions; case provenance retains historical run and input-evidence identities.
The two large HTML reports are retained as evidence and are the only large-file hook exceptions.

GitHub Actions are pinned by commit SHA. CPU CI runs tests, archive verification, both
synthetic demos, package construction and a standalone wheel smoke test. This does not
qualify a Newton/CUDA environment or rerun the cable optimization.

## Licensing and integration

Existing runtime dependencies retain their own licenses: NumPy uses BSD-3-Clause
with bundled components under additional permissive licenses, CMA-ES uses
BSD-3-Clause, SciPy uses BSD licensing, and optional Pyglet uses BSD licensing.
Consult the installed distributions for their complete notices; these dependencies
are not relicensed by this repository.

Original contributions are Apache-2.0; retain third-party notices and identify new
dependency licenses. See [NOTICE](NOTICE) for the original contribution and Newton patch.

Use NumPy for the core runtime. CMA-ES, cable preprocessing and GL playback are
optional extras. Newton is installed explicitly for the cable example.
Do not silently replace the pinned patched solver with a released package.

Follow [AGENTS.md](AGENTS.md) for portable content and documentation scope.
See the [cable runtime requirements](examples/cable_calibration/README.md#5-construct-or-rerun-a-stage-with-newton)
for the pinned solver dependency. Discuss interface changes using a runnable case and
structured evaluation results before changing the public package.
