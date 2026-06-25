6MRR fixed-backbone redesign: ProteinMPNN + ColabFold validation

Summary

This mini-project tested a fixed-backbone redesign workflow using 6MRR chain A as a small benchmark target. ProteinMPNN was used to generate redesigned amino acid sequences for the 6MRR chain A backbone, and ColabFold/AlphaFold2 was used to test whether the designed sequences fold back into the intended backbone.

Seven representative ProteinMPNN candidates were selected from a temperature sweep and evaluated with ColabFold. After correcting the RMSD reference parsing issue, all seven candidates showed successful fixed-backbone recovery against a deduplicated 68-residue 6MRR chain A reference.

Workflow

1. Downloaded and prepared 6MRR chain A backbone.
2. Generated ProteinMPNN sequences across sampling temperatures 0.1, 0.3, 0.5, and 1.0.
3. Selected seven representative candidates using MPNN score and sequence recovery.
4. Predicted each selected sequence using ColabFold/AlphaFold2.
5. Evaluated self-consistency using C-alpha RMSD to the intended 6MRR chain A backbone.
6. Audited and corrected the RMSD reference after detecting a 71-vs-68 C-alpha mismatch in the raw PDB parsing step.

Reference audit

The first RMSD calculation appeared borderline because the downloaded raw 6MRR chain A PDB was counted as having 71 C-alpha atom records, while the ColabFold predicted structures had 68 C-alpha atoms.

A follow-up audit showed that the raw PDB contained 71 C-alpha atom records, but only 68 unique-residue C-alpha atoms. A deduplicated 68-residue 6MRR chain A reference was therefore generated and used for the final RMSD calculation.

Final reference audit:

* Raw C-alpha atom records in downloaded 6MRR chain A: 71
* Unique-residue C-alpha count: 68
* Deduplicated reference C-alpha count: 68

This indicates that the initial mismatch was caused by raw PDB duplicate/alternate atom records being counted directly, not by an actual mismatch between the ProteinMPNN design target and ColabFold outputs.

Final validation results

Using the deduplicated 68-residue reference, the final C-alpha RMSD values were:

* T0p5__sample01: RMSD 0.907 Å, mean pLDDT 84.484
* T0p3__sample05: RMSD 0.912 Å, mean pLDDT 84.173
* T0p1__sample10: RMSD 1.022 Å, mean pLDDT 87.321
* T0p5__sample10: RMSD 1.030 Å, mean pLDDT 86.114
* T0p3__sample08: RMSD 1.564 Å, mean pLDDT 85.655
* T1p0__sample01: RMSD 1.594 Å, mean pLDDT 77.442
* T1p0__sample10: RMSD 2.255 Å, mean pLDDT 85.114

Most candidates achieved RMSD below 2 Å, indicating strong fixed-backbone self-consistency. The T=1.0 candidates also recovered the backbone, but were weaker overall based on MPNN score, pLDDT, and/or RMSD.

Interpretation

The final result supports that the ProteinMPNN → ColabFold → RMSD validation pipeline is functional for this benchmark. The strongest candidates came from lower to moderate sampling temperatures, especially T=0.3 and T=0.5.

The main technical lesson from this run was that raw PDB files should not be used directly for RMSD analysis without checking duplicate atoms, alternate conformations, chain selection, and residue-level uniqueness. Future runs should automatically save the exact cleaned reference backbone used for ProteinMPNN and use that same reference for RMSD validation.

Limitations

This is a computational self-consistency benchmark, not an experimental validation. No wet-lab expression, stability assay, or functional test was performed. The project demonstrates a reproducible computational workflow and validation logic, but does not prove experimental foldability or function.

The code and report were developed with AI assistance, while the workflow was executed, debugged, interpreted, and organized by the user as part of a learning-oriented protein design portfolio.

Next steps

* Preserve the exact cleaned ProteinMPNN input backbone in every run.
* Automate deduplicated-reference generation and RMSD validation.
* Run a larger candidate screen with stricter lead selection.
* Extend the workflow to a more biologically meaningful target after closing this 6MRR benchmark.너가   
