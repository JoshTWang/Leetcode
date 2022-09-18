#### Machine learning Model

> A **machine learning algorithm** is the process that uncovers the underlying relationship within the data.
>
> The outcome of a machine learning algorithm is called **machine learning model**, which can be considered as a `function` $F$, which outputs certain results, when given the input.
>
> Rather than a predefined and fixed function, a machine learning model is derived from historical data. Therefore,  when fed with different data, the output of machine learning algorithm changes, i.e. the machine learning mode changes.
>
> 
>
> The task of machine learning, is to ***learn*** the function, from the vast mapping space.



* What distinguishes a machine learning algorithm from a non-machine-learning algorithm, such as a program that controls traffic lights, is its ability to **`adapt`** its behaviors to new input. And this adaptation, which seems to have no human intervention, occasionally leads to the impression that the machine is actually `learning`. 

* However, underneath the machine learning model, this adaptation of behaviors is as rigid as every bit of machine instructions that are programmed by humans. 



#### Supervised VS. Unsupervised

* For any machine learning problem, we start from a data set, which consists of a group of **`samples`**. Each sample can be represented as a tule of **`attributes`**.

##### Supervised Learning

In a **supervised** learning task, the data sample would contain a target attribute $y$, also known as **ground truth**. And the task is to learn a function $F$, that takes the non-target attributes $X$ and output a value that approximates the target attribute, *i.e.* $F(X)≈y$. The target attribute $y$ serves as a teacher to guide the learning task, since it provides a benchmark on the results of learning. Hence, the task is called supervised learning. 

In the Iris data set, the *class* attribute (category of iris flower) can serve as a target attribute. The data with a target attribute is often called "**labeled**" data. Based on the above definition, for the task of predicting the category of iris flower with the labeled data, one can tell that it is a supervised learning task. 

##### Imsupervised Learning

In contrary to the supervised learning task, we do not have the ground truth in an unsupervised learning task. One is expected to learn the underlying patterns or rules from the data, without having the predefined ground truth as the benchmark.

One might wonder, without the *supervision* of the ground truth, can we still learn anything? The answer is yes. Here are a few examples of the unsupervised learning tasks:

- **Clustering**: given a data set, one can cluster the samples into groups, based on the similarities among the samples within the data set. For instance, a sample could be a customer profile, with attributes such as the number of items that the customer bought, the time that the customer spent on the shopping site *etc*. One can cluster the customer profiles into groups, based on the similarities of the attributes. With the clustered groups, one could devise specific commercial campaigns targeting each group, which might help attract and retain customers. 

- **Association**: given a data set, the association task is to uncover the hidden association patterns among the attributes of a sample. For instance, a sample could be a shopping cart of a customer, where each attribute of the sample is a merchandise. By looking into the shopping carts, one might discover that customers who bought beers *often* bought diapers as well, *i.e.* there is a strong association between the beer and the diaper in the shopping cart. With this learned insight, the supermarket could rearrange those strongly associated merchandise into the nearby corners, in order to promote the sales of one or another.

##### Semi-supervised Learning

In a scenario where the data set is massive but the labeled sample are few, one might find the application of both supervised and unsupervised learning. We can call this task as ***semi-supervised learning***.

In many scenarios, it is prohibitively time-consuming and expensive to collect a large amount of labeled data, which often involves manual efforts. It takes two and a half years for a research team from Stanford to curate the famous [ImageNet](http://image-net.org/about-stats) which contains millions of images with thousands of manually labeled categories. As a result, it is often the case that one has a large amount of data, yet few of them are accurately "labeled", e.g. videos without category or even a title.

> By combining both the supervised and unsupervised learning in a data set with few labels, one could exploit the data set to a better extend and obtain a better result than just applying each of them individually. 

For example, one would like to predict the label of images, but only $10%$ of the images are labeled. By applying supervised learning, we train a model with the labeled data, then we apply the model to predict the unlabeled data. It would be hard to convince ourselves that the model would be general enough, after all we learned from only the minority of data set. A better strategy could be to first cluster the images into groups (unsupervised learning), and then apply the supervised learning algorithm on each of the groups individually. The unsupervised learning in the first stage could help us to narrow down the scope of learning so that the supervised learning in the second stage could obtain better accuracy.