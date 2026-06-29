6MRR metric interpretation and candidate triage

Purpose

This note summarizes how the main metrics in the 6MRR fixed-backbone redesign benchmark should be interpreted.

The goal is not to claim experimental protein design success. The goal is to evaluate whether ProteinMPNN-designed sequences are predicted by ColabFold/AlphaFold2 to recover the intended 6MRR chain A backbone.

RMSD

RMSD measures the coordinate difference between the predicted structure and the reference structure.

In this project, the key value is C-alpha RMSD between each predicted rank-001 structure and the deduplicated 68-residue 6MRR chain A reference.

RMSD is the most important metric for this fixed-backbone self-consistency benchmark because it directly tests whether the designed sequence folds back close to the intended backbone.

A low RMSD supports backbone recovery. A high RMSD suggests that the predicted structure does not match the intended input backbone well.

However, RMSD does not prove experimental stability, expression, solubility, binding, or biological function.

pLDDT

pLDDT is AlphaFold/ColabFold’s local confidence score for the predicted structure.

It reflects how confident the model is about the local residue-level geometry of its prediction.

A high pLDDT means the model is relatively confident in the local structure. A low pLDDT means the prediction is less reliable or may contain uncertain/flexible regions.

However, pLDDT does not directly measure thermodynamic stability or biological function. It also does not directly tell whether the prediction matches the intended backbone.

A design can have high pLDDT but poor RMSD if AlphaFold confidently predicts a structure that is different from the target backbone.

PAE

PAE stands for predicted aligned error.

It estimates how uncertain AlphaFold/ColabFold is about the relative position of one residue or structural region compared with another.

PAE is useful for judging whether the relative arrangement of different parts of a structure is reliable.

It is not simply pLDDT in another unit. pLDDT describes local confidence, while PAE describes confidence in relative positioning between residues or regions.

PAE does not directly prove target-backbone recovery. It should be interpreted together with RMSD, pLDDT, and the structure itself.

pTM

pTM is a predicted TM-score-like confidence metric for the overall fold or topology.

A higher pTM suggests that AlphaFold/ColabFold is more confident in the global structure.

However, pTM does not directly compare the predicted structure to the intended 6MRR backbone. For fixed-backbone recovery, RMSD is still required.

ProteinMPNN score

The ProteinMPNN score reflects how plausible or likely a designed sequence is under the ProteinMPNN model given the input backbone.

In general, lower ProteinMPNN scores are better.

A favorable MPNN score suggests that the sequence is more compatible with the given backbone according to the ProteinMPNN model.

However, MPNN score alone does not prove that the sequence will fold into the intended structure. It is a design-stage score, not a final validation metric.

If the MPNN score is weak, it may mean that the sequence is less natural or less compatible with the backbone under the model. It does not by itself prove whether the sequence or backbone is biologically invalid.

Why multiple metrics are needed

No single metric proves that a designed protein is good.

RMSD checks predicted backbone recovery.

pLDDT checks local prediction confidence.

PAE checks uncertainty in relative residue or region placement.

pTM checks global fold confidence.

MPNN score checks sequence plausibility under the backbone-conditioned design model.

Together, these metrics provide a candidate triage system. They help decide which designs are worth keeping, which are backup candidates, and which should be lower priority.

They do not replace wet-lab validation.

Candidate triage logic

A simple triage scheme for this project is:

* LEAD: low RMSD and good AF2 confidence
* BACKUP: acceptable RMSD but weaker confidence or lower priority
* LOWER_PRIORITY: poor RMSD, weak confidence, or inconsistent metric support

Suggested rule:

* LEAD: RMSD < 1.2 Å and mean pLDDT >= 84
* BACKUP: RMSD < 2.0 Å and mean pLDDT >= 77
* LOWER_PRIORITY: RMSD >= 2.0 Å or weak confidence

This rule is not a universal biological truth. It is a practical filtering rule for this small 6MRR computational benchmark.

Main limitation

This analysis supports computational self-consistency only.

It does not prove that the designed proteins are experimentally stable, expressible, soluble, functional, or biologically active.

Experimental validation would require wet-lab work such as synthesis, expression, purification, structural characterization, stability assays, and functional assays.
