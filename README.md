# Kaggle-competition-tabular-playground-series-jul-2022

In this challenge, you are given a dataset where each row belongs to a particular cluster. Your job is to predict the cluster each row belongs to. You are not given any training data, and you are not told how many clusters are found in the ground truth labels.  

https://www.kaggle.com/competitions/tabular-playground-series-jul-2022

## Data Analysis Step
EDA :  
* Histograms of each features
* Correlation between all features

 Semi-Supervised：
1. Determine the optimal number of clusters using GMM and BIC scores  
    * Using SOM neural network topology map & Gaussian Mixture Model find the number of cluster which can minimise the BIC score.
    * Choose  7 as number of cluster
2. Estimate Feature importance
    * Using Sharpiro test 
3. Unupervised - Cluster the data using soft-voting
    * we fit the model multiple times with different random seeds and sum the predicted probabilities. The class with the highest predicted probability will then be use for the final class assignment.
    * Evaluate clustering performance, using David Bouldin score Calinski Harabasz score and Silhouette score
4. Supervised - Classification using the confident predictions from clustering as training labels
    * We fit our classification model using points the clustering algorithm was confident that it got correct.
    * We use the classification model to predict the points it was not confident that it got correct.
5. Modeling 
    * Using 5 models: ET,QDA,LDA,BGMM and LGBM
    * 5 fold Cross validation to evaluate performance of models, finally choose LGBM
6. Iterative Classification with BGMM Classifier


## Final submmition result
* Adjusted Rand Index = 0.81202
* Rank = 150/1253 (Top 12%)
![螢幕擷取畫面 2023-03-15 023535](https://user-images.githubusercontent.com/102510341/225386105-025dc745-e660-4488-98d3-0b7392072746.png)
![螢幕擷取畫面 2023-03-15 023334](https://user-images.githubusercontent.com/102510341/225386174-1a1ef946-8988-45b9-b7aa-ab8e5342590c.png)