# 数据科学入门之二
## 机器学习基础概念

### 什么是机器学习

机器学习是一门交叉科学，涉及到数学、统计学、计算机科学、认知科学等多门学科知识。类似于任何交叉学科，机器学习的定义也十分繁杂，取决于看待问题的角度。譬如从人工智能的角度来看，
>“机器学习是一门人工智能的科学，该领域的主要研究对象是人工智能，特别是如何在经验学习中改善具体算法的性能” *Langley（1996)*。

而从数据科学的角度来理解，机器学习的主要目的是利用计算机来 **理解数据并且帮助决策** 因此机器学习的流程也可以拆解为两步：
  1. **理解数据**：通过一些数学模型来理解数据的内在联系；
  2. **帮助决策**：利用模型来对新的数据进行决策。

从方法论角度来讲，上述两个步骤是在近似模拟人类的基本学习能力，即 **归纳-推广**。相应的，机器学习也需要解决这两个问题，即：
- **估计**：我们如何从现有的数据（*训练数据*）中归纳出一般规律，特别是当数据中存在大量噪声的时候；
- **泛化**：我们如何把这些规律应用到新的数据上，即使这些数据我们在旧的数据中从未遇见；

针对这些问题我们可以用六个不同的维度来刻画这些问题和他们的解决方法：**任务分类、假设、评价指标、模型分类、模型选择、实现算法**。其中前三个维度是用来刻画问题的，后三个维度是来刻画解决方法的。下面我们会具体来讲解这六个不同的维度。

### 任务分类

机器学习中存在很多的任务类别，一般我们根据所提供的数据和我们要得到的结果来进行分类，常见的几种类别如下：
  1. **监督学习**
  2. **无监督学习**
  3. **增强学习**

**监督学习**

在监督学习中，我们的数据是存在标签的，即我们的训练数据的格式为`(x, y)`。其中`x`是待预测的数据，一般是一个`d`维向量，其中每个维度叫做 **特征** ；`y`是预测结果，一般叫做 **目标值**。我们的终极目的是训练出一个函数$y=f(x)$，使得对于新的输入$x_(new)$，我们可以给出对应的预测值$y_(new)$。根据目标值`y`的不同，我们可以把监督学习分为两类，如果`y`是连续变量，则称为 **回归**；如果`y`是离散变量，则称之为 **分类**。在分类问题中，若`y`是二值变量，则称之为 **二分类** 问题；若`y`是多值变量且取值单一，则是 **多分类** 问题；若`y`是多值变量且取值不唯一，则是 **多标签** 问题，多标签问题可以转化为多个二分类问题解决。

**无监督学习**

在无监督学习中，我们的数据不存在标签，换言之，我们的数据格式为`x`。无监督学习也可以根据目的不同，细分为几类，其中常见的包括：**概率估计，降维，聚类**。概率估计是给定一组数据`x`，我们已知$x_i$都是独立同分布，希望以此推断新的数据$x_new$的概率。降维是对于一组给定的`D`维数据`x`，我们希望将其转化为`d`维（`d<D`）数据，但是不损失（或少损失）信息。一般而言，上述两种无监督学习任务都是为进一步的监督学习任务建立基础的，譬如概率估计可以应用到采样中；而降维一般是在做分类或回归问题时用于特征选择或数据可是化。降维可以更好的帮助我们理解高维数据，提高运算速度。聚类也是一种常见的无监督学习，其目标是在一组数据中将其分组，使得每一组中的数据尽可能相似。聚类可以分为硬聚类和软聚类，软聚类相比较于硬聚类，它提供的是每一组数据出现在每个组的概率。

**增强学习**

增强学习中，我们的目的是给定一个观测值`x`，预测目标值`y`。然而与监督学习不同，我们的数据并不是`(x, y)`,而是`(x,y,r)`。即我们没有正确的目标值`y`,而是对于每个目标值`y`设定一个奖励值`r`，以此来使模型学会预测正确的目标值。如果以学生学习英语来比喻，有监督学习类似于老师写出正确的单词然后让学生模仿，而强化学习则是老师给了学生一个字母表让他们自己练习拼写单词，拼对了奖励，拼错了惩罚，如果试验次数足够多，他们依然可以学会正确的拼写。增强学习较少出现在数据科学的应用中，常应用在人工智能领域，比如著名的 *AlphaGo*。

除了上述几种问题之外，还有半监督学习，主动学习，转移学习等，但是因为应用不广，因此在这里不再介绍。

### 假设

