# 6MRR RMSD audit v3: deduplicated reference

## Key correction
The apparent 71-vs-68 C-alpha mismatch can arise when the raw PDB contains duplicate CA atom records, such as alternate conformations. This audit creates a deduplicated chain A reference by keeping one atom per residue/atom-name key, preferring blank altloc, then altloc A, then higher occupancy.

- Raw target PDB: `/content/drive/MyDrive/result_split7/6MRR.pdb`
- Raw CA atom records in downloaded target: `71`
- Unique-residue CA count in downloaded target: `68`
- Deduplicated reference PDB: `/content/drive/MyDrive/result_split7/6MRR_chain_A_deduplicated_reference.pdb`
- Deduplicated reference CA count: `68`

## Ranked result
|   priority_order | short_id       |   dedup_reference_rmsd_A |   mean_plddt |   ptm |   mpnn_score |   seq_recovery | self_consistency_status   | reference_mode                    | target_window_label       |
|-----------------:|:---------------|-------------------------:|-------------:|------:|-------------:|---------------:|:--------------------------|:----------------------------------|:--------------------------|
|                1 | T0p5__sample01 |                    0.907 |       84.484 |  0.63 |        1.137 |          0.456 | PASS_STRONG               | deduplicated_chain_A_exact_length | full_deduplicated_chain_A |
|                2 | T0p3__sample05 |                    0.912 |       84.173 |  0.62 |        0.96  |          0.515 | PASS_STRONG               | deduplicated_chain_A_exact_length | full_deduplicated_chain_A |
|                3 | T0p1__sample10 |                    1.022 |       87.321 |  0.68 |        0.878 |          0.574 | PASS_STRONG               | deduplicated_chain_A_exact_length | full_deduplicated_chain_A |
|                4 | T0p5__sample10 |                    1.03  |       86.114 |  0.63 |        1.234 |          0.529 | PASS_STRONG               | deduplicated_chain_A_exact_length | full_deduplicated_chain_A |
|                5 | T0p3__sample08 |                    1.564 |       85.655 |  0.64 |        1.023 |          0.574 | PASS_STRONG               | deduplicated_chain_A_exact_length | full_deduplicated_chain_A |
|                6 | T1p0__sample01 |                    1.594 |       77.442 |  0.57 |        1.887 |          0.368 | PASS_ACCEPTABLE           | deduplicated_chain_A_exact_length | full_deduplicated_chain_A |
|                7 | T1p0__sample10 |                    2.255 |       85.114 |  0.62 |        1.666 |          0.368 | PASS_ACCEPTABLE           | deduplicated_chain_A_exact_length | full_deduplicated_chain_A |