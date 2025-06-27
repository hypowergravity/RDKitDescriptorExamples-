# This is a Partial Guide to RDKit Molecular Descriptors: 

To work on some example listed you can try to use the notebook available in this repository and run in colab or jupyter notebook.

*A attempt to partially explore the RDKit Molecular Descriptors for cheminformatics, drug discovery, and QSAR modeling*

## Introduction

In this exercise, we will explore the RDKit Molecular Descriptors which might be useful for understanding the chemical space of molecules. These descriptors might be useful in many applications.
RDKit, one of the most popular open-source cheminformatics toolkits, provides an extensive collection of molecular descriptors that capture different aspects of molecular structure and properties. In this exercise, I have used RDKit version 2025.03.3 for analysis which contains 217 descriptors.



## What Are Molecular Descriptors?

Molecular descriptors are numerical values that characterize specific aspects of molecular structure and properties. They serve as the bridge between molecular structure and properties which can be used a molecular fingerprint and features for machine learning model. 
It has many application such as:

- **QSAR modeling**: Quantitative Structure-Activity Relationship studies
- **Drug discovery**: Lead optimization and property prediction
- **Chemical space analysis**: Understanding molecular diversity
- **Virtual screening**: Filtering large chemical libraries
- **ADMET prediction**: Absorption, Distribution, Metabolism, Excretion, and Toxicity

## The RDKit Descriptor Collection

RDKit's descriptors (217 in 2025.03.03 version) can be broadly categorized into several groups:

1. **Basic Molecular Properties** (9 descriptors)
2. **Charge & Electrostatic Properties** (4 descriptors)
3. **Topological & Connectivity Descriptors** (33 descriptors)
4. **Shape & 3D Descriptors** (8 descriptors)
5. **Surface Area Descriptors** (39 descriptors)
6. **Structural Count Descriptors** (47 descriptors)
7. **Fragment Descriptors** (85 descriptors)

## Complete Descriptor Reference Tables

### Basic Molecular Properties (9 descriptors)

| Descriptor | Description | Example Value | Typical Range | Drug Discovery Use |
|------------|-------------|---------------|---------------|-------------------|
| **MolWt** | Average molecular weight | Aspirin: 180.16 | 50-800 Da | Lipinski's Rule (≤500) |
| **ExactMolWt** | Exact mass (most abundant isotopes) | Aspirin: 180.0423 | Same as MolWt | Mass spectrometry |
| **HeavyAtomMolWt** | Molecular weight excluding H | Aspirin: 168.15 | ~65-75% of MolWt | Structure analysis |
| **NumValenceElectrons** | Total valence electrons | Ethanol: 20 | Variable | Electronic properties |
| **NumRadicalElectrons** | Unpaired electrons | Usually: 0 | 0-2 | Reactivity prediction |
| **MolLogP** | Wildman-Crippen LogP | Aspirin: 1.19 | -2 to 5 | Lipinski's Rule (≤5) |
| **MolMR** | Molar refractivity | Aspirin: 49.33 | Variable | Binding affinity |
| **qed** | Quantitative drug-likeness | Aspirin: 0.71 | 0.0-1.0 | Drug-likeness (≥0.67) |
| **SPS** | Spatial score (complexity) | Decalin: 0.61 | 0.2-3.0 | Structural complexity |

### Charge & Electrostatic Properties (4 descriptors)

| Descriptor | Description | Example Value | Typical Range | Application |
|------------|-------------|---------------|---------------|-------------|
| **MaxPartialCharge** | Most positive partial charge | Acetone: +0.47 | +0.2 to +0.8 | Electrophilic sites |
| **MinPartialCharge** | Most negative partial charge | Acetone: -0.51 | -0.8 to -0.2 | Nucleophilic sites |
| **MaxAbsPartialCharge** | Largest absolute charge | Acetone: 0.51 | 0.1-1.0 | Reactivity prediction |
| **MinAbsPartialCharge** | Smallest absolute charge | Acetone: 0.008 | Close to 0 | Chemical stability |

### Topological & Connectivity Descriptors (33 descriptors)

