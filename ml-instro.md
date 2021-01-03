Machine learning has taken over pretty much every industry, owing to the automation and flexibility it is bringing to work. Companies of all sizes are using machine learning tools and cloud services. Services like [AWS Comprehend ](https://medium.com/better-programming/3-natural-language-processing-tools-from-aws-to-python-954dbb34b189)and other similar services to improve their business workflows and create new products.





由于机器学习带来的自动化和灵活性，机器学习几乎已经占据了所有行业。各种规模的公司都在使用机器学习工具和云服务。像AWS这样的服务可以理解和其他类似的服务，以改进他们的业务流程和创建新产品。





由于机器学习带来的自动化和灵活性，机器学习几乎已经占据了所有行业。各种规模的公司都在使用机器学习工具和云服务。像AWS这样的服务可以理解和其他类似的服务，以改进他们的业务流程和创建新产品。



然而，MLOps是其中一个稍微更新的概念，在复杂的机器学习部署环境中被证明是有帮助的。



后缀“Ops”是不是有点用过头了？对。



但MLOps在科技界有自己的位置。这实际上是一种成熟纪律的表现。随着机器学习模型管理和部署的最佳实践越来越具体化，开发能够管理机器学习工作流中许多平凡且容易出错的步骤的自动化平台变得更加容易。



这就是为什么最近有很多产品充斥市场，试图争夺你的注意力。有开源的MLOps选项和企业解决方案。



一些人非常关注机器学习模型部署工作流中的一个步骤，而另一些人则试图管理整个过程。



在今天的文章中，我们将讨论如何通过使用DevOps和实现机器学习的五个最佳工具实现机器学习的自动化。



## 1. MLflow



使用MLflow等工具，数据专业人员现在可以轻松地自动化复杂的模型跟踪。MLflow在2018年Spark+AI峰会上首次亮相，是Apache的又一个项目。MLflow允许数据科学家自动化模型开发。通过MLflow，可以使用跟踪服务器更容易地选择最优模型。参数、属性和性能指标都可以记录到这个服务器上，然后可以用来快速寻找符合特定条件的模型。flow和MLflow正迅速成为自动化机器学习模型的实现、集成和开发的主要工具。



虽然MLflow是一个强大的工具，用于对日志记录的模型进行排序，但它几乎不能回答应该生成什么模型的问题。这是一个有点困难的问题，因为根据您的模型，培训可能需要大量的资源，超参数可能是不直观的，或者两者兼而有之。即使是这些问题，在一定程度上也可以自动解决。





[MLflow](https://www.mlflow.org/) 是用于管理端到端机器学习生命周期的开源平台。 它具有以下主要组件：

- 跟踪：用于跟踪试验，以记录和比较参数与结果。
- 模型：用于通过各种 ML 库管理模型，并将其部署到各种模型服务和推理平台。
- 项目：用于将 ML 代码打包成可重用、可再现的格式，以便与其他数据科学家共享或转移到生产环境。
- 模型注册表：使你可以将模型存储集中化，以便使用版本控制和批注的功能来管理模型的完整生命周期阶段转换：从过渡到生产。
- 模型服务：可用于将 MLflow 模型以 REST 终结点的形式托管。

MLflow 支持 [Java](https://www.mlflow.org/docs/latest/java_api/index.html)、[Python](https://www.mlflow.org/docs/latest/python_api/index.html)、[R](https://www.mlflow.org/docs/latest/R-api.html) 和 [REST](https://docs.azure.cn/zh-cn/databricks/dev-tools/api/latest/mlflow) API。

https://github.com/mlflow/mlflow







## 2. Pachyderm



https://www.pachyderm.com/

管理您的数据管道、模型和数据集是一个复杂的过程，其中包含许多活动部件。厚皮动物旨在简化这一过程，使其既可追溯又可复制。



Pachyderm是一个数据科学平台，它将端到端管道与Kubernetes上的数据沿袭相结合。该平台以企业规模为基础，为任何项目增加基础。这个过程从数据版本控制和数据管道结合开始，这将导致数据沿袭，最后部署机器学习模型。



它不仅跟踪数据修订，还跟踪相关的转换。此外，Pachyderm澄清了转换依赖关系以及数据沿袭。它使用保持所有数据最新的数据管道为数据提供版本控制。





## 3. Kubeflow



Kubeflow是一个机器学习平台，用于管理Kubernetes上ML工作流的部署。Kubeflow最棒的部分是它提供了一个可伸缩和可移植的解决方案。



这个平台最适合希望构建和试验数据管道的数据科学家。Kubeflow还非常适合将机器学习系统部署到不同的环境，以便执行测试、开发和生产级别的服务。



Kubeflow是由Google创建的一个运行TensorFlow的开源平台。因此，它最初是通过Kubernetes运行TensorFlow作业的一种方式，但后来扩展为一个运行整个ML管道的多云、多架构框架。使用Kubeflow，数据科学家不需要学习新的平台或概念来部署他们的应用程序或处理网络证书等，他们可以像在TensorBoard上一样部署他们的应用程序。

https://www.kubeflow.org/



## 4. DataRobot



DataRobot is a very useful AI automation tool that allows data scientists to automate the end-to-end process for deploying, maintaining, or building AI at scale. This framework is powered by open source algorithms that are not only available on the cloud but also on-premise. DataRobot allows users to empower their AI applications easily and quickly in just ten steps. This platform includes enablement models that focus on delivering value.

DataRobot not only works for data scientists but also non-technical people who wish to maintain AI without having to learn the traditional methods of data science. So, instead of having to spend loads of time developing or testing machine learning models, data scientists can now automate the process with DataRobot.

The best part of this platform is its ubiquitous nature. You can access DataRobot anywhere via any device in multiple ways according to your business needs.







DataRobot是一个非常有用的人工智能自动化工具，它允许数据科学家自动化部署、维护或大规模构建人工智能的端到端过程。这个框架由开源算法提供支持，这些算法不仅在云上可用，而且在本地也可用。DataRobot让用户只需十步就可以轻松快速地为他们的人工智能应用程序授权。该平台包括专注于交付价值的支持模型。



DataRobot不仅为数据科学家工作，也为那些希望在不必学习传统数据科学方法的情况下维护人工智能的非技术人员工作。科学家们现在可以用机器学习数据，而不是用机器来测试数据。



这个平台最好的部分是它无处不在的特性。根据您的业务需要，您可以通过任何设备以多种方式访问DataRobot。





## 5. Algorithmia

https://algorithmia.com/



最后，最流行的MLOps工具之一绝对是算法。这个框架使用人工智能来产生一组不同的IT架构。此服务允许创建使用社区贡献的机器学习模型的应用程序。除此之外，算法为算法智能的高级开发提供了可访问性。



目前，该平台拥有超过60000名开发者，拥有4500个算法。



Algorithmia于2014年由两位总部位于华盛顿的开发人员创建，目前拥有70名员工，发展迅速。



这个平台不仅允许您从任何框架或语言部署模型，而且还可以连接到大多数数据源。它在云和本地基础设施上都可用。算法使用户能够通过测试、保护和管理来持续管理他们的机器学习生命周期。



主要目标是实现机器学习模型的部署、服务和管理的无障碍路线。







https://www.theseattledataguy.com/5-great-mlops-tools-to-launch-your-next-machine-learning-model/#page-content

