# Contact-angle dataset inventory

Audit date: 2026-11-16. Source: user-provided Contact angle.zip, identified by SHA256 in [audit_summary.json](audit_summary.json). ID labels are not segmentation annotations.

## Counts

| Quantity | Count |
| --- | ---: |
| All images | 78 |
| Main sample images | 59 |
| Named Main droplet groups | 16 |
| Original Test-folder images | 19 |
| 20× Main images | 7 |
| 30× Main images | 24 |
| 50× Main images | 28 |
| Image dimensions | 2880 × 2160 |

All images decode. No exact-file or identical-pixel duplicate sets were found. Different pictures of one physical droplet remain correlated.

The archive contains no reference masks or reference contact-angle measurements. All filenames carry 2026-10-15; this does not establish the acquisition-session count.

## IDs and user-confirmed naming

IMG001–IMG059 map Main images; IMG060–IMG078 map original Test-folder images. D001–D016 identify named Main groups, with physical independence across time/specimens unresolved.

- A: without UVO. B: with UVO.
- Time codes: 1 = 0 min, 2 = 30 min, 3 = 60 min, 4 = 180 min.
- Subsequent tokens: droplet number, magnification, optional shot sequence.
- Original Test-folder images have unresolved treatment/time/droplet identities.

Example: 20261015_A1_1_50_2.jpg maps to IMG003 and D001: without UVO, 0 min, droplet 1, 50×, shot 2. [image_manifest.json](image_manifest.json) preserves all mappings and original-image SHA256 values.

## Named groups

| Group ID | Filename group | Treatment | Time (min) | Droplet number | Images | Magnifications (×) |
| --- | --- | --- | ---: | ---: | ---: | --- |
| D001 | 20261015_A1_1 | Without UVO | 0 | 1 | 3 | 30, 50 |
| D002 | 20261015_A1_2 | Without UVO | 0 | 2 | 3 | 30, 50 |
| D003 | 20261015_A2_1 | Without UVO | 30 | 1 | 3 | 30, 50 |
| D004 | 20261015_A2_2 | Without UVO | 30 | 2 | 3 | 30, 50 |
| D005 | 20261015_A3_1 | Without UVO | 60 | 1 | 3 | 30, 50 |
| D006 | 20261015_A3_2 | Without UVO | 60 | 2 | 3 | 30, 50 |
| D007 | 20261015_A4_1 | Without UVO | 180 | 1 | 3 | 30, 50 |
| D008 | 20261015_A4_2 | Without UVO | 180 | 2 | 3 | 30, 50 |
| D009 | 20261015_B1_1 | With UVO | 0 | 1 | 4 | 20, 30, 50 |
| D010 | 20261015_B1_2 | With UVO | 0 | 2 | 1 | 30 |
| D011 | 20261015_B2_1 | With UVO | 30 | 1 | 5 | 20, 30, 50 |
| D012 | 20261015_B2_2 | With UVO | 30 | 2 | 5 | 20, 30, 50 |
| D013 | 20261015_B3_1 | With UVO | 60 | 1 | 5 | 20, 30, 50 |
| D014 | 20261015_B3_2 | With UVO | 60 | 2 | 5 | 20, 30, 50 |
| D015 | 20261015_B4_1 | With UVO | 180 | 1 | 5 | 20, 30, 50 |
| D016 | 20261015_B4_2 | With UVO | 180 | 2 | 5 | 20, 30, 50 |

## Coverage and measurement limits

Each treatment/time combination contains two named groups. A groups have 30× and 50× images; the seven 20× files occur in B groups. Future collection should use a matched view/magnification protocol across treatments.

Contact-sheet inspection shows reflections, very flat B-condition profiles and many one-sided close-ups. Many 50× views crop the opposite side. A visible-side angle needs its own contact region and sufficiently supported substrate line; a missing opposite contact point must not be invented.

IMG031 and IMG047 needed the opposite preview rotation to appear upright. Original bytes remain unchanged. Verify orientation before geometric analysis.

The original Test folder is not an approved model holdout. Establish identities, provenance and prior use before defining splits. Full-resolution contact-point precision and angle-reference quality remain to be assessed.

## Independence and collection decision

Confirm whether droplet numbers denote fresh deposition at each time or the same physical droplets followed across time. Keep all related times, views and magnifications together when splitting. Add specimen/session grouping as required by the generalization claim.

The named-group count is 16; the confirmed independent physical-droplet count is unknown.

A practical next pilot milestone is five fresh droplets per treatment/time cell: 40 total. If the current 16 groups are physically distinct, collect three more per cell, or 24 additional droplets. This is a planning target, not a statistically powered final requirement or a guarantee of adequate training/test coverage.

Use independently logged sessions and specimens, and capture a wider view with both contact regions plus useful close-ups. Final sample size depends on reference quality, measured error variability, required precision, failure rates, clustering and condition coverage. [NIST sample-size guidance](https://www.itl.nist.gov/div898/handbook/prc/section2/prc222.htm)

## Artifacts and reproducibility

The original archive, byte-preserving ID-prefixed image copies, ID-labeled review previews, five contact sheets and editable workbook were produced locally during the audit. The repository records the portable text manifest and summary, using original filenames and archive-relative metadata rather than machine-specific paths.

No retraining or new angle-accuracy experiment is established by this audit. [Next tasks](../../TODO.md).
