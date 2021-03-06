# embeddings-word2vec
词项目模型 嵌入


当你在处理文本中的单词时，最终会有数以万计的类来预测，每个单词都是一个。尝试对这些单词进行一次热编码是非常低效的，您将一个元素设置为1，另一个元素设置为0.进入第一个隐藏层的矩阵乘法将几乎所有结果值都为零。这是一个巨大的浪费计算。

![one-hot encodings](assets/one_hot_encoding.png)

为了解决这个问题，大大提高了网络的效率，我们使用了所谓的嵌入。嵌入式操作只是一个完全连接的层，就像您之前看过的那样。我们称这个层为嵌入层，权重为嵌入权重。我们通过相反直接从权重矩阵中获取隐藏层值来跳过嵌入层的乘法。我们可以做到这一点，因为单热编码向量与矩阵的乘法返回对应于“开”输入单元的索引的矩阵行。

![lookup](assets/lookup_matrix.png)

而不是进行矩阵乘法，我们使用权重矩阵作为查找表。我们将单词作为整数进行编码，例如“heart”被编码为958，“mind”为18094.然后为了获取“heart”的隐藏层值，您只需要嵌入矩阵的第958行。这个过程称为**嵌入查询**，隐藏单位数是**嵌入维度**。

<img src='assets/tokenize_lookup.png' width=500>
 
这里没有什么神奇的东西。嵌入查找表只是一个权重矩阵。嵌入层只是一个隐藏层。查找只是矩阵乘法的一个快捷方式。查找表也像任何权重矩阵一样被训练。

当然，嵌入不仅用于词语。您可以将它们用于您拥有大量课程的任何模型。称为** Word2Vec **的特定类型的模型使用嵌入层来查找包含语义含义的单词的向量表示。

## Word2Vec

word2vec算法通过查找表示单词的向量来找到更有效的表示。 这些向量还包含有关单词的语义信息。 在类似的上下文中出现的单词（例如“黑色”，“白色”和“红色”）将具有彼此靠近的向量。 有两种实现word2vec，CBOW（Continuous Bag-Of-Words）和Skip-gram的架构。

<img src="assets/word2vec_architectures.png" width="500">

在这个实现中，我们将使用skip-gram架构，因为它比CBOW更好。 在这里，我们通过一个字，并尝试预测文本中的单词。 以这种方式，我们可以训练网络来学习在类似语境中显示的单词的表示。

