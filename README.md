# Machine Learning Methods for Induction Motor Fault Detection

![Aalto logo](/images/Logo.png)<br>
**Master's Thesis**<br>

**Author** Semen Koveshnikov<br>
**Programme** Automation and Electrical Engineering<br>
**Thesis supervisor** Prof. Anouar Belahcen<br>
**Thesis advisor** Billah Md, MSc

## Abstract

This is the code for the master's thesis, written for Aalto University. The thesis aimed to find the best suitable ML model for induction motor broken rotor bar fault classification task. Three ML algorithms were compared, namely, SVM, GBM, and MLP to identify the most accurate one. The classic ML models were built with Scikit-learn, while the NN was developed using TensorFlow. The pipelines for the experiments were implemented via [DVC](https://dvc.org/) by iterative.ai.

The repository contains the source code in /src folder, where the pipeline stage files are placed. The functions are well explained with doc strings. The pipeline includes 4 stages: Features, Data, Training, and Evaluation. The first stage loads data from [.mat](https://ieee-dataport.org/open-access/experimental-database-detecting-and-diagnosing-rotor-broken-bar-three-phase-induction) files and creates features. The second stage deletes specified load levels from the training set, placing them in the test set. Next, a chosen model is trained, which is evaluated in the fourth stage on F1 and log-loss scores. Also, confusion matrices are created.

## Instructions

Clone the repository to your local machine. Install DVC extension to MS VSCode from the extensions store. Then follow the instructions in the extension to enable DVC experiments, creating a virtual environment for running the tests. The *requirements.txt* contains the necessary libraries needed for the project. They will be automatically installed by DVC during the setup, or install them yourself using pip:

```cmd
pip install -r requirements.txt
```

## Functionality

The ML pipeline parameters are placed in `params.yaml` file, in which it is possible, for example, to choose the type of ML algorithm you want to explore or FFT windowing parameters. The pipeline comprises four stages defined in `dvc.yaml` file. 

```mermaid

---
title: DVC Pipeline
---
flowchart LR
    A[Features] --> B[Data]
    B --> C[Training]
    C --> D[Evaluation]
```

With the current version the influence of FFT windowing function and cycle number per FFT window can be explored. The motor phase current frequency spectrum visibility changes with different windowing functions, as shown below, which might be used for improvements in ML accuracy predictions

⠀|⠀
:---------:|:-------------:
![Rectangular window](/images/Uniform_windowing.png) |![Hanning window](/images/Hanning_windowing.png)

Also, the visibility of side-bands differs with different number of cyces per window, as presented in figure below.

⠀|⠀
:---------:|:-------------:
![Hanning window, 20 cycles](/images/20_cycles.png) |![Hanning window, 70 cycles](/images/70_cycles.png)