| Descriptor | Description | Example Value | Interpretation | Use Case |
|------------|-------------|---------------|----------------|----------|
| **BalabanJ** | Balaban's J index | n-Hexane: 1.63 | Linear: 1.5-2.0, Branched: 2.0-4.0 | Molecular complexity |
| **BertzCT** | Bertz complexity index | n-Hexane: 16.25 | Simple: <20, Complex: >100 | Structural complexity |
| **AvgIpc** | Average information content | Benzene: 3.82 | Variable | Symmetry analysis |
| **Ipc** | Information content | Benzene: 22.92 | Variable | Graph symmetry |
| **HallKierAlpha** | Branching correction | Isobutane: -0.48 | Negative = branched | Branching degree |
| **Phi** | Flexibility index | Cyclohexane: 5.64 | Variable | Conformational flexibility |
| **Chi0** | 0th order connectivity | n-Butane: 2.91 | Variable | Basic connectivity |
| **Chi0n** | Normalized Chi0 | n-Butane: 0.73 | 0.4-1.2 | Size-independent connectivity |
| **Chi0v** | Valence Chi0 | n-Butane: 2.91 | Variable | Heteroatom-corrected |
| **Chi1** | 1st order connectivity | n-Butane: 1.73 | Variable | Branching patterns |
| **Chi1n** | Normalized Chi1 | n-Butane: 0.58 | 0.2-1.0 | Size-independent branching |
| **Chi1v** | Valence Chi1 | n-Butane: 1.73 | Variable | Heteroatom-corrected |
| **Chi2n** | Normalized 2nd order Chi | n-Butane: 1.00 | Variable | Path connectivity |
| **Chi2v** | Valence 2nd order Chi | n-Butane: 1.00 | Variable | Higher order patterns |
| **Chi3n** | Normalized 3rd order Chi | Variable | Variable | Complex connectivity |
| **Chi3v** | Valence 3rd order Chi | Variable | Variable | Complex patterns |
| **Chi4n** | Normalized 4th order Chi | Variable | Variable | Very complex patterns |
| **Chi4v** | Valence 4th order Chi | Variable | Variable | Highest order connectivity |

### Kappa Shape Descriptors (3 descriptors)

| Descriptor | Description | Linear Example | Branched Example | Cyclic Example | Interpretation |
|------------|-------------|----------------|------------------|----------------|----------------|
| **Kappa1** | 1st order shape | Hexane: 5.00 | 2,2-Dimethylbutane: 3.27 | Cyclohexane: 3.00 | Length-like |
| **Kappa2** | 2nd order shape | Hexane: 2.78 | 2,2-Dimethylbutane: 2.22 | Cyclohexane: 2.00 | Area-like |
| **Kappa3** | 3rd order shape | Hexane: 1.67 | 2,2-Dimethylbutane: 1.67 | Cyclohexane: 1.33 | Volume-like |

**Shape Classification:**
- **Rod-like**: κ1 >> κ2 > κ3 (e.g., linear alkanes)
- **Disc-like**: κ1 > κ2 >> κ3 (e.g., flat aromatics)  
- **Spherical**: κ1 ≈ κ2 ≈ κ3 (e.g., highly branched molecules)

### Surface Area Descriptors (39 descriptors)

#### Core Surface Area Descriptors

| Descriptor | Description | Example Value | Drug Design Threshold | Application |
|------------|-------------|---------------|----------------------|-------------|
| **TPSA** | Topological polar surface area | Aspirin: 63.6 Ų | <90: BBB, 90-140: Oral | Permeability prediction |
| **LabuteASA** | Approximate surface area | Aspirin: 101.88 Ų | Variable | Molecular size |

#### PEOE_VSA Descriptors (14 descriptors - Charge-based Surface Area)

