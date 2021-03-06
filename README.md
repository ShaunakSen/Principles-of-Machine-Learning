# Principles-of-Machine-Learning
## Module 1
___

## Introduction to Classification
___

**Classification**: raining set of observations + test set used for evaluations
We want to run predictions on test set
A bit of noise on training data is Ok
Training data:more the merrier

Represent each observation as a vector of nos.
Label: -1 : not chair, 1: chair

Each obs is rep by a set of nos (features):
manhole: [5 3 120 12 1 0]
Indices:
0: no of events last yr
1: no of serious evts last yr
2: no of electric cables
....

Computaion is easier for fewer features, but then we leave out info..

Now you think that manholes with more cables more recent serious events and so on would
be more prone to explosions and fires in the near future, but what combination of them
would give you the best predictor? How do you combine them together? You could add them
all up, but that might not be the best thing. You could give them all weights and add them
all up, but how do you know the weights? And that’s what machine learning does for you.
**It tells you what combinations to use to get the best predictors.**

But for the manhole problem,
we want to use the data from the past to predict the future. So for instance, the future data
might be from 2014 and before, and the label would be 1 if the manhole had an event in
2015. So that’s our training set, and then for the test set, the feature data would be
from 2015 and before and then we would try to predict what would happen in 2016.

So just to be formal about it, we have each observation being represented by our set of features,
and the features are also called predictors or covariant or explanatory variables or independent
variables, whatever they are – you can choose whatever terminology you like. And then we
have the labels, which are called y

Let’s take a simple example of – simple
version of the manhole example, where we have only two features: the year the oldest cable
was installed and the number of events that happened last year. So each observation can
be represented as a point on a two-dimensional graph, which means I can plot the whole dataset.
So something like this, where each point here is a manhole and I’ve labelled it with whether
or not it had a serious event in the training set. So these are the manholes that didn’t
have events, and these are the ones that did. And then I’m going to try to create a function
here that’s going to divide the space into two pieces, where on one side of this – on
one side over here of the decision boundary, I’m going to predict that there’s going
to be an event, and on the other side of the decision boundary, I predict there will be
no event. So this decision boundary is actually just the equation where the function is 0,
and then where the function is positive we’ll predict positive and where the function is
negative we’ll predict negative. And so this is going to be a function of these two
variables, the oldest cable and then the number of events last year. And the same idea holds
for the commuter vision problem that we discussed earlier. We’re trying to create this decision
boundary that’s going to chop the space into two pieces, where on one side of the
decision boundary we would predict positive, and then on the other side we’d predict
negative. 

And the trick is, how do we create this decision boundary? How do we create this
function f? Okay, so given our training data, we want to create our classification model
f that can make predictions. The machine learning algorithm is going to create the function
f for you, and no matter how complicated that function f is, the way to use it is not very
complicated at all. The way to use it is just this: the predicted value of y for a new x


Classification is for yes or no questions. You can do a lot if you can answer yes or
no questions. 
- So for instance, think about like handwriting recognition. For each letter
on a page, we’re going to evaluate whether it’s a letter A, a yes or no. 
- And if you’re
doing like spam detection, right, the spam detector on your computer has a machine learning
algorithm in it. Each email that comes in has to be evaluated as to whether or not it’s
spam. 
- Credit defaults: right, whether or not you get a loan depends on whether the bank
predicts that you’re going to default on your loan, yes or no.


## Loss functions for classification:
___

how do we measure classification error?

one very very simple way to do it is to use
just a fraction of times our predictions are wrong. So just the fraction of times the sign
of f(x) is not equal to the truth y, and I can write it like: 

![img:pic1](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic1.PNG)

The issue with
this particular way of measuring classification error is that if you want to try to minimize
this, you could run into a lot of trouble because it’s computationally hard to minimize
this thing.
So let’s give you the geometric picture here: the decision boundary is this
line right here, and f being positive is here and f being negative is here, and the red
points are all misclassified
![img:pic1](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic1.PNG)

Okay so over here
![img:pic2](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic2.PNG)

on the right either f is positive and y is also positive, so y-f is
positive, or they’re both negative so the product is positive again. And then over here
on the left, we have cases where the sign of f is different from y, so the product is
negative. And then the ones I suffer a penalty for are all these guys over there.

Now
this function tells us what kind of penalty we’re going to issue for being wrong. Okay
so right now, if y times f is positive, it means we got it right and we lose 0 points.
And if we get it wrong, the point is on the wrong side and so we lose one point. Now I’m
just going to write this function another way which is like this, okay, so we lose one
point if y-f is less than 0, and otherwise we lose no points. And this is the classic
0-1 loss. It just tells you whether your classifier is right or wrong. And then this thing is
called a loss function, and there are other loss functions too, and this one’s nice
because – but it’s problematic because it’s not smooth, and we have issues with
things that are not smooth in machine learning.

![img: pic3](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic3.PNG)

these points over here are the ones that
are very wrong, because they’re on the wrong side of the decision boundary, but they’re
really far away from it too. And these points are wrong, but they’re not as bad; they’re
on the wrong side of the decision boundary but they’re pretty close to it. And then
we’ll say these points are sort of correct, and we’ll say these points are very correct.

![img: pic3](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic4.PNG)

And what we’ll really like to have are loss functions that don’t penalize the very correct
ones, but the penalty gets worse and worse as you go to the left. But maybe we can use
some other loss function, something that – you know, maybe we get a small penalty for being
sort of correct and then a bigger penalty for being sort of wrong and then a huge penalty
for being very wrong.

