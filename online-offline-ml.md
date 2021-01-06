

https://www.c-sharpcorner.com/article/batch-and-online-machine-learning/

https://www.ververica.com/blog/flink-for-online-machine-learning-and-real-time-processing-at-weibo

https://dziganto.github.io/data%20science/online%20learning/python/scikit-learn/An-Introduction-To-Online-Machine-Learning/

hinge-loss



#### 离线学习

In machine learning, systems which employ offline learning do not change their approximation of the target function when the initial training phase has been completed.[citation needed] These systems are also typically examples of eager learning.





#### 增量学习





#### 在线学习



In [computer science](https://en.wikipedia.org/wiki/Computer_science), **online machine learning** is a method of [machine learning](https://en.wikipedia.org/wiki/Machine_learning) in which data becomes available in a sequential order and is used to update the best predictor for future data at each step, as opposed to batch learning techniques which generate the best predictor by learning on the entire training data set at once. Online learning is a common technique used in areas of machine learning where it is computationally infeasible to train over the entire dataset, requiring the need of [out-of-core](https://en.wikipedia.org/wiki/Out-of-core) algorithms. It is also used in situations where it is necessary for the algorithm to dynamically adapt to new patterns in the data, or when the data itself is generated as a function of time, e.g., [stock price prediction](https://en.wikipedia.org/wiki/Stock_market_prediction). Online learning algorithms may be prone to [catastrophic interference](https://en.wikipedia.org/wiki/Catastrophic_interference), a problem that can be addressed by [incremental learning](https://en.wikipedia.org/wiki/Incremental_learning) approaches.





The main objective of online learning algorithms is to minimize the regret
在线学习算法的主要目标是使regret最小化





准确地说，Online Learning并不是一种模型，而是一种模型的训练方法，Online Learning能够根据线上反馈数据，实时快速地进行模型调整，使得模型及时反映线上的变化，提高线上预测的准确率。Online Learning的流程包括：将模型的预测结果展现给用户，然后收集用户的反馈数据，再用来训练模型，形成闭环的系统。如下图所示：