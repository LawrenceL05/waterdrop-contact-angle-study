# When does learned droplet segmentation improve contact-angle measurement?

Research-gap assessment for the waterdrop-contact-angle study. Prepared 14 November 2026.

Status: literature-backed working contribution, ready for advisor review. This document completes the literature-investigation portion of Stage 1; advisor agreement and dataset feasibility remain open. No new model experiments were run for this assessment.

## Abstract

Automated contact-angle measurement already includes classical contour fitting, learned angle prediction, neural segmentation followed by geometry, and per-frame uncertainty analysis. Published work also addresses reflections, cropped droplets, and independent-video testing. Consequently, implementing U-Net or comparing it with SegFormer would provide insufficient novelty on its own. This assessment identifies a narrower candidate contribution: a controlled side-view measurement study that determines when learned segmentation provides a practically meaningful improvement over classical extraction at a given annotation budget, and when contact-region or substrate-line errors prevent that improvement. The study should hold downstream processing constant, assess unseen physical droplets or acquisition groups, and report angle errors, failed measurements, and reference uncertainty together. Existing studies support the importance of these controls, but the reviewed evidence does not settle this decision for the intended imaging setting. The resulting contribution would be empirical guidance about measurement reliability and labeling effort. It remains conditional on sufficient independent data and credible angle references.

## 1. Research brief

Scope: optical side-view images of water droplets on substrates, including reflections, uncertain substrate lines, changes in magnification, and partially visible droplets. Intended readers are reviewers in surface measurement, experimental imaging, and applied machine learning.

The literature investigation asks:

1. Which components of automated contact-angle measurement are already established?
2. What does existing validation establish about the relationship between image processing and final angle accuracy?
3. What useful, testable contribution remains feasible for this project?