![img: pic5](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic5.PNG)

Okay so start here: the misclassification error is the fraction
of times that the sign of f is not equal to the truth y that’s this. I can rewrite it
this way, okay, the number of times y times f is less than 0. And then we’ll upper-bound
this by these loss functions. Okay, so then what is a good way to try to reduce the misclassification
error which is that guy? Well you could just try to minimize the average loss. So if you
had a choice of functions f, you could try to choose f to minimize this thing, which
hopefully would also minimize this but in a computationally easier way.

![img: pic6](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic6.PNG)

## Statistical Learning Theory for Supervised Learning
___

The key principle in statistical learning theory is the principle of Ockham’s razor

>Now Ockham’s razor is the idea that the best models are simple >models that fit the
>data well 

 Ok, so let’s start with a basic one dimension
regression model. This model I have on the screen there is not good; it’s really over-fitted.
So it’s just not going to generalize well to new points; it just can’t predict well.

![img: pic7](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic7.PNG)


Now let’s say that I have some way to measure model complexity, and the more complex the
models I have, the more they tend to over-fit and the simpler models, they tend to under-fit.
Now this plot is the key to understanding learning theory. If I plot training error,
which is this curve over here, then as the models grow more and more complex, the training
error continues to decrease, because I can just over-fit more and more. But at the same
time, if I do that, the test error gets worse and worse. If I, on the other hand, under-fit,
then I won’t do well for either training or test. Where I want to go, is this sweet
spot in the middle here. And the idea of this plot it holds true for classification, progression,
whatever.

![img: pic8](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic8.PNG)

So the idea is that the best models are simple models that fit the data well.
So what we need is a balance between accuracy and simplicity.

So the most common machine learning methods, they choose
their function f, to minimize training error and model complexity, which aims to thwart
the cursive dimensionality. So the cursive dimensionality is that we tend to over-fit
when we have a lot of features and not as much data. Data needs to increase exponentially
with the number of features in order not to have this issue of over-fitting. So we’re
going to choose a model that’s both simple – low complexity – and has low training
error; and this exactly is the principle of Ockham’s razor. 

![img: pic9](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic9.PNG)

**So
this is the main foundation of machine learning; it’s all about creating functions that minimize
the loss, but also keep the model simple**

## Logistic regression
___

Now, logistic regression uses this loss function
over here that we talked about. You saw this before. It’s the dark blue curve over here.

![img: pic10](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic10.PNG)

Now, we have to choose what kind of
model f is going to be, and we’ll choose a linear model. So it’s a weighted sum of
the features. For instance, if we’re trying to predict income, our model might look like
three times the hours a person works, plus four times the years of experience and so
on. So here, the first feature x1 is hours and beta one is 3 and so on. I can write it
here in summation notation. So f is the sum of the weighted features, where the weights
are called beta. And I also call the beta “coefficients”

![img: pic11](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic11.PNG)

So here, all I did was
plug this form of f into that minimization problem for logistic regression. So now, it’s
going to try to find the weights that minimize the sum of the training losses. And this is
what logistic regression does; no more, no less. It just chooses the coefficients (those
betas) to minimize this thing.

## Maximum Likelihood Perspective

___

Logistic Function:

![img: pic12](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic12.PNG)

It was a very early **population model**

When a country gets full popn saturates

Prob lies bw 0 and 1
so u can enter any no in the function and it outputs a probability

Formula for function:

![img: pic13](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic13.PNG)

so when t is really big, then e to the t is much bigger than 1,
and so this one basically gets ignored down here and you get 1. And if t is really small,
then the top goes to 0 and the bottom goes to 1, and you get 0.

where does logistic regression come in?

Let’s model the probability that the outcome is – the outcome y is 1 for a specific accent
beta just like this

![img: pic14](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic14.PNG)

So why would we do this? It looks like a complicated function;
where did I get this? So here’s the trick: the thing on the left is a probability, so
the thing on the right had better be a probability. And guess what, we know it is. It’s just
a logistic function, and a logistic function only produces probabilities. Okay so now this
model makes sense, that’s why I want to model a probability like this. And now I’m
just putting it in matrix notation, just to make my life a little bit easier instead of
having to write all these sums all over the place, I can just write this matrix x times
the vector beta.

Now I also can compute the probability that the label is minus 1, given
xi and beta using the model. So it’s just one minus the probability that it’s 1, so
it’s just 1 minus that guy, and you can simplify that and make it look like this.
Now I’m going to need to calculate the likelihood of each of the observations, which is the
probability to observe the label y that I actually observed, given it’s x in the model
beta.

![img: pic15](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic15.PNG)

And I am actually almost there already, because I’ve already done all of that already.
So this is it, right, if y is minus 1, then you use this one. If y is plus 1, then you
use this one, and that’s – that’s this probability right here. 

![img: pic16](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic16.PNG)


And then I can simplify
this a little bit more, because remember y is minus 1, so I can always put a minus y
here because minus y is just 1, and I can do this same thing with the other term here.
So first thing I want to just divide top and bottom by e to the x beta, and I end up with
something that looks like that. And then I can always multiply by 1 in disguise, because
remember y is positive 1, so I can just write this as minus yx because I just multiply by
1 here which is just the y. Now the interesting thing is these two expressions should look
rather similar to you; in fact, they should look exactly the same because they are.

![img: pic17](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic17.PNG)

hen I compute the likelihood for all
the data, I have to multiply all these probabilities together. 

![img: pic18](https://github.com/ShaunakSen/Principles-of-Machine-Learning/blob/master/pic18.PNG)
