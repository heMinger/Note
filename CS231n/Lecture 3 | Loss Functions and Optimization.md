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
