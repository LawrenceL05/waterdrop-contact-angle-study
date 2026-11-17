# waterdrop-contact-angle-study

Paper workspace for comparing classical computer vision, U-Net, and SegFormer for water-droplet contact-angle measurement.

The working format is an original experimental evaluation supported by a literature review. The study asks when learned segmentation improves reliable angle measurement enough to justify labeling effort, using shared downstream geometry and independent groups. Scope, target venue and deadline remain subject to advisor agreement.

- [Research plan](RESEARCH_PLAN.md): questions, experiments, metrics and manuscript structure.
- [Research-gap assessment](RESEARCH_GAP.md): related work, bounded novelty and limitations.
- [Current TODO list](TODO.md): completed work and ordered next actions.
- [Dataset inventory](data/inventory/README.md): 78 image IDs, 16 named groups and unresolved independence questions.

## Current implementation

The supplied WaterDropML working copy has a classical baseline for 59 Main images, completed initial QC, three corrected masks, a 15-image annotation candidate list, and a U-Net pipeline with a recorded three-image pilot. WaterDropML on GitHub also documents an expanded 14-image run. The [research plan](RESEARCH_PLAN.md#starting-evidence) records both runs separately and explains their limits.

Contact-angle photo plotting is implemented locally but remains uncommitted in WaterDropML. SegFormer, independent angle references, and the final controlled evaluation remain planned.

Updated 2026-11-16. This update records existing implementation and evidence. It establishes no new model ranking or contact-angle accuracy result.
