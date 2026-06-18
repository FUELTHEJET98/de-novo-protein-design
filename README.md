README.md
De novo protein design pilot

Goal

This repository documents a pilot protein design workflow using RFdiffusion, ProteinMPNN, and ColabFold/AlphaFold self-consistency checks.

The main goal is to understand whether designed sequences fold back into the intended backbone structure.

Current experiments

1. Fixed-backbone design using 6MRR

* Input backbone: 6MRR
* Design method: ProteinMPNN
* Variable tested: sampling temperature
* Validation: ColabFold/AlphaFold structure prediction
* Evaluation metrics: pLDDT, PAE, RMSD

2. RFdiffusion-based de novo backbone design

* Backbone generation: RFdiffusion
* Sequence design: ProteinMPNN
* Validation: ColabFold/AlphaFold
* Evaluation: self-consistency between designed backbone and predicted structure

Workflow

1. Prepare or generate a backbone structure.
2. Design amino acid sequences using ProteinMPNN.
3. Predict the structure of each designed sequence using ColabFold/AlphaFold.
4. Compare the predicted structure to the input backbone.
5. Evaluate self-consistency using pLDDT, PAE, and RMSD.

Key concepts

* ProteinMPNN designs sequences for a given backbone.
* RFdiffusion generates new backbone structures.
* ColabFold/AlphaFold predicts the 3D structure of a designed sequence.
* Self-consistency means that the predicted structure folds back into the intended backbone.
* Low RMSD and high pLDDT suggest a more self-consistent design.

Current status

This is an early pilot project.
The notebooks have been executed, but the file structure, output files, and metric interpretation are still being organized.

Next steps

* Identify input, output, FASTA, PDB, and score files.
* Build a result table comparing 6MRR and RFdiffusion experiments.
* Summarize best, middle, and worst candidates.
* Write a short technical report explaining the workflow and results.