The starting point is the [repository research plan](https://github.com/LawrenceL05/waterdrop-contact-angle-study/blob/main/RESEARCH_PLAN.md). Its 14-image pilot and 95.91% mean test IoU establish preliminary segmentation feasibility only. The two test images represent one held-out droplet, so they cannot establish population-level reliability or angle accuracy.

## 2. Search method and evidence boundaries

Three independent searches covered learned methods, classical measurement and uncertainty, and adversarial searches for studies already matching the proposed contribution. Follow-up searches targeted SegFormer, small training sets, learning curves, cropped droplets, interface errors, and 2026 publications. Searches used scholarly web retrieval and publisher or institutional records, including ACS, RSC, Wiley, Nature, IEEE, and Aalto's repository. Representative queries included "contact angle segmentation U-Net reflection dataset", "contact angle SegFormer", "contact angle learning curves", and "contact angle cropped measurement deep learning".

This is a targeted gap assessment, not an exhaustive systematic review. Twelve primary works inform the comparison below. Publisher and institutional full text was used where available; some papers were accessible only through abstracts or indexed excerpts. Unknown details are explicitly distinguished from absent methods. Search results that predicted wettability from chemistry without optical measurement were excluded from direct comparisons. Tomography studies were retained as adjacent methodological prior art.

| Evidence type | What it can establish | Limitation |
| --- | --- | --- |
| Analytical or synthetic known-angle images | Algorithmic errors against a specified reference | Rendering and shape assumptions limit physical realism |
| Same-image comparison with manual/software angles | Agreement under shared acquisition | Shared geometric bias can remain |
| Separate instrument or acquisition comparison | Practical measurement agreement | Different droplets, timing, and protocols can confound differences |
| Segmentation scores | Agreement with labeled masks | They do not directly establish angle accuracy |

## 3. Related-work comparison

The literature establishes most individual ingredients; the remaining opportunity concerns a controlled decision about labeling investment and final measurement quality. "Unverified" below means the accessed evidence did not settle the item, not that the original study omitted it.

| Work | Data and reference evidence | Measurement method and validation | Consequence for our contribution |
| --- | --- | --- | --- |
| Akbari & Antonini, 2021 [1] | Virtual and real droplets | Dropen compares fitting and mask approaches; automated contact-point detection can operate without mirror reflections | Generic automation and classical method comparison are established. Include a competent classical comparator. |
| Xu, 2014 [2] | Real and numerically generated water-drop profiles | Evaluates circle, ellipse, and ADSA-P fitting under noise and different conditions | A shared fitter can impose common bias; check its limits separately. |
| Vuckovac et al., 2019 [3] | Theory and experiments | Quantifies baseline-placement sensitivity, especially at high angles | Baseline uncertainty is established prior art. |
| Nurmi et al., 2025 [4] | Synthetic references and commercial-goniometer validation | Propagates edge/baseline measurement uncertainty per frame | Reporting uncertainty alone is insufficient novelty. |
| Kabir & Garg, 2023 [5] | 3,375 labeled images; comparison with ImageJ and blur tests | CNN angle estimation; examines training-set size and cropped images when the complete baseline remains visible | Robustness, some data-sufficiency analysis, and partial-visibility handling already exist. Physical-droplet split details are unverified. |
| Shumaly et al., 2023 [6] | 14,000 frames from 1,400 videos; test videos separate from training/validation; synthetic angle references | Super-resolution plus edge extraction and optimized fitting; baseline/reflection treatment | Held-out-video testing and learned preprocessing evaluated by angle accuracy are established. Train/validation mutual video independence is unverified. |
| Shaw et al., 2024 [7] | More than 7.2 million synthetic half-contours; experimental benchmark | Conan-ML, applicable above 110 degrees, incorporates roughness, gravity, image scale, and reflections | Reflection-aware learned estimation and synthetic reference angles are established; half-contours do not establish arbitrary-occlusion robustness. |
| Kumar & Chandraprakash, 2023 [8] | Nonorthogonal smartphone images; standard-goniometer comparison | EfficientNet-B4/U-Net silhouettes followed by 3D reconstruction | Segmentation followed by quantitative angle measurement is established, though the acquisition differs from ours. |
| Honkasalo, 2025 [9] | Real and synthetic sessile/pendant images; indexed thesis abstract | Compares U-Net, PSPNet, and SegFormer using Dice/IoU; SegFormer ranks highest | Direct architecture-comparison prior art. Full split, dataset-size, and angle-evaluation details remain unverified. This is a master's thesis. |
| Fischer et al., 2026 [10] | 406 images from seven campaigns, random train/validation division; separate 50-image segmentation test; manual and instrument angle comparisons | Width-scaled U-Net plus geometry in a reflective spin-coating setup; reported cross-device MAE 4.15 degrees; baseline procedure limited to angles at or below 90 degrees | Closest hybrid-pipeline threat: small-data learned segmentation plus geometric fitting under difficult optics already exists. |
| Gao et al., 2024 [11] | Multiphase X-ray images of rocks | Gradient-aware CNN segmentation followed by contact-angle measurement, emphasizing interface quality | The distinction between whole-image accuracy and physically important boundary accuracy is established in an adjacent domain. |
| Pan et al., 2026 [12] | Synthetic/physics-driven learning and sessile experiments spanning 112–163 degrees | Physics-informed autoencoders for profile-based angle and surface-tension estimation; experimental training data are unnecessary in the reported approach | Annotation efficiency must be motivated against alternatives that reduce experimental labeling requirements. Detailed split and angle-error evidence was not inspected. |

## 4. What prior work establishes

Classical measurement already offers multiple fitting choices and comparisons, while baseline-error and per-frame uncertainty studies show why fitting accuracy cannot be inferred from contour appearance alone. Together, [1–4] motivate separating segmentation, baseline placement, and fitting errors. Holding a fitting method constant is useful experimental control, but does not make that fitter physically correct for every shape.

Learned approaches span direct angle prediction, super-resolution, contour prediction, and segmentation with geometry. The different input domains in [5–8,10,12] prevent a meaningful ranking from published headline errors. In particular, the hydrophobic range in [7] and the baseline restriction in [10] illustrate why applicability limits must accompany performance comparisons. A CNN-versus-transformer comparison also needs to acknowledge the direct segmentation precedent in [9].

Global image metrics and local measurement errors have already been distinguished: [6] evaluates final angle accuracy beyond reconstructed-image quality, and [11] emphasizes contact-interface segmentation. The project can test the strength and practical consequence of this relationship in its own optical setting. It should not claim discovery of the general principle that boundary errors affect measured angles.

## 5. Proposed research gap and contribution

**Working gap:** The reviewed evidence does not yet establish, for the intended side-view water-droplet imaging setting, which segmentation approach provides the lowest reliable contact-angle error at a given labeling budget when baseline placement and angle fitting are controlled. In particular, it does not settle when global mask-score improvements translate into useful angle improvements on unseen droplets, or when local contact-region errors and baseline ambiguity dominate.

This is a bounded synthesis of the reviewed evidence, not a claim that no related benchmark exists. Its value must come from answering a practical decision: how much labeling is worthwhile, which method is reliable under which conditions, and when a measurement should be rejected or reviewed.

**Advisor-ready contribution statement:**

> We propose a controlled evaluation of classical and learned droplet segmentation for contact-angle measurement under limited annotation. Using shared downstream geometry, independent droplet or acquisition groups, and documented reference uncertainty, the study will determine how labeling effort and imaging conditions affect angle error and measurement success. It will quantify whether errors near the contact region explain outcomes better than global mask overlap and identify conditions where improved segmentation fails to improve the measurement.

This is prospective language. Results, model rankings, and numerical improvements must be established experimentally.

The following claims are already undermined by prior work: first use of U-Net for contact angles; first U-Net/SegFormer droplet comparison; first reflection-aware method; first held-out-video test; first baseline-uncertainty analysis; first small-data segmentation-plus-geometry pipeline; first observation that interface errors affect angles. Likewise, cropped-drop capability alone is insufficient because [5] already treats an incomplete drop with the baseline fully visible.

## 6. Experiments that would resolve the gap

| Question | Required comparison | Useful outcome, including a negative result |
| --- | --- | --- |
| When is learned segmentation worth labeling? | Classical extraction, specified U-Net, and specified SegFormer on nested training sets grouped by independent droplet; repeated seeds; fixed validation/test groups | Learning curves identify a useful improvement threshold, or show classical extraction remains competitive. Record actual annotation minutes where possible. |
| Does mask ranking predict measurement ranking? | Paired IoU/Dice, local contact-region boundary errors, angle MAE/bias, and failure rate on identical examples | Quantifies whether global mask ranking transfers to measurement; rank reversal is a hypothesis, not an assumed result. |
| What limits improvement? | Reference-mask and reference-baseline diagnostic runs; controlled baseline displacement and tilt; a small fitter-sensitivity check | Separates front-end errors from baseline/fitter limitations. Reference-mask results are a diagnostic ceiling, not absolute physical truth. |
| Which conditions are reliable? | Prespecified strata for reflection, contrast/blur, magnification, angle range, and partial visibility; genuine condition holdouts when data permit | Establishes a bounded operating range and explicit failure criteria. |

The primary endpoint should be angle error in degrees against a justified reference, accompanied by success rate. Report errors on successful measurements with their denominator; otherwise a method can appear accurate by failing on difficult cases. Select the practically meaningful angle tolerance before final testing. Confidence intervals and resampling should use the independent experimental unit, not treat adjacent frames or two sides of a droplet as independent samples.

For partial views, distinguish a missing apex or opposite side from a missing contact point. A visible-side angle requires sufficient local interface and substrate evidence. A missing contact region is a different inference problem and should be excluded or explicitly marked unmeasurable unless a validated shape assumption supports reconstruction. Synthetic cropping is a controlled stress test, not proof of generalization to naturally obstructed acquisitions.

Add synthetic known-angle images to test geometry, while retaining a real-image reference protocol with repeat annotations and independent checks. Agreement with an angle computed from a corrected mask using the same fitter supports pipeline agreement; it does not independently establish physical accuracy. Imaging resolution and reference disagreement may limit how small an improvement can be interpreted.

## 7. Feasibility, counterarguments, and remaining decisions

The strongest reviewer objection is that combining familiar components is incremental. Answering it requires adequate independent coverage, controlled comparisons, and a useful empirical conclusion about labeling effort or failure mechanisms. An attractive pipeline diagram and a slightly higher IoU would not establish this contribution.

An additional risk is that a fixed fitter disadvantages a method that was designed with its own backend. Keep the controlled comparison as the primary segmentation experiment, and describe its scope explicitly. Where resources permit, include an established complete measurement pipeline as a secondary practical reference; choose it according to the dataset's actual angle range and imaging assumptions.

The current pilot is too small to resolve these questions. The next stage must count independent droplets, specimens, sessions, and magnifications; establish visible contact-region coverage; and assess whether meaningful label-budget subsets and held-out groups are possible. Do not invent a target image count before this inventory. If independent coverage remains limited, narrow the paper to a feasibility study with appropriately limited claims.

Remaining literature work before submission: inspect Honkasalo's full thesis; verify supplementary evaluation details and implementation availability for the closest methods; refresh the search; and have the advisor assess whether the scoped measurement question is valuable for the target venue. These are limitations of the current gap assessment, not evidence that the proposed contribution is absent from the literature.

## 8. Conclusion

RQ1: Automation, neural segmentation, U-Net/SegFormer comparisons, reflection handling, video-independent testing, and uncertainty analysis are established individually.

RQ2: Existing validation demonstrates the importance of acquisition conditions, reference quality, contact-region fidelity, and baseline/fitting assumptions. Published results use different domains and protocols and cannot establish a universal best method for our setting.

RQ3: The strongest candidate contribution is an empirical measurement study of when labeling and segmentation choices improve reliable contact-angle estimates on independent droplets. The literature supports pursuing this question; its novelty and feasibility remain bounded by the stated search limitations and the forthcoming dataset audit.

## References

1. R. Akbari and C. Antonini. "Contact angle measurements: From existing methods to an open-source tool." Advances in Colloid and Interface Science 294, 102470 (2021). [Publisher](https://doi.org/10.1016/j.cis.2021.102470).
2. Z. N. Xu. "An algorithm for selecting the most accurate protocol for contact angle measurement by drop shape analysis." Review of Scientific Instruments 85, 125107 (2014). [Publisher](https://doi.org/10.1063/1.4903198).
3. M. Vuckovac et al. "Uncertainties in contact angle goniometry." Soft Matter 15, 7089–7096 (2019). [Publisher](https://pubs.rsc.org/en/content/articlehtml/2019/sm/c9sm01221d).
4. H. A. Nurmi et al. "In situ error analysis in contact angle goniometry." Soft Matter 21, 2422–2429 (2025). [Publisher](https://doi.org/10.1039/d4sm01509f).
5. H. Kabir and N. Garg. "Machine learning enabled orthogonal camera goniometry for accurate and robust contact angle measurements." Scientific Reports 13, 1497 (2023). [Full text](https://pmc.ncbi.nlm.nih.gov/articles/PMC9883237/).
6. S. Shumaly et al. "Deep Learning to Analyze Sliding Drops." Langmuir 39, 1111–1122 (2023). [Publisher](https://doi.org/10.1021/acs.langmuir.2c02847).
7. D. G. Shaw et al. "Accurate and Robust Static Hydrophobic Contact Angle Measurements Using Machine Learning." Langmuir 40, 16757–16770 (2024). [Publisher](https://doi.org/10.1021/acs.langmuir.4c01050).
8. A. Kumar and C. Chandraprakash. "Computer Vision-Based On-Site Estimation of Contact Angle From 3-D Reconstruction of Droplets." IEEE Transactions on Instrumentation and Measurement 72, 2524108 (2023). [Publisher](https://ieeexplore.ieee.org/document/10221781/).
9. M. Honkasalo. "AI-based droplet detection." Master's thesis, Aalto University (2025). [Institutional record](https://aaltodoc.aalto.fi/handle/123456789/138027).
10. S. Fischer, M. Hiegle, and H. Röhm. "In Situ Contact Angle Measurement for Autonomous Spin Coating in Self-Driving Labs." Advanced Intelligent Discovery, e70139 (2026). [Publisher](https://doi.org/10.1002/aidi.70139).
11. Y. Gao et al. "Gradient Information Enhanced Image Segmentation and Automatic In Situ Contact Angle Measurement Applied to Images of Multiphase Flow in Porous Media." Water Resources Research 60, e2023WR036869 (2024). [Publisher](https://doi.org/10.1029/2023WR036869).
12. C. Pan et al. "Robust measurement of surface tension and contact angle using physics-informed autoencoders." Colloids and Surfaces A 730, 138972 (2026). [Publisher](https://www.sciencedirect.com/science/article/pii/S0927775725028766).
