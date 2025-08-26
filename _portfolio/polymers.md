---
title: "Polymer Properties Prediction"
collection: portfolio
---

Project for predicting five key polymer properties based on the polymer's molecular structure. 

The data primarily comes from the Kaggle competition ["NeurIPS - Open Polymer Prediction 2025"](https://www.kaggle.com/competitions/neurips-open-polymer-prediction-2025/) and is supplemented by smaller datasets from [(Seok et al. 2024)](http://dx.doi.org/10.6084/m9.figshare.24219958.v1), and [(Borredon et al. 2023)](https://www.sciencedirect.com/science/article/pii/S2590159123000377#ec0005).

<img src="/images/portfolio/polymers_examples.png" alt="polymers" />

# Key project features

1. **Exploratory data analysis**: analyzed the dataset to understand its structure and the relationships between variables.
2. **Feature engineering**: used the RDKit library to generate relevant features from the molecular structure data.
3. **Model training**: trained a predictive model using RandomForestRegressor and optimized its hyperparameters with Optuna.
4. **Model deployment**: deployed the trained model using FastAPI, Docker, and AWS. 
5. **User interface**: built an application with Streamlit and hosted it on  [HuggingFace Spaces](https://huggingface.co/spaces/mkhalil-ds/polymers-streamlit).

Code links: [Notebook](https://github.com/MKhalil-DS/Kaggle-projects/blob/main/polymer-prediction/polymer-prediction.ipynb), [deployment files](https://github.com/MKhalil-DS/Kaggle-projects/tree/main/polymer-prediction/deployment), [Streamlit app](https://huggingface.co/spaces/mkhalil-ds/polymers-streamlit/tree/main).


# Exploratory data analysis

The dataset consists of molecular structures expressed using the Simplified Molecular Input Line Entry System [(SMILES)](https://en.wikipedia.org/wiki/Simplified_Molecular_Input_Line_Entry_System). 
The target variables are

- `Tg` - Glass transition temperature (°C).
- `FFV` - Fractional free volume.
- `Tc` - Thermal conductivity (W/m·K).
- `Density` - Polymer density (g/cm^3).
- `Rg` - Radius of gyration (Å).

The dataset includes 11,401 entries for SMILES, with the following counts of non-null target variables: (`Tg`:  8349, `FFV`: 7892, `Density`: 1247, `Tc`: 866, `Rg`: 614). The following plots show the distribution of the target variables:

<img src="/images/portfolio/polymers_targets_boxplot.png" alt="boxplot of target variables" />

<img src="/images/portfolio/polymers_targets_dist.png" alt="distribution of target variables" />

The target variables show weak to moderate correlations with each other.

<img src="/images/portfolio/polymers_target_correlations.png" alt="correlations of target variables" />

# Feature engineering

To prepare the data for modeling, I followed these steps:

1. **Molecular descriptors**: used the [RDKit](https://www.rdkit.org/) package to generate approximately 200 molecular descriptors for each SMILES entry. These descriptors include important characteristics such as molecular weight, the number of hydrogen bond acceptors and donors, and the LogP value (a measure of hydrophobicity). I also complemented those descriptors by simple features, such as the molecule length and the number of carbon atoms.
2. **Handling missing values**: removed descriptors with more than 10% missing values and filled in the remaining gaps with the median values.
3. **Data splitting**: divided the dataset into five separate dataframes, each corresponding to one of the target properties.
4. **Correlation analysis**: computed the correlations matrix and dropped features with very high correlations with each other or very low correlations with the target variable.

This process resulted in about 100 features for each target property.

<img src="/images/portfolio/polymers_top_features.png" alt="Top features" />

# Predictive modeling using random forest

I developed a machine learning model through the following steps:

1. **Train-test split**: divided the data into training and testing sets, with 10% for the test set, since the available datasets for `Tc` and `Rg` are small.
2. **Model experimentation**: tested several models, including linear regression, decision trees, random forest, and XGBoost with default hyperparameters. Random forest and XGBoost showed the smallest errors. However, since the random forest algorithm is more computationally efficient, I chose it for further tuning.
3. **Hyperparameter tuning**: optimized the hyperparameters of the random forest model using Optuna, separately for each target, by minimizing the mean absolute error using 5-fold cross-validation. 

The final models achieved the following scaled mean absolute errors on the train set: (`Tg`: 0.0379, `FFV`: 0.0129, 'Tc': 0.0219, 'Density': 0.0359, 'Rg': 0.0824) with a total weighted error of 0.0452.

<img src="/images/portfolio/polymers_test.png" alt="compare test data to predictions" />


# Model deployment

I deployed the model using the following steps:

1. Created an API using *FastAPI*, that takes the SMILES input and outputs the predictions for the five target properties.
2. Containerized the model using *Docker*.
3. Hosted the container on *AWS*.
4. Built a frontend app using *Streamlit* and added it on [HuggingFace Spaces](https://huggingface.co/spaces/mkhalil-ds/polymers-streamlit).

1. **API creation**: built and API using FastAPI that takes SMILES input and returns predictions for the five target properties.
2. **Containerization**: packaged using Docker to ensure it runs consistently across different environments.
3. **Cloud hosting**: hosted the Docker container on AWS.
4. **Frontend development**: created a simple UI app using Streamlit and hosted it on [HuggingFace Spaces](https://huggingface.co/spaces/mkhalil-ds/polymers-streamlit).

The following image is a Screenshot of the Streamlit app.

<img src="/images/portfolio/polymers_app.png" alt="Streamlit app" width=300 />

# Conclusions and next steps

**Key Insights**
- RDKit descriptors provide useful features for polymer properties
- Random forest models provide accurate predictions and are efficient to train.
- Hyperparameter optimization with Optuna enhances model performance.
- Deploying the model makes it accessible for everyone.

**Next steps**
- Explore using [Morgan fingerprints](https://greglandrum.github.io/rdkit-blog/posts/2023-01-18-fingerprint-generator-tutorial.html), which provide a binary representation of SMILES.
- Use principal component analysis (PCA) to reduce the number of features, particularly if Morgan fingerprints are used.
- Investigate using neural network models, such as using LSTM to process SMILES strings.