| Descriptor | Charge Range | Description | Application |
|------------|--------------|-------------|-------------|
| **PEOE_VSA1** | Most negative | VSA with charges ≤ -0.30 | Nucleophilic regions |
| **PEOE_VSA2** | Very negative | VSA with charges -0.30 to -0.25 | Strong H-bond acceptors |
| **PEOE_VSA3** | Negative | VSA with charges -0.25 to -0.20 | Moderate H-bond acceptors |
| **PEOE_VSA4** | Slightly negative | VSA with charges -0.20 to -0.15 | Weak H-bond acceptors |
| **PEOE_VSA5** | Weakly negative | VSA with charges -0.15 to -0.10 | Slightly polar regions |
| **PEOE_VSA6** | Nearly neutral (-) | VSA with charges -0.10 to -0.05 | Nearly neutral regions |
| **PEOE_VSA7** | Neutral | VSA with charges -0.05 to 0.00 | Neutral regions |
| **PEOE_VSA8** | Nearly neutral (+) | VSA with charges 0.00 to 0.05 | Nearly neutral regions |
| **PEOE_VSA9** | Weakly positive | VSA with charges 0.05 to 0.10 | Slightly polar regions |
| **PEOE_VSA10** | Slightly positive | VSA with charges 0.10 to 0.15 | Weak H-bond donors |
| **PEOE_VSA11** | Positive | VSA with charges 0.15 to 0.20 | Moderate H-bond donors |
| **PEOE_VSA12** | Very positive | VSA with charges 0.20 to 0.25 | Strong H-bond donors |
| **PEOE_VSA13** | Highly positive | VSA with charges 0.25 to 0.30 | Very polar regions |
| **PEOE_VSA14** | Most positive | VSA with charges ≥ 0.30 | Electrophilic regions |

#### SlogP_VSA Descriptors (12 descriptors - Lipophilicity-based Surface Area)

| Descriptor | LogP Range | Description | Application |
|------------|------------|-------------|-------------|
| **SlogP_VSA1** | ≤ -0.40 | Most hydrophilic regions | Water-loving surface |
| **SlogP_VSA2** | -0.40 to -0.20 | Very hydrophilic regions | Polar interactions |
| **SlogP_VSA3** | -0.20 to 0.00 | Hydrophilic regions | Moderate polarity |
| **SlogP_VSA4** | 0.00 to 0.10 | Slightly hydrophilic | Balanced regions |
| **SlogP_VSA5** | 0.10 to 0.15 | Nearly neutral | Transition zones |
| **SlogP_VSA6** | 0.15 to 0.20 | Balanced regions | Neutral interactions |
| **SlogP_VSA7** | 0.20 to 0.25 | Slightly lipophilic | Moderate hydrophobicity |
| **SlogP_VSA8** | 0.25 to 0.30 | Lipophilic regions | Hydrophobic interactions |
| **SlogP_VSA9** | 0.30 to 0.40 | Very lipophilic | Strong hydrophobic |
| **SlogP_VSA10** | 0.40 to 0.50 | Highly lipophilic | Very hydrophobic |
| **SlogP_VSA11** | 0.50 to 0.60 | Extremely lipophilic | Membrane association |
| **SlogP_VSA12** | ≥ 0.60 | Most lipophilic regions | Strongest hydrophobic |

#### SMR_VSA Descriptors (10 descriptors - Molar Refractivity-based Surface Area)

| Descriptor | MR Range | Description | Application |
|------------|----------|-------------|-------------|
| **SMR_VSA1** | ≤ 1.29 | Smallest MR contributions | Small atom regions |
| **SMR_VSA2** | 1.29 to 1.82 | Small MR contributions | Light atom regions |
| **SMR_VSA3** | 1.82 to 2.24 | Low MR contributions | Moderate size atoms |
| **SMR_VSA4** | 2.24 to 2.45 | Medium-low MR | Standard carbon regions |
| **SMR_VSA5** | 2.45 to 2.75 | Medium MR contributions | Typical organic regions |
| **SMR_VSA6** | 2.75 to 3.05 | Medium-high MR | Larger atoms/groups |
| **SMR_VSA7** | 3.05 to 3.63 | High MR contributions | Aromatic/heteroatom regions |
| **SMR_VSA8** | 3.63 to 3.80 | Very high MR | Large aromatic systems |
| **SMR_VSA9** | 3.80 to 4.00 | Extremely high MR | Complex aromatic regions |
| **SMR_VSA10** | ≥ 4.00 | Highest MR contributions | Largest atom contributions |

