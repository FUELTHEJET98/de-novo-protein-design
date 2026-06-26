De novo protein design pilot

This repository documents a small AI-assisted protein design workflow using ProteinMPNN and ColabFold/AlphaFold2.

The current completed benchmark is a fixed-backbone redesign of 6MRR chain A. ProteinMPNN was used to generate redesigned sequences for the 6MRR chain A backbone, and ColabFold/AlphaFold2 was used to test whether the designed sequences fold back into the intended backbone.

This is a computational self-consistency benchmark, not experimental wet-lab validation.

Completed benchmark

6MRR chain A fixed-backbone redesign

Workflow:

1. Prepared the 6MRR chain A backbone.
2. Generated ProteinMPNN sequence candidates across sampling temperatures 0.1, 0.3, 0.5, and 1.0.
3. Selected seven representative candidate sequences.
4. Predicted candidate structures with ColabFold/AlphaFold2.
5. Evaluated fixed-backbone recovery using C-alpha RMSD against a cleaned 6MRR chain A reference.
6. Audited and corrected an initial RMSD reference mismatch caused by duplicate/alternate CA atom records in the raw downloaded PDB.

Key result

The 6MRR fixed-backbone self-consistency benchmark was completed successfully.

After deduplicating the 6MRR chain A reference, most selected candidates achieved C-alpha RMSD below 2 Å against the 68-residue reference structure.

Best candidate:

* Candidate: T0p5__sample01
* C-alpha RMSD: 0.907 Å
* Mean pLDDT: 84.484

Other strong candidates included:

* T0p3__sample05: RMSD 0.912 Å, mean pLDDT 84.173
* T0p1__sample10: RMSD 1.022 Å, mean pLDDT 87.321
* T0p5__sample10: RMSD 1.030 Å, mean pLDDT 86.114

T=1.0 candidates passed the self-consistency screen but were treated as lower-priority leads because their RMSD, pLDDT/PAE, and ProteinMPNN scores were relatively weaker.

Reference audit

The initial RMSD calculation appeared problematic because the raw downloaded 6MRR chain A PDB contained 71 CA atom records, while the predicted structures contained 68 CA atoms.

A reference audit showed that the raw PDB contained duplicate/alternate CA atom records. After deduplication, the unique-residue CA count was 68, matching the predicted structures.

Final reference counts:

* Raw CA atom records in downloaded target: 71
* Unique-residue CA count in downloaded target: 68
* Deduplicated reference CA count: 68

The final RMSD values were calculated against the deduplicated 68-residue 6MRR chain A reference.

Repository structure

.
├── results/
│   ├── FINAL_6MRR_design_validation_table_v3_dedup_reference.csv
│   └── 6MRR_chain_A_deduplicated_reference.pdb
│
├── notes/
│   ├── 6MRR_fixed_backbone_redesign_report.md
│   └── RMSD_REFERENCE_AUDIT_v3_dedup_reference.md
│
└── notebooks/
    └── 6mrr_rmsd_audit_v3_deduplicated_reference.ipynb

Important files

* results/FINAL_6MRR_design_validation_table_v3_dedup_reference.csv
    Final validation table with ProteinMPNN scores, sequence recovery, RMSD, pLDDT, pTM, PAE, and self-consistency status.
* results/6MRR_chain_A_deduplicated_reference.pdb
    Cleaned 68-residue 6MRR chain A reference used for final RMSD calculation.
* notes/RMSD_REFERENCE_AUDIT_v3_dedup_reference.md
    Audit note explaining the 71-vs-68 CA atom mismatch and the deduplicated reference correction.
* notes/6MRR_fixed_backbone_redesign_report.md
    Technical report summarizing the workflow, results, interpretation, and limitations.
* notebooks/6mrr_rmsd_audit_v3_deduplicated_reference.ipynb
    Reproducibility notebook for reference deduplication and RMSD recalculation.

Limitations

This project does not claim experimental protein design success. The result only supports computational self-consistency: the designed sequences were predicted by ColabFold/AlphaFold2 to fold back close to the intended 6MRR chain A backbone.

The workflow was AI-assisted. Code drafts, report drafts, and interpretation support were generated with ChatGPT, while the notebook execution, file organization, result checking, and metric interpretation were performed by the repository owner.

Next steps

Planned next improvements:

1. Build a cleaner pipeline that automatically saves the input backbone, deduplicated reference, selected FASTA files, ColabFold outputs, and RMSD tables.
2. Apply the workflow to a more meaningful target beyond this small 6MRR benchmark.
3. Add clearer result visualizations and structure comparison figures.
