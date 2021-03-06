# 一些简单的科普

## 一些常见的算法

### 1 KNN

- K-Nearest Neighbors

  - 分类算法

- 思路

  - 根据邻居判断一个新数据类型

- 水果判断实例

  - 大小和颜色是数据特征
  - 苹果和梨是数据的标签
  - 根据样本的大小，颜色找到它在坐标系中的位置
  - 再根据已经确定的苹果和梨都在哪儿

    - 附近苹果多则是苹果，附近梨多就是梨
    - 此处对比🍉书第三章线性判别的思路

- 理论

  - KNN中的k值得是"K个"邻居

    - k过小

      - 会受到单个个例的影响

    - k过大

      - 会受到较远距离的特殊数据的影响

  - 计算距离

    - 欧式距离
    - 曼哈顿距离

  - K的取值

    - 问题自身
    - 数据集大小

- 应用

  - 判断植物的类别
  - 将文本分词、统计词频等处理后判断文章类型
  - 电商、视频网站可以找到与你类似的用户

- 缺陷

  - 要先计算新样本与所有样本之间的距离
  - 按照由近及远排序
  - 按照k值确定分类

### 2 BP

- 问题背景

  - 决定神经网络优劣，神经元之间连接的权重和神经元的阈值
  - 确定这些数字

    - 大部分时间使用的是反向传播

- 原理

  -  根据网络输出的答案与正确答案之间的误差，不断调整网络的参数

     - 如果误差是负值，提升权重
     - 如果误差是正值，降低权重

  -  调整的程度受一定的比率即{学习率}的制约

     - 用来控制参数调整程度的高低

- 问题

  - 由于很强的调整能力

    - BP算法控制下的神经网络容易过拟合

  - 解决办法

    - 提前停止策略
    - 将数据按照一定比例划分为训练集和验证集

      - 训练集调整参数
      - 验证集估算误差

### 3 决策树(decision tree)

- 概念

  - 用于分类，构成它的元素和边
  - 节点会根据样本的特征做出判断

- 构建决策树

  - 确定节点的角色

    - 具体哪一个是根节点，叶子节点

  - 概念

    - 熵

      - 代表分支下样本种类的丰富性
      - 样本种类越多越混乱

        - 熵越大

      - 如果分支下节点都是同一类

        - 熵为0

  - 思路

    - 在随着深度下降的时候，熵快速降低
    - 熵下降的速度越快，代表决策树分类效率越高

- 优点

  - 天然的可解释性

- 缺点

  - 因为数据肯定会是有特例的，如果能完美分类训练集，那肯定是过拟合的。
  - 解决办法

    - 剪枝操作

      - 去掉一些分支

    - 两种剪枝

      - 预剪枝 

        - 在训练开始前规定条件

          - 比如树达到一定深度就停止训练

      - 后剪枝

        - 先找到树，再依据一定条件

          - 如限制叶子节点的个数，去掉一部分分支

### 4 随机森林（random  forset）

- 背景

  - 随机森林是决策树的升级版
  - 随机

    - 树的“生长过程”

      - 世上没有两片相同的树叶
      - 随机森林中的树也各不相同

- 在构建决策树时的特点

  - 1 从训练数据中有放回的随机选取一部分样本
  - 2 不使用数据的全部特征，随机选取部分特征进行训练

- 这样训练的原因， 在训练最初。

  - 不知道那些是异常样本
  - 不知道那些特征对分类结果影响更大

- 输出

  - 随机森林的输出结果由投票决定，服从多数决策树结果

- 优点

  - 因为每棵树是独立的

    - 所以不会产生过拟合

  - 特征是随机选取的 

    - 不需要做特征选择，能处理高维数据

  - 合理训练后准确性很高
  - 不知道使用什么分类方法时，试试随机森林准没错

- ML领域中random forset 是集成学习

  - 将多个模型组合起来解决问题

    - 这些模型会独立的选择数据，训练，预测
    - 投票出结果
    - 准确度比单独的模型高

  - 集成学习内部，不必都是决策树，也可包含神经网络

### 5 GBDT

