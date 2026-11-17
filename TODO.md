# Research TODO

Updated 2026-11-16. Working format: original experimental evaluation with a supporting literature review. Advisor approval of scope and venue is pending.

## Completed

- [x] Prepare the [literature-backed working gap assessment](RESEARCH_GAP.md), with close prior work and evidence limitations.
- [x] Inspect Contact angle.zip and verify that all 78 image files decode.
- [x] Assign IMG001–IMG078 and D001–D016 using the user-confirmed filename convention.
- [x] Inventory 59 Main images, 19 original Test-folder images and magnification coverage.
- [x] Check exact-file and identical-pixel duplicates: no duplicate sets found.
- [x] Produce local ID-labeled previews, five contact sheets and an editable inventory, preserving original image bytes.
- [x] Record the portable [manifest](data/inventory/image_manifest.json) and [audit summary](data/inventory/audit_summary.json).
- [x] Define a conditional next pilot milestone: 24 additional fresh droplets to reach five per treatment/time cell if the current 16 groups are independent.

## Existing implementation and recorded results

- [x] Implement the classical pipeline and record 59 Main-image rows, including 57 circle estimates and two failures.
- [x] Record initial QC for all 59 Main images: 14 good, 12 fixable and 33 bad.
- [x] Prepare a 15-image annotation candidate list and three corrected masks in the supplied local checkout.
- [x] Implement U-Net data preparation, training, prediction and evaluation, with a Colab notebook.
- [x] Record the three-image corrected-label pilot and distinguish it from the expanded 14-image run documented on GitHub.
- [x] Implement contact-angle photo plotting in the local working copy. This change remains uncommitted and needs validation and publication.
- [ ] Validate the plotting geometry and publish the local implementation change in WaterDropML after review.
- [ ] Reconcile local and remote annotation/run manifests, including image overlap, label versions and prior development exposure.
- [ ] Confirm that the project degree of completion reflects the [implementation snapshot](RESEARCH_PLAN.md#implementation-snapshot-from-the-supplied-waterdropml-folder). Existing mask scores do not establish angle accuracy.

## 1. Next: annotation protocol and representative batch

- [ ] Select development images covering both treatments, all four times, magnifications, full/partial views and difficult optics.
- [ ] Review selected images at full resolution for orientation, focus, substrate evidence and visible contact regions.
- [ ] Define the visible-liquid segmentation target and consistent rules for reflections, highlights, image boundaries and liquid below the substrate.
- [ ] Specify substrate-line, contact-point and droplet-boundary annotations, left/right angle conventions and units.
- [ ] Define visible-side measurability and rejection rules when contact-region evidence is missing.
- [ ] Agree with the advisor on credible reference angles and their uncertainty. Distinguish same-fitter agreement from independent physical accuracy.
- [ ] Manually annotate the batch; independently repeat a subset to estimate boundary, baseline and angle disagreement.
- [ ] Document ambiguous cases and adjudication before expanding labeling.
- [ ] Validate the existing classical baseline against agreed reference angles. Record angle error, signed bias, success rate and failure reasons. Re-run after freezing label conventions and any code changes.

## 2. Resolve provenance and independence

- [ ] Confirm fresh deposition at each time versus repeated observations of the same droplets.
- [ ] Assign verified physical-droplet, specimen and acquisition-session IDs; link repeated times where applicable.
- [ ] Resolve the identities and intended role of the 19 Test-folder images.
- [ ] Verify acquisition metadata rather than treating one filename date as a session count.
- [ ] Reconcile images and annotation versions from both the three-image pilot and expanded 14-image run. Record prior development/tuning exposure.
- [ ] Record substrate material, treatment protocol, timing definition, camera settings and calibration.
- [ ] Complete full-resolution contact-region eligibility review. Contact sheets do not establish angle-reference precision.

## 3. Collect the next pilot batch

- [ ] If current groups are physically distinct, collect three fresh droplets per treatment/time cell: 24 more and 40 total.
- [ ] If time points are repeated observations, revise the count and design using verified physical units.
- [ ] Spread collection across independently logged sessions and specimens.
- [ ] Capture a whole-droplet view with both contact regions plus useful close-ups.
- [ ] Match magnification/view protocols across treatments; A currently has no 20× images.
- [ ] Use reference-angle variability and desired precision to determine final sample size. Forty is a pilot milestone, not a final adequacy claim.

## 4. Freeze evaluation and compare methods

- [ ] Select a meaningful angle-error tolerance and required uncertainty with the advisor.
- [ ] Reuse the existing U-Net implementation after review. Specify the SegFormer variant, pretrained weights, tuning budgets, seeds and annotation-time recording.
- [ ] Implement SegFormer and connect its masks to the same downstream geometry before the controlled comparison.
- [ ] Freeze training/validation/final-test groups before model selection. Keep all times, views, magnifications and both sides of a physical droplet together.
- [ ] Use specimen/session grouping when required by the generalization claim; document previously inspected development examples.
- [ ] Hold orientation correction, substrate estimation and downstream angle fitting constant across the main comparison.
- [ ] Validate fitting conventions on known-angle synthetic profiles and check baseline/fitter sensitivity separately.
- [ ] Evaluate classical extraction, U-Net and SegFormer on identical examples.
- [ ] Report angle MAE, signed bias, measurement success/failure rates and denominators with grouped uncertainty.
- [ ] Report IoU/Dice and local contact-region boundary errors alongside final angle outcomes.
- [ ] Run nested label-budget learning curves with fixed validation/test groups and repeated seeds.
- [ ] Analyze conditions where better masks do or do not improve measured angles.

## 5. Advisor review and manuscript

- [ ] Agree on format, contribution, venue, timeline and responsibilities.
- [ ] Review the gap assessment and unresolved full-text/supplementary details of close prior work.
- [ ] Confirm that independent data coverage and reference quality support the intended claims.
- [ ] Refresh the literature before submission and verify final references.
- [ ] Draft rankings, results and contributions only after experiments establish them.
- [ ] Package provenance, annotation protocol, splits, configurations, environments and reproducible tables/figures.
- [ ] Review data release permissions, licenses and venue requirements.

A new photograph, magnification or angle is not automatically a new independent droplet. D001–D016 currently identify filename groups. The inventory establishes no new accuracy ranking, physically independent sample count or statistically powered final requirement.
