# Image Analogies

## Abstract
 So, this paper describes a framework to get the analogy images. \
 This framework uses there images as input, A, A' and B, respectively. Then we could got image B', that B' is same filter version to B with A' is filtered by A.

## Some problems
1. A : A' :: B : B'
2. could learn a very complex and non-linear image filters, which could create a vatious types of artistic rendering.
3. all types of rendering could done by a same general  mechanism, and don't need to invented individually
4. definition of similarity\
   4.1 what should measure\
     4.1.1 relationship between unfiltered image adn its respective filtered version\
     4.1.2 relationship between the source pair and target pair, taken as a whole\
   4.2 In this paper \
     4.2.1 based on an approxiamtion to a Markov random field model\
     4.2.2 using raw pixel values & optional steerable filter responsed.\
     4.2.3 joint statistics of neighborhoods -> to measure relationships between the source and target image pair.\
5. index and search image A, A' and B\
     5.1 to choose the appropriate parts of the transform A->A' in synthesizing B->B'\
     5.2 correspond to best_match.py: combination of best approximate search and best coherence search
6. analyze by the luminance space

## Algorithm
