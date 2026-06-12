# dbzk-stylometry

Dataset and models for the stylometric attribution of the 1900 Polish translation of the Ukrainian short story "Дай Боже здоровля корові! / Daj Bože zdorovlja korovi!" (DBZK). 

This repository contains the data, execution script, and Support Vector Machine (SVM) models used in the study: **"Classical literary science versus machine learning: Apropos authorship attribution of a Polish translation of one Ukrainian short story."** The project tests the traditional, uncorroborated attribution of this translation to Ivan Franko by employing a binary classification task based on TF-IDF weighted character n-grams.

## Repository Structure

The repository is divided into two main directories: `models/` for the pre-trained SVM classifiers and `txt/` for the raw texts and processed datasets.

```text
├── models/
│   ├── models64/
│   ├── models78/
│   └── models87/
├── txt/
│   ├── 100_polish_novels/
│   ├── franko/
│   ├── new/
│   ├── full200_64.csv
│   ├── full200_78.csv
│   ├── full200_87.csv
│   ├── full250_64.csv
│       ...
│   └── full500_87.csv
├── README.md
└── authorship.ipynb
```

### Code

*   **`authorship.ipynb`**: The main Jupyter Notebook containing the execution script for the authorship analysis. It includes the complete pipeline for text chunking, TF-IDF vectorization (utilizing character n-grams), SVM model training, cross-validation, and generating the classification heatmaps.

### Data (`txt/`)

The `txt/` directory contains the source texts and the artificially expanded datasets divided into uniform chunks.

*   **`franko/`**: Contains 34 authentic Polish texts written by Ivan Franko, serving as the positive ('Franko') class for the model.
*   **`100_polish_novels/`**: This folder serves as an empty placeholder. The background corpus of late 19th- and early 20th-century Polish novels used to compile the negative ('Other') class must be downloaded from the external repository: [https://github.com/computationalstylistics/100_polish_novels](https://github.com/computationalstylistics/100_polish_novels).
*   **`new/`**: Contains unseen external texts used for independent validation of the trained models, including additional texts by Franko and other period authors.
*   **`.csv` Datasets**: The CSV files contain the pre-processed chunks used for training and testing. The naming convention `full[CHUNK_SIZE]_[PROPORTION].csv` reflects the parameters of the dataset:
    *   `[CHUNK_SIZE]`: The target word count for each text chunk (e.g., 200, 250, 300 words).
    *   `[PROPORTION]`: The **original target percentage** of the 'Other' category utilized to balance the dataset (64, 78, 87). Note that due to word-boundary and sentence constraints during the chunking process, the **final proportions** of these datasets reflect 66%, 79%, and 88%, as reported in the study's official tables.

### Models (`models/`)

This directory contains the sample SVM models trained on character bigrams. To prevent overfitting and manage data scarcity, the models were trained using a linear kernel. The subdirectories organize the models according to the original target proportions of the 'Other' category:

*   **`models64/`**: Models trained targeting a 64% proportion of texts in the 'Other' category (resulting in an actual dataset proportion of ~66%)..
*   **`models78/`**: Models trained targeting a 78% proportion of texts in the 'Other' category (resulting in an actual dataset proportion of ~79%).
*   **`models87/`**: Models trained targeting a 87% proportion of texts in the 'Other' category (resulting in an actual dataset proportion of ~88%).

**Model File Extensions**
The file extensions within these directories denote the specific cross-validation splitting strategy utilized during training:
*   **`.sav`**: Models trained using random chunk-level splits.
*   **`.sav1`**: Models trained using rigorous document-level splits designed to prevent data leakage.
