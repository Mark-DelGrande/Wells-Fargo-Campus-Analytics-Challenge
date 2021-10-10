# Wells-Fargo-Campus-Analytics-Challenge

Wells Fargo Campus Analytics Challenge 2021: Machine Learning Model to
Predict Suspected Elder Fraud

October 11, 2021 | Mark Del Grande

Feature Engineering {#h.rrar1dgps27e .c11}
===================

The first step in making a model was to understand what all of the data
represented. After examining the data I had a few initial thoughts about
what useful features I could create from the data and which pre-existing
feature would be important. Here they are:![](images/image4.png)

Is this an in-state transaction? {#h.qzl25hpt1jm7 .c4}
--------------------------------

For this feature I standardized all the values in both the
STATE\_PRVNC\_TXT, and CUST\_STATE columns. I then compared the two to
see if they were the same and then converted it to binary 1 for in state
0 for out of state. As you can see from the confusion matrix on the left
there is some level of correlation between being an Instate transaction
and a fraudulent transaction.

Customer Age {#h.n9uk3gqbtygh .c4}
------------

Clearly, since this whole competition was based around Elder fraud I
knew from the very beginning this was going to be an important Feature.

Days Between Transaction and Last Account Update {#h.4dvmbvz9cm0p .c4}
------------------------------------------------

My thoughts with this feature were that people may have had their
account updated without them knowing so there could be a link between a
 recent password or phone number update with the account and a
fraudulent transaction. For this I made two features called
DAYS\_SINCE\_PWD\_UPDT and DAYS\_SINCE\_PH\_NUM\_UPDT.

Percentage of Account the Transaction is For {#h.3m0prbp7p0kk .c4}
--------------------------------------------

Next I wanted to look at what percentage of the account was being
withdrawn. For example I would think that if the entire account balance
was being withdrawn and one transaction that would raise some red flags.
In addition to this I use the TRAN\_AMT and ACCT\_PRE\_TRAN\_AVAIL\_BAL
to understand how much money this percentage was worth.

Device Age Compared to Account Age {#h.63qeittzswtc .c4}
----------------------------------

Another feature I created was looking at how long the account had been
open compared to how long this device had been associated with the
account. This allowed for me to see if an account had just been opened
and that's why the device is new or if this device had just been added
to a preexisting old account. A new device on an old account may be
represented by a hacker adding a device to someone's account to make a
fraudulent transaction.

One Hot Encodings {#h.35qld53ottsq .c4}
-----------------

The last feature engineering I tired was one hot encoding on several of
the categorical columns such as AUTHC\_PRIM\_TYPE\_CD, ALERT\_TRGR\_CD,
DVC\_TYPE\_TXT, and AUTHC\_SCNDRY\_STAT\_TXT. I dropped all of these
except for the ALERT\_TRGR\_CD encoding for MOBL since they had
negligible impacts on the end results and led to a more complicated
model.

 {#h.xnml42owikti .c1}

Classification Model {#h.ihqgc9tdk9mj .c11}
====================

Once the data was formatted and ready for predictions I started by
training an XG boost classification model. The data was split into 67%
for training and 33% for testing. With this data split my model achieved
an Accuracy rate of 95.09%.

![](images/image2.png)

Here is the importance of all the features. In my final model I found
that these 12 features were the most beneficial to my predictions.
Therefore, I dropped all other features I had made to keep the model
relatively simple and still have accurate results.

![](images/image5.png)

Above is what the tree plot looked like once the XG boost Classification
model was trained.

![](images/image3.png)

Lastly, here is an example of a test prediction. The top picture shows
the data that was inputted into the model and the bottom pictures show
the score given to this data and the reasoning behind the score. It
scored a -6.688 and this means the model was 99.9% sure that this was
not a fraudulent transaction. ![](images/image1.png)

![](images/image6.png "footer graphic")

