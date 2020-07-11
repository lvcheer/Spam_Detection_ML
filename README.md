# Spam Email Classifier Using NaiveBayes and XGBoost Classifiers

This is a project I am working on while learning concepts of data science and machine learning. The goal here is to identify whether an email is spam or ham. We will take a dataset of labeled email messages and apply classification techniques. We can later test the model for accuracy and performance on unclassified email messages. Similar techniques can be applied to other NLP applications like sentiment analysis etc.

## Data

I am using Spambase dataset from [UCI's ML Repository](https://archive.ics.uci.edu/ml/datasets/Spambase) which can be downloaded from the link.

The last column of 'spambase.data' denotes whether the e-mail was considered spam (1) or not (0), i.e. unsolicited commercial e-mail. Most of the attributes indicate whether a particular word or character was frequently occuring in the e-mail. The run-length attributes (55-57) measure the length of sequences of consecutive capital letters. Here are the definitions of the attributes:

- 48 continuous real [0,100] attributes of type word_freq_WORD
= percentage of words in the e-mail that match WORD, i.e. 100 * (number of times the WORD appears in the e-mail) / total number of words in e-mail. A "word" in this case is any string of alphanumeric characters bounded by non-alphanumeric characters or end-of-string.

- 6 continuous real [0,100] attributes of type char_freq_CHAR]
= percentage of characters in the e-mail that match CHAR, i.e. 100 * (number of CHAR occurences) / total characters in e-mail

- 1 continuous real [1,...] attribute of type capital_run_length_average
= average length of uninterrupted sequences of capital letters

- 1 continuous integer [1,...] attribute of type capital_run_length_longest
= length of longest uninterrupted sequence of capital letters

- 1 continuous integer [1,...] attribute of type capital_run_length_total
= sum of length of uninterrupted sequences of capital letters
= total number of capital letters in the e-mail

- 1 nominal {0,1} class attribute of type spam
= denotes whether the e-mail was considered spam (1) or not (0), i.e. unsolicited commercial e-mail.


## Model

We use Multinomial Naive Bayes Classifier and then XGBoost Classifier to fit the model looking for improvement in results. In the end, the accuracy score and confusion matrix tell us how well our model works.

### Multinomial Naive Bayes Classifier

In statistics, Naïve Bayes classifiers are a family of simple "probabilistic classifiers" based on applying Bayes' theorem with strong (naïve) independence assumptions between the features. They are among the simplest Bayesian network models. Naïve Bayes classifiers are highly scalable, requiring a number of parameters linear in the number of variables (features/predictors) in a learning problem.

With a multinomial event model, samples (feature vectors) represent the frequencies with which certain events have been generated by a multinomial {\displaystyle (p_{1},\dots ,p_{n})}(p_1, \dots, p_n) where `{\displaystyle p_{i}}p_{i}` is the probability that event i occurs (or K such multinomials in the multiclass case). A feature vector `{\displaystyle \mathbf {x} =(x_{1},\dots ,x_{n})}{\mathbf  {x}}=(x_{1},\dots ,x_{n})` is then a histogram, with `{\displaystyle x_{i}}x_{i}` counting the number of times event i was observed in a particular instance. This is the event model typically used for document classification, with events representing the occurrence of a word in a single document (see bag of words assumption). The likelihood of observing a histogram x is given by

`{\displaystyle p(\mathbf {x} \mid C_{k})={\frac {(\sum _{i}x_{i})!}{\prod _{i}x_{i}!}}\prod _{i}{p_{ki}}^{x_{i}}}{\displaystyle p(\mathbf {x} \mid C_{k})={\frac {(\sum _{i}x_{i})!}{\prod _{i}x_{i}!}}\prod _{i}{p_{ki}}^{x_{i}}}`

The multinomial naïve Bayes classifier becomes a linear classifier when expressed in log-space:

`{\displaystyle {\begin{aligned}\log p(C_{k}\mid \mathbf {x} )&\varpropto \log \left(p(C_{k})\prod _{i=1}^{n}{p_{ki}}^{x_{i}}\right)\\&=\log p(C_{k})+\sum _{i=1}^{n}x_{i}\cdot \log p_{ki}\\&=b+\mathbf {w} _{k}^{\top }\mathbf {x} \end{aligned}}}{\displaystyle {\begin{aligned}\log p(C_{k}\mid \mathbf {x} )&\varpropto \log \left(p(C_{k})\prod _{i=1}^{n}{p_{ki}}^{x_{i}}\right)\\&=\log p(C_{k})+\sum _{i=1}^{n}x_{i}\cdot \log p_{ki}\\&=b+\mathbf {w} _{k}^{\top }\mathbf {x} \end{aligned}}}`
where `{\displaystyle b=\log p(C_{k})}b=\log p(C_{k})` and `{\displaystyle w_{ki}=\log p_{ki}}w_{{ki}}=\log p_{{ki}}`.

### [Passive Aggressive Classifier](http://jmlr.csail.mit.edu/papers/volume7/crammer06a/crammer06a.pdf)
The passive-aggressive algorithms are a family of algorithms for large-scale learning.
Intuitively, passive signifies that if the classification is correct, we should keep the model, and, aggressive signifies that if the classification is incorrect, update the model to adjust to more misclassified examples. Unlike most others, it does not converge, rather it makes updates to correct the loss.

## Results

The model outputs accuracy of ~97% which is decent enough. We have less than 1.5% false positive and false negative classification each. Check the confusion matrix and classification report below:

![](results.png)

## Future Work
I intend to expend this project by adding a graphical user interface (GUI) where one can paste any piece of text and get its classification in the results.