### EState VSA Descriptors (11 descriptors - Electrotopological State-based Surface Area)

| Descriptor | Description | Application |
|------------|-------------|-------------|
| **EState_VSA1** | VSA with EState ≤ -0.39 | Most electron-rich regions |
| **EState_VSA2** | VSA with EState -0.39 to 0.29 | Moderate electron density |
| **EState_VSA3** | VSA with EState 0.29 to 0.72 | Balanced electron regions |
| **EState_VSA4** | VSA with EState 0.72 to 1.17 | Slightly electron-poor |
| **EState_VSA5** | VSA with EState 1.17 to 1.54 | Moderate electron deficiency |
| **EState_VSA6** | VSA with EState 1.54 to 1.81 | Electron-poor regions |
| **EState_VSA7** | VSA with EState 1.81 to 2.05 | Very electron-poor |
| **EState_VSA8** | VSA with EState 2.05 to 2.39 | Highly electron-deficient |
| **EState_VSA9** | VSA with EState 2.39 to 4.69 | Extremely electron-poor |
| **EState_VSA10** | VSA with EState 4.69 to 9.17 | Most electron-deficient |
| **EState_VSA11** | VSA with EState ≥ 9.17 | Highest electron deficiency |

### VSA EState Descriptors (10 descriptors - Alternative EState binning)

| Descriptor | Description | Application |
|------------|-------------|-------------|
| **VSA_EState1** | VSA with EState 4.78 to 9.17 | High electron deficiency |
| **VSA_EState2** | VSA with EState 2.39 to 4.78 | Moderate electron deficiency |
| **VSA_EState3** | VSA with EState 2.05 to 2.39 | Electron-poor regions |
| **VSA_EState4** | VSA with EState 1.81 to 2.05 | Slightly electron-poor |
| **VSA_EState5** | VSA with EState 1.54 to 1.81 | Balanced regions |
| **VSA_EState6** | VSA with EState 1.17 to 1.54 | Slightly electron-rich |
| **VSA_EState7** | VSA with EState 0.72 to 1.17 | Electron-rich regions |
| **VSA_EState8** | VSA with EState 0.29 to 0.72 | Moderate electron density |
| **VSA_EState9** | VSA with EState -0.39 to 0.29 | High electron density |
| **VSA_EState10** | VSA with EState ≤ -0.39 | Highest electron density |

### Structural Count Descriptors (47 descriptors)

#### Core Structural Features

| Descriptor | Description | Example Value | Drug Design Threshold | Application |
|------------|-------------|---------------|----------------------|-------------|
| **HeavyAtomCount** | Non-hydrogen atoms | Aspirin: 13 | ≤30 (~MW≤500) | Lipinski's Rule |
| **FractionCSP3** | Fraction of sp³ carbons | Cyclohexane: 1.0 | >0.5 preferred | 3D character |
| **RingCount** | Total rings | Aspirin: 1 | Variable | Rigidity/complexity |
| **NumAromaticRings** | Aromatic rings | Aspirin: 1 | 1-3 typical | π-π interactions |
| **NumAliphaticRings** | Non-aromatic rings | Cyclohexane: 1 | Variable | Conformational constraint |
| **NumSaturatedRings** | Fully saturated rings | Cyclohexane: 1 | Variable | Rigidity |
| **NumAliphaticCarbocycles** | Aliphatic carbon-only rings | Cyclohexane: 1 | Variable | Hydrophobic constraint |
| **NumAliphaticHeterocycles** | Aliphatic rings with heteroatoms | Tetrahydrofuran: 1 | Variable | Polar constraint |
| **NumAromaticCarbocycles** | Aromatic carbon-only rings | Benzene: 1 | Variable | π-system |
| **NumAromaticHeterocycles** | Aromatic rings with heteroatoms | Pyridine: 1 | Variable | H-bonding + π-system |
| **NumSaturatedCarbocycles** | Saturated carbon-only rings | Cyclohexane: 1 | Variable | Hydrophobic rigidity |
| **NumSaturatedHeterocycles** | Saturated rings with heteroatoms | Tetrahydrofuran: 1 | Variable | Polar rigidity |
| **NumHeterocycles** | Rings containing heteroatoms | Pyridine: 1 | Variable | Polarity/H-bonding |