如同任何科学一样，我们在应用机器学习进行建模的时候，我们同样对数据进行假设，其中最常见的假设便是 **独立同分布**。独立同分布是指一个数据集中每一条数据相互独立，并且来源于同一个分布。对于序列数据，常见的假设则是数据来自 **马尔科夫模型**，即某一时刻的数据，只与之前`n`个状态相关，与`n+1`及更早的状态无关。譬如天气，明天天气只与今天相关，与昨天或者前天无关。正确的假设可以减少刻画总体分布的数据量，提高模型描述的准确性。

### 评价指标

在这里评价指标是指我们如何来衡量模型给出的预测的优劣，即预测值与标准答案之间的偏差（*注意*：这里评价的是指模型预测值，而非模型本身）。我们通常用一个函数`L(g, a)`来描述预测值和实际值直接的偏差，这个函数被叫做 **损失函数**， 其中`g`是模型的预测值，`a`是实际值。不同任务对应的评价指标不同，如二分类任务中，常用的损失函数为 **0-1损失**：若`g=a`，损失为0；若不等，损失为1。对于回归任务，则 **常用平方损失**：`L(g,a)=(g-a)^2`。在某些情况下，如雷达预警，漏报的损失远大于误报，这时可以定义不对称损失函数，譬如漏报的损失为100，而误报的损失为1。定义好合适的损失函数后，一般希望模型可以使损失函数的期望（即 **风险**）最小。

### 模型分类

我们来假想一下我们有一组简单的数据`y_train`，我们如何根据`y_train`来对新的数据`y_new`进行预测。基于这个预测的过程的不同原理，我们可以把模型分为四类：

**无模型**

预测可以仅仅基于训练数据本身，譬如我们使用训练数据的平均值（或其他特征，如众数），这类算法的典型就是`k-NN`算法。因为这类算法不需要任何预训练过程，可以直接进行预测，因此又被叫做 **懒惰学习** 模型。

**基于规则模型**

基于规则模型可以理解为给定训练数据`y`,可以拟合出函数`h(y;p)`，其中`p`是对应的参数。而后给定新的数据`y_new`，我们带入函数中即得到预测值。这里我们的模型可以直接给出预测结果，这类算法的代表就是 **决策树** 模型。

**基于概率模型**

基于概率模型可以理解为基于规则模型的变种，它也需要拟合一个模型，但是不同的是，这里给出的预测是一个概率。譬如我们希望预测西瓜是不是熟了，基于规则模型会告诉你熟或者不熟，而基于概率模型则会说这个西瓜80%可能性输了，20%可能性没熟。如果还是难以理解的话，可以参考天气预报的降水概率。我们需要再建立一个规则把概率转化为我们需要的预测。这类算法的典型代表是 **对数几率(logistic)回归**。使用概率模型的好处在于我们把模型和损失函数区分开，我们可以随时根据我们的任务调整预测方法，而不需要重新训练模型。

**贝叶斯模型**

贝叶斯模型与上述两种模型的不同之处在于，它的模型参数`p`并不是一个确定的值，而是同样服从某一个分布。在训练之前，我们假定它服从一个分布，即 **先验分布**， 而后通过训练数据来 *更新* 它的分布，即 **后验分布**。而我们的模型的预测可以理解为这些符合同一分布的模型们（相同模型，不同参数）一起给出的。

*注意*：这一部分比较难以理解，涉及到贝叶斯学派和统计学派对统计的理解，如果没有理解可以暂时放在一旁，在后面慢慢体会。

### 模型选择及实现算法

如何根据合适的任务选择合适的模型是机器学习的重中之重，因此我们不在这里展开阐述，而是会和机器学习模型一起讲解。同样，实现算法也是和具体模型息息相关，因此也会在模型讲解的时候一起描述。这里提一个简单的概念，叫做 **偏差-方差平衡**。一个模型的预测的平均风险（*注意*：这里描述的整个模型，而不是某个特定预测值）可以分解为三部分：**偏差，方差，噪声**。其中噪声是和数据相关，这个是无法避免的，误差和方差则是和模型本身相关：偏差是指模型预测的期望与实际值期望的差，方差则是模型预测值的离散程度。数据量越大，可以训练的模型就越复杂，模型的偏差就越小，但是其方差就会增大。偏差越小，预测的整体准确率就越高；而方差大，则意味这它对与数据越发敏感，导致其泛化能力减弱。所以复杂模型的更容易出现过拟合的问题。

### 结语

这一讲从理论上讲解了一下机器学习的要点，可能内容比较枯燥，但是认真理解上述概念，对进一步学习机器学习有很大的帮助。学习一门知识重要的是要在脑海中形成一张知识网，这一篇导论就是这个知识网的地图。我们下一讲将会讲解机器学习和数据科学中常见的概念。
