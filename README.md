# dbzk-stylometry

Dataset and models for the stylometric attribution of the 1900 Polish translation of the Ukrainian short story "Дай Боже здоровля корові! / Daj Bože zdorovlja korovi!" (DBZK). 

This repository contains the data and Support Vector Machine (SVM) models used in the study: **"Classical literary science versus machine learning: Apropos authorship attribution of a Polish translation of one Ukrainian short story."** The project tests the traditional, uncorroborated attribution of this translation to Ivan Franko by employing a binary classification task based on TF-IDF weighted character n-grams.

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
    *   `[PROPORTION]`: The percentage of the 'Other' category utilized to balance the dataset (e.g., 64%, 78%, 87%).

### Models (`models/`)

This directory contains the sample SVM models trained on character bigrams. To prevent overfitting and manage data scarcity, the models were trained using a linear kernel. The subdirectories organize the models according to the proportion of the 'Other' category used during training:

*   **`models64/`**: Models trained with a 66% (approx. 64% in final compilation) proportion of texts in the 'Other' category.
*   **`models78/`**: Models trained with a 79% (approx. 78% in final compilation) proportion of texts in the 'Other' category.
*   **`models87/`**: Models trained with an 88% (approx. 87% in final compilation) proportion of texts in the 'Other' category.
