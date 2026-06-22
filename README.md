# De novo protein design pilot
De novo protein design pilot

Purpose

This repository documents a pilot workflow for computational protein design using RFdiffusion, ProteinMPNN, and ColabFold/AlphaFold-based self-consistency checks.

The goal is not to claim successful experimental protein design yet. The current goal is to understand the design-validation pipeline and convert notebook execution into a reproducible, interpretable mini-project.

Project question

Can designed amino acid sequences fold back into the intended backbone structure according to AlphaFold/ColabFold self-consistency metrics?

Workflows tested

1. Fixed-backbone redesign using 6MRR

* Input: 6MRR protein backbone from the PDB
* Sequence design: ProteinMPNN
* Variable tested: ProteinMPNN sampling temperature
* Validation: ColabFold/AlphaFold structure prediction
* Evaluation: pLDDT, PAE, and backbone RMSD against the input backbone

2. RFdiffusion-based de novo backbone design

* Backbone generation: RFdiffusion
* Sequence design: ProteinMPNN
* Validation: ColabFold/AlphaFold
* Evaluation: self-consistency between the generated backbone and the predicted structure

Conceptual summary

ProteinMPNN designs amino acid sequences for a given protein backbone. ColabFold/AlphaFold then predicts the 3D structure of each designed sequence. If the predicted structure is close to the intended backbone, with low RMSD and high confidence metrics, the design is considered more self-consistent within this computational workflow.

For RFdiffusion, the backbone itself is generated de novo before sequence design. This makes the self-consistency test more demanding than fixed-backbone redesign of a natural PDB structure such as 6MRR.

Self-consistency is not proof of experimental folding or biological function. It is an early computational screen for prioritizing candidates and identifying failures before deeper analysis or wet-lab validation.

Current status

* 6MRR fixed-backbone ProteinMPNN runs were attempted.
* ProteinMPNN sampling temperature was varied.
* RFdiffusion + ProteinMPNN + ColabFold workflow was also attempted.
* Current limitation: output files, score files, and metric locations are still being organized.
* The next goal is to build a result table with pLDDT, PAE, RMSD, and self-consistency judgments.

Planned repository structure

de-novo-protein-design/
├── README.md
├── notebooks/
│   └── diffusion.ipynb
├── inputs/
│   └── 6mrr.pdb
├── outputs/
│   ├── rfdiffusion_backbones/
│   ├── mpnn_sequences/
│   └── colabfold_predictions/
├── results/
│   └── summary_table.md
└── reports/
    └── pilot_report.md

Result table to be completed

experiment	backbone	method	temperature	candidate	pLDDT	PAE	RMSD	self-consistent?	note
6MRR fixed-backbone	6MRR	ProteinMPNN + ColabFold	?	?	?	?	?	unclear	Need to locate output files
6MRR fixed-backbone	6MRR	ProteinMPNN + ColabFold	?	?	?	?	?	unclear	Need to locate output files
RFdiffusion backbone	de novo	RFdiffusion + ProteinMPNN + ColabFold	?	?	?	?	?	unclear	Need to locate output files

Immediate next steps

1. Locate or rerun the Colab notebook outputs.
2. Identify input PDB, designed FASTA, predicted PDB, and score/ranking files.
3. Fill the result table with pLDDT, PAE, and RMSD.
4. Compare 6MRR fixed-backbone results with RFdiffusion-generated backbone results.
5. Write a short technical report explaining the workflow, results, and limitations.