#### Hydrogen Bonding Features

| Descriptor | Description | Example Value | Drug Design Threshold | Application |
|------------|-------------|---------------|----------------------|-------------|
| **NumHAcceptors** | H-bond acceptor atoms | Aspirin: 4 | ≤10 | Lipinski's Rule |
| **NumHDonors** | H-bond donor atoms | Aspirin: 1 | ≤5 | Lipinski's Rule |
| **NHOHCount** | NH or OH groups | Ethanol: 1 | Variable | H-bonding potential |
| **NOCount** | N or O atoms | Water: 1 | Variable | Polar interactions |

#### Flexibility and Stereochemistry

| Descriptor | Description | Example Value | Threshold | Application |
|------------|-------------|---------------|-----------|-------------|
| **NumRotatableBonds** | Rotatable bonds | Ibuprofen: 4 | ≤10 | Oral bioavailability |
| **NumAtomStereoCenters** | Chiral centers | L-Alanine: 1 | Variable | Stereoselectivity |
| **NumUnspecifiedAtomStereoCenters** | Undefined chirality | Variable | 0 preferred | Purity/specificity |

#### Special Structural Features

| Descriptor | Description | Example Value | Application |
|------------|-------------|---------------|-------------|
| **NumAmideBonds** | Amide linkages | Acetamide: 1 | Peptide character |
| **NumBridgeheadAtoms** | Bridgehead positions | Adamantane: 4 | Rigidity |
| **NumSpiroAtoms** | Spiro centers | Spiro compound: ≥1 | 3D complexity |
| **NumHeteroatoms** | Non-C, non-H atoms | Water: 1 | Polarity |

### Electronic Properties

| Descriptor | Description | Example Value | Application |
|------------|-------------|---------------|-------------|
| **NumValenceElectrons** | Total valence electrons | Methane: 8 | Electronic properties |
| **NumRadicalElectrons** | Unpaired electrons | Usually: 0 | Reactivity/stability |

### EState Indices (4 descriptors)

| Descriptor | Description | Interpretation | Application |
|------------|-------------|----------------|-------------|
| **MaxEStateIndex** | Maximum EState value | Higher = more electron-deficient | Electrophilic sites |
| **MinEStateIndex** | Minimum EState value | Lower = more electron-rich | Nucleophilic sites |
| **MaxAbsEStateIndex** | Max absolute EState | Higher = more extreme | Most reactive sites |
| **MinAbsEStateIndex** | Min absolute EState | Lower = more neutral | Least reactive sites |

### Fingerprint Density Descriptors (3 descriptors)

| Descriptor | Description | Radius | Application |
|------------|-------------|--------|-------------|
| **FpDensityMorgan1** | Morgan fingerprint density | 1 bond | Local environment |
| **FpDensityMorgan2** | Morgan fingerprint density | 2 bonds | Extended environment |
| **FpDensityMorgan3** | Morgan fingerprint density | 3 bonds | Larger environment |

### BCUT Descriptors (8 descriptors - Eigenvalue-based)

| Descriptor | Description | Property Weighting | Application |
|------------|-------------|-------------------|-------------|
| **BCUT2D_MWHI** | Highest eigenvalue | Molecular weight | Size/bulk properties |
| **BCUT2D_MWLOW** | Lowest eigenvalue | Molecular weight | Size distribution |
| **BCUT2D_CHGHI** | Highest eigenvalue | Partial charge | Charge distribution |
| **BCUT2D_CHGLO** | Lowest eigenvalue | Partial charge | Charge polarization |
| **BCUT2D_LOGPHI** | Highest eigenvalue | LogP | Lipophilicity distribution |
| **BCUT2D_LOGPLOW** | Lowest eigenvalue | LogP | Hydrophilicity/lipophilicity |
| **BCUT2D_MRHI** | Highest eigenvalue | Molar refractivity | Polarizability distribution |
| **BCUT2D_MRLOW** | Lowest eigenvalue | Molar refractivity | Size/polarizability |

### Fragment Descriptors (85 descriptors)

