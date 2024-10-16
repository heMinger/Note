# Image Classification

## 日期
日期：2024-10-16

## 课程目标 
- dive into details, starts to see, in much more depth, how these learning algorithm actually work in practice.
- 目标 2
- 目标 3

## Image classification
### 1. Chanllenges
- Viewpoint variation: different viewpoint of same object, got a completely different pixels.
- Illumination: too brightness or dark.
- Deformation: various pose of same category.
- Occlusion: part or most of object is obscured.
- Background Clutter
- Intraclass variation: One category spans different visual appearances, like color of cat can be different.

## 2. Data-Driven Approach
1. collect a dataset of images and labels
2. use Machine Learning to train a classifier
3. Evaluate the classifier on new images

#### simple classifier
##### Nearest Neighbor 
- Train: memorize all data and labels
- Predict: predict the label of the most similar training image.
- How to compare, define similarity: L1 distance.
- Thoughts: 很不合理啊，如果image A中的小猫占据了整张图片，imageB中的小猫蜷缩在图片右下角，他们两个按照这种定义的相似度应该很低吧。
- Question:
-   1. fast train process & slow predict process : With N examples, training: O(1), predict: O(n); *We can accept slow train and fast predict*.
    2. 

##### K-Nearest Neighbors
1. take majority vote from K closest points.
2. distance function: specify different distance metrics, KNN can be applied very generally to basically any type of data.
- L1 distance depends on the choice of coordinates systems.(sort of coordinate dependent)
- L2: won't change by coordinates systems
3. hyperparameter K:
- usually, try some parameters and choose the best one.
- experience value: K = 1 usually work well
4. split data
- choose hyperparameters that work best on the data(whole data): Bad
- split data into train and test, choose hyparameters that work best on test data: Bad, because no idea how algorithm will perform on new data.
- split data into train, val and test, choose hyparameters on val and evaluate on test: Better
5. Cross-Validation
  - split data into folds, try each fold as validation and average the results: Useful for small datasets, but not used frequently in deep learning.

## Parametric Approach

f(x, W): take the input and some weights or parameters
**summarize knowledge of the trainin data and stick all that knowledge into these paramenters, W.**
In KNN, we should keep the whole training data and use them during test time. But in parametric approach, we could throw out the training data and use W only.


### Linear Classification
neural networks kind of like Lego, we can stack different layers arbitrily, and linear classification is kind of like the most basic building blocks.
f(x, W) = Wx + b
