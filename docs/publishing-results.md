# Publishing calibration results

The repository contains a static GitHub Pages site. It needs no Python, Newton, Node, or simulation at serving time.

## One-time repository setting

After the files are pushed, a repository administrator or maintainer enables publication:

1. Open [repository Pages settings](https://github.com/SamdianJ/TaskTuning/settings/pages).
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select **main** and **/(root)**, then save.
4. Wait for the **pages build and deployment** run in [Actions](https://github.com/SamdianJ/TaskTuning/actions) to finish.
5. Open [the results homepage](https://samdianj.github.io/TaskTuning/).

The files alone do not enable Pages. SSH push access does not provide permission to change Pages settings through the REST API. Before enablement and the first successful deployment, the site links may return 404.

GitHub documents this setup in [Configuring a publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site). The root `.nojekyll` file selects static serving without Jekyll processing; `index.html` provides the homepage. Subsequent pushes to main trigger publication through GitHub's branch deployment mechanism; no custom workflow is required.

## Public entry points

- [Results homepage](https://samdianj.github.io/TaskTuning/) — cable, plug, junction roadmap, and full demo
- [Plug result preview](https://samdianj.github.io/TaskTuning/#plug)
- [Plug calibration report](https://samdianj.github.io/TaskTuning/examples/plug_calibration/reports/plug_calibration_en.html)
- [Calibration pipeline](https://samdianj.github.io/TaskTuning/pipeline.html) — six-stage workflow, ten members, skills and agent integration
- [Full task demo](https://samdianj.github.io/TaskTuning/#demo)
- [English report](https://samdianj.github.io/TaskTuning/examples/cable_calibration/reports/cable_calibration_en.html)
- [Chinese report](https://samdianj.github.io/TaskTuning/examples/cable_calibration/reports/cable_calibration_zh.html)

The cable reports retain their existing paths and language switch. Source references link to GitHub so Markdown and JSON evidence remain accessible from the website. Cable figures/styles are embedded for offline reading; source references need internet access. The plug report uses shared figures in `assets/task-calibration/` and links back to the homepage.

## Update the preview

The PNG preview is derived from archived values, not a fresh simulation or a hand-drawn result. Regenerate it from the repository root:

```bash
python -m pip install matplotlib
python -m examples.cable_calibration.verify
python -m examples.cable_calibration.render_preview
```

Matplotlib is only a preview-generation dependency, not a core or deployed-site dependency. The renderer reads processed observations, archived traces, and expected metrics. It plots the no-plug coordinate RMSE for A/B/B*/C and the measured/predicted z coordinate at 150 mm along the cable, using the scoring mask.

Keep uncertainty and acceptance statements when updating figures: A → B is not an angle-only ablation; B* and C share the dynamic objective; plugged validation remains unresolved. Update report export hashes in archive/provenance.json whenever an HTML report changes.

## Local preview and checks

From the repository root:

```bash
python -m http.server 8000 --bind 127.0.0.1
```

Visit `http://127.0.0.1:8000/`. Check the desktop and narrow layouts, both language links, chart toggles in the report, and source links to GitHub. Stop the server when finished.

After pushing, confirm the Pages deployment succeeds and check the homepage, both reports, and preview image over HTTPS. A successful Git push alone does not prove the website is live.

## Plug results and full demo

The homepage shows the final local RJ45 insertion result, with a two-panel force comparison and a link to `examples/plug_calibration/reports/plug_calibration_en.html`. The separate report holds the calibration method, CAE comparison, model parameters and validation details. Evidence is through 19 October 2026, with project status updated on 27 October. `assets/task-calibration/plug-evidence.json` records the displayed metrics and SHA-256 hashes of the experiment sources. The two technical PNG figures are copied from the archived CAE comparison and latest timestep-refinement report. `plug-final-preview.png` shows only the final axial/lateral simulation against the five real recordings; its processing and source hashes are recorded in the evidence summary.

Keep the comparison scopes separate: the CAE intermediate is a retrospective offline addition, while the real-calibrated candidate applies an equivalent force inside the dynamics. The five development recordings pass the stated observation criteria; numerical qualification and independent holdout validation remain open. The latest local force candidate is not the configuration used in the full-scene replay. Junction calibration has not started; real2sim reconstruction is available and sim2real is in progress.

`synopsys-demo-v6.mp4` is the complete 55.7-second source demo transcoded to H.264 CRF 22 with fast-start metadata. It retains 1920×1080, 60 fps, and the original AAC audio stream. `demo-provenance.json` records source and web-file hashes. The page uses native playback controls, no autoplay, a poster, and a download link. To replace the demo, preserve full duration and audio, decode the entire output to check it, verify the playback metadata, then check the published MP4 response and byte-range support.

## Agent-driven calibration pipeline

The homepage `#pipeline` section introduces the outer-agent / inner-runtime responsibilities and links to `pipeline.html`. The detail page adapts the supplied `newton-calibration-seed/index_en.html` design, retaining its six-stage selector, qualification-mode selector, ten-member reference, five-skill routing and agent integration contract. It is a documentation update only; runtime implementation and experiment acceptance statuses are unchanged.

The English detail page links back to this results site and its cable/plug reports. Supporting Markdown guides and skills open the public repository; source-code and unavailable companion-page links are not carried over. The design snapshot can be newer than the published runtime baseline. Check all six stage buttons, previous/next boundaries, both qualification modes and cross-page anchors when validating changes.