- 梯度提升树gradient boosting decision tree
- 决策树分类

  - 分类树

    - 苹果分类为好和坏

  - 回归树

    - 苹果好坏程度打分

- 结构

  - 包含了多课决策树

- 和random forset相区别

  - GBDT中的树都是回归树
  - GBDT中的每一棵树都建立在前一棵树基础上

    - 1 先训练一棵树大体预测一下苹果的分数 75
    - 2 再去训练一棵树屈预测他们与真实分数间的差距 6
    - 3 如果75+6和真实苹果分数85还有差距，就再训练第三课树预测这部分差距2，递归进行减少这些误差
    - 。。。。

- 应用

  - 网页，商品，电影

    - 通过预测关联程度、点击率或是用户的喜好程度来排序
    - 在搜索、广告、推荐系统等领域有着广泛应用

- 特点

  - 优点

    - 能处理标签、数值等各类数据，解释性强

  - 不足

    - 由于数和树之间有关联，训练时间长

- ML领域中GBDT是集成学习

  - 多个学习模型
  - 集成学习（EMSEMBLE learning）分类

    - 提升 boosting

      - 线性前后依赖

    - 装袋 bagging
    - 堆叠stacking

      - 多个模型的输出由一个模型决定后再输出

### 6 SVM

- 背景

  - 想要知道水果是梨还是苹果

    - knn画圈
    - 画条线

      - 通过将两者所在的空间做出区分
      - 这条线就是SVM支持向量机

- support vector machine需要注意点

  - 线位置
  - 样本和线之间的距离，代表样本的可信程度

    - 越远可能性越高

- 找到能让所有样本的分类可信程度最高的那条线

  - 不必计算所有的样本，只需要找到线附近的样本，让他们和线的距离越远越好
  - 分类间隔,margin
  - 决定了线的样本

    - 这些样本被称为支持向量，support vector

- 问题

  - 当出现无法被线正确分类的样本与线之间的距离

    - soft margin maximization
    - 找到能最小化这个距离的线

  - 如果样本分布不理想 

    - 将数据映射到一个能用直线区分的空间
    - 寻找分类线

- 特点

  - 在深度学习出现前，随机森林和SVM是最好用的分类方法
  - 对样本依赖小，不会过拟合
  - 小样本也能很好的预测

- 应用

  - 文本分类
  - 垃圾邮件识别
  - 图像识别
  - 分类蛋白质

### 7 K-means

- 背景

  - 分类水果

    - knn画圈，通过相邻判断
    - svm画线，通过所处的区域

  - 如果在最开始，没有足够的已知信息

    - 需要使用k-means均值算法 

- 详细流程

  - k 代表样本的类别数

    - k =2 希望将水果分成两类

  - 步骤

    - 1 在空间中随机选定两个样本作为分类基准，计算比较其他样本与他们之间的距离

      - 离哪一个近，就归为哪一类

    - 2 迭代

      - 2.1 找到两个类别的中心，计算所有样本和中心点的距离

        - 按照距离远近，再进行分类

      - 2.2 再进行迭代，寻找新的类别中心，计算距离，再进行分类

    - 迭代多次，知道某次分类的结果和上一次一样，停止迭代

      - 训练完毕

- 特点

  - k-means能自主寻找数据的内部结构

    - 基于的假设

      - 特征空间中，两个距离很近的数据很可能属于同一个类额

  - 这种通过分析数据在空间中的分布状况进行分类的方法

    - 聚类clustering

  - 不需要标签信息，无监督学习
  - 优势

    - 可解释性好，实现简单
    - 分类效果也可行

  - 不足

    - 准确度比监督学习差
    - 对k值敏感

## 目前自己遇到的一些常见数学公式

### 置信度

### 相关系数

- 公式
- 这个式子的分母是两个随机变量的标准差，起到归一化的作用。

### 自相关

- 处理数据，可以发现隐藏在杂乱信号中的有用信息。自相关找出重复信息（被噪声掩盖的周期信号），或识别隐含在信号谐波中小时的基频，常用于时域信号的分析。
- 公式

  -  
  -  t 是进行“比较”时移动的“步距”。而整个公式的意思是“将x(t)进行时移，得到x(t+τ)，然后将其与x(t)在整个范围内逐点进行相乘，得到一条新曲线，这条曲线下方所围成的面积就是一个R值。改变τ的取值，再来一次，……，如此不断重复，R的一系列值将成为R(τ)曲线，这就是自相关曲线”

