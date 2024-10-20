# Loss Funcations and Optimization

## Date: 10/17/24
Writer: heMing

## Recall
1. challenge of image recognization\
and try to hone in on idea of a **data-driven approach**.
2. k-nearest neighbor classifier:\
learn decision boundries to seperate these data points into classes
cross validation and hyperparameters
3. linear classification:
an example of **parametric classifier**, _all of knowledges about training data gets summarized into parameters matrix W_.
each rows corresponds to a weighting between the pixel values of image and that class -> **learn a template**

### TODO 
1. **loss function**: quantifies unhappiness with the scores aross the training data.
to define how good the model are.
to quantify the badness of any particular W.
2. **optimization**: a way that efficiently find the parameters that minimize the loss function.

## Loss
$L_i$: loss of $x_i$
$L = sum L_i$
### multi-class SVM loss
![{3532C671-D543-4922-81ED-EE8CC76CF3F7}](https://github.com/user-attachments/assets/fece5771-7d8a-4dbd-9401-356210029614)
$L_i$, for $x_i$, when compute loss, we only count the score that greater than i, i.e. if socre of some categories is less than the socre of correct category, we did't count this in.

- we don't care about the specific value of score, we only care that if the correct score is the largest. We only care about is getting the correct score to be greater than one (margin) more than the incorrect scores.
- minimum loss: 0; maximum loss: infinity.
- Q3: An initialization W is small so all s(calculate score) is about 0. What is the loss?
Answer: number of class minus 1. It's not zero beacause there is margin exists.
- Q4: loss function of total loss is average of $L_i$ instead of sum
A: doesn't change anything, we also get the same classifier. Just resacle the loss.
- ![{21B7C3E9-20D0-43BF-B857-B8B7EA4F72FD}](https://github.com/user-attachments/assets/ba0c69c8-4f3f-4ff8-a445-4187650cc49f)
this would be difference.
change the trade-offs between good and badness in a non-linear way, this would end up actually computing a different loss function.

**different between squared loss and non-squared loss**:
- squared loss: we don't want any wrong, if it's wrong, we got squared loss, that's big.
- non-squared loss: we don't care between being a little bit wrong and being a lot wrong, being a lot wrong kind of like, if an example is a lot wrong, we increase it and make it a little bit less wrong.
- the choice is up to how much we care about different categories of errors.

### regularization loss
- if we got W which has the zero loss, the W is not unique and there are many Ws.
- we don't actually care about the classier performance on training data, we only care about the performance on test data. -> solution: **Regularization**
- object: penalize the complexity of the model, rather than explicitly trying to fit the training data.
- simpler W has a high priority, beacause it is more likely to generalize to new observations in the future. Among competing hypotheses, the simplest is the best. - Occam's Razor
- whole loss function: data loss(to fit the data) + regularization loss(encourage model to somehow pick a simpler W)
- common regularization method:
![image](https://github.com/user-attachments/assets/e750a10e-8d28-468e-b948-8e811832409e)

  1. L2 regularizaiton
  2. L1 regularization : has property like encouraging sparsity in matrix W.
  3. Elastic net (L1 + L2)
  4. Max norm regularization
  5. Dropout
  6. Batch normalization stochastics depth
- examples
-   training data x: vector of four ones, W1 = (1, 0, 0, 0), W2 = (0.25, 0.25, 0.25, 0.25)
-   1. in terms of linear classification, W1 is same to W2, beacuse the results of product between x and Ws are same.
    2. L2 regularization prefer W2, because it has a smaller norm. prefer to spread the infulence across all different values of x. maybe it could be more robust.
    3. L1 regularization prefer W1, because model with W1 is less complex. generally prefers sparse solutions. maybe we measure model complexity by the number of non-zero entries in the weight vector.
 
### softmax classifier
![image](https://github.com/user-attachments/assets/938185d9-34d0-4542-b495-8e2c7c63e1bd)
- target: the output is, we want the score of correct class is one.
- Q1: min and max possible softmax loss: min: 0 max: infinity.
probability distribution that we want is one on the correct class and zero on the incorrect classes.
- Q2: Usually at initialization W is small so all s is about 0, what is the loss?
log(C), C is the number of classes.
- 
### softmax vs. SVM
- Q. suppose I take a datapoint and I jiggle a bit(changing its score slightly). What happens to the loss in both cases?
softmax might got a different result, but SVM won't change.

## Optimization

### gradient descent
use gradient to decide the direction we will take
- Stochastic Gradient Descent(SGD): at every iteration, we sample some small set of training examples, called a minibatch. use minibatch to compute an estimate of the full sum and true gradient.
