# 基于百度自研模型ERNIE进行对话意图识别任务

意图识别是指分析用户的核心需求，输出与查询输入最相关的信息，例如在搜索中要找电影、查快递、市政办公等需求，这些需求在底层的检索策略会有很大的不同，错误的识别几乎可以确定找不到能满足用户需求的内容，导致产生非常差的用户体验；在对话过程中要准确理解对方所想表达的意思，这是具有很大挑战性的任务。

例如用户输入查询“仙剑奇侠传”时，我们知道“仙剑奇侠传”既有游戏又有电视剧还有新闻、图片等等，如果我们通过用户意图识别发现该用户是想看“仙剑奇侠传”电视剧的，那我们直接把电视剧作为结果返回给用户，就会节省用户的搜索点击次数，缩短搜索时间，大大提升使用体验。而在对话中如果对方说“我的苹果从不出现卡顿”，那么我们就能通过意图识别判断出此刻的苹果是一个电子设备，而非水果，这样对话就能顺利进行下去。

本示例使用ERNIE预训练模型，在[CrossWOZ](https://github.com/thu-coai/CrossWOZ) 数据集上完成任务型对话中的槽位填充和意图识别任务，这两个任务是一个pipeline型任务对话系统的基石。

## 1. 方案设计

本实践设计方案将基于ERNIE，在CrossWOZ数据集上完成意图识别和槽位填充任务。在本实践中，意图识别和槽位填充本质上是一个句子分类任务和一个序列标注任务，如图1所示，CLS token位置的输出将被用来进行语句分类，文本串的实际token将被用来进行序列标注任务。在训练过程中，会将两者的loss结合，从而实现意图识别和槽位填充的多任务学习。

<center><img src="https://ai-studio-static-online.cdn.bcebos.com/d9ff881921d74602acb6eb27c8523cb50285f07a7beb4a3cbfa1edbd9b3f9c5c"/></center>
<center>图1 ERNIE进行对话意图识别架构图</center>
<br/>

## 2. 数据说明
CrossWOZ 是第一个大规模的中国跨域任务导向的数据集。 它包含5个领域，共计6K对话和102K语句，包括酒店、餐厅、景点、地铁和出租车。 此外，语料库包含丰富的用户和系统端对话状态和对话行为的注释。 

关于数据集的更多信息请参考论文[ CrossWOZ: A Large-Scale Chinese Cross-Domain Task-Oriented Dialogue Dataset ](https://arxiv.org/abs/2002.11893) 。

## 3. 使用说明
### 3.1 模型训练
可按如下方式，使用训练集进行模型训练。

```shell
sh run_train.sh
```

### 3.2 模型测试
可按如下方式，使用测试集进行模型测试。

```shell
sh run_evaluate.sh 
```

### 3.3 模型推理
```shell
sh run_predict.sh
```