### 归一化互相关（Normalized Cross Correlation）

- 模板匹配中较为常见的互相关计算方法，来描述两个同维向量，窗口或样本之间的相关性。其取值范围是-1~1，-1代表两向量不相关，1代表两向量相关
- NCC常做作为相似性的度量。当NCC为-1时，两向量负相关（你东我西），当为0时，两向量不相关（你东我随意），当为1时，两向量正相关（你东我东）。NCC值越大，两向量越相似。反正不相似
- 公式

  - 
  - f(),t(),为两个向量或样本，n为向量维数或窗口的大小，σ为各种样本的标准差，μ为各自样本的均值。

### 贝叶斯

- 先验，后验
- 公式
- 待深究

## 一些常见的网络模型

### 1 SOTA

- state of the art

  - 当前最佳
  - ML中用来形容模型

- 在前人基础上更进一步的指标

  - 0到1 而不是1到1.1，1.2

### 2 NN

- 仿照人脑的机构和工作原理，构建了神经网络

  - 人

    - 苹果光信号=》电信号
    - 电信号=》神经元
    - 神经元根据颜色、方向、边缘、材质等
    - =》得出判断是苹果

  - 节点连接的网络
  - 神经元

    - 抽象的概念
    - 大部分时间用来存储数字

  - 神经突触

    - 抽象概念
    - 有权重的连接

      - 决定数字将怎么改变
      - 数字将被传递给那些神经元

- 结构

  - input layer

    - 数据转换为NN可以识别的数据

      - 图像=》灰度值

  - hidden layer

    - 隐含层中的每一层试图认出一部分特征

  - output  layer

    - 给出答案

- 改造

  - GNN

    - 把输入的内容从图片语音转换为图

  - CAPSNET

    - 把神经元打包成胶囊

  - CNN

    - 使用卷积对图像进行处理

### 3 CNN

- 卷积核
- 图片灰度矩阵
- 卷积

  - 对应各自上的数字相乘后再相加，得到的数字填入新矩阵
  - 卷积核移动的距离

    - 步长

  - 得到的新矩阵更小，能反应图片的特征

    - 特征图

      - 是这一层的输出
      - 也是下一层的输入

    - 不同的卷积核得到不同的特征

- CNN的训练

  - 就是让网络根据已有的数据和他们的标签通过训练自动确定卷积核中的数字

    - alexnet 

      - 5个卷积层

        - 边缘，纹理，组成
        - 越靠后的卷积层提取出的特征越抽象

- 结构

  - conv 卷积层
  - maxpooling 池化层
  - full connect  全连接层

- 池化层

  - 降维

    - 选取图像的主要特征

  - 常用的maxpooling是保留窗口覆盖区域的最大数值
  - 矩阵被池化后，参数会大量减少
  - 4*4 =》2*2

- 全连接层

  - 通常在卷积的最后
  - 能将提取到的特征集合在一起
  - 

- 应用

  - 1 图片处理
  - 2 将声音当作图谱处理可以完成语音识别
  - 3 将词语作为向量处理可以完成机器翻译

### 4 GNN

- 图神经网络 Graph Neural Network
- 通常神经网络的输入是图片，声音，文字

  - GNN的输入则是图
  - 此处的图是由节点和边组成

    - 节点

      - 实体（包含他们的属性）

    - 边

      -  描述实体之间的关系

- 图神经网络的计算对象

  - 与图片文字语音相比，图能表达的内容非常广泛
  - 社交网络

    - 用户为节点
    - 关系做边

  - 分子组成
  - 地铁网络，交通网络
  - 电路图
  - 商品关联购买推荐
  - 
  - 人视为由点组成

### 5 CAPSNET

