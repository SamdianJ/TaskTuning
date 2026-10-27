# Viewing and maintaining calibration reports

Reports and their supporting evidence are bundled in the repository. Local preview
does not require a hosted site or a publishing workflow.

## Local preview

From the repository root:

```bash
python -m http.server 8000 --bind 127.0.0.1
```

Open `http://127.0.0.1:8000/` for the results index, full task demo, and cable and plug
reports. Check narrow and desktop layouts, language links, chart toggles, and source links.
Stop the server when finished.

- [Results index](../index.html)
- [Plug calibration report](../examples/plug_calibration/reports/plug_calibration_en.html)
- [Full task demo](../index.html#demo)
- [English report](../examples/cable_calibration/reports/cable_calibration_en.html)
- [Chinese report](../examples/cable_calibration/reports/cable_calibration_zh.html)
- [Case and reproduction guide](../examples/cable_calibration/README.md)

The cable HTML reports embed their figures, plots, and styles and can also be opened directly
after download. Keep both files in the same folder for language switching. Source links
are relative to the repository, so browsing the evidence requires the surrounding checkout.

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

## Plug results and full demo

The homepage retains the RJ45 insertion results and the full task reconstruction demo.
The [plug report](../examples/plug_calibration/reports/plug_calibration_en.html) uses shared
figures in [assets/task-calibration/](../assets/task-calibration/).
[Plug evidence](../assets/task-calibration/plug-evidence.json) records the displayed metrics,
processing conditions, and original experiment hashes.

Keep the comparison scopes separate: the CAE intermediate is a retrospective offline
addition, while the real-calibrated candidate applies an equivalent force inside the
dynamics. The five development recordings pass the stated observation criteria;
numerical qualification and independent holdout validation remain open. This candidate
is not the configuration used in the full-scene replay. Junction calibration has not
started; real2sim reconstruction is available and sim2real is in progress.

The complete 55.7-second demo retains 1920×1080 resolution, 60 fps, and the original
audio stream. [Demo provenance](../assets/task-calibration/demo-provenance.json) records
source and web-file hashes. When replacing the video, preserve full duration and audio,
decode the output, and verify playback metadata before checking playback and seeking.
