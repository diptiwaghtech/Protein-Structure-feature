# Protein Structure Feature Engineering Pipeline for Generative Deep Learning

## Overview

This project implements a feature extraction, encoding, and decoding framework for structure-based generative learning using a protein structure provided in PDB format.

The objective is to convert protein structural and physicochemical information into a machine-learning-friendly representation suitable for downstream generative deep learning models.

---

## Protein Representation

A residue-level graph representation was chosen.

- Nodes represent amino acid residues
- Edges represent spatial interactions between residues
- Edge criterion: distance < 8 Å

This representation preserves biological information while efficiently capturing the three-dimensional topology of the protein.

---

## Extracted Features

### Biological Features

- Residue Type

### Physicochemical Features

- Hydrophobicity (Kyte-Doolittle Scale)
- Residue Charge

### Spatial Features

- Cα Coordinates (x, y, z)
- Distance Matrix
- Neighborhood Connectivity

---
## Feature Extraction Pipeline

1. Parse PDB structure using BioPython.
2. Extract residue-level information.
3. Retrieve Cα coordinates.
4. Assign hydrophobicity values.
5. Assign residue charge values.
6. Compute pairwise distance matrix.
7. Build graph connectivity using an 8 Å threshold.

---

## Graph Construction

The protein is represented as a graph:

- Node = Amino Acid Residue
- Edge = Spatial Contact

Adjacency matrix generation:

```python
adjacency = (distance_matrix < 8).astype(int)
```

---

## Feature Encoding

The encoder converts extracted features into numerical representations using:

- One-Hot Encoding of residue identities
- Coordinate normalization using StandardScaler
- Hydrophobicity encoding
- Charge encoding
- Graph adjacency matrix construction

Outputs:

- Node Feature Matrix
- Adjacency Matrix

---

## Feature Decoding

The decoder reconstructs:

- Residue identities
- Original coordinates
- Graph structure

Inverse transformations are used to recover the original representation.

---

## Validation
Coordinate Reconstruction MSE:

```text
4.9 × 10⁻¹⁴
```

The near-zero reconstruction error demonstrates that the encoding-decoding pipeline preserves structural information with negligible loss.

---

## Results

| Metric | Value |
|----------|----------|
| Protein Representation | Residue-Level Graph |
| Nodes (Residues) | 306 |
| Edges (Spatial Contacts) | 1460 |
| Reconstruction MSE | 4.9 × 10⁻¹⁴ |

---

## Suitability for Generative Learning

The proposed representation captures:

- Biological properties
- Physicochemical properties
- Spatial relationships

making it suitable for downstream Graph Neural Networks (GNNs), protein generation models, and structure-based drug discovery workflows.

---

## Future Improvements

- Secondary structure features
- Solvent accessibility
- Additional physicochemical descriptors
- Graph Neural Network integration
- Large-scale protein dataset processing

---

## Conclusion

This project demonstrates a complete feature engineering workflow for protein structures, including feature extraction, graph representation, encoding, decoding, and validation. The resulting representation is deterministic, interpretable, and suitable for generative deep learning applications.