Fragment descriptors count specific functional groups and structural motifs important for biological activity and toxicity prediction.

#### Basic Functional Groups

| Descriptor | Description | SMARTS Pattern | Toxicity/Activity Notes |
|------------|-------------|----------------|------------------------|
| **fr_Al_OH** | Aliphatic alcohols | [OH][CH] | Metabolic liability |
| **fr_Al_OH_noTert** | Non-tertiary aliphatic alcohols | [OH][CH2,CH3] | Primary/secondary OH |
| **fr_Ar_OH** | Aromatic alcohols (phenols) | [OH][c] | Antioxidant activity |
| **fr_phenol** | Phenolic OH | [OH][c] | Estrogen receptor binding |
| **fr_phenol_noOrthoHbond** | Phenols without ortho H-bonding | Complex pattern | Free phenolic OH |

#### Carbonyl-containing Groups

| Descriptor | Description | SMARTS Pattern | Notes |
|------------|-------------|----------------|-------|
| **fr_ketone** | Ketone groups | [C](=O)[C] | Metabolic target |
| **fr_ketone_Topliss** | Topliss ketones | Modified pattern | Drug design relevant |
| **fr_aldehyde** | Aldehyde groups | [CH]=O | Reactive/toxic |
| **fr_ester** | Ester groups | [C](=O)O[C] | Hydrolyzable |
| **fr_lactone** | Lactone rings | Cyclic ester | Bioactive natural products |
| **fr_lactam** | Lactam rings | Cyclic amide | β-lactam antibiotics |

#### Nitrogen-containing Groups

| Descriptor | Description | SMARTS Pattern | Biological Activity |
|------------|-------------|----------------|-------------------|
| **fr_NH0** | Tertiary amines | [N]([C])([C])[C] | Basic, membrane permeable |
| **fr_NH1** | Secondary amines | [N]([C])[C] | Moderate basicity |
| **fr_NH2** | Primary amines | [N]([C])[H] | Strong bases |
| **fr_amide** | Amide groups | [C](=O)[N] | H-bonding, peptide character |
| **fr_amidine** | Amidine groups | [C](=[N])[N] | Strong bases |
| **fr_aniline** | Aniline groups | [c][N] | Aromatic amines |
| **fr_quatN** | Quaternary nitrogen | [N+] | Permanent charge |

#### Aromatic Systems

| Descriptor | Description | Notes |
|------------|-------------|-------|
| **fr_benzene** | Benzene rings | Basic aromatic unit |
| **fr_pyridine** | Pyridine rings | N-containing aromatic |
| **fr_imidazole** | Imidazole rings | Histidine-like |
| **fr_thiazole** | Thiazole rings | S,N-aromatic |
| **fr_oxazole** | Oxazole rings | O,N-aromatic |
| **fr_furan** | Furan rings | O-aromatic |
| **fr_thiophene** | Thiophene rings | S-aromatic |

#### Halogen-containing Groups

| Descriptor | Description | Toxicity Notes |
|------------|-------------|----------------|
| **fr_halogen** | Halogen atoms | Metabolic liability |
| **fr_alkyl_halide** | Alkyl halides | Potential alkylating agents |

#### Sulfur-containing Groups

| Descriptor | Description | Activity Notes |
|------------|-------------|----------------|
| **fr_SH** | Thiol groups | Cysteine-like, redox active |
| **fr_sulfide** | Sulfide groups | Potential oxidation |
| **fr_sulfone** | Sulfone groups | Metabolite |
| **fr_sulfonamd** | Sulfonamide groups | Antibiotic activity |

#### Phosphorus-containing Groups

| Descriptor | Description | Activity Notes |
|------------|-------------|----------------|
| **fr_phos_acid** | Phosphoric acid | Phosphate mimic |
| **fr_phos_ester** | Phosphate ester | Prodrug strategy |

#### Reactive/Toxic Groups

| Descriptor | Description | Toxicity Concern |
|------------|-------------|------------------|
| **fr_epoxide** | Epoxide rings | Highly reactive |
| **fr_azide** | Azide groups | Explosive, toxic |
| **fr_diazo** | Diazo groups | Potentially mutagenic |
| **fr_isocyan** | Isocyanate groups | Respiratory sensitizer |
| **fr_isothiocyan** | Isothiocyanate groups | Protein reactive |

#### Bioactive Fragments

| Descriptor | Description | Activity Association |
|------------|-------------|---------------------|
| **fr_urea** | Urea groups | Kinase inhibitors |
| **fr_guanido** | Guanidine groups | Arginine mimic |
| **fr_morpholine** | Morpholine rings | CNS activity |
| **fr_piperdine** | Piperidine rings | CNS activity |
| **fr_piperzine** | Piperazine rings | Antipsychotic activity |
| **fr_benzodiazepine** | Benzodiazepine core | Anxiolytic activity |
| **fr_barbitur** | Barbiturate core | Sedative activity |

#### Metabolic Liability Fragments

| Descriptor | Description | Metabolic Concern |
|------------|-------------|-------------------|
| **fr_Ndealkylation1** | N-dealkylation site 1 | CYP metabolism |
| **fr_Ndealkylation2** | N-dealkylation site 2 | CYP metabolism |
| **fr_para_hydroxylation** | Para-hydroxylation site | Phase I metabolism |
| **fr_allylic_oxid** | Allylic oxidation site | CYP metabolism |

#### Carboxylic Acid Derivatives

| Descriptor | Description | Notes |
|------------|-------------|-------|
| **fr_COO** | Carboxylic acid | Acidic, charged |
| **fr_COO2** | Alternative carboxylic acid | Different pattern |
| **fr_Ar_COO** | Aromatic carboxylic acid | Benzoic acid-like |
| **fr_Al_COO** | Aliphatic carboxylic acid | Fatty acid-like |

## 1. Basic Molecular Properties

### Molecular Weight Descriptors

**MolWt, ExactMolWt, HeavyAtomMolWt**

These fundamental descriptors describe the mass characteristics of molecules:

- **MolWt**: Average molecular weight including isotopic contributions
- **ExactMolWt**: Exact mass using most abundant isotopes
- **HeavyAtomMolWt**: Molecular weight excluding hydrogen atoms

**Example**: Aspirin (CC(=O)OC1=CC=CC=C1C(=O)O)
- MolWt: 180.16 Da
- ExactMolWt: 180.0423 Da  
- HeavyAtomMolWt: 168.15 Da

**Drug Discovery Relevance**: Molecular weight is a key parameter in Lipinski's Rule of Five, with drug-like molecules typically having MW ≤ 500 Da.

### Physicochemical Properties

**MolLogP** - Wildman-Crippen LogP
The partition coefficient between octanol and water, indicating lipophilicity:
- < 0: Hydrophilic (water-loving)
- 0-2: Balanced 
- 2-5: Lipophilic (fat-loving)
- > 5: Highly lipophilic

**Example Applications**:
- Ethanol (CCO): LogP = -0.31 (hydrophilic)
- Octane (CCCCCCCC): LogP = 3.36 (lipophilic)

**MolMR** - Molar Refractivity
Related to molecular volume and polarizability, important for:
- Drug-receptor binding
- Membrane permeability
- Optical properties

**qed** - Quantitative Estimate of Drug-likeness
A composite score (0-1) incorporating multiple drug-like properties:
- 0.67-1.0: Excellent drug-likeness
- 0.3-0.67: Moderate drug-likeness
- 0.0-0.3: Poor drug-likeness

## 2. Charge & Electrostatic Properties

### Partial Charge Descriptors

**MaxPartialCharge, MinPartialCharge, MaxAbsPartialCharge, MinAbsPartialCharge**

These descriptors capture electrostatic properties using Gasteiger partial charges:

**Applications**:
- Predicting reaction sites
- Understanding intermolecular interactions
- Modeling enzyme-substrate binding

**Example**: Acetone (CC(=O)C)
- MaxPartialCharge: +0.47 (carbonyl carbon - electrophilic site)
- MinPartialCharge: -0.51 (oxygen - nucleophilic site)

## 3. Topological & Connectivity Descriptors

### Complexity Indices

