# Drug-Induced Cell Phenotype Predictor (DICPP) using CNN and Grad-CAM
## Overview

This project builds a deep learning pipeline that analyzes fluorescence microscopy images of cells and predicts the *drug-induced phenotype (mechanism of action, MoA)*

Given three grayscale TIFF images representing different cellular structures (DAPI, Actin, Tubulin), the model:

- classifies the phenotype into predefined MoA classes
- outputs prediction probabilities
- generates Grad-CAM visualizations to show which regions influenced the prediction

The final result is a usable inference tool that can take new microscopy images and produce interpretable predictions.

## What the Project Does
- Preprocesses multi-channel microscopy images
- Trains a CNN (ResNet18) to classify drug-induced phenotypes
- Handles class imbalance and compound-level data splitting
- Evaluates model performance on unseen compounds
- Provides an inference tool for new image prediction
- Uses Grad-CAM for model interpretability

## Input Format

Each sample consists of three grayscale TIFF images:
- DAPI (nuclear stain)
- Actin (cytoskeleton structure)
- Tubulin (microtubule network)

These are combined into a 3-channel input for the model.

## How to Use the the inference tool

Open:
`inference tool/phenotype_inference_tool_v2.ipynb`

### Demo mode
The notebook runs automatically using example images stored in:
`examples/`

### Custom input
Replace the image paths in the custom input block:

```python
custom_dapi = Path("path/to/dapi.tif")
custom_actin = Path("path/to/actin.tif")
custom_tubulin = Path("path/to/tubulin.tif")
```

Run the prediction cell to get results.

## Output

### Prediction Table
Saved in:
`tool_outputs/example_predictions_table.csv`
Includes:
- predicted phenotype
- confidence score
- top-3 class probabilities
- correctness (for demo examples)

### Grad-CAM Visualizations
Saved in:
`tool_outputs/`
Each image shows:
- input microscopy composite
- heatmap highlighting regions used by the model

## Model Details
- Architecture: ResNet18
- Input: 3-channel microscopy images (DAPI, Actin, Tubulin)
- Training strategy: compound-level data split, class filtering (minimum sample threshold), weighted sampling to address imbalance
- Loss function: Cross-Entropy

## Strengths
- End-to-end pipeline from raw images to prediction tool
- Works on real microscopy data
- Uses biologically meaningful multi-channel inputs
- Provides interpretable outputs via Grad-CAM
- Portable and easy to reuse

## Limitations
- Class imbalance still affects performance
- Some phenotypes are visually similar and hard to distinguish
- Model confusion observed between related classes (e.g. microtubule stabilizers vs destabilizers)
- Limited dataset size compared to large-scale screening setups
- Requires all three channels; single-channel inference is not supported

## Future Improvements
- Improve class balance and data coverage
- Enhance separation between similar phenotypes
- Add uncertainty detection for low-confidence predictions
- Support batch inference for large datasets
- Improve robustness across different imaging conditions

***DISCLAIMER:***
This is a personal research project built for learning and experimentation purposes and should not be used for clinical, diagnostic, or other real-world decision-making. If anyone wants to experiment with it, feel free to do so. Have fun
