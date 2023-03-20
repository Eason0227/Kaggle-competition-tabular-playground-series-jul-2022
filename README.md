# Kaggle-competition-tabular-playground-series-jul-2022

For this challenge, you are given (simulated) manufacturing control data that can be clustered into different control states. Your task is to cluster the data into these control states.

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
6. Combine prediction  
    * Combine the probabilities from the different classification/clustering algorithms
7. Iterative Classification with BGMM Classifier
    * We iteratively use the the predicted labels from the previous iteration's model as our training labels for the current iteration's model.
    * Iteration = 20
8. Submmition

## Final submmition result
* Adjusted Rand Index = 0.81202
* Rank = 150/1253 (Top 12%)
![螢幕擷取畫面 2023-03-15 023535](https://user-images.githubusercontent.com/102510341/225386105-025dc745-e660-4488-98d3-0b7392072746.png)
![螢幕擷取畫面 2023-03-15 023334](https://user-images.githubusercontent.com/102510341/225386174-1a1ef946-8988-45b9-b7aa-ab8e5342590c.png)

---
## 分析流程：　　
1. EDA：Correlation、Data visulization
2. 決定最佳分群數：使用Gaussian Mixture Model的BIC分數和SOM
3. Unupervised ：使用Gaussian Mixture Model和soft vote進行分群
4. Supervised ：使用來自分群的預測信心水準作為訓練標籤進行分類
5. 建模：使用ET、QDA、LDA、BGMM 和 LGBM
6. 混和預測：將分群預測結果與分類預測結果合併
7. 迭代分類：使用 BGMM 分類器進行
