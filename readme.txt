Module 1
_______________________________

Introduction to Classification
_______________________________

Classification: raining set of observations + test set used for evaluations
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
It tells you what combinations to use to get the best predictors.

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
negative. And the trick is, how do we create this decision boundary? How do we create this
function f? Okay, so given our training data, we want to create our classification model
f that can make predictions. The machine learning algorithm is going to create the function
f for you, and no matter how complicated that function f is, the way to use it is not very
complicated at all. The way to use it is just this: the predicted value of y for a new x


Classification is for yes or no questions. You can do a lot if you can answer yes or
no questions. So for instance, think about like handwriting recognition. For each letter
on a page, we’re going to evaluate whether it’s a letter A, a yes or no. And if you’re
doing like spam detection, right, the spam detector on your computer has a machine learning
algorithm in it. Each email that comes in has to be evaluated as to whether or not it’s
spam. Credit defaults: right, whether or not you get a loan depends on whether the bank
predicts that you’re going to default on your loan, yes or no.


Loss functions for classification:

how do we measure classification error?

one very very simple way to do it is to use
just a fraction of times our predictions are wrong. So just the fraction of times the sign
of f(x) is not equal to the truth y, and I can write it like [img:pic1]. The issue with
this particular way of measuring classification error is that if you want to try to minimize
this, you could run into a lot of trouble because it’s computationally hard to minimize
this thing.
So let’s give you the geometric picture here: the decision boundary is this
line right here, and f being positive is here and f being negative is here, and the red
points are all misclassified.[img:pic1]

Okay so over here[img: pic2], on the right either f is positive and y is also positive, so y-f is
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
things that are not smooth in machine learning.[img: pic3]

these points over here are the ones that
are very wrong, because they’re on the wrong side of the decision boundary, but they’re
really far away from it too. And these points are wrong, but they’re not as bad; they’re
on the wrong side of the decision boundary but they’re pretty close to it. And then
we’ll say these points are sort of correct, and we’ll say these points are very correct.[img: pic3]

And what we’ll really like to have are loss functions that don’t penalize the very correct
ones, but the penalty gets worse and worse as you go to the left. But maybe we can use
some other loss function, something that – you know, maybe we get a small penalty for being
sort of correct and then a bigger penalty for being sort of wrong and then a huge penalty
for being very wrong. [img: pic5]

Okay so start here: the misclassification error is the fraction
of times that the sign of f is not equal to the truth y that’s this. I can rewrite it
this way, okay, the number of times y times f is less than 0. And then we’ll upper-bound
this by these loss functions. Okay, so then what is a good way to try to reduce the misclassification
error which is that guy? Well you could just try to minimize the average loss. So if you
had a choice of functions f, you could try to choose f to minimize this thing, which
hopefully would also minimize this but in a computationally easier way.[img:pic6]











