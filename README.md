# Protein Secondary Structure Prediction using BiLSTM

This repository contains a PyTorch implementation of a **Bidirectional Long Short-Term Memory (BiLSTM)** model designed to predict the secondary structure of proteins. Given a primary amino acid sequence, the model classifies each residue into one of three secondary structure states: **Helix (H)**, **Sheet (E)**, or **Coil (C)**.

The entire workflow, including data preprocessing, model training, and evaluation, is detailed in the `protien.ipynb` Jupyter Notebook.

***

## 🧬 Dataset

The model is trained and validated using the `data.csv` file and tested on the independent `CB513.csv` dataset.

The original 8-state secondary structure assignments from DSSP (`dssp8`) are simplified into a 3-state classification (`dssp3`) for this task. The mapping is as follows:
* **Helix ($H$):** States `H` (α-helix), `G` (3-10 helix), `I` (π-helix)
* **Sheet ($E$):** States `E` (extended strand), `B` (isolated β-bridge)
* **Coil ($C$):** States `T` (turn), `S` (bend), `-` (loop or irregular)

***

## 🤖 Model Architecture

The core of this project is a BiLSTM network built with PyTorch. The architecture is composed of three main layers:

1.  **Embedding Layer**: Converts integer-encoded amino acid tokens into dense, low-dimensional vectors. A `padding_idx` is used to handle variable sequence lengths.
2.  **Bidirectional LSTM (BiLSTM) Layer**: Processes the sequence of embeddings to capture contextual information from both forward and backward directions. This is crucial for understanding the structural context of each amino acid.
3.  **Linear Layer**: A fully-connected layer that maps the output from the BiLSTM layer to the final three prediction classes (H, E, C).

***

## 📊 Performance

The model was trained for 5 epochs on the training dataset. The performance was evaluated on both the validation set and the external CB513 test set.

### **Validation Set Results**
The model achieves an overall **accuracy of 70%** on the validation data.

### **Validation Set Performance (Accuracy: 70%)**

| Class         | Precision | Recall | F1-Score | Support  |
|:--------------|:---------:|:------:|:--------:|:--------:|
| **H (Helix)** |   0.76    |  0.71  |   0.74   | 149,739  |
| **E (Sheet)** |   0.65    |  0.58  |   0.61   | 93,089   |
| **C (Coil)** |   0.67    |  0.75  |   0.71   | 166,535  |
|               |           |        |          |          |
| **Macro Avg** |   0.69    |  0.68  |   0.69   | 409,363  |
| **Wtd Avg** |   0.70    |  0.70  |   0.70   | 409,363  |

<br>

### **CB513 Test Set Performance (Accuracy: 69%)**

| Class         | Precision | Recall | F1-Score | Support  |
|:--------------|:---------:|:------:|:--------:|:--------:|
| **H (Helix)** |   0.74    |  0.70  |   0.72   | 49,006   |
| **E (Sheet)** |   0.62    |  0.57  |   0.60   | 31,921   |
| **C (Coil)** |   0.68    |  0.74  |   0.71   | 63,084   |
|               |           |        |          |          |
| **Macro Avg** |   0.68    |  0.67  |   0.68   | 144,011  |
| **Wtd Avg** |   0.69    |  0.69  |   0.69   | 144,011  |
