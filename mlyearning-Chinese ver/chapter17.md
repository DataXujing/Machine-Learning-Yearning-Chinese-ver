## 17. 如果你有一个很大的开发集，拆分为两半，并只关注其中一个

假设你有一个5000个样本大小的开发集，其中误差是20%，也就是说，你的算法大约误分类了1000个样本。手动检查这1000个样本需要花费很长时间，因此我们决定在误差分析中只使用一部分误分类样本。

在这种情况下，我会明确地将开发集分为两个子集，并全力关注其中一个，通常对于您手动查看的那部分样本会很快的出现过拟合现象。你可以使用另一个子集来对参数进行调优。

![](https://raw.githubusercontent.com/AlbertHG/Machine-Learning-Yearning-Chinese-ver/master/md_images/8.jpg)

让我们继续上边的例子，在这里，算法对5000个开发集样本分类，结果是大约有1000个样本被误分类了，同时假设我们将要手动检查100个误分类样本（占总错误的10%）。

你应当随机选择10%的开发集样本，将其放入一个我们称之为“眼球开发集(​Eyeball dev set)”的集合中，以提醒自己正在使用我们自己的眼睛来观察（人工检查）。（对于语音识别项目，我们是用耳朵来听音频片段，可能将这部分样本集合称作“耳朵开发集”更贴切一点）。因此，这个“眼球开发集”有500个样本组成，我们希望我们的算法在此数据机上的误分类样本个数大概有100个（误差是20%）。

对于开发集的另一个子集，称为“黑盒开发集(Blackbox dev set)”，将会拥有4500个样本。你可以用这个“黑盒开发集”通过测量误差率来自动评估分类器，你也可以使用这部分样本来选择算法或者调整超参数。然而你应该避免对它进行人工检查，我们之所以使用“黑盒”这个词，就是要强调我们使用的这部分数据只是为了用来获取黑盒对分类器的评估。

![](https://raw.githubusercontent.com/AlbertHG/Machine-Learning-Yearning-Chinese-ver/master/md_images/10.jpg)

为什么我们要明确地将开发集分为“眼球开发集”和“黑盒开发集”呢？因为既然你能够直接对眼球开发集中的样本进行人工检查，意味着这部分数据会很快出现过拟合现象。如果你发现算法在眼球开发集的性能表现比黑盒开发集中的提升的更快，那么意味着你已经过拟合了眼球开发集了。在这种情况下，你可能需要放弃这部分数据，并通过将更多的黑盒开发集的数据转移到眼球开发集中，或者通过获取新的标记数据来找到新的眼球开发集。

将你的开发集数据明确的拆分为眼球开发集”和“黑盒开发集”，可以让你及时知道在手动误差分析的过程中何时过拟合了眼球开发集。