# Research plan

Updated 2026-11-16.

## Submission goal

Prepare a journal or conference submission comparing classical computer vision, U-Net, and SegFormer for water-droplet contact-angle measurement. The working framing is an experimental evaluation paper. The target venue, deadline, and final novelty claim will be selected with the advisor after reviewing related work and dataset coverage.

## Central question

When does learned droplet segmentation improve contact-angle measurement, and which errors still limit accuracy?

### Research questions

1. **Accuracy.** How do classical vision, U-Net, and SegFormer compare in contact-angle error on unseen droplets?
2. **Failure modes.** How do reflections, uncertain substrate lines, magnification, and partially visible droplets affect each method?
3. **Annotation efficiency.** How much hand-labeled data is needed before a learned method provides a meaningful improvement?

## Starting evidence

The earlier WaterDropML U-Net pilot used 14 distinct images, with nine training images, three validation images, and two test images. The two test images represent one held-out droplet. Mean test IoU was 95.91%. This establishes preliminary segmentation feasibility. Contact-angle accuracy and performance across independent droplets remain to be measured.

Some pilot annotations extend below the contact line. Review these before using them as reference labels. Previously inspected pilot examples should be identified as development data when designing the final evaluation.

[Earlier training report](https://github.com/LawrenceL05/WaterDropML/blob/main/outputs/handcorrected_20261108/README.md)

## Current status — 2026-11-16

The working paper format is an **original experimental evaluation**, supported by a literature review. A review-only paper would need a different plan and would not require the proposed model experiments or data collection. Final scope and venue remain for advisor agreement.

- The [working gap assessment](RESEARCH_GAP.md) identifies the contribution as determining when learned segmentation improves reliable angle measurements enough to justify labeling effort, and when contact-region or substrate-line errors limit that improvement. Architecture comparison alone is insufficient novelty.
- The supplied archive has 78 images: 59 Main images in 16 named droplet groups, plus 19 original Test-folder images with unresolved identities. [Inventory and coverage](data/inventory/README.md).
- Image IDs IMG001–IMG078 and named-group IDs D001–D016 are assigned. No exact-file or identical-pixel duplicate sets were found.
- Physical-droplet, specimen and acquisition-session independence remain unconfirmed. Establish whether droplet numbers represent fresh deposition at each time or the same droplets followed over time.
- All filenames carry 2026-10-15. That date alone does not establish acquisition-session count. The original Test folder does not define an approved model holdout.
- The earlier 14-image pilot and the current archive must not be summed as independent datasets without checking overlap.
- Immediate work is a representative development annotation batch and annotation protocol, followed by reference measurements and a classical baseline. [Prioritized TODO list](TODO.md).

### Next collection milestone

There are two named groups in each of eight treatment/time cells. A practical next pilot milestone is five fresh physical droplets per cell: 40 total, requiring 24 more if the current 16 groups are physically distinct. This is a provisional collection milestone, not a powered final sample size or publication-readiness guarantee.

Collect across independently logged sessions and specimens, using the same view protocol for both treatments. Include a whole-droplet view with both contact regions plus useful close-ups. Final training budgets and test-group counts depend on credible reference angles, observed variability, required precision and condition coverage. Multiple views and two sides of a droplet are correlated observations.

## Work plan and completion criteria

| Stage | Work | Deliverable and completion criterion |
| --- | --- | --- |
| 1. Establish the research gap | Review classical and learned contact-angle measurement studies. Compare datasets, reference measurements, angle estimators, failure handling, and evaluation protocols. | Verified related-work table and an advisor-reviewed contribution statement. |
| 2. Audit the dataset | Count independent droplets, specimens, sessions, treatments, and magnifications. Identify duplicate images, repeated views, and missing metadata. | Dataset manifest and coverage table with the independent sampling unit explicitly defined. |
| 3. Define reference measurements | Specify substrate lines, contact points, droplet boundaries, visible-side angle definitions, and exclusions. Have a second annotator independently review a subset and quantify disagreement. | Annotation protocol, adjudication rules, reference-quality report, and a justified procedure for reference angles. |
| 4. Freeze evaluation | Group related observations into the same split. Choose validation and final test groups before model selection. Define failure criteria, metrics, uncertainty estimates, and meaningful angle-error thresholds. | Versioned split files and evaluation protocol reviewed before final experiments. |
| 5. Run controlled comparisons | Compare classical vision, U-Net, and a specified SegFormer variant. Use the same labeled data and record preprocessing, pretrained weights, tuning budgets, seeds, and checkpoints. | Reproducible main-results table, configurations, logs, and checkpoints. |
| 6. Explain results | Analyze conditions, labeling budgets, contact-point boundary errors, and the relationship between IoU and angle error. | Failure taxonomy, ablations, and figures tied to the research questions. |
| 7. Write and package | Draft from completed results and build scripts that reproduce every reported table and figure. | Manuscript, supplement, reproducibility package, and advisor/coauthor review. |

Stages are ordered by dependencies. Calendar dates and final dataset targets will be assigned after the audit and venue decision.

## Experimental design

### Controlled comparison

Hold orientation correction, substrate estimation, and downstream angle fitting constant across the three segmentation approaches in the main experiment. This isolates the effect of segmentation.

Evaluate substrate-line uncertainty separately using a reference baseline or controlled baseline perturbations. Report the baseline procedure used for each result. Verify the angle-fitting convention and its behavior for partial views before interpreting numerical errors.

### Independence and splits

- Keep all views and magnifications of the same physical droplet in one split.
- Audit dependence between droplets from the same specimen or acquisition session. Match the split unit to the intended generalization claim.
- Use validation data for tuning and checkpoint selection.
- Reserve final test groups for the frozen protocol. Record any earlier inspection or use of candidate test images.
- Determine the number of independent test groups from coverage and desired uncertainty after the audit. Image count alone does not establish sample size.

### Reference quality

Define how an independent reference angle is obtained and its uncertainty. An angle generated by the same fitting procedure from a corrected mask measures agreement with that procedure. Support physical accuracy claims with a justified independent measurement or reference protocol.

Review the droplet rim, substrate intersection, reflected regions, and partial views consistently. Quantify inter-annotator differences in both boundaries and angles on a subset.

### Metrics

| Role | Metrics and reporting |
| --- | --- |
| Primary | Absolute contact-angle error in degrees, signed bias, and measurement success rate. |
| Secondary | Mask IoU and Dice, boundary error near contact points, and processing time on specified hardware. |
| Reliability | Variation across training seeds and uncertainty estimated using independent droplets or experimental groups. |
| Partial views | Error on visible contact angles, explicit missing-side records, and coverage counts. |
| Failures | Predefined reasons and denominators. Report error on valid measurements alongside success rate. |

Use paired comparisons on the same test examples. Account for multiple views and two contact angles from the same droplet when estimating uncertainty. Select an application-relevant error tolerance with the advisor before final testing.

### Annotation-efficiency experiment

Train on nested subsets of labeled training droplets while keeping validation and test groups fixed. Compare learning curves across multiple seeds and record annotation effort where available. Choose subset sizes after the independent-droplet inventory is known.

### Proposed experiment matrix

| Experiment | Research question | Main output |
| --- | --- | --- |
| Shared-pipeline comparison of the three methods | RQ1 | Angle errors, success rates, and segmentation metrics |
| Results by reflection, magnification, partial view, and acquisition condition | RQ2 | Condition-specific errors and failure taxonomy |
| Substrate-line sensitivity | RQ2 | Change in angle error under baseline perturbation |
| Labeling-budget learning curves | RQ3 | Performance versus independent labeled droplets |
| Segmentation-to-angle relationship | RQ1 and RQ2 | IoU and local boundary errors compared with angle errors |

These are planned analyses. Model rankings and improvement claims will follow the measured results.

## Manuscript outline

1. **Introduction.** Measurement motivation, a concrete failure example, verified research gap, research questions, and supported contributions.
2. **Related work and task definition.** Prior approaches, angle conventions, imaging setting, and intended generalization.
3. **Dataset and reference annotations.** Collection, independent groups, annotation rules, quality checks, and splits.
4. **Methods and evaluation protocol.** Three segmentation methods, shared processing, training settings, metrics, and statistical analysis.
5. **Results.** Overall accuracy, failure conditions, baseline sensitivity, and annotation efficiency.
6. **Discussion and limitations.** Reference uncertainty, dataset coverage, practical implications, and remaining failure modes.
7. **Conclusion.** Findings supported by the completed experiments.

### Introduction logic

Move from the measurement application and a concrete example to the literature-supported evaluation gap, then the three research questions. Explain why the protocol requires independent groups, trustworthy angle references, and shared downstream processing. Introduce the study and state contributions supported by the final evidence.

### Candidate contributions to establish

- A documented dataset and reference protocol for contact-angle evaluation, supported by Section 3.
- A reproducible comparison that isolates segmentation effects and measures final angle accuracy, supported by Sections 4 and 5.
- Evidence about failure conditions and annotation requirements, supported by Sections 5 and 6.

### Planned figures and tables

- A motivating image showing how boundary or baseline differences affect a contact angle.
- A shared processing and evaluation pipeline.
- Dataset coverage and split statistics.
- A related-work comparison table.
- The main accuracy and success-rate table.
- Angle-error distributions and paired method comparisons.
- Annotation-efficiency curves and representative failure overlays.

## Journal or conference readiness

- [ ] Confirm venue, audience, deadline, and author responsibilities with the advisor.
- [ ] Verify the literature gap and all references.
- [ ] Complete dataset provenance, coverage, and independence audit.
- [ ] Establish reference-angle quality and annotator agreement.
- [ ] Freeze splits, failure rules, metrics, and model-selection procedures.
- [ ] Run all three methods under the documented protocol.
- [ ] Quantify uncertainty and report failed measurements.
- [ ] Connect every contribution claim to an experiment or documented artifact.
- [ ] Review code and data release permissions and licenses.
- [ ] Package configurations, environment versions, checkpoints, and executable evaluation scripts.
- [ ] Check the selected venue's formatting, anonymization, and submission requirements.
- [ ] Complete advisor/coauthor review.

The immediate priorities are a representative development annotation batch and protocol, resolution of physical-droplet identities, credible angle references, and a classical baseline. See [TODO.md](TODO.md) for ordered actions and unresolved decisions.