- Capsule Networks
- 判断人脸

  - 
  - 1 2 是 3不是
  - 使用CNN的到的却可能是 1 3 是 2 不是

    - 这是因为CNN在提取特征时，会忽视特征与特征之间的相对关系，也很难理解事务的旋转和缩放
    - 解决办法

      - 增加不能角度，不同方位，不同视角下同一事物的数据

- 胶囊

  - 一组打包好的神经元

    - 神经元输出数值
    - 胶囊可以输出向量

      - 向量的长度代表胶囊对特诊的认可程度
      - 同时携带了一定的姿态信息
      - 底层的胶囊在获取基础特征后，会对图片追踪可能是什么做出预测，如果找到共同认可的高层胶囊特征 ，就认为更可能是这一胶囊代表的内容。

        - routing by agreement

    - 胶囊网络相比CNN 

      - 能更好的理解事务的组成、位置、姿态等信息

- 目前尚未流行的原因

  - 目前在手写数据MNIST上取得SOTA外，胶囊网络尚未在更大的数据集上表现出更好的准确性
  - 胶囊网络训练的时间也更长，动态路由过程很消耗资源
  - 起步阶段

### 6 RNN

- 问题背景

  - 识别图像的时候，输入的每张图片都是孤立的，认出一张图片是苹果，并不会对认出下张图片是梨造成影响
  - 但对于语音来说顺序是十分重要的

    - 词语顺序的改变表达了完全不同的意义
    - 顺序也提供了一定的信息

      - 例如吃大概率会接食物

- 高度重视序列信息的网络
- 结构

  - NN

    - 特征提取

  - W BOX

    - 记录数据输入时神经网络的状态
    - 盒子中的信息被称为隐状态hidden state

- 应用

  - NLP(natural language  processing)

    - 翻译

      - 机器翻译寻找相同的意义序列，在不同语言中的表达

    - 诗歌生成

      - 按照一定的规则输出有逻辑的词语序列

  - 改变数据类型

    - 看图说话：输入图片输出句子

  - 语音同样可以看作声音信号按时间顺序组成的序列

    - 语音识别和语音生成同样在RNN的能力范围内

  - 量化交易模型quantitative trading

    - 股票价格也可以看作是一个受时间影响的序列

- 缺陷

  - 数据输入的越早，在隐状态中占据的影响越小

    - 如果一个句子很长，RNN就会忘记开始说了什么

  - 针对此有了改良版

    - LSTM 长短时记忆模型

### 7 LSTM

- 问题背景

  - RNN 有一定的记忆能力

    - 但只能保留短期记忆

  - 思路

    - 记忆是有取舍的

      - 无法记住所有的
      - 只能记住部分
      - 丢掉不重要的
      - 选择记住一部分重要的
      - 参照这个记忆机制改造小盒子，并找到了门机制

        - 门是用来决定信息如何保留的小开关
        - 数值在0到1之间

          - 1 keep
          - 0 drop

- 新版小盒子

  - 结构

    - 遗忘门

      - 决定小盒子要保留多少原有信息
      - 也就是丢掉那些不重要的记忆

    - 输入门

      - 决定了当前网路信息有多少要被保存到小盒子里
      - 也就是记住那些新东西

    - 输出门

      - 决定了多大程度的输出小盒子中的信息

  - 特点

    - 既能通过输入门对当前网路状态有所了解
    - 又能利用遗忘门留下过往的重要信息

  - 改良

    - MGU(minmal gated unit)
    - SRU(simple recurrment ubint)
    - GRU(gated recurrent unit)

      - 只有两个门

        - 更新门

          - 遗忘门和输入门的结合体
          - 决定丢弃那些旧信息，添加那些信息

        - 重置门决定写入多少上一时刻网络到的状态，用来捕捉短期记忆

      - 结构简介
      - 效果更高效

### 8 自编码器

- 实例

  - 对输入图片进行编码，解码，实现图片重建

    - 图片去噪

- 结构

### 9 DBM

- 深度置信网络
- RBM

  - Restricted
    Boltzmann Machine
    受限玻尔兹曼机

  - 1. 由隐藏层和可见层组成

2. 权重矩阵 𝑾 指定了边的权重
3. 可见单元有偏置 𝑎_𝑗
4. 隐藏单元有偏置 𝑏_𝑗

