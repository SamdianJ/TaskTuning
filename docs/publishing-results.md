# Viewing and maintaining calibration reports

Reports and their supporting evidence are bundled in the repository. This repository
does not configure a hosted report site or an automatic publishing workflow.

## Local preview

From the repository root:

```bash
python -m http.server 8000 --bind 127.0.0.1
```

Open `http://127.0.0.1:8000/` for the English TaskTuning framework overview.
Use the EN / 中文 switch for the Chinese version, or follow the cable example link
to choose the English or Chinese report. Check narrow and
desktop layouts, navigation, language links, chart toggles, and source links.
Stop the server when finished.

- [Framework overview (English, default)](../index_en.html)
- [Framework overview (Chinese)](../index_cn.html)
- [Calibration examples: cable, plug, and task reconstruction](../examples/index.html)
- [Agent-driven calibration pipeline](../pipeline.html)
- [Plug calibration report](../examples/plug_calibration/reports/plug_calibration_en.html)
- [English report](../examples/cable_calibration/reports/cable_calibration_en.html)
- [Chinese report](../examples/cable_calibration/reports/cable_calibration_zh.html)
- [Case and reproduction guide](../examples/cable_calibration/README.md)

The HTML reports embed their figures, plots, and styles and can also be opened directly
after download. Keep both files in the same folder for language switching. Source links
are relative to the repository, so browsing the evidence requires the surrounding checkout.

## Task results and pipeline

The [results page](../examples/index.html) retains the matched before/after cable and
plug comparisons, the task reconstruction roadmap, and the full demonstration video.
The [plug report](../examples/plug_calibration/reports/plug_calibration_en.html#scope)
separates the retrospective CAE comparison from the calibrated force model. Its five
development recordings meet the stated observation criteria; numerical qualification
and independent holdout validation remain open. The latest local force candidate is
not the configuration used in the full-scene replay.

The full video and its provenance remain in `assets/task-calibration/`. Preserve its
complete duration, audio, and source identities when updating its web presentation.

The [pipeline page](../pipeline.html) explains the six-stage workflow, member
responsibilities, and standalone and agent-assisted use. Check its stage selector,
qualification-mode selector, and navigation when changing the page. Use the
[implementation status](implementation-status.md) for the current runtime boundaries.

## Update the preview image

The PNG preview is generated from archived values. Regenerate it from the repository root:

```bash
python -m pip install matplotlib
python -m examples.cable_calibration.verify
python -m examples.cable_calibration.render_preview
```

Matplotlib is a preview-generation dependency, not a core runtime dependency. The renderer
reads processed observations, archived traces, and expected metrics. It plots the no-plug
coordinate RMSE for A/B/B*/C and measured/predicted z at 150 mm using the scoring mask.

Retain uncertainty and acceptance statements: A to B is not an angle-only ablation;
B* and C share the dynamic objective; plugged validation remains unresolved.
Git tracks report revisions. Keep historical run and original evidence fingerprints in
`examples/cable_calibration/archive/provenance.json` unchanged when editing reports.
Check links and run the archive verifier before submitting the change.