**BalabanJ** - Balaban's J Index
Measures molecular branching and complexity:
- Linear molecules: 1.5-2.0
- Branched molecules: 2.0-4.0
- Highly complex structures: >4.0

**BertzCT** - Bertz Complexity Index
Quantifies structural complexity considering:
- Branching patterns
- Heteroatom presence
- Ring systems

### Connectivity Indices (Chi Descriptors)

**Chi0, Chi1, Chi2n, Chi3n, Chi4n** (and their variants)
Kier & Hall connectivity indices describe molecular connectivity patterns:
- **Chi0**: Simple connectivity (bond count)
- **Chi1**: First-order connectivity (branching)
- **Higher orders**: More complex structural patterns

**Variants**:
- No suffix: Simple connectivity
- `n`: Normalized by atom count
- `v`: Valence-corrected (considers heteroatoms)

### Shape Descriptors

**Kappa1, Kappa2, Kappa3** - Kier Shape Indices
Describe molecular shape in 1D, 2D, and 3D:

**Shape Classification**:
- **Rod-like**: κ1 >> κ2 > κ3 (linear alkanes)
- **Disc-like**: κ1 > κ2 >> κ3 (flat aromatics)
- **Spherical**: κ1 ≈ κ2 ≈ κ3 (highly branched)

## 4. Surface Area Descriptors

### TPSA - Topological Polar Surface Area

One of the most important descriptors for drug discovery:
- **< 90 Ų**: Good blood-brain barrier penetration
- **90-140 Ų**: Good oral absorption
- **> 140 Ų**: Poor membrane permeability

### VSA Descriptors

**PEOE_VSA1-14**: Surface area partitioned by partial charge ranges
**SlogP_VSA1-12**: Surface area partitioned by lipophilicity contributions
**SMR_VSA1-10**: Surface area partitioned by molar refractivity

These descriptors provide detailed surface property distributions crucial for:
- Molecular recognition
- Binding affinity prediction
- ADMET modeling

## 5. Structural Count Descriptors

### Lipinski's Rule of Five Components

**HeavyAtomCount**: Total non-hydrogen atoms (≤30 for drug-likeness)
**NumHAcceptors**: Hydrogen bond acceptors (≤10)
**NumHDonors**: Hydrogen bond donors (≤5)
**NumRotatableBonds**: Rotatable bonds (≤10 for oral bioavailability)

### Ring System Descriptors

**RingCount**: Total number of rings
**NumAromaticRings**: Aromatic ring count
**NumAliphaticRings**: Aliphatic ring count
**NumSaturatedRings**: Saturated ring count

### Stereochemistry Descriptors

**NumAtomStereoCenters**: Chiral centers
**NumUnspecifiedAtomStereoCenters**: Undefined chiral centers
**FractionCSP3**: Fraction of sp³ carbons (3D character)

**Modern Drug Design Insight**: Higher FractionCSP3 (>0.5) often correlates with improved drug properties, moving away from "flat" aromatic compounds.

## 6. Fragment Descriptors (fr_* descriptors)

RDKit provides 85 fragment descriptors that count specific functional groups and structural motifs. These are invaluable for:
- Structure-Activity Relationship analysis
- Toxicity prediction
- Metabolic pathway prediction

### Key Fragment Categories

**Basic Functional Groups**:
- `fr_Al_OH`: Aliphatic alcohols
- `fr_ketone`: Ketone groups
- `fr_ester`: Ester linkages
- `fr_amide`: Amide bonds
- `fr_NH2`: Primary amines

**Aromatic Systems**:
- `fr_benzene`: Benzene rings
- `fr_phenol`: Phenolic OH groups
- `fr_pyridine`: Pyridine rings

**Reactive Groups**:
- `fr_aldehyde`: Aldehyde groups
- `fr_halogen`: Halogen atoms
- `fr_epoxide`: Epoxide rings





## Resources

- **RDKit Documentation**: https://rdkit.org/
- **Interactive Notebook**: Available in this repository
- **Further Reading**: 
  - Todeschini, R. & Consonni, V. "Molecular Descriptors for Chemoinformatics"
  - Leach, A.R. & Gillet, V.J. "An Introduction to Chemoinformatics"

