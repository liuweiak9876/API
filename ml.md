# 机器学习简介  

核心思想  

数据驱动：依赖大量数据来训练模型自适应性：模型能够根据新数据不断优化自身  

# 与传统编程的区别  

·传统编程依赖明确的规则和逻辑。  
·机器学习通过数据学习规律，适用于复杂或难以手工编写规则的任务。  

![](images/7366ec7211112be3c9a1423715a63334e280823fa8b41c137ff513510c1f8f17.jpg)  

机器学习算法利用样本数据（训练数据）构建数学模型，用于未来的预测或自动决策。  

# 机器学习的基本组成  

数据  

数据是机器学习的基础，包括训练数据和测试数据。  
数据的质量和数量直接影响模型的性能。  

# 算法  

·算法是解决问题的方法或步骤，如线性回归、决策树、聚类算法等。模型  

模型是通过算法和数据训练得到的，用于预测或分类。  

训练过程：模型学习数据中的模式。  
测试过程：评估模型在新数据上的表现。  

# 机器学习的类型  

常见的机器学习类型。  

# 监督学习  

通过标注的数据进行训练，目标是学习输入与输出之间的映射关系。  

使用未标注的数据，目标是发现数据中的潜在结构或模式。  

强化学习  

通过与环境的交互，学习如何采取行动以最大化累积奖励。  

利用少量标记数据和大量未标记数据来提高模型的准确性与适应性。  

# 监督学习  

监督学习通过标注的数据进行训练，目标是学习输入与输出之间的映射关系。主要任务  

分类：将输入数据分到预定义的类别中（如垃圾邮件识别）  

回归：预测连续值 （如房价预测）  

常见算法  

·线性回归、逻辑回归、决策树、随机森林、神经网络、支持向量机（SVM）等。优点与局限  

优点：在有充足标注数据时表现良好。  

局限：需要大量标注数据，数据标注成本高。  

# 无监督学习  

无监督学习使用未标注的数据，目标是发现数据的内在结构或分布。  

# 主要任务  

聚类：将数据分组为若干簇（如客户细分）。关联规则学习：发现变量之间的关系（如购物篮分析）  

# 常见算法  

聚类算法、异常检测等  

# 优点与局限  

优点：不需要标注数据，适用于数据探索。  
局限：难以评估模型性能，结果解释性较弱。  

整体的流程方法是类似的，同时，不同的场景，算法类型（监督、无监督），也会带来细节的不同（数据处理与编码，评估的指标等）。  

# 机器学习的通用流程：无监督学习  

无监督学习的流程 （聚类）  

![](images/20db830e51f2060c0d0c3f084c31828eb81bf53062699f042eacc6f821aef6b7.jpg)  

# 常用的算法  

围绕有监督、无监督，不同的任务类型，可以有不同的算法选择。  

![](images/d9c802b84487922238a140c5a671cbbc9b38cf27718cdfbda2cebaffa35ede80.jpg)  

# 常用的性能评估指标  

分类：准确率、精确率、召回率、F1回归：RMSE(均方根误差)、MAE(平均绝对误差)、MAPE(平均绝对百分比误差)  

# 常用的性能评估指标：分类  

二元分类器的每个输出都有四种可能的结果 （混淆矩阵）  

![](images/4069e734f927d859f9727d51e61f02753add5d205b47b791c4c572cf7f54a175.jpg)  

TP（True Positive，真正例）：被正确识别为好人的人（实际是好人，预测也是好人）TN（TrueNegative，真反例）：被正确识别为坏人的人（实际是坏人，预测也是坏人）FP（FalsePositive，假正例）：被错误识别为好人的坏人（实际是坏人，但预测为好人）FN（FalseNegative，假反例）：被错误识别为坏人的好人（实际是好人，但预测为坏人）  

# 准确率（Accuracy）  

<html><body><table><tr><td rowspan="3">分子</td><td></td><td>预测为好人</td><td>预测为环人</td></tr><tr><td>实际为好人 （正例）</td><td>真正例（TP）：好人被释放</td><td>假反例（FN）：好人被宽柱</td></tr><tr><td>实际为坏人 （反例）</td><td>假正例（FP）：坏人逃之天天</td><td>真反例（TN）：环人被惩罚</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="3">分母</td><td></td><td>预测为好人</td><td>预测为坏人</td></tr><tr><td>实际为好人 （正例）</td><td>真正例（TP）：好人被释放</td><td>假反例（FN）：好人被冤枉</td></tr><tr><td>实际为坏人 （反例）</td><td>假正例（FP）：坏人逃之天天</td><td>真反例（TN）：坏人被惩罚</td></tr></table></body></html>  

# 精确率 (Precision)  

<html><body><table><tr><td rowspan="3">分子</td><td></td><td>预测为好人</td><td>预测为坏人</td></tr><tr><td>实际为好人 （正例）</td><td>真正例（TP）：好人被释放</td><td>假反例（FN）：好人被冤枉</td></tr><tr><td>实际为坏人 (反例）</td><td>假正例（FP）：坏人逃之天天</td><td>真反例（TN）：坏人被惩罚</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="3">分母</td><td></td><td>预测为好人</td><td>预测为坏人</td></tr><tr><td>实际为好人 （正例）</td><td>真正例（TP）：好人被释放</td><td>假反例（FN）：好人被冤枉</td></tr><tr><td>实际为坏人 （反例）</td><td>假正例（FP）：坏人逃之天天</td><td>真反例（TN）：坏人被惩罚</td></tr></table></body></html>  

$$
\mathrm{Accuracy}={\frac{T P+T N}{T P+T N+F P+F N}}
$$  

准确率表示模型预测正确的样本占所有样本的比例，反映模型整体的正确性。  

关注模型正确判断的频率，无论是释放好人还是惩罚坏人。  

$$
{\mathrm{Precision}}={\frac{T P}{T P+F P}}
$$  

精确率是指模型预测为正类的样本中，真正为正类的比例，即模型在预测为正类时的准确性。  

关注的是当模型预测一个人是好人时，这个预测有多准确，有多少是真正的好人？  

# 召回率 (Recall)  

<html><body><table><tr><td rowspan="3">分子</td><td></td><td>预测为好人</td><td>预测为坏人</td></tr><tr><td>实际为好人 (正例)</td><td>真正例（TP）：好人被释放</td><td>假反例（FN）：好人被冤枉</td></tr><tr><td>实际为坏人 （反例）</td><td>假正例（FP）：坏人逃之天天</td><td>真反例（TN）：坏人被惩罚</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="3">分母</td><td></td><td>预测为好人</td><td>预测为坏人</td></tr><tr><td>实际为好人 （正例）</td><td>真正例（TP）：好人被释放</td><td>假反例（FN）：好人被冤枉</td></tr><tr><td>实际为坏人 （反例）</td><td>假正例（FP）：坏人逃之天天</td><td>真反例（TN）：坏人被惩罚</td></tr></table></body></html>  

$$
{\mathrm{Recall}}={\frac{T P}{T P+F N}}
$$  

召回率表示真实为正类的样本中，模型成功预测为正类的比例，即模型对正类的敏感度。  

关注的是在所有实际为好人的人中，有多少被模型正确识别，好人被释放的比例有多高。  

# 准确率、精确率、召回率的取舍  

如何取舍取决于具体场景的目标与优先级。  

# 司法系统  

·若释放坏人的代价高（引发社会不安），优先考虑精确率，减少坏人逃脱。  
·若冤枉好人代价高（损害社会正义），优先考虑召回率，尽量减少冤枉好人。  

# 医疗诊断：  

·若误诊代价大（不必要的治疗），优先考虑精确率，确保确诊的患者确实有病。  
·漏诊严重疾病的后果更严重，优先考虑召回率，确保尽可能诊断出所有患者。  

# F1分数  

种常用的分类模型性能评价指标，适用于类别不平衡的场景。  

Precision x Recall F1=2x ·Precision 精确率 Precision + Recall ·Recall 召回率  

当Precision和 Recall都较高时，F1分数也会高。如果其中一个很低，F1分数会显著下降。比简单平均更能惩罚极端值（即两者差距很大时F1会低）  

# 性能指标计算  

# 可以方便的通过sklearn.metrics计算  

from sklearn.metrics import accuracy_score, precision_score, recall_score,f1_score  

#类别不平衡的示例 y_true $=[0,$ 0,0, 0,0, 1, 1, 1,1, 1] y_pred $=[0,0,0,0,0,0,0,1,1,1]$ accuracy $=$ accuracy_score(y_true,y_pred) precision $=$ precision_score(y_true, y_pred) recall $=$ recall_score(y_true, y_pred) f1 $=$ f1_score(y_true, y_pred)  

print(f"Accuracy:{accuracy:3f},Precision:precision:3f) Recall:{recall:.3f},F1 Score: (f1:3f})  

![](images/48a50c8595a99fff9773e0994186e7f8b78932426dd69524688e98efdda4ed5b.jpg)  

# 常用的性能评估指标：回归  

![](images/be1067c0d9612f78324c9c1d1c7266d066e7060be692daf897d3096031e71e58.jpg)  

# 偏差（bias)：  

模型的预测值与实际值之间的偏离关系。  

# 方差 (variance)  

训练数据在不同迭代阶段的训练模型中，预测值的变化波动情况（或称之为离散情况）  

# 数值型评估指标  

RMSE（均方根误差）：预测值与真实值的平方差异的平均值的平方根。  
MAE（平均绝对误差）：预测值与真实值的绝对值差异的平均值。  
MAPE（平均绝对百分比误差）：预测值与真实值的绝对百分比差异的平均值。RMSE \~ 3.11  
测试集：[5,8, 9]MAE\~2.33  
预测集:[7,3, 9]MAPE\~0.34  

# 数值型评估指标  

RMSE（均方根误差）：预测值与真实值的平方差异的平均值的平方根。MAE（平均绝对误差）：预测值与真实值的绝对值差异的平均值。$\cdot$ MAPE（平均绝对百分比误差）：预测值与真实值的绝对百分比差异的平均值。  

测试集：[5,8,9] 预测集：[7,3,9]  

# RMSE:  

1.计算每对真实值和预测值的误差平方：  
$(7-5)^{2}=4,(3-8)^{2}=25,(9-9)^{2}=0$   
2.误差平方和：4+25+0=29  
3.求均值： $\textstyle{\frac{29}{3}}=9.67$   
4.开平方:√9.67\~3.11  

MAE:  
1.计算每个预测与真实值的绝对差：$\vert7-5\vert=2,\vert3-8\vert=5,\vert9-9\vert=0$   
2.求绝对误差的和：$2+5+0=7$   
3.求均值：${\frac{7}{3}}\approx2.33$   
MAPE:  
1.计算每个预测的相对误差百分比：  
$\left|\frac{7-5}{5}\right|\times100=40\%,\quad\left|\frac{3-8}{8}\right|\times100=62.5\%,\quad\left|\frac{9-9}{9}\right|\times100=0\%$   
2.求相对误差百分比的和：  
$0.40+0.625+0=1.025$   
3.求均值：  
$\frac{1.025}{3}\approx34.17\%$  

# 性能指标计算  

可以方便的通过sklearn.metrics计算。  

importnumpyasnp   
from sklearn.metrics import mean_squared_error, mean_absolute_error,   
mean_absolute_percentage_error  

y_true=np.array([5,8,9]) #真实值 y_pred $=$ np.array([7,3,9]) $\#$ 预测值  

# 从基础到进阶的变化  

「专家就是在大部分时间，大部分场景下，做的又快又稳的人。」  

熟悉更多的算法（工具）并送代优化熟悉更多的场景与方法思路。  
能够更好的理解需求以及沟通解释。求解的过程更为严谨规范。  
讨厌重复，会「偷懒」～  

![](images/6c6a30e142edecbed9afdae0ddc24432e9ce0109412c12c93a4331a11596ffbd.jpg)  

# 从基础到进阶的变化  

专家知道很多，知道自己哪些不知道，有时候会不知道自己知道（隐性知识）  

更多算法：时间序列、层次聚类、异常检测、XGBoost。场景与方法思路：特征工程，出货预测、供应商分级、物流异常。理解需求以及沟通解释：通用的流程，模型的可解释性。求解的过程更为严谨规范：交叉验证，提升泛化能力。会「偷懒」：自动化调参、AutoML（AI辅助建模）。  

![](images/2cc882a81a34006dac2920243ac7da2ea9f98afb72e1f5a56c037fc1d5e90e37.jpg)  

# 机器学习的工具与环境  

围绕通用的机器学习流程，常用的工具环境有：  

代码方式：Python、R图形化工具：Knime、RapidMiner、IBM SPSS Modeler  

![](images/1a719bc63881dcdf022a1e7e00e8f25bdbc837b68589a28db62c58b1e3855528.jpg)  

# 代码方式  

紧密团结在以Python为核心的开源库与社区环境里。  

代码格式：Jupyter Notebook或.py代码  
编程工具：VS Code、PyCharm  
社区：Kaggle，和鲸社区、天池（阿里云）  
基于常用的开源库：·数据准备与计算：Pandas，NumPy·图表：Matplotlib、Seaborn·统计：SciPy、Statsmodels·机器学习：Scikit-learn、TensorFlow、PyTorch  

![](images/09193d381ec5bfc9e286a76f1c72c2d524a0719f150b41648e1061a18c323349.jpg)  

![](images/10c8dc66d2c5f4a2793fc18a3d5eaca50c9b5958196a7dbc3ff42a9f7aac1099.jpg)  

二三二 i pd se sepued od 二二二#  

# 代码方式  

规范、高效、易维护。  

熟悉Pandas，Scikit-learn库。  
熟悉通用的机器学习代码流程。  
·更为规范方便的Scikit-learn的Pipeline与ColumnTransformer。  
·常见的代码任务（数据处理、特征编码、性能指标），指挥AI来完成。  

![](images/10e6962a479965de69a8601c7c66d35c81ea21e59402b54972a9df35e68d29d6.jpg)  

importpandasaspd from sklearn.model_selection import train_test_split from sklearn.tree importDecisionTreeClassifier from sklearn.metrics import accuracy_score  

#读取数据data $=$ pd.read_csv("./data/titanic/train.csv")  

#将分类变量转换为数值 data['Sex'] $=$ data['Sex'].map(f'male': 0, 'female': 1)) data['Embarked'] $=$ data['Embarked’].map(('S': 0, 'C': 1, 'Q': 2)})  

$\#=======$ 填充缺失值 $=======$   
#数值列用中位数填充   
for col in ['Age','Fare']: data[col].fillna(data[col].median(),inplace $\risingdotseq$ True)   
$\#$ 类别列用众数填充   
data['Embarked’].fillna(data['Embarked’].mode([0],   
inplace=True)   
#选择特征列   
features $=$ ['Pclass’‘Sex''Age''SibSp''Parch’,'Fare，   
'Embarked']   
$x=$ data[features]   
$y=$ data['Survived']   
#划分训练集和测试集（8:2）   
X_train, X_test, y_train, y_test $=$ train_test_split(x,y,   
test_size $=0.2$ ,random_state $=42$   
#创建并训练决策树模型   
model $=$ DecisionTreeClassifier max_depth $=5$ ， #树的最大深度 random_state $=42$   
#模型训练   
model.fit(x_train,y_train)   
#在测试集上预测   
y_pred $=$ model.predict(x_test)   
#输出准确率   
acc $=$ accuracy_score(y_test,y_pred)  

# 任务流程  

# 代码流程。  

数据读取  
分类变量编码  
填补缺失值选择特征列划分训练、测试集  
决策树训练与预测输出准确率  

# 图形化工具方式  

Knime是一个开源的数据分析和数据挖掘工具平台。它以其高度模块化和可扩展的特性广泛用于数据集成、数据清洗、数据挖掘、预测建模和机器学习等任务。  

![](images/ed335268b208af882c378cd0c1e3702d50a164b3890154085308df58e30bd6ea.jpg)  

Knime的核心是一个工作流式的界面，用户可以通过拖放节点来构建数据分析流程。  

# 图形化工具的实现  

同样的任务流程，不同的实现方式。  

·数据读取、处理的任务、编码 $\rightarrow$ 对应的数据准备Tools  
·数据划分→对应的数据划分Tool  
·算法模型→找到对应的决策树Tool代码流程 $\rightarrow$ 连线方式代码的Print输出调试 $\rightarrow$ 查看不同tool的运行状态与数据  

tools $^+$ 连线 $^+$ 运行调试。  

1数据读取与准备  

![](images/d8a2550e8b9c046864d495114290eab22d5fdf80cd89417b1b91f54bf82da4ef.jpg)  

2算法调用与预测输出  

![](images/9cb81fcc2eaf73fbf6fa68fdf9dfea9a6692555f320882374eb11eae504e2948.jpg)  

# 代码方式or图形化工具？  

常见的数据准备、算法调用，运行调试，图形化工具更为直观方便。但选择了图形化的界面，也就选择了某种限制（算法模型更新会滞后，参数设置不如代码的完整），以及，不方便与其他系统的集成。  

新手：借助图形化工具跑起来，先解决自己的问题。进阶：掌握代码实现，考虑项目实施。·高手：图形化工具或氛围编程（vibe coding）快速验证，代码方式定制优化。  

![](images/92dd4b8f3c71256b678eace847e631e83470a1db94de48c23cb3b3cb784b411b.jpg)  

可以结合起来用。  
不用像「哈姆雷特」那么纠结。  

![](images/ee0535153892557a46d0fdd471fc443951d7cdd9d64df5f3e6215a1013bb1ed3.jpg)  

# 特征工程深入（上）  

特征工程是把杂乱的数据打磨成能让模型理解、学习并发挥作用的特征。涵盖清洗、编码、选择与降维等步骤，并最终影响模型的复杂度与表现，在实战中决定成败。  

特征工程是什么  
特征工程的流程与关注点  
数据清洗：缺失值处理、异常检测与处理策略  
特征编码&特征提取  

# 特征工程是什么  

特征工程是将数据转换为能更好地表示潜在问题的特征，从而提高机器学习性能的过程。  

特征：有意义的数据属性。性能：可度量的表现，也就是模型的效果  

# 特征工程的流程  

理解问题 $\rightarrow$ 清洗 $\rightarrow$ 构造 $\rightarrow$ 编码 $\rightarrow$ 选择/降维 $\rightarrow$ 验证选代。  
我们有时候会说，机器学习 $=80\%$ 数据处理 $+20\%$ 模型选择与调参。  

1.理解数据和问题  
2.数据清洗  
3.特征构造  
4.特征编码  
5.特征选择  
6.特征降维（可选）  
7.验证与迭代  

# 特征工程的关注点  

在质量、相关性、可解释性和效率之间找到平衡，让模型能学得好又跑得稳。  

1.数据质量：保证缺失值、异常值等问题被合理处理，否则影响整体建模效果。  
2.特征相关性：生成和选择能真实反映潜在问题的特征，而不是无关噪声。  
3.可解释性：特征应当尽量清晰易懂，方便业务理解与应用。  
4.复杂度与效率：控制特征维度，避免过拟合和计算资源浪费。  
5.泛化能力：确保模型不仅在训练集上表现好，在新数据上也保持稳定。  

# sibsp对家庭关系的定义：  

·兄弟姐妹包括：兄弟、姐妹、继兄弟、继姐妹  
·配偶包括：丈夫、妻子（情妇和未婚夫不计入）  
parch对家庭关系的定义：  
·父母包括：母亲、父亲·子女包括：女儿、儿子、继女、继子·有些孩子仅和保姆同行，因此这些乘客的parch=0。  

# 特征工程的经验法则：泰坦尼克数据举例  

以泰坦尼克数据集为例，基于常见的业务背景，数据处理经验，也可以做好初步的筛选判断。  

性别、年龄、舱位等级，这些会直接影响生存  
·SibSp和 Parch都是“家庭关系”→考虑合并成“FamilySize”  
舱号有用，但缺失严重，就先排除  
票号主要是无规律的数字，也排除  
姓名看起来没法用，不过可以提取下头衔  

# 数据清洗：缺失值处理、异常检测与处理策略  

在数据清洗环节，缺失、异常的处理是最为常见的任务。如何处理判断，需要额外的经验与方法。这部分工作也和特征工程密切相关。  

常见的缺失值处理方法异常检测与处理  

# 数据清洗：缺失值处理  

缺失值容易发现，但如何处理，可以有不同的方法策略。判断  

缺失比例：缺失率高到 $70\%{-}80\%$ ，考虑放弃·缺失模式：是随机缺失还是特定缺失（比如某个港口的票号缺失）  

# 处理  

·简单填补：均值/中位数/众数  
→·分类填补：按某个类别下，取均值或中位数。（比如已知男女的年龄分布不同）  
$\rightarrow$ ·模型填补：用回归或KNN预测缺失值·缺失标记：直接加一列“是否缺失”，让模型自己学  

# 数据清洗：缺失值处理  

泰坦尼克数据集，用Pclass和Sex的Age均值，来填补Age的缺失。  

import pandas as pd file_path $=$ "./data/titanic/train.csv"" df $=$ pd.read_csv(file_path)  

#检查Age缺失情况 missing_age_before $=$ df['Age'].isnull().sum() print(f"缺失值数量（填补前）:[missing_age_before}")  

#用Pclass和Sex分组的Age均值填补缺失 df['Age'] $=$ df['Age'].fillna( df.groupby(['Pclass,'Sex'])['Age'].transform('mean')  

Pclass female male1 34.6 41.32 28.7 30.73 21.8 26.5各个船舱等级的男女的平均年龄不同，分类填补更合适。  

![](images/871a5646b15f7b4221c916c2ca9a24b54bbc77a7629f5cf99df7942eb316e20d.jpg)  

# 数据清洗：缺失值处理  

用KNN算法（k-nearestneighbors，k近邻算法）来填补。  
找出age缺失数据的距离最近的k个样本，取平均。  

importpandas aspd from sklearn.impute import KNNimputer from sklearn.preprocessing import LabelEncoder file_path="/data/titanic/train.csv" df=pd.read_csv（file_path)  

dff'Sex']=LabelEncoder(.fit_transform(df['Sex'])   
features=['Age,‘Pclass’'Sibsp'‘Parch’Fare’‘Sex’]   
#拟合KNNimputer，5个邻居   
imputer=KNNimputer(n_neighbors=5)   
imputed_array $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ imputer.fit_transform(df[features])   
$\#$ 保存填补后的Age   
df['Age_imputed'] $=$ imputed_arrayl:,0]  

$\#$ 查看填补前后的 Age列df[l'Age''Age_imputed'].head(-10)  

# 优点：  

基于多个特征找相似，更合理。不会像整体、分类取平均填补那么死板。填补完，容易保持原有的数据分布。  

缺点： 速度慢适合小数据。对噪声和异常值敏感  

# 数据清洗：异常值处理  

相比于明显的缺失，异常需要额外的判断。  

# 判断  

统计方法：箱线图、Z-score（比如 $>\!30$ 当成异常）逻辑检查：年龄为负、票价为0这种明显不合理。  

# 处理  

修正：数据录入错误就改（比如多输入了一个0）裁剪：对超出范围的值做上下限截断变换：长尾分布的变量用对数或分箱（收入高中低）删除：如果异常点确实噪声，不多的话可以直接剔除  

![](images/fc18dda8a1869e14e2714db5f4a8a406f95e11f04da6dae0af550488cac96a1b.jpg)  

95岁老人开车买麦当劳早餐异常值 $\neq$ 错误值。  

# 数据清洗：异常值处理  

某些字段的值特别高，会对模型或统计分析造成不平衡的影响（增加偏差）。  
不同舱位的票价不同（英镑）有少数数据（土豪）明显高于整体，需要截断处理。  

![](images/6b646a569362f386309cc438dbf6921285f57f8d0b6475af2bc71d04a53dc1f5.jpg)  

# 数据清洗：异常值处理  

对泰坦尼克的头等舱票价数据做截断。先计算3倍IQR，超出的截断到3倍IQR。  

importpandas aspd  

df $=$ pd.read_csv("/data/titanic/train.csv") df_first $=$ df[df["Pclass"] $\mathbf{\omega}=\mathbf{\omega}_{1}$ ].copy(）#只处理一等舱  

#计算IQR和3倍上界   
$92=$ df_first["Fare"].quantile(0.25)   
$93=$ df_first["Fare"].quantile(0.75)   
$i q r=93-91$   
upper_ $3=93+3^{\star}$ iqr  

$\#$ 截断票价 df_first["Fare_capped"] $=$ df_first["Fare"].clip(upper=upper_3)  

$\#$ 查看结果   
print（("3倍IQR上界：",upper_3)   
display(df_first.loc[df_first["Fare"] $>$ upper_3, ["Passengerld","Name","Ticket”,"Fare","Fare_capped".  

# 特征编码&特征提取  

在机器学习场景里，特征编码（featureencoding）主要处理数值型和类别型两大类。其他类型（时间序列、文本、图像等）本质上还是要先“转化成数值或类别”，再交给编码环节。  

# 特征编码-数值  

连续或离散的数值数据。例如销量、库存量、运输时间。  

编码方法  

标准化  

归一化  

# 目的  

让不同量纲的特征在同一尺度下对模型产生影响。  

运输时间：0-72小时  
运输成本：100-10,000元 供应商聚类  
准时率：0-1  

# 特征编码-类别  

取值为有限个类别的变量，如供应商类别、仓库区域。  

One-HotEncoding将每个类别转化为二进制向量。  
Label Encoding将类别映射为整数。  

# 目的  

让类别变量能被模型使用。  

![](images/3a886e1e61f02bfe048300d764ca687cf8ea987e3ea095fc3163fb75f2c41302.jpg)  

# 特征提取－时间序列  

原始时间序列往往不能直接作为输入，需要通过特征提取把时间信息转化为可供模型学习的特征。同时，时间序列的特征提取也是比较需要经验的。  

时间衍生变量滞后特征滑动窗口特征  

# 特征提取－时间序列的时间衍生变量  

时间衍生变量（Date/TimeDerived Features）是由时间字段提取或转换得到的新变量，如年、月、日、季度、周、时段、节假日等。  

# 周期性特征  

日历特征：年、月、周、日、小时  
周期特征：季度、工作日/周末  
节假日特征：是否节假日、节假日前后几天  
季节性特征：春夏秋冬  

春节，长假需要配置表。  

# 场景  

月末：可能触发集中采购或结算，销量上升春节：物流延迟、销量下降或提前拉高  

![](images/f3d50b4ea88b4ad2bec22c140ca6770f7f6fdafec72dfe5e91cbc10b12fb8da9.jpg)  

# 特征提取－时间序列的滞后特征  

滞后特征（LagFeatures）用过去某一时刻的值作为当前的输入特征。  

例子  

销量_t-1 （昨天销量）销量_t-2 （前天销量）销量_t-7 （上周同日销量）  

# 场景  

预测某天销量 $\rightarrow\overline{5}1$ 入昨天、上周同日的销量  

# 技巧  

·一般是同时生成多天（周、月）的滞后特征，然后，通过相关系数，找出最合适的滞后期。比如：计算滞后期1-30的出货量，计算与出货量的相关系数。  

# 特征提取-时间序列的滞后特征  

出货量的滞后期与销量的相关系数计算。  

日期 shipment ssles2026-01-01 120 1002025-01-02 135 1102025-01-03 140 115皮尔逊相关系数（Pearson Correlation Coefficient,r）  

相关系数范围 相关程度说明  
0.8\~1.0 极强相关（非常密切）  
0.6\~0.8 强相关  
0.4\~0.6 中等程度相关  
0.2\~0.4 臀相关  
0.0\~0.2 极相关或无相关  

<html><body><table><tr><td>日期</td><td>shipment</td><td>seles</td><td>lag_1</td><td>Iag_2</td><td>lng_3</td><td>leg_4</td><td>lag_5</td></tr><tr><td>2025-01-01</td><td>120</td><td>100</td><td>NaN</td><td>NaN</td><td>NaN</td><td>NaN</td><td>NaN</td></tr><tr><td>2025-01-02</td><td>135</td><td>110</td><td>120</td><td>NaN</td><td>NaN</td><td>NaN</td><td>NaN</td></tr><tr><td>2025-01-03</td><td>140</td><td>115</td><td>135</td><td>120</td><td>NaN</td><td>NaN</td><td>NaN</td></tr><tr><td>2025-01-04</td><td>150</td><td>125</td><td>140</td><td>135</td><td>120</td><td>NaN</td><td>NaN</td></tr><tr><td>2025-01-05</td><td>160</td><td>130</td><td>150</td><td>140</td><td>135</td><td>120</td><td>NaN</td></tr><tr><td>2025-01-06</td><td>170</td><td>145</td><td>160</td><td>150</td><td>140</td><td>135</td><td>120</td></tr><tr><td>2025-01-07</td><td>180</td><td>155</td><td>170</td><td>160</td><td>150</td><td>140</td><td>135</td></tr><tr><td>2025-01-08</td><td>200</td><td></td><td>180</td><td>170</td><td>160</td><td>150</td><td>140</td></tr></table></body></html>  

![](images/73eb3f2470c69a35b3a6b60bc5d27f0970f2c76dadc82db6899a9769728521c3.jpg)  

# 特征提取-时间序列的滑动窗口特征  

滑动窗口特征（Rolling/WindowFeatures）是在固定时间窗口内，对目标变量或特征做统计汇总，用于捕捉短期趋势和波动。  

# 统计量  

常见统计量：均值、最大值、最小值、标准差、中位数、偏度、峰度窗口大小：7天、30天、90天（依业务场景）  

# 场景  

过去7天销量均值 （短期趋势）过去30天销量标准差 （需求波动性）  

# 特征提取－时间序列的滑动窗口特征  

以过去7天销量均值为例，我们不是要用过去7天的均值直接算出预测结果，而是把它作为一个特征，交给机器学习模型去学习。模型会结合其他特征，一起推断未来销量。  

预测未来更多天数数值时，最近7天缺失问题的处理：  

滚动预测 （Recursive Forecasting）  

模型先预测第1天（t+1）的值→把预测值当作“真实值”填回去缺点：预测误差会累积，越往后越不准。  

# 直接预测 (Direct Forecasting)  

使用回归算法（比如随机森林或XGBoost），一次性预测未来30天。  
这样不会累积误差；  
缺点：模型复杂度高，需要更多训练数据。  

# 特征提取－文本  

文本特征是指来自非结构化文本数据的信息，例如订单备注、物流异常说明、客户反馈等。其目标是将自然语言转化为结构化的数值或类别特征，以便模型使用。除了传统的NPS方法，也可以结合LLM的能力。  

# 处理方法  

关键词提取 $\rightarrow$ 是否包含“延迟”“缺货”  
特征化（标签） $\rightarrow$ 订单备注“急单”“退货”“贵重物品”  
分类 $\rightarrow$ 天气原因/交通原因/供应商原因  
情感分析 $\rightarrow$ 正面/负面/中性  

# 场景  

·订单备注文本：识别客户备注“急单”，作为加急特征。运输异常说明：提取关键词“天气”“堵车”，作为运输延迟的输入特征。  

# 小结  

特征工程是机器学习过程中的重要一环，除了数据的准备、计算、编码，还涉及到业务的理解。作为业务背景的学员，在这方面会更有优势，因为很多特征的提取或计算思路，也是日常商业分析中会涉及的。  

熟悉特征工程的流程与关注点，有助于从全局、业务的视角，来组织机器学习的全流程，做好模型选择与分析优化。  

![](images/dcf7b7d13173fa7ebaa99023d0e51c9b65055aaeacc31889699f966b35885c5b.jpg)  

# 时间序列分析  

时间序列分析的核心思想是基于过去预测未来，通过研究历史数据的趋势、周期和随机波动，建立模型来推测未来的发展变化。  

背景与基础回顾  
·时间序列分析的常用算法  
ARIMA算法原理与应用Prophet算法简介与应用总结与展望  

# 背景与基础回顾  

在开始新的算法与应用前，先回顾下基础知识与通用的流程。  

时间序列分析的常见应用场景时间序列模式时间序列分析的通用流程  

# 时间序列分析的常见应用场景  

以供应链场景为例：  

需求预测：帮助企业估计未来产品需求。  
库存管理：根据预测制定补货计划，优化库存成本。  
价格预测：预测原材料价格波动，辅助采购决策。  

# 时间序列模式 (Time series patterns)  

时间序列的数据会表现为以下的一种或多种模式的组合。  

1.趋势性（Trend）：整体上升或下降的趋势。  
2.季节性（Seasonality）：固定周期的波动，如季度、月份、周、日的数据波动。  
3.周期性（Cycle）：不固定的长周期波动，通常与经济周期相关。  
4.随机成分（Noise）：不规则的、偶然的、无法预测的波动。  

![](images/5a6de409c9fdda182bc884548c7ae37ae17fee51de6bdffbec8ba9ede41cd604.jpg)  
时间序列模式 (Time series patterns)  
澳大利亚季度电力产值  
周期 美国新建房屋销售额  

![](images/349f9d5ea7f5265a17ff66517a71f7f3eba2d94fbc96c4378c71aac7d4caf041.jpg)  
航空公司乘客数  
Google每日收盘股价  

![](images/34fb00243ca69a88e715b4017e6923424b3d1d612f9afe4c5f7a0d88c9ded96c.jpg)  

# 柏林旅游人数时间序列分解  

时间序列分解图（Time SeriesDecompositionPlot）是一种将时间序列拆解为不同组成部分的分析工具，帮助我们理解数据变化的结构与规律。  

![](images/69bb3f4a1d86dd5e50b5f6c5b6999a0b252f5ae75c6af757803f4e35751948a3.jpg)  

原始数据（observed）趋势（Trend）·占比：28.52%季节性（Seasonal）·占比： $56.23\%$ 残差（Residual）·占比： $1.41\%$  

# 随机波动的时间序列数据例子  

如果残差（随机波动或异常）占比很高，那么会难以做未来的预测分析。  

趋势（Trend）占比： $6.65\%$ 季节性（Seasonal）占比： $20.80\%$ 残差（Residual）占比： $69.25\%$  

![](images/e0c32468bd6ff0327c976b89ee61a100cbba1ac08105aff2700d3a04bea0639c.jpg)  

# 时间序列分析的通用流程  

整体的流程与机器学习相似，只不过各个环节的关注点、方法会有所不同。  

1.定义问题  
2.数据预处理  
3.探索性分析  
4.建模方法  
5.模型评估  

# 定义问题－预测目标的量化  

目标量化的过程也是细化分解的过程。  

预测的粒度：品类、产品、天／周/月？  
预测的时间范围：未来多久？  
间隔频率：需要多久做一次预测？  
评判标准：选择合适的准确率指标（比如：MAPE）  
要达到的目标：准确率  

# 评估指标  

RMSE（均方根误差）：预测值与真实值的平方差异的平均值的平方根。  
MAE（平均绝对误差）：预测值与真实值的绝对值差异的平均值。  
MAPE（平均绝对百分比误差）：预测值与真实值的绝对百分比差异的平均值。  

测试集：[5,8,9] 预测集：[7,3,9]  

# RMSE:  

1.计算每对真实值和预测值的误差平方：  
（7-5)²=4,(3-8)²=25,(9-9）²=0  
2.误差平方和：4+25+0=29  
3.求均值： $\textstyle{\frac{29}{3}}=9.67$   
4.开平方：√9.673.11  

# MAE:  

1.计算每个预测与真实值的绝对差：17-5|=2,13-8|=5,19-9|=0  
2.求绝对误差的和：2+5+0=7  
3.求均值：$\frac{7}{3}\approx2.33$   
MAPE:  
1.计算每个预测的相对误差百分比：  
$\left|\frac{7-8}{5}\right|\times100-40\%,\quad\left|\frac{3-8}{8}\right|\times100=62.5\%,\quad\left|\frac{9-9}{9}\right|\times100=0\%$   
2.求相对误差百分比的和：  
0.40+0.625+0=1.025  
3.求均值：  
$\frac{1.025}{3}\approx34.17\%$  

# 时间序列分析的常用算法  

基于要分析的数据是单变量还是多变量时间序列，可以有不同的算法。  

单变量 (时间戳 $^+$ 一个观测值)·每日气温股票收盘价每日新用户数  

多变量（时间戳 $^+$ 多个相关变量）：·气温预测：温度、湿度、气压、风速·门店销量：位置、等级，假期，促销采购量：生产计划、订单预测、供应商产能  

# ARIMA算法介绍  

ARiMA是一种常用的时间序列预测模型，全称是AutoRegressive IntegratedMovingAverage（自回归积分滑动苹均模型）。  

扩展  

ARIMA：单变量、无季节性的时间序列。  
SARIMA：在ARIMA的基础上，增加了季节性成分。  
SARIMAX：在SARIMA的基础上，增加了外部变量（如气温、促销力度）  
使用statsmodels库  
ARIMA→statsmodels.tsa.arima.model.ARiMA  
5ARIMA/SARIMAX→statsmodels.tsa.statespace.sarimax.SARIMAx  

# ARIMA算法介绍  

适用场景：单变量、无季节性的时间序列。  

参数形式：ARIMA（p，d，q）  

p：自回归阶数，表示使用前多少个时刻的数据。  
d：差分次数（使序列平稳），表示差分的次数。  
q：移动平均阶数，利用过去的误差项（预测残差）来修正预测。  

# ARIMA算法介绍  

假设我们要预测某个仓库的的季度出货量，每一年有4个季度，数量单位是百方。  
数据从1960年开始，以最后一年1980年作为测试集。  

![](images/07d756df93407f1c612a012d54856b3ceaccba78e07cded2f6e6f39679a2a840.jpg)  

门店季度收入数据荐在趋势性与季节性，因此原始序列并不平稳。·涌过二次差分（d=2）后，序列趋于平稳。当前季度收入与前3个季度收入相关性显著→p=3。·残差部分还与前3个季度的扰动项存在相关性→0=3  

最终得到模型：ARIMA（3,2,3）  

# ARIMA算法介绍  

差分（Diferencing）是时间序列分析里的一种平稳化方法，核心思想是：把当前值减去前一期的值，来消除趋势或季节性，使序列更加平稳。  

![](images/de32e87ccf1b54a22e92d84494194e32e3c2d9477eba1f4e406377760113a2c3.jpg)  

# SARIMA 简介  

SARIMA在ARIMA模型的基础上，加入了季节性因素的扩展模型，专门用于处理同时存在趋势和季节性的时间序列。  

·周期性重复：在固定时间间隔内（例如每年、每季度、每月、每周甚至每天）都会出现相似的波动。·固定或近似固定的频率：例如零售销售额通常在每年年底假期（12月）达到高峰。·可叠加在趋势上：季节性往往和长期趋势叠加，形成整体序列模式。  

# SARIMA 算法介绍  

参数形式：SARIMA（P,d,q）)（P，D,Q,S)  

非季节部分  

p：自回归阶数（AR）d：差分阶数（1）q：移动平均阶数（MA）  

# 季节部分  

·P：季节性自回归阶数  
D：季节性差分阶数  
Q：季节性移动平均阶数s：季节周期长度（如月度数据常取12，季度数据常取4，周数据常取7）  

# SARIMA 算法介绍  

以航空公司的乘客数据为例，拆分训练测试集，预测最后一年的每个月的乘客数。  

![](images/7901f61ed3b3fcd67e9d9c723a231ba1288b05621bbededec059bd27aa88ae87.jpg)  

# SARIMA (2,1,1)(1,1,2,12) $\rightarrow$ MAPE:2.99%  

# 季节部分  

<html><body><table><tr><td>修数</td><td>名称</td><td>值</td><td></td></tr><tr><td>P</td><td>自回归阶数（AR）</td><td>2</td><td>使用前2期的乘客数预测当前值</td></tr><tr><td>d</td><td>差分阶数（）</td><td></td><td>对序列做1次非季节性差分，消除趋势</td></tr><tr><td>a</td><td>移动平均阶数（MA）</td><td></td><td>使用前1期的误差修正预测</td></tr></table></body></html>  

# 非季节部分  

<html><body><table><tr><td>参数</td><td>名称</td><td>值</td><td></td></tr><tr><td>P</td><td>季节性自回归阶数</td><td></td><td>使用前1个季节（12个月前）的乘客数预 测当前值</td></tr><tr><td>D</td><td>季节性差分阶数</td><td></td><td>对序列做1次季节性差分（间隔12个 月），消除季节性趋势</td></tr><tr><td>Q</td><td>季节性移动平均阶数</td><td>2</td><td>使用前2个季节（12个月间隔）的误差修 正预测</td></tr><tr><td>S</td><td>季节周期长度</td><td>12</td><td>一个周期为12（即一年，适合月度数据）</td></tr></table></body></html>  

# SARIMAX 算法介绍  

在SARIMA的基础上，允许引I入外部参考变量，用于捕捉额外的影响因素。  

![](images/e041de849de863e4cc2424dd0e815a9272c60d4e077d312e30cd429241698338.jpg)  

importpandasaspd fromstatsmodels.tsa.statespace.sarimaximportSARiMAx  

#y $=$ 乘客数   
$\#x=$ 外部参考变量，比如节假日和促销活动   
$x=$ pd.DataFrame({ "holiday": [.],. "promotion": [...]   
1, index=y.index)  

# 有没有自动化调参的方法？  

参数这么多，自己观察和尝试，费时费力。  

网格搜索（Grid Search）设定参数范围，遍历所有组合。  
pmdarima（auto_arima）最为常用方便。  

![](images/0239b4c7a44b0ddf8fab34c8ea81df6c3cb7e5c29a953d357f634ff1b264fefd.jpg)  

# auto_arima 自动化调参  

auto_arima是pmdarima库里最常用的函数，用来自动选择ARIMA / SARIMA 模型的最佳参数。它会通过统计检验+遍历搜索+信息准则（AIC/BIC/CV)来找到合适的模型。  

# import pmdarima aspm  

model $=$ pm.auto_arima( train[Passengers']，#训练集的月度乘客数据 seasonal=True, $m=12$ #季节周期12 stepwise=True，#启用逐步搜索（效率高） suppress_warnings=True, trace=True #打印搜索过程  

SARIMAX（3,0,0）（0,1,0,12） $\rightarrow$ MAPE: $3.1\%$  

自动化调参不一定最优，但整体方便稳定。  

手工调参：  
SARIMA (2,1,1) (1,1,2,12)  
$\rightarrow$ MAPE: $2.99\%$  

# 如何判断预测表现或好坏？  

百分百的预测准确是不存在的，以MAPE为例，什么是可接受的，什么是表现好的？  

和基准方法比较（移动平均，最近一期的值）  

基于经验的参考区间（5%，10%，20%）·和数据的波动、稳定性有关（比如每日上班人数稳定）·和行业场景有关（电商，金融会不同，后者要求更高）  

![](images/1d9187be351f50e74d83a69dab0b11f074333dc3709c59cb769c7f199c907787.jpg)  

# Prophet算法简介与应用  

Prophet是Meta在2017年开源的时间序列预测工具，主要用于处理具有明显季节性、趋势性和节假日效应的数据。设计目标是让非专业人员也能快速得到准确的预测结果。  

自动建模趋势、季节性和节假日影响对缺失值和异常值具有鲁棒性可以灵活加入人为规则（如特殊节日、营销活动）  

# Prophet算法简介与应用  

# 继续以乘客数据为例。  

importpandasaspd from prophet importProphet from sklearn.metricsimport mean_absolute_percentage_error df=pd.read_csv(./data/air-passengers.csv") df.columns $=$ ['ds,'y'] dff'ds']=pd.to_datetime(dff'ds')  

#划分训练集（除最后12个月）和测试集（最后12个月）   
train=df.iloc[:-12]   
test=df.iloc[-12:]  

#建模并拟合 model=Prophet( model.fit（train)  

#生成未来日期，预测未来12个月）   
future=model.make_future_dataframe(periods=12,freq=Ms）   
forecast=model.predict(future)  

#提取预测结果（最后12个月对应test） pred= forecast[l'ds,'yhat']].iloc[-12:]  

#计算MAPE   
mape = mean_absolute_percentage_error(test('y')l.values,   
pred['yhat'].values)   
print(f"MAPE:(mape:4f)")  

# Prophet算法简介与应用  

继续以乘客数据为例。  

![](images/f0fd5341bb13eb694f13fdab324db295d12a1db1fe37ddff859ae7ae3553df43.jpg)  

# Prophet算法简介与应用  

参数与调用说明。  

输出的数据列固定：ds，y  
通用的机器学习函数命名：fit，predict  
使用future_dataframe来设置要预测的未来的时间范围  
预测值的名字是：yhat  

model=Prophet()使用默认参数，即可运行。  

# Prophet算法简介与应用  

model $=$ ProphetO主要参数 growth：趋势类型，linear （默认） 或logistic。  

seasonality_mode：季节性类型，additive（加法，默认）或multiplicative（乘法）changepoint_prior_scale：趋势转折点的灵活度（越大越容易弯曲，默认0.05）。seasonality_prior_scale：控制季节性幅度。  
·holidays_prior_scale：控制节假日效应幅度。  

![](images/ec9c85a1477bc1d2308786f0c09a6b24c59e8551f5df5c39e054772f4493a7cf.jpg)  

也可以通过网格搜索方式，得到最佳参数。changepoint_prior_scale $=0.025$ seasonality_prior_scale $_{=0.08}$  

# Prophet算法简介与应用  

继续以乘客数据为例。  

![](images/f5417cce0b4f4d9f82be1171e17f8a6d1a311b4b51a557ff09cd4a36d070a7b6.jpg)  

model $=$ Prophet() # seasonality_mode='additive' model.fit(train)  

MAPE:0.0662  

![](images/cc19988eb9a191f784d8f9fd02c8474fecc27ad62b9d6395023c3b0f6b55da82.jpg)  

model $=$ Prophet(seasonality_mode='multiplicative) model.fit(train)  

MAPE:0.0446  

# Prophet算法简介与应用  

在Prophet中，节假日（holidays）的建模是一个很重要的特性。它允许你显式告诉模型某些日期（节日、活动、促销等）对时间序列有额外的影响。  

节假日类型  

固定、不固定  

节日前后的影响天数  

假设是圣诞树的销售，会是圣诞前为主。  

节日前后影响的天数  

笔记本的销售，会和哪些节日或活动相关？  

![](images/b3f160b5cf6d306870b539fa2142bfd3455bc0aa21989b54c93eef7de162eb8d.jpg)  

mode = Prophet(holidays=holidays_df) 1"upper_window:[1,1,1,1,1,1]#节日后的天数 import pandas as pd  

节假日的配置，可以是一种或多种节日，包括节日前后的影响天数。 Prophet算法简介与应用  

# 小结  

ARIMA家族模型（含SARIMA、SARIMAX）擅长处理平稳且有季节性的时间序列，适合统计学意义上的建模与短期预测。  

而 Prophet通过趋势+季节性+节假日的分解方式，参数直观、结果可解释，更适合业务场景下的中长期预测。  

![](images/1290606d007039bcc678e3f939ba60cd729397b450e9885368052d05397d5abd.jpg)  

# 层次聚类算法  

聚类算法是无监督学习里的最为常用、实用的算法。  
这一次我们来介绍层次聚类，也会和k-means做一下比较。  
背景知识回顾  
层级聚类原理与使用介绍  
场景案例  

# 机器学习的常见学习类型  

# 有监督学习 （supervised learning）  

特点：数据有标签（比如“这是好供应商”“这是坏供应商”）目标：训练一个模型，把新样本分到已有的类别例子：垃圾邮件识别（邮件要么是spam，要么是ham）  

# 无监督学习 (unsupervised learning)  

特点：数据没有标签，模型自已找结构  
目标：发现数据内部的相似性或潜在规律  
例子：根据消费习惯把顾客分群，但事先没人告诉你「顾客应该分成几类」  

# 聚类算法的作用  

聚类是无监督学习的典型代表。不需要标签，只需要数据本身。  

数据探索（看清数据结构）  
降维或预处理（比如先分群，再建模）  
业务分析场景（客户分群、供应商分群、SKU分群）  

# K-Means 算法回顾  

![](images/dec0031641bc6ef25e588f2b0c0ff7b25205df02bf3e95488e8c9afb01b2bac6.jpg)  

1.初始化中心：随机选择K个数据点作为初始聚类中心（质心）  

2.分配：将每个数据点分配给最近的聚类中心，根据距离（通常使用欧几里得距离）。  
3.更新中心：重新计算每个簇的质心，方法是计算分配给该簇的所有数据点的均值。  

重复运行，直到聚类中心不再发生显著变化或达到预设的迭代次数。  

# K-Means 的局限性  

K-Means容易理解，性能也不错但也有自己的局限性。  

1.运行前必须指定k  
2.偏向球状簇  
3.对噪声敏感、可能陷入局部最优  

![](images/4f069c5c6be0a524ef15b35ac9642a9f713b39c6b6afd98ca5e21e8f08aecdce.jpg)  

# 应用层次聚类（Hierarchical Clustering）来提升  

# 优点：  

1.适合做探索性分析，先看数据整体结构，而不是拍脑袋定簇数（K）  
2.给出一个完整的“层级结构”，可以从粗到细任意切割  
3.可通过树状图（dendrogram）直观展示聚类过程  

# 缺点：  

1.计算复杂度较高，大数据集上性能会下降。  
2.对噪声敏感。  
3.一旦合并或分裂，不能回退  

# 层次聚类原理  

据样本之间的相似度，逐层构建一个“聚类树” (hierarchy)  

自底向上（凝聚式，agglomerative）  
起点：每个样本单独作为一类  
步骤：  
1.计算所有簇之间的距离  
2.找到最近的两个簇，合并  
3.更新距离矩阵  
4.重复，直到所有点合成一个簇  
自顶向下（分裂式，divisive）  
起点：所有样本先是一类  
步骤：逐步把某一类分成两类，直到每  
个点独立  

# 层次聚类原理  

自底向上的聚类过程。  

![](images/771b5a42918e9213817bee99bc0ff85e89a11155a8c9170246baae9abc75f33d.jpg)  

# 以供应商分层来举例  

假设我有很多供应商的数据，包括：价格指数，不良率，质量分，准时率，交付周期，距离等信息  

![](images/22566ca85567e655863a885c8273362f1ac069cdc8d721ae1f22d0cecd0f0a3f.jpg)  

# 以供应商分层来举例：K-means  

分别指定不同的K值运行。不同的K值单独求解。  

![](images/6cec73996f146e6e52dbf3e0d66d8276c7e37e5e4e80d88d986b156a17e437c8.jpg)  

# 以供应商分层来举例：层次聚类  

K: $4\rightarrow3$ 时，是一个明显的合并的过程。  

![](images/39ed90b363adb07d47db405180b09f88a4601edd078f4cd011725df53ecd6284.jpg)  

# 以供应商分层来举例：层次聚类  

完整的数据只计算一次，生成树状关系。指定不同的K值来“剪树” (cutthe tree)  

![](images/c41a122adb02486e79c6f5ab39b1c36694e3b3a015590edc595c858bb6d83c4c.jpg)  
以供应商分层来举例：层次聚类  

![](images/21547a08e392c84690a5d2bcd5fecf2c99d9217b2af52f8390efd207549870d2.jpg)  

# 以供应商分层来举例：层次聚类  

![](images/385d9a6091decdf674a1ee32400c13d2cf8cecbf8f6b1de3073c6ca886e1b3a9.jpg)  

# 以供应商分层来举例：层次聚类  

K: $4\rightarrow3$ 时，是一个明显的合并的过程。  

![](images/bfe50a7a622e09696afccff5238e739fd11229214c13dbf87e8831b45015fb96.jpg)  

# k-means与层次聚类的比较  

![](images/7679e8d76b5bf377a42ab78887995793e55dbb544f2e1096bbaedcdb1066d11d.jpg)  

K-Means箱子数量变了，物品需要重新寻找最佳存放位置。  

![](images/002038e2a728d45f668f92a092923e9ac71b5fee45f99a14e9eb0c704db531b0.jpg)  

层次聚类像一个有序的书架，每本书在固定的位置。  

# 层次聚类  

![](images/0a4663a85f2b5e3932f4b7b581508efea0118505c3706e13ca650c5786286092.jpg)  

# 代码实现  

importpandasaspd from sklearn.preprocessing import StandardScaler from scipy.cluster.hierarchyimport linkage,fclustr file_path=”/data/供应商数据.csv” df =pd.read_csv（file_path)  

cols=[”price_index”,“defect_rate_pct”]#要使用的列  

标准化   
scaler= StandardScaler()   
data_scaled= scaler.fit_transform(df[cols])  

层次聚类 Z=linkage(data_scaled,method="ward")  

不同的K值剪枝clusters_k3=fcluster（Z,3,criterion=maxclust")clusters_k4=fcluster（Z,4,criterion=maxclust")  

合并结果 data_with_clusters=dffcols].copy( data_with_clusters["cluster_k3"]=clusters_k3 data_with_clusters["cluster_k4"]=clusters_k4 输出结果 display(data_with_clusters.head(100))  

1.使用scipy.cluster.hierarchy库  
2.只计算一次，生成树状关系  
3.根据不同的K值剪枝  

<html><body><table><tr><td>prlce_Index</td><td>detectrate_pet</td><td>cluster_ka</td><td>cfuster_ka</td></tr><tr><td>1.012</td><td>0.40</td><td></td><td>2</td></tr><tr><td>1.080</td><td>0.48</td><td></td><td>2</td></tr><tr><td>1.056</td><td>0.53</td><td></td><td>2</td></tr><tr><td>1.043</td><td>0.32</td><td>1</td><td>2</td></tr><tr><td>1.034</td><td>0.37</td><td></td><td>2</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td>0.879</td><td>1.25</td><td></td><td>3</td></tr><tr><td>0.838</td><td>1.04</td><td>2</td><td></td></tr><tr><td>0.799</td><td>1.12</td><td></td><td></td></tr><tr><td>0.889</td><td>1.14</td><td></td><td></td></tr><tr><td>0.796</td><td>0.65</td><td>2</td><td>3</td></tr></table></body></html>  

# 距离的度量  

single average complete Ward  

![](images/e183cacf9c5d6ed32cd9b51c637198d8c6abf2aa07594fea56408bfb613d0ba5.jpg)  

# linkage(data_scaled,method $=$ ......  

单链接（single linkage）：·两簇最近的两个点之间的距离·直观效果：容易拉成链状（“chainingeffect”）  
平均链接（average linkage）：·两个簇之间所有点对的平均距离·折中方法，效果稳定  
完全链接（complete linkage）：·两簇最远的两个点之间的距离·直观效果：簇更紧凑，不容易拉成一条线  
Ward方法：·合并后增加的“平方误差和”最小·本质上追求簇内方差最小，和 $k$ -means思想接近  

# 距离的度量  

![](images/964e5dbe6ff80c53750ab3110ca35532addc63273e78c7fd5ff8f9f4670ae466.jpg)  

# 单链接（singlelinkage）  

两簇最近的两个点之间的距离·直观效果：容易拉成链状（“chainingeffect”）  

![](images/58aee37ce2d53e6b9b13565989916ac0e91f9d492de57ce28cee6288bfd30a55.jpg)  

# 完全链接（complete linkage）  

两簇最远的两个点之间的距离直观效果：簇更紧凑，不容易拉成一条线  

# 代码实现  

import matplotlib.pyplot asplt importmatplotlib from scipy.cluster.hierarchy import dendrogram $z=$ linkage(data_scaled,method="ward")  

#绘制树状图 plt.figure(figsize=(10,5) plt.title（"层次聚类树状图"） plt.xlabel(“样本索引l") plt.ylabel("距离")  

#传入聚类结果：Z dendrogram(Z)  

plt.axhline（y=Z[-3,2],color=red，linestyle='--，label='K=3分界线）  
plt.legend()  
plt.show()  

![](images/f69a521861b22e72614c91b81b723150c53c78eba2dd0b508475daebd38c8542.jpg)  

# 层次聚类的应用  

我们用供应商数据构建了“聚类树”（hierarchy），然而不同的K值，群组只是数据的划分，还需要「业务视角」的解读。  

1.自上而下， $\kappa=2$ ，3，4.....分别解读  
2.计算各个群组的：数据量，参数值的特性分布  
3.命名和解释  

# 层次聚类的应用  

使用完整的字段分别取 $k=2$ ，3  

字段名 supplier_id price_index quality_score on_time_rate lead_time_days defect_rate_pct distance_km capacity_score annual_spend_million orders_per_year min_moq contract_years risk_score  

含义供应商编号，S001...S200。价格指数，1.0约等于市场均价，小于1更便宜。质量分，0-100。准时率百分比。交付周期（天）不良率百分比。距离（公里），跨国显著更远，方便模型“看见”边界。产能评分。年度采购额（百万）。年订单数。最小起订量。合作年限。风险评分（越高越糟）  

# 层次聚类的应用  

#选择用于聚类的字段   
cols=[ "price_index”,“quality_score”,"on_time_rate",“lead_time_days"， "defect _rate_pct”,"distance_km","capacity_score",   
"annual_spend_million", "orders_per_year","min_moq","contract_years","risk_score”  

scaler=StandardScaler() data_scaled = scaler.fit_transform(df[cols)  

#计算层次聚类 Z=linkage(data_scaled,method="ward")  

#生成不同K值的聚类标签 df["cluster_k2")=fcluster(Z,2,criterion="maxclust") df["cluster_k3"]=fcluster（Z,3,criterion="maxclust")  

display(df.groupby("cluster_k2")[cols].mean(.reset_index()  

cluster_kz count price_Index quality_score on_time_rate lead_time_days 1 40 0.798650 75.42500 83.61750 8.90000 2 160 1.076725 90.93125 92.71375 15.54375   
delect_rate_pct distance_km capacity_score annual_spend_million 1.438750 132.07600 40.175 0.730225 0.479563 1582.26875 76.826 3.169713   
orders_per_year min_mog contract_years risk_score 37.60000 71.75000 0.70000 48.2000 37.68125 1175.89375 5.13125 24.6375  

# $k=2$ 聚类均值特征  

Cluster 1:整体低价、质量偏低、距离近$\rightarrow$ “基础供应商”，成本低但不太稳定。  

Cluster2:  
高价、高质、距离远  
$\rightarrow$ “优质供应商”，交付稳定、能力强。  

![](images/21edcf0deb79c5559305d6f59c086f06e2927fe27b50bfe09782db66934bcecd.jpg)  
层次聚类的应用  

# $k=3$ 聚类均值特征  

Cluster 1:  
还是K2的「基础供应商」  
Cluster2:  
中等价格、距离近，质量高、交付准时  
$\to$ “战略合作伙伴”  
Cluster2:  
价格高、距离远、支出高、订单少、交期长  
$\rightarrow$ “高端远程供应商”  

![](images/f535756cf91f2fb232844524d1c6f73f7b3d55ac0e3a5e9964d16835ed6fa1a9.jpg)  

![](images/ef24c329f1ee4ca9fa9bc101428db695fb4f6a22e34833a0c56b9fbb7934c136.jpg)  

# 小结  

层次聚类是无监督算法的一种实现。相比于k-means更为方便，也有助于业务场景的讲解与解释。  

k-means：适合大规模、快速、要定好簇数的情况。  
层次聚类：适合探索性分析，不用先定簇数，能展示层级结构。  

# 特征工程深入（下）：特征选择&降维  

特征工程是把杂乱的数据打磨成能让模型理解、学习并发挥作用的特征。涵盖清洗、编码、选择与降维等步骤，并最终影响模型的复杂度与表现，在实战中决定成败。  

特征选择的评估  
特征选择的常用方法  
降维  
小结  

# 特征选择&降维  

特征选择是在众多特征中挑出对目标最有用的。  
降维：把高维特征压缩到低维空间，保留主要信息。先特征选择 $\rightarrow$ 去掉无关/噪声特征，减轻负担。  
再降维 $\rightarrow$ 对剩余特征做压缩，提取主要信息。  

# 特征选择  

特征选择是从大量候选特征中筛选出最有用的子集，以提升模型效果和训练效率。  

特征选择的评估特征选择的方法  

a.树模型输出特征重要性 3.嵌入法（Embedded）——训练时自动选择 b.后向剔除：从全特征开始，逐步去掉无用的特征 a.前向选择：从空集开始，逐步加特征，保留提升性能的特征 2.包裹法（Wrapper）——基于模型性能 b.方差过滤 a.相关性分析 1.过滤法（Filter）——独立评估特征 在开始特征子集的选择前，先要明确好坏的标准，提升的程度 特征选择的方法  

5.可解释性与鲁棒性（在不同时间段、不同样本上的表现是否稳定) W 1.明确目标和指标（准确率、召回率？） 在开始特征子集的选择前，先要明确好坏的标准，提开的程度。 特征选择的评估步骤整体模型效果的评估（比如交义验证）， 看某个新增/转换特征对模型性能的影响 建立基准模型（baseline），得到一组性能指标关注泛化能力  

![](images/7af914391bc518a292b2fa9f2090ba6c1b3b8bdaf0271d198e6c8a0ad42634b6.jpg)  

<html><body><table><tr><td>如果一个特征的取值几乎没有变化（方差接近0），那么它对区分类别或预测目标 特证选择的方法-方差过忘</td><td>删除小于该阀值的特征。 对每个特征单独计算方差，并设定一个值， 数值型归一化，类别型One-hot编码后计算。 本没有贡献，可以直接去掉。 计算方式：</td></tr></table></body></html>  

10 10 10 3 8 50 00  

# 特征选择的方法－卡方检验  

importnumpyasnp from scipy.stats import chi2_contingency  

#新的数据：接近独立，但各区域比例略有不同  
data_almost $=$ np.array([[67,33],[71,29],[70,30]]  

#卡方检验 p_almost,-,_=chi2_contingency(data_almost)  

print(f"p={p_almost:.4f})  

仓库区域 准时交付（1） 延迟交付（0） 总计华北 67 33 100华东 71 29 100华南 70 30 100  

P值 $=0.8156$ 接近独立，但各区域比例略有不同  

# 小结  

根据统计指标评估特征与目标的关系，独立于模型。过滤法是快速初筛（砍掉没用的特征），包裹法是精细挑选（优化子集性能）  

优点：计算快、实现简单，适合初筛缺点：忽略特征之间的交互  

# 特征选择的方法－包裹法 (Wrapper Methods)  

包裹法是一种以模型预测性能为标准的特征选择方法。  

把特征选择当作一个搜索问题：尝试不同的特征子集→训练模型→评估性能→选择最优子集。  

前向选择：从空集开始，逐步加特征，保留提升性能的特征后向剔除：从全特征开始，逐步去掉无用的特征  

# 特征选择的方法－前向选择  

从空特征集开始，每次加入一个能最大提升模型性能的特征。直到性能不再提升或达到预设特征数。  

运输时效预测  

1.先加入节假日→模型性能明显提升  
2.再加入天气 $\rightarrow$ 性能继续提升  
3.最后周几 $\rightarrow$ 提升有限 $\rightarrow$ 停止  

![](images/fd6b0a472edc42e72c4a78145eca2fe5273c86a76619561a43f314224f265e58.jpg)  

#  

![](images/56f8614bc651e1fc4b0e27706257b5a6f230247a1c7c7d54f9acd70dec29538c.jpg)  

# 降维  

降维：把高维特征压缩到低维空间，保留主要信息。  

特征选择→去掉无关/噪声特征，减轻负担。  
降维→对剩余特征做压缩，提取主要信息。  

# 降维-场景案例  

以供应链预测销量为例，包含很多原始特征：产品ID、仓库编码、供应商ID、日期、天气、节假日、促销活动、备注文本··  

# 1.特征选择  

去掉无关的（如订单号、票据号）删除信息量极低的（几乎不用的仓库编码）保留：天气、节假日、促销、历史销量等特征数 $50\rightarrow13$ ，全是“有用特征2.降维把13维压缩成3维主成分这3个“组合特征”涵盖了大部分信息量结果：数据更简洁，减少余，模型更稳定  

# 降维-场景案例  

剩下的10多个有用特征里，可能还有多重相关（当多个特征之间存在较强相关性时，就叫做多重相关），如“节假日”和“促销活动”高度相关。它们提供的信息有大量重复（余）。  

# 解决办法  

特征选择：删掉其中的余特征降维（PCA等）：把高度相关的特征合并成一个“主成分”  

# 使用PCA方法进行降维  

PCA（Principal ComponentAnalysis，主成分分析）是一种最常用的线性降维方法。通过线性变换，把数据投影到一组新的正交坐标轴（主成分）上，使得前几个主成分保留最多的方差信息。  

# PCA的使用：  

指定主成分个数（也就是降到几维）或保留的累计方差比例（一般是0.95）  

PCA的结果查看：查看各个主成分的特征与参数  

使用PCA方法进行降维  


<html><body><table><tr><td>销量</td><td>节假日</td><td>促销强</td><td>天气温</td><td>降雨量</td><td>季节编</td><td>特殊节</td><td>大型促</td><td>库存水</td><td rowspan="6"></td><td>指标 节假日</td><td>PC1 0.2460</td><td>PC2 0.6351</td><td>PC3 0.1722</td></tr><tr><td></td><td></td><td>度</td><td>度</td><td></td><td>码</td><td>假目</td><td>销活动</td><td>平 94</td><td>促销强度</td><td>0.0383</td><td>0.6924</td><td>-0.1908</td></tr><tr><td>94</td><td></td><td></td><td>28</td><td>28</td><td>2</td><td></td><td></td><td></td><td>天气温度</td><td>0.6090</td><td>0.0520</td><td>-0.2360</td></tr><tr><td>167</td><td>0</td><td></td><td>35</td><td>10</td><td></td><td></td><td></td><td>107</td><td>降雨量</td><td>-0.2960</td><td>0.0788</td><td>0.0899</td></tr><tr><td>167</td><td></td><td></td><td></td><td></td><td>2</td><td></td><td>o</td><td>167</td><td>季节编码</td><td>-0.5823</td><td>0.2581</td><td>0.2585</td></tr><tr><td>137</td><td>0</td><td></td><td>25</td><td>11</td><td>N</td><td></td><td>1</td><td>137 171</td><td>特殊节假日</td><td></td><td>-0.0627 0.0871</td><td>0.3308</td></tr><tr><td>171</td><td></td><td>四</td><td>35</td><td>41</td><td>N</td><td></td><td>o</td><td></td><td></td><td>大型促销活动 库存水平</td><td>-0.2720 -0.2501</td><td>-0.0363 0.1810</td><td>-0.6614 -0.5064</td></tr></table></body></html>  

<html><body><table><tr><td>日期</td><td>仓库编码</td><td>配送区域</td><td>供应商ID</td></tr><tr><td>2025-07-01</td><td>W3</td><td>E</td><td>S1</td></tr><tr><td>2025-07-02</td><td>W1</td><td>D</td><td>S4</td></tr><tr><td>2025-07-03</td><td>W2</td><td>B</td><td>S4</td></tr><tr><td>2025-07-04</td><td>W2</td><td>E</td><td>S4</td></tr><tr><td>2025-07-05</td><td>W3</td><td>C</td><td>S4</td></tr></table></body></html>

类别型需要额外的one-hot编码  

PC1 $\approx$ +0.61天气温度-0.58季节编码-0.30降雨量-0.27大型促销活动-0.25库存水平+0.25节假日-0.06特殊节假日+0.04促销强度PC2≈+0.69促销强度+0.64节假日+0.26季节编码+0.18库存水平+0.09特殊节假日+0.08降雨量+0.05天气温度-0.04大型促销活动PC3 $\approx$ -0.66大型促销活动-0.51库存水平+0.33特殊节假日-0.26季节编码-0.24天气温度-0.19促销强度+0.17节假日+0.09降雨量  

# 使用PCA方法进行降维  

importpandas aspd from sklearn.linear_model import LinearRegression from sklearn.metrics import mean_squared_error  

$x=$ df_data["节假日”，"促销强度"，"天气温度”，"降雨量”，季节编码"，"特殊  
节假日”大型促销活动”库存水平“!】  
$y=$ df_data["销量"]  

$\#$ 划分训练集 $c=5$ 9月16日）和测试集（>9月16日）train_mask $=$ df_data["日期"] $<=$ "2025-09-16"X_train,X_test $=$ X[train_mask], X[\~train_mask]y_train,y_test $=$ y[train_mask], y[\~train_mask]$\#$ 线性回归model $=$ LinearRegression().fit(X_train, y_train)y_pred $=$ model.predict(x_test)  

import pandas aspd   
from sklearn.linear_model import LinearRegression   
from sklearn.metrics import mean_squared_error   
from sklearn.preprocessing import StandardScaler   
from sklearn.decomposition import PcA   
$x=$ df_data[”节假日”促销强度”，”天气温度”，降雨量，季节编码”，特殊   
节假日”，”大型促销活动”，库存水平“]】   
$y=$ df_data["销量"]   
#标准化 $^+$ PCA   
scaler $=$ StandardScaler()   
X_scaled $=$ scaler.fit_transform(x)   
pca $=$ PCA(n_components=3)   
X_pca $=$ pca.fit_transform(x_scaled)   
#划分训练集和测试集   
train_mask $=$ df_data[日期"] $<=$ "2025-09-16"   
X_train,X_test $=$ X_pca[train_mask],X_pca[\~train_mask]   
y_train,y_test $=$ y[train_mask],y[\~train_mask]   
#线性回归   
model $=$ LinearRegression().fit（X_train,y_train)   
y_pred $=$ model.predict(x_test)   
print("MSE(用PCA):,mean_squared_error(y_test,y_pred)  

# 使用PCA方法进行降维  

import pandasaspd fromsklearn.preprocessingimportStandardscaler from sklearn.decomposition lmport PcA  

#特征矩阵   
×=df_datall“节假日”"促销强度””天气温度”“降雨量”"季节编码”"“特殊   
节假日””大型促销活动”“库存水平”1   
标准化+PCA   
scaler=Standardscaler()   
X_scaled=scaler.fit transform(x)   
pca=PcA（n_components=3)   
pca.fit(x scaled)   
#输出载荷矩阵   
loadings =pd.DataFrame( pca.components_.T, index=X.columns, columns=[f"pc{i+1)" foriin range(pca.n_components_)]  

print(loadings)  

载荷矩阵指标 PC1 PC2 PC30.2460 0.6351 0.1722  
节假白0.0383 0.6924 -0.1908  
促销强度0.6090 0.0520 -0.2360  
关气酒度-0.2960 0.0788 0.0899  
季节维码 -0.5823 0.2581 0.2585  
特殊节假日 -0.0627 0.0871 0.3308  
大型促销活动 -0.2720 -0.0363 -0.6614  
存永单 -0.2501 0.1810 -0.5064  

# 可视化多维的聚类结果  

PCA在聚类分析中也非常有帮助，尤其是当原始数据维度较高时。  
可以将高维数据投影到2D或3D空间。  

![](images/5808816a64c9d30cba819f61559cf3d39ca51a01f456cecef717ed7dbd18adcf.jpg)  

#  

#  

#  

# 算法的层级分类  

XGBoost是梯度提升算法的一种实现与增强。  

![](images/c5496c89643e8c1a87ed4f7b3e2a8f509a39eb8d0986999aedd27f2148f721f2.jpg)  

<html><body><table><tr><td>对比维度</td><td>AdaBoost</td><td>Gradient Boosting</td></tr><tr><td>基本思想</td><td>基于调整样本权重，关注被错分的样本</td><td>基于损失函数的梯度下降优化</td></tr><tr><td>误差处理方式</td><td>每一轮更新样本权重，被错分样本权重变大</td><td>每一轮拟合前一轮的残差（负梯度）</td></tr><tr><td>稳定性</td><td>对噪声和异常值敏感</td><td>更鲁棒，可调学习率、正则化等参数控制</td></tr><tr><td>可扩展性</td><td>损失函数固定（指数损失）</td><td>可灵活选择损失函数（MSE、log loss、MAE 等）</td></tr><tr><td>代表算法</td><td>AdaBoost.M1,AdaBoost.M2</td><td>GBM,XGBoost,LightGBM,CatBoost等</td></tr></table></body></html>  

![](images/655daccf4eb7b0668642f3cf6ab6aded77c5d781472c17afc36106ec277ec1d0.jpg)  
背景知识回顾  

# 以泰坦尼克数据集为例  

预测是否Survived？  

<html><body><table><tr><td>变量</td><td>定义</td><td>说明</td></tr><tr><td>survival</td><td>生存</td><td>0=未生还，1=生还</td></tr><tr><td>pclass</td><td>舱位等级</td><td>1=一等舱，2=二等舱，3=三等舱</td></tr><tr><td>sex</td><td>性别</td><td></td></tr><tr><td>Age</td><td>年龄</td><td>以岁为单位</td></tr><tr><td>sibsp</td><td>同行的兄弟姐妹/配偶数</td><td>泰坦尼克号上的兄弟姐妹或配偶人数</td></tr><tr><td>parch</td><td>同行的父母／子女数</td><td>泰坦尼克号上的父母或子女人数</td></tr><tr><td>ticket</td><td>票号</td><td></td></tr><tr><td>fare</td><td>票价</td><td>乘客支付的票价</td></tr><tr><td>cabin</td><td>舱号</td><td></td></tr><tr><td>embarked</td><td>登船港口</td><td>C=瑟堡，Q=皇后镇，S=南安普顿</td></tr></table></body></html>  

# 决策树算法  

决策树算法是构建了一颗规则树，乘客的特征会代入到这棵树，一直走到叶子节点（是否获救）。  

![](images/5192efcf2659ff52d1b8b7a8264432f455bfeeb5581545efb9e3b8a66eca791f.jpg)  

# 随机森林 (Random Forest)  

三等舱（Pclass）的47岁的女士，有一位同行的配偶（SibSp），能否获救？  

![](images/b6ec11794913a8022cbdcfd294cda97dd1a1bbd6e10445651117c556afd50368.jpg)  

# 梯度提升-第1颗树  

串行地构建多个决策树，每一棵新树都针对前一轮模型的误差进行修正，逐步提升整体预测能力。假设是3颗树。  

![](images/9c8e55058e357fcc10a6b06ff882163e22adfedb4021602e0189703ea33b1f9a.jpg)  
Tree O: Boosting Step  

模型的“起点”，试着捕捉“幸存VS未幸存”的基本规律。最明显的分裂是Sex，Pclass（舱位），Age模型发现“女性、高舱位乘客 $\rightarrow$ 幸存几率更高  

# 梯度提升-第2颗树  

Tree 1:Boosting Step 2  

![](images/60fbc569221cfad6367dc88b44d100bfa56f092e67347afb5e7eb4e1deab6d73.jpg)  

这棵树不再预测标签本身，而是预测第一棵树的错误（残差）。如果第一棵树低估了某些女性乘客的生存概率，这棵树会往上“拉”；如果高估了某些男性乘客的生存概率，这棵树会往下“压”。·每个叶子的输出值就是当前节点对前一轮误差的修正量。  

# 梯度提升-第3颗树  

Tree 2: Boosting Step 3  

![](images/e7e75eb7bf458af24484bc1f2473679458e1354dd2ffcaa3884406354cdd4b84.jpg)  

0 t0-   
80-  

![](images/c86a33d477feba5a913cde867bc841b57443ba89157bcbaa7af06212ed598288.jpg)  

# XGBoost代码调用  

# 以泰坦尼克数据集的分类问题为例。  

importpandas aspd from xgboost import xGBClassifier from sklearn.model_selection import train_test_split from sklearn.metricsimportaccuracy_score  

data =pd.read_csv("./data/train.csv")  

选择特征列   
features=['Pclass''Sex''Age’'Sibsp，‘Parch’'Fare’'Embarked’]   
$x=$ data[features]   
y=data['Survived\`]  

对Sex和 Embarked进行独热编码X=pd.get_dummiesX,columns=[Sex,'Embarked])  

划分训练集和测试集（8：2）   
X_train,X_test,y_train,y_test=train_test_lit（x,y,test_size=.2,   
random_state=42)  

#创建并训练XGBoost模型（ model=xGBClassifier（ n_estimators=200, learning_rate=0.05, max_depth=5, objective='binary:logistic', eval_metric='logloss', use_label_encoder=False, random_state=42  

#树的数量  
#学习率  
#树的最大深度  
#二分类任务  
#二分类常用评估指标  
#禁用旧版标签编码器  
#随机种子  

#模型训练 model.fit(x_train,y_train)  

#在测试集上预测 y_pred $\underline{{\underline{{\mathbf{\Pi}}}}}$ model.predict(x_test)  

#输出准确率 acc $\underline{{\underline{{\mathbf{\Pi}}}}}$ accuracy_score(y_test,y_pred) print（f"测试集准确率：{acc:4f))  

# XGBoost参数说明  

参数名 含义 说明越多模型越复杂，训练时间更长；  
n_estimators 弱学习器（树）的数量 一般100\~500较常见。控制每棵树的权重缩减，数值越小  
learning_rate 学习率 越稳健（常设0.01\~0.1）。  
max_depth 树的最大深度 控制模型复杂度，过大会导致过拟  
objective 目标函数 from xgboost import xgbclassifier“ogloss”是二分类常用指标， 分类问题，使用这一组参数。  
eval_metric 评估指标 其他可选如”auc、error。False表示关闭旧版标签编码  
use_label_encoder 标签编码控制 器，需要自行处理y。固定随机性，保证实验结果可重  
random_state 随机种子 复。  
分类任务常用评估指标（eval_metric）：·logloss：二分类、多分类常用；默认指标。error：简单直观，适用于初步监控。  
$\cdot$ auc：二分类模型表现评价的重要指标。  
$\cdot$ merror：适用于多分类任务。mlogloss：适用于多分类任务；与概率预测相关。  

# XGBoost代码调用  

# 假设需要预测泰坦尼克上的乘客年龄 （回归问题）  

importpandas aspd   
importnumpyasnp   
from xgboost import XGBRegressor   
from sklearn.model_selection import train_test_split   
from sklearn.metrics import mean_squared_error,   
mean_absolute_error,r2_score  

data =pd.read_csv("./data/train.csv")  

data = data.dropna(subset=['Age'])  

features =[’Pclass’‘Sex’‘Sibsp’Parch，Fare’‘Embarked’] X=data[features] y=data['Age’]#目标变量：年龄（连续值）  

#对Sex和 Embarked 进行独热编码 X=pd.get_dummies（X,columns=[Sex'Embarked’)  

#划分训练集和测试集（8:2）   
Xtran,st,rain_tst=raistlitx,y,ts_siz. random_state=42)   
#创建并训练XGBooSt回归模型   
model =XGBRegressor( n_estimators=200, #树的数量 learning_rate=0.o5, #学习率 max_depth=5, #树的最大深度 objective='reg：squarederror,#回归任 eval_metric='rmse', random_state=42  

#回归任务目标函数 #回归常用评估指标 model.fit（x_train,y_train) y_pred $=$ model.predict(x_test)  

rmse $=$ np.sqrt(mean_squared_error(y_test,y_pred)) mae = mean_absolute_error(y_test,y_pred) r2=r2_score(y_test,y_pred)  

print（f"测试集RMSE:{rmse:4f}") print（f"测试集MAE:{mae:.4fy") print（f"测试集R2:{r2:.4f)")  

# XGBoost参数说明  

参数名 含义 说明越多模型越复杂，训练时间更长；一般  
n_estimators 弱学习器（树）的数量 100\~500较常见。控制每棵树的权重缩减，数值越小越稳  
learning_rate 学习率 健（常设0.01\~0.1）。  
max_depth 树的最大深度 控制模型复杂度，过大会导致过拟合。  
objective 目标函数 测归备使用reg:quarederor 预 from xgboost import xgbregressor回归问题，使用这一组参数。  
eval_metric 评估指标 rmse、‘mae'常用于回归。  
random_state 随机种子 固定随机性，保证实验结果可重复。eval_metric  
用于训练过程中的模型表现监控，和最终评估指标（模型验证阶段）尽量一致。  
回归问题常用的评估指标（eval_metric）：rmse：均方根误差（RootMean Squared Error）mae：平均绝对误差（MeanAbsoluteError）  
$\cdot$ rmsle：对数误差（适合跨度大的目标）  

# XGBoost的易用性提升  

功能强大且易用，这是xGBoost获得巨大影响力的关键。  

·自动处理缺失值  
·无需特征标准化或归一化  
·支持sklearn接口（fit、predict、score、GridSearchcV等通用接口）  
·内置特征重要性分析（model.feature_importances_或plot_importance(））  
·原生支持类别型特征自动早停（early stopping）机制  

![](images/a661ae4f4a87dd685f14cceea22fe88a838114ad0190972c62ad43b07d6034bd.jpg)  
《战争之王》数据科学界的AK47  

# 易用性提升：内置特征重要性分析  

除了常规的画图，也提供简化的方式  

#计算特征重要性并排序   
feature_importance $=$   
pd.Series(model.feature_importances_,   
index=X.columns).sort_values(ascending=True)   
#画条形图   
feature_importance.plot（kind='barh'figsize=(8,4))   
plt.title（“特征重要性（FeatureImportance))   
plt.ylabel("重要性分数")   
plt.xlabel("特征")   
plt.tight_layout()   
plt.show()   
from xgboost importXGBclassifier,plot_importance   
importmatplotlib.pyplot asplt   
plot_importance(model,importance_type='gain)   
plt.grid(False)   
plt.show()  

![](images/1809754d1342a34ec2609f6d899ba0fcb838534b336fd587698ce3bdb858a4b4.jpg)  

importance_type:weight：特征在所有树中被使用的次数（默认）gain：该特征在分裂中带来的平均增益。cover：特征在分裂中涉及的样本平均覆盖数。  

![](images/928f8237288e72a41a0b662949d70c89ae852bfa1e4f2e5e9c3b1c232ead9714.jpg)  

易用性提升：支持类别型特征model =XGBClassifier(enable_categorical=True #启用类别型特征支持 model=XGBClassifier( datal'Embarked’] = datal'Embarked’].astype(category 分变为cataryc(不是映财成数学）  

减供理生，划维度爆One速度更快列，不会人为  

![](images/2a30ee18d2c07a14e20b54e494ced428a671d98f4db9a46e34b0f7549f5c18fc.jpg)  

·XGBoost的备选基学习器 第三部分XGBoost进阶 用XGBoost发现系外行星 XGBoost超参数 XGBoost揭秘 第二部分XGBoost 从梯度提升到XGBoost 随机森林与装袋法 深入浅出决策树 机器学习概览 第一部分装袋和提升  

CoreyWade 《梯度提升算法实战（基于XGBoost和scikit-learn） 图书推荐 今天一共刷了126道题，性 model.best_iteration 连续10道题还没学到新知识就提前收工 early_stopping_rounds=10 最多刷200道题 n_estimators 性价比最佳  

![](images/0f78fca17dc401bc28e496d27b260bbbbf16a53c5dad6130236c4d19d1cc7c58.jpg)  

# 供应链场景的出货量预测  

在供应链场景中，出货及销售预测无疑是利用数据转换为信息的非常重要的手段，预测的准确与否直接关系到企业的供应链、销售链和库存管理。在这个场景中，我们会基于XGBoost来预测。  

# 如图：  

企业发货到区域属于一级销售，这是产品出货部分；  
各区域将产品卖给消费者属于二级销售，这是产品销售部分。  

![](images/810072db4fbd291e97177ebd32c4c45bb8869ea64925f41b5a8bb70b53546c80.jpg)  

本课题主要是对产品出货部分进行预测  

![](images/fa25e3bf775f76382513eb1bfe9aa0b360cf71e0b8f63acc2b7251eaf7559de1.jpg)  

# 数据表说明  

![](images/f5a39ea394b0ec4cfaf7466d2e65d96369c6f7d0eb54363756feb610dad1bcd1.jpg)  
ShipmentData出货数据  

产品的历史出货信息（一级销售）2014-01-01到2017-11-30频率：到天  

SalesData 销售数据  


<html><body><table><tr><td>Column</td><td>Description</td></tr><tr><td>Region</td><td>区域</td></tr><tr><td>ItemCode</td><td>产品编码</td></tr><tr><td>SalesQty</td><td>销售日期</td></tr><tr><td>SalesDate</td><td></td></tr></table></body></html>  

产品的历史销售信息（二级销售）2014-01-01到2017-11-30频率：到天  

# 量化问题  

目标是：预测未来1个月每个产品到每个区域的出货量。  

$$
{\mathrm{FA}}=1-{\frac{\sum_{1}^{n}a b s(F c s t-A c t)}{\sum_{1}^{n}A c t}}
$$  

其中Fcst为预测值，Act为真实值。  
希望达到的FA是70%或以上。  

# 整体的流程与思路  

在这个案例里，拿到的数据是完整干净的。这样只要关注数据的准备，特征，模型，评估优化即可。  

数据准备： ·模型选择与参数设置·数据聚合（从天到月） ·时间序列·数据关联（出货表、销售表) ·特征选择描述性分析： ·常用的回归模型·了解数据的趋势与分布 ·评估与优化特征工程： ·FA结果，调参优化·份额占比 ·沟通汇报滞后系数 ·整体的思路，行动建议等  

# 数据准备：数据聚合  

原始数据的粒度是天，先新增yearMonth字段，再通过聚合的方式，调整数据粒度。  

# ShipmentData  

按Region，ItemCode，BrandCode，Package，yearMonth聚合ShipQty·SalesData  

按Region，ItemCode，yearMonth聚合SalesQty  

![](images/196836cb678c0ca213a420dc3b7cf834b8fc963944ec3b54ecce74bfa81d33c0.jpg)  

# 数据准备：数据关联  

聚合后的出货、销售表按：yearMonth，Region，ItemCode来关联。  
需要注意是Join的方向，这儿选择以ShipmentData为主表，leftjoin的方式。  

<html><body><table><tr><td>yearMonth String</td><td>Region String</td><td>ItemCode String</td><td>BrandCode String</td><td>Package String</td><td>ShipQty Number(Float)</td><td>SalesQty Number(Float)</td></tr><tr><td>2014-01</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>4,340.675</td><td>14,092.434</td></tr><tr><td>2014-02</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>4,580.527</td><td>19,698.485</td></tr><tr><td>2014-03</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>2,007.392</td><td>2,771.151</td></tr><tr><td>2014-04</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>1,651.48</td><td>3,096.133</td></tr><tr><td>2014-05</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>6,113.119</td><td>26,282.811</td></tr><tr><td>2014-06</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>896.073</td><td>2,914.21</td></tr><tr><td>2014-07</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>2,039.29</td><td>2,437.581</td></tr><tr><td>2014-08</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>3,485.649</td><td>1,089.573</td></tr><tr><td>2014-09</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>3,934.424</td><td>3,672.253</td></tr><tr><td>2014-10</td><td>East</td><td>2111256114</td><td>33</td><td>pack2</td><td>1,193.252</td><td>6,452.03</td></tr></table></body></html>  

# 描述性分析  

在这个环节，可以围绕数据本身，分析的关注点，做一些常见的趋势、占比、分布的可视化呈现。目的是直观的了解数据的特点，为下一步的特征工程，算法的选择做好准备。  

![](images/434a0f651d1d88eebdabb19e2b9d4b81c42675a254df0c9de851f35b78d33e82.jpg)  
到月的出货情况   
到月、到区域的出货情况  

![](images/fb5b20f96c14794a7b032c67b49be53036146ecfa7262e23147d34a903b55eec.jpg)  
出货量与销量的关系  
各个Brandcode的出货情况  

![](images/53f80e2fdfabaf8f8a3afd99736586e919bc9ac5fb64717f63aa9872cc0f3db2.jpg)  

![](images/39998843012f178d7b118172cba997c4db3e6acd6c948b981c6ffc3b3c0b4221.jpg)  

# 特征工程：份额占比  

·计算每个itemCode的ShipQty占所在月、Region的占比。  
·不同区域、不同月份的总体发货量规模可能差别很大。直接使用“发货量”会让模型被这些绝对数值主导。转成占比后，就相当于在局部（区域和月份）范围内做了归一化，让模型更关注相对表现而不是总量。  

<html><body><table><tr><td colspan="6"></td><td colspan="2">SalesQty Month</td><td>ItemShare</td></tr><tr><td>yearMonth String</td><td>Region String</td><td>ItemCode String</td><td>BrandCode Package String String</td><td>ShipQty Number(Float)</td><td>Number(Float)</td><td>String</td><td>Number (Float)</td></tr><tr><td>2014-01</td><td>East</td><td>2111256114</td><td>33 pack2</td><td>4,340.675</td><td>14,092.434</td><td>01</td><td>0.132</td></tr><tr><td>2014-02</td><td>East</td><td>2111256114</td><td>33 pack2</td><td>4,580.527</td><td>19,698.485</td><td>02</td><td>0.183</td></tr><tr><td>2014-03</td><td>East</td><td>2111256114</td><td>33 pack2</td><td>2,007.392</td><td>2,771.151</td><td>03</td><td>0.083</td></tr><tr><td>2014-04</td><td>East</td><td>2111256114</td><td>33 pack2</td><td>1,651.48</td><td>3,096.133</td><td>04</td><td>0.058</td></tr><tr><td>2014-05</td><td>East</td><td>2111256114</td><td>pack2 33</td><td>6,113.119</td><td>26,282.811</td><td>05</td><td>0.207</td></tr><tr><td>2014-06</td><td>East</td><td>2111256114</td><td>pack2 33</td><td>896.073</td><td>2,914.21</td><td>06</td><td>0.041</td></tr><tr><td>2014-07</td><td>East</td><td>2111256114</td><td>33 pack2</td><td>2,039.29</td><td>2,437.581</td><td>07</td><td>0.072</td></tr><tr><td>2014-08</td><td>East</td><td>2111256114</td><td>33 pack2</td><td>3,485.649</td><td>1,089.573</td><td>08</td><td>0.127</td></tr><tr><td>2014-09</td><td>East</td><td>2111256114</td><td>33 pack2</td><td>3,934.424</td><td>3,672.253</td><td>60</td><td>0.196</td></tr></table></body></html>  

# 特征工程：滞后变量  

某些经济变量不仅受到同期各种因素的影响，而且也受到过去某些时期的各种因素甚至自身的过去值的影响。通常把这种过去时期的，具有滞后作用的变量叫做滞后变量。  

某产品本月发了多少货，可能与该产品上个月，或者前几个月的销量或者出货有关系，那么这个时候，我们就可以把销量的滞后期或者出货的滞后期加入到模型中。  

![](images/7d346847d25ac66b71313836400edf8dca3832729e7faddcc225f37caeac70ad.jpg)  

# 特征工程：滞后变量  

滞后变量的计算是简单的，引用上个月，上上个月的对应数值。这儿引用的月份的数量，称为滞后期（1个月、2个月.）。  

![](images/fc42bfd0394f33cd76849c583af2403b2840daf5d2031465ff622decb5b7b39b.jpg)  

# 特征工程：滞后变量  

对ShipQty、SalesQty，ItemShare分别计算滞后变量。以及，我们还希望知道这些滞后变量和要预测的ShipQty的相关性，这样方便做后边的特征选择。  

<html><body><table><tr><td>ShipQty(-1) Number(Float)</td><td>ShipQty(-2)</td><td>ShipQty(-3) Number (Float)</td><td>ShipQty(-4) Number(Float)</td><td>SalesQty(-1) Number(Float)</td><td>SalesQty(-2) Number (Float)</td><td>SalesQty(-3) Number(Float)</td><td>ItemShare(-1) Number(Float)</td></tr><tr><td>1,651.48</td><td>Number (Float) 2,007.392</td><td>4,580.527</td><td>4,340.675</td><td>3,096.133</td><td>2,771.151</td><td>19,698.485</td><td>0.058</td></tr><tr><td>6,713.719</td><td>1,651.48</td><td>2,007.392</td><td>4,580.527</td><td>26,282.811</td><td>3,096.133</td><td>2,771.151</td><td>0.207</td></tr><tr><td>896.073</td><td>6,113.119</td><td>1,651.48</td><td>2,007.392</td><td>2,914.21</td><td>26,282.811</td><td>3,096.133</td><td>0.041</td></tr><tr><td>2,039.29</td><td>896.073</td><td>6,113.119</td><td>1,651.48</td><td>2,437.581</td><td>2,914.21</td><td>26,282.811</td><td>0.072</td></tr><tr><td>3,485.649</td><td>2,039.29</td><td>896.073</td><td>6,113.119</td><td>1,089.573</td><td>2,437.581</td><td>2,914.21</td><td>0.127</td></tr><tr><td>3,934.424</td><td>3,485.649</td><td>2,039.29</td><td>896.073</td><td>3,672.253</td><td>1,089.573</td><td>2,437.581</td><td>0.196</td></tr><tr><td>1,193.252</td><td>3,934.424</td><td>3,485.649</td><td>2,039.29</td><td>6,452.03</td><td>3,672.253</td><td>1,089.573</td><td>0.078</td></tr><tr><td>1,030.921</td><td>1,193.252</td><td>3,934.424</td><td>3,485.649</td><td>1,346.271</td><td>6,452.03</td><td>3,672.253</td><td>0.101</td></tr></table></body></html>  

# 特征工程：相关系数计算  

相关系数是用以反映变量之间线性相关程度的统计量。常用的有皮尔逊相关系数。  
取值范围是-1到 $+1.$ 。相关性高的滞后期，优先作为特征选择。  

![](images/92466b0e212c7165c5cfc123d210f8eff070392c63278a173b5f9bfd3e3f1f5e.jpg)  

前1个月的SalesQty和当前月的ShipQty相关性高  

# 特征工程：滞后变量  

对ShipQty、SalesQty，ItemShare分别计算滞后变量。以及，我们还希望知道这些滞后变量和要预测的ShipQty的相关性，这样方便做后边的特征选择。  

<html><body><table><tr><td>ShipQty(-1) Number (Float)</td><td>ShipQty(-2) Number (Float)</td><td>ShipQty(-3) Number (Float)</td><td>ShipQty(-4) Number (Float)</td><td>SalesQty(-1) Number (Floet)</td><td>SalesQty(-2) Number (Float)</td><td>SalesQty(-3) Number (Float)</td><td>ItemShare(-1) Number (Float)</td></tr><tr><td>1,651.48</td><td>2,007.392</td><td>4,580.527</td><td>4,340.675</td><td>3,096.133</td><td>2,771.151</td><td>19,698.485</td><td>0.058</td></tr><tr><td>6,713.719</td><td>1,651.48</td><td>2,007.392</td><td>4,580.527</td><td>26,282.811</td><td>3,096.133</td><td>2,771.151</td><td>0.207</td></tr><tr><td>896.073</td><td>6,113.119</td><td>1,651.48</td><td>2,007.392</td><td>2,914.21</td><td>26,282.811</td><td>3,096.133</td><td>0.041</td></tr><tr><td>2,039.29</td><td>896.073</td><td>6,113.119</td><td>1,651.48</td><td>2,437.581</td><td>2,914.21</td><td>26,282.811</td><td>0.072</td></tr><tr><td>3,485.649</td><td>2,039.29</td><td>896.073</td><td>6,113.119</td><td>1,089.573</td><td>2,437.581</td><td>2,914.21</td><td>0.127</td></tr><tr><td>3,934.424</td><td>3,485.649</td><td>2,039.29</td><td>896.073</td><td>3,672.253</td><td>1,089.573</td><td>2,437.581</td><td>0.196</td></tr><tr><td>1,193.252</td><td>3,934.424</td><td>3,485.649</td><td>2,039.29</td><td>6,452.03</td><td>3,672.253</td><td>1,089.573</td><td>0.078</td></tr><tr><td>1,030.921</td><td>1,193.252</td><td>3,934.424</td><td>3,485.649</td><td>1,346.271</td><td>6,452.03</td><td>3,672.253</td><td>0.101</td></tr></table></body></html>  

# 特征工程：相关系数计算  

相关系数是用以反映变量之间线性相关程度的统计量。常用的有皮尔逊相关系数。  
取值范围是-1到+1。相关性高的滞后期，优先作为特征选择。  

![](images/9d24deb6120b27dd9b68f38f8a34319ab5ae035bba8753ca0fa7e5ec65fed137.jpg)  

# 模型选择与参数设置  

在应用更为强大的梯度提升树的XGBoost前，可以先用时间序列算法来做预测。除了快速的看到一些结果外，也可以作为基线的模型（即新的模型应该好于时间序列预测）。  

时间序列：应用Arima算法  

# 模型选择与参数设置：时间序列  

importpandas aspd   
importnumpy asnp   
from statsmodels.tsa.statespace.sarimax import SARIMAX   
$\#$ 用前n-1个月做训练，最后1个月做测试   
train $=$ series.iloc[:-1]   
test $=$ series.iloc[-1:]  

Region FA   
West 0.797233   
North 0.727075   
South 0.630141   
Inner 0.593019   
East 0.544776  

整体SARIMA预测表现：FA（预测准确率）：0.6539#拟合模型result $=$ model.fit(disp=False)  

# 特征选择  

哪些字段可以作为备选的特征？如何避免信息泄露？  

哪些滞后变量作为特征，可以参考前面的相关系数计算。  

<html><body><table><tr><td>Name Type Region</td><td rowspan="7"></td><td>Name</td><td>Type</td></tr><tr><td>yearMonth string</td><td>ItemShare</td><td>Number (Float)</td></tr><tr><td>string</td><td>ShipQty(-1)</td><td>Number (Float)</td></tr><tr><td>String ItemCode</td><td>ShipQty(-2)</td><td>Number (Float)</td></tr><tr><td>String BrandCode</td><td>ShipQty(-3)</td><td>Number (Float)</td></tr><tr><td>Package String shipQty</td><td>ShipQty(-4)</td><td>Number (Float)</td></tr><tr><td>Number (Float) Number (Float)</td><td>SalesQty(-1)</td><td>Number (Float)</td></tr><tr><td>SalesQty</td><td></td><td>SalesQty(-2)</td><td>Number (Float)</td></tr><tr><td>Month</td><td>String</td><td>SalesQty(-3)</td><td>Number (Float)</td></tr><tr><td></td><td></td><td>ItemShare(-1)</td><td>Number (Float)</td></tr></table></body></html>  

![](images/c8831206b29c11f19412b2c7b0f07afe970b95c4366c51f0814f953f6004f8a6.jpg)  

# 模型的选择  

在应用了时间序列算法后，基于这儿的任务类型，尝试和选择合适的模型。  

![](images/6de1867568acd3b2b8b56ddbdbd0a879d9fb9786e74fadad2cd34261d7251bbf.jpg)  

# 模型的选择：随机森林与XGBoost  

随机森林： “高偏差、低方差”，稳健不过拟合。  
XGBoost: “低偏差、高方差”，精度高但更需调参控制。  

![](images/e23bb9185ec8fde8ff0c58d6fb707a604020d690ebd77dc4b075beb8171b0c51.jpg)  

![](images/e9643ac3cd3f3c73c4a8f2351cf0eb34555be13cda6c402b47c7760145d4bd3f.jpg)  

# 应用随机森林进行预测  

importpandas aspd   
importnumpy asnp   
from sklearn.ensembleimport RandomForestRegressor   
$\#==========$ 分类特征处理（使用One-Hot编码）   
cat_cols $=$ ["Region","ItemCode","Package"]   
df $=$ pd.get_dummies(df,columns=cat_cols,drop_first=True)  

$\#==========$ 训练集/测试集划分 $===========$ df $=$ df.sort_values("yearMonth").reset_index(drop=True) last_month $=$ df["yearMonth"].max() train_df $=$ df[df["yearMonth"] $<$ last_month] test_df $\leq$ df[df["yearMonth"] $=$ last_month] $\#$ 特征选择·  

model $=$ RandomForestRegres n_estimators=200, max_depth $=5$ min_samples_split=4, min_samples_leaf=2, random_state=42, n_jobs=-1  

model.fit(X_train,y_train) pred $=$ model.predict(x_test)  

整体预测表现：FA（预测准确率）：0.7944  

![](images/4aab3c6279eca58839b5450f941af60fbbe4165200c7f331dbd1a45ad2348da3.jpg)  

# 应用XGBoost进行预测  

importpandasaspd   
import numpy asnp   
from xgboost import XGBRegressor   
#不做One-hot编码，让XGBoost原生处理分类特征   
cat_cols=["Region","ItemCode","Package”]   
for cin cat_cols: df[c] $\leq$ df[c].astype("category")  

训练集/测试集划分 df= df.sort_values("yearMonth").reset_index(drop=True) last_month = df("yearMonth").max() train_df=df[df("yearMonth"]<last_month] test_df=df[df("yearMonth"]== last_month] #特征选择 model =XGBRegressor( random_state=42, tree_method="hist", enable_categorical=True, early_stopping_rounds=100, \*\*best_params model.fit(X_train,y_train,eval_set=[(x_test,y_test)], verbose=False) #预测 pred_best=model.predict(x_test)  

整体预测表现：FA（预测准确率）：0.8201  

![](images/09171cceb7d6d5b056ebbae3304c7c5d225d9474ffb416a64a505752fdee648a.jpg)  

# XGBoost调参与优化  

#定义XGBoost的参数搜索空间，用于网格搜索（GridSearchCV）  
param_grid $=$ #树的最大深度，控制模型复杂度。越大越容易过拟合。"max_depth":[3,4,5],#学习率（步长）  
#控制每次迭代的更新幅度。越小越稳健，但需要更多迭代。"learning_rate":[0.01,0.02,0.05],  

#子样本比例（用于训练每棵树），防止过拟合。"subsample":[0.7,0.9],  

#每棵树随机选取特征的比例，防止特征间的相关性导致过拟合。 "colsample_bytree":[0.7,0.9],  

#L1正则化系数（类似LasSo），控制特征选择与稀疏性。"reg_alpha":[0,0.3,0.5],  

#L2正则化系数（类似Ridge），控制模型复杂度。"reg_lambda":[1,2],  

best_params $=$ 'max_depth':5, 'learning_rate':0.02, 'subsample':0.9, 'colsample_bytree':0.7, 'reg_alpha':0.5, 'reg_lambda':1, 'n_estimators':500  

搜索最佳参数，同时使用early_stopping_rounds机制。  

# 不同模型的表现  

整体来讲，使用回归模型的表现更好。不同模型与参数，也会有所差异。  

![](images/8c56cad1562b53a9c347c33a2234f9a2773de5fde7b0ca65b55339fc19bf191a.jpg)  

# XGBoost的特点  

结合到本案例的模型的选择、参数优化，与最终的结果。XGBoost整体来讲，更为方便易用，同时性能表现也很明显  

${}>>{}$ 自动处理缺失值，内置特征重要性分析，支持类别型特征，自动早停机制。  

![](images/ed64fb4609e9f6236a53554aa70611d5993e7ca2cf6e53d7ab10c03138dafc1c.jpg)  

能力好，易用性好。  

![](images/6438425c303a03755b1d428446c6a4f810a8825e5bf592e4c3b9e0828965eea7.jpg)  

参数细节多，需要更多了解原理。  
精度高，但也要防止过拟合。  

![](images/eed7fba7068c4ec6344a883621db7537e7e136afbc0297fcee92d3fbae052ad2.jpg)  

# 进一步的优化  

商业分析、机器学习是一个不断送代的过程。  

尝试不同的模型  
引入新的特征：过去3期的滚动平均、环比增长率等  
特征的选择（基于经验的人工选择，包裹法，嵌入法）  
观察细分表现（不同Region，ItemCode的性能表现）  
不同的训练方式（整体，按Region或ltemCode单独训练）  
回到预测的起点，是否可以补充更多的参考数据（天气、商品信息），  
FA性能指标是否合适？  

# 沟通汇报  

总结需求与关注点，数据探索，模型选择与优化，最终的结果。以及，更重要的洞察发现与行动建议。  

# 比如：  

各区域的份额占比，潜力与发展空间。围绕不同区域、商品的市场策略。预测的出货量与KPI的差距（是否有可能达标）  

# 算法的选择  

从简单到复杂，注重可解释性，结合数据特点与目标，多算法的比较与调优。  

![](images/ac53b1dd882aef59ff1464bebb36fe98b2732f40fa08af8d77fd02389e67d3df.jpg)  

# 算法的选择  

可以通过多个算法的投票（Voting投票集成是一种常用集成学习方法）来得到一个更稳定、更准确的最终预测。优点是容易实现，提升稳定性，缓解过拟合。  

from sklearn.linear_model import LinearRegression from sklearn.ensemble import RandomForestRegressor, GradientBoostingRegressor,VotingRegressor  

#构建投票回归器   
voting_reg $\equiv$ VotingRegressor( estimators=[ ("Ir',LinearRegression(), ('rf', RandomForestRegressor(n_estimators=100,   
random_state $=42$ ('gb'GradientBoostingRegressor(random_state $=42$  

from sklearn.linear_model import LogisticRegression from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier,VotingClassifier  

$\#$ 构建投票分类器  
voting_clf $\v{U}=\v{U}$ VotingClassifier(estimators=[('lr',LogisticRegression(max_iter=10oo)),('rf',RandomForestClassifier(n_estimators=100,random_state=42)),('gb' GradientBoostingClassifier(random_state=42))],voting='soft'#可选hard （一人一票）或soft （概率分布）  

voting_clf.fit（x_train,y_train) y_pred $=$ voting_clf.predict（x_test)  

# 模型调优与评估深入  

机器学习的项目实践是一个不断迭代与优化的过程。为此，需要关注算法的选择，特征与参数的选择与运行结果的评估。  

算法的选择  

性能指标的选择  

交叉验证的方法  

特征的选择  

参数调优：GridSearch、RandomSearch  

提升模型的泛化能力  

# 算法的选择  

围绕不同的场景与问题，选择合适的算法。围绕回归、分类、聚类、异常检测都有不同的代表性的算法。如何选择，可以从这几个方面考虑。  

算法是否易于理解  
算法参数与结果的可解释性  
算法的能力与稳健性  
算法的性能、扩展性、主流程度  

# 性能指标的选择  

在机器学习中，性能指标（PerformanceMetrics）是用来衡量模型好坏的定量标准，也就是「模型到底表现得好不好？」。根据任务类型选择指标，并考虑场景。  

<html><body><table><tr><td>任务类型</td><td>指标</td><td>含义</td><td>适用场景</td></tr><tr><td rowspan="4">分类</td><td>accuracy</td><td>整体正确率</td><td>类别平衡时使用</td></tr><tr><td>precision</td><td>预测为正中有多少是真的</td><td>虚警代价大时</td></tr><tr><td>recall</td><td>真实为正的被预测对的比例</td><td>漏判代价大时</td></tr><tr><td>Fl-score</td><td>精确率与召回率的平衡</td><td>样本不平衡时</td></tr><tr><td rowspan="5">回归 聚类</td><td>MAE</td><td>平均绝对误差</td><td>稳健，不受离群点影响</td></tr><tr><td>MSE/RMSE</td><td>平方误差/均方根误差</td><td>惩罚大误差更重</td></tr><tr><td>R2</td><td>拟合优度（越接近1越好）</td><td>评估整体拟合效果</td></tr><tr><td>MAPE</td><td>平均百分比误差</td><td>关注相对误差比例</td></tr><tr><td>Silhouette（轮廓系数）</td><td>聚类紧密度与分离度</td><td>无监督聚类，评估聚类效果</td></tr></table></body></html>  

# 交叉验证的方法  

常用的有K折法，用于评估模型的稳定性和泛化能力。  

![](images/8b5074c712a4e7cd331137de54c817bc97ae727e94c285d10d58d7993d848154.jpg)  

数据集切成K份，轮流把其中一份作为测试集，剩下的作为训练集。  

from sklearn.model_selection import KFold   
from sklearn.metrics import accuracy_score   
fromsklearn.ensembleimportRandomForestClassifier   
import numpy as np   
#shuffle=True划分数据前，先随机打乱   
$k\mathsf{f}=\mathsf{K F o l d}$ (n_splits $=5$ ,shuffle=True,random_state=42)   
scores $=[]$   
for train_idx,test_idx in kf.split(x): Xtrain,X_test $=$ X[train_idx],x[test_idx] y_train,y_test $=$ y[train_idx],y[test_idx] model $=$ RandomForestClassifier(random_state=42) model.fit(x_train, y_train) y_pred $=$ model.predict（x_test) scores.append(accuracy_score(y_test,y_pred))   
print（"平均准确率：np.mean（scores））  

# 交叉验证的方法  

可以使用cross_val_score简化代码封装。  

from sklearn.model_selection import cross_val_score fromsklearn.ensembleimportRandomForestClassifier  

model $\mathbf{\mu}=$ RandomForestClassifier(random_state=42) scores $\leq$ cross_val_score(model,x,y,cv=5,scoring='accuracy)  

print（“每折准确率：scores）print（"平均准确率：”scores.mean()）  

cv=5指定折几份，默认就是KFold。  

from sklearn.model_selection import cross_val_score,KFold fromsklearn.ensembleimportRandomForestClassifier  

$k+=$ KFold(n_splits=5,shuffle=True,random_state=42) model $=$ RandomForestClassifier(random_state $=42$  

scores $=$ cross_val_score（model,X,y,cv=kf,scoring='accuracy)print（"平均准确率:scores.mean(）  

# CV $=$ 指定的交叉验证对象，方便参数细节的指定  

拆分器  
KFold  
StratifiedKFold  
RepeatedKFold  
ShuffleSplit  
说明  
普通K折交叉验证  
分层K折交叉验证（保持类别比例一致）在KFold的基础上多次重复交又验证随机多次划分训练/测试集  

# 交叉验证的方法  

时间序列的特点是：“未来不能用于预测过去。  
需要按时间的先后顺序扩展训练集。  

from sklearn.model_selection import TimeSeriesSplit importnumpy asnp  

$x=$ np.arange(10) tscv $=$ TimeSeriesSplit(n_splits $=3$ ,test_size $=2$ for fold,(train_idx, test_idx) in enumerate(tscv.split(x),1) print(f"Fold {fold}:") print("训练集索引l:",train_idx) print("测试集索引l:",test_idx)  

Fold 1:训练集索引1：[0123]测试集索引：[45]  
Fold 2:训练集索引1：[012345]测试集索引：[67]  
Fold 3:训练集索引1：[01234567]测试集索引：[89]  

![](images/8edea0c5a2ffc9dc9e7b50eb3f43b8efc0858e42817484073588a7cbae90db09.jpg)  

# 特征的选择  

# 以包裹法为例（把特征选择当作一个搜索问题）。前向选择：从空集开始，逐步加特征，保留提升性能的特征后向剔除：从全特征开始，逐步去掉无用的特征  

fromsklearn.feature_selectionimport SequentialFeatureSelector 前向选择（Forward Selectioh）   
sfs_forward=SequentialFeatureSelector( model, n_features_to_select=4, direction='forward', scoring='accuracy, CV=5   
sfs_forward.fit(x_train,y_train)   
print（"选择的特征："list（X.columns[sfs_forward.get_support(】)   
from sklearn.feature_selection import SequentialFeatureSelectar   
print(\*\n===后向特征剔除（Backward Elimination）==")   
sfs_backward =SequentialFeatureSelector( model, n_features_to_select=4, direction='backward', scoring='accuracy', CV=5   
sfs_backward.fit（x_train,y_train)   
print（"选择的特征：“,list（X.columns[sfs_backward.get _support0])）)  

# 特征的选择  

以包裹法为例 （把特征选择当作一个搜索问题）  

前向选择（SFS）：从空集开始，逐步加特征，保留提升性能的特征后向剔除（RFE）：从全特征开始，逐步去掉无用的特征  

from sklearn.feature_selection import SequentialFeatureSelector   
# 前向选择（Forward Selection）   
sfs_forward $=$ SequentialFeatureSelector( model, n_features_to_select=4, direction='forward', scoring='accuracy', CV=5   
sfs_forward.fit(X_train,y_train)   
print("选择的特征：",list（X.columns[sfs_forward.get_support()])）   
from sklearn.feature_selection import SequentialFeatureSelector   
#- 后向特征剔除（Backward Elimination）   
sfs_backward $=$ SequentialFeatureSelector( model, n_features_to_select=4, direction='backward', scoring='accuracy' CV=5   
sfs_backward.fit(x_train,y_train)   
print（"选择的特征："list（X.columns[sfs_backward.get_support(】)  

# 特征的选择  

从易用性角度，推荐RFECV（递归特征消除与交叉验证）。不需要手动指定n_features_to_select，它会自动找到“最优特征数量”  

from sklearn.feature_selection import RFECV  

rfecv $=$ RFECV（model,cv=5,scoring='accuracy') rfecv.fit(x_train,y_train)  

print（最优特征数量：”,rfecv.n_features_）print(“被选择的特征：",list（X.columns[rfecv.support_)）  

# 参数调优：GridSearch、RandomSearch  

参数调优（HyperparameterTuning）是机器学习中优化模型性能的重要步骤。  

网格搜索GridSearchcV通过穷举法，验证列表中的每一个参数。随机搜索RandomizedSearchcV从参数分布或列表中随机采样若干组合。  

# 参数调优：GridSearch、RandomSearch  

参数调优是机器学习中优化模型性能的重要步骤。  

from sklearn.model_selection import GridSearchcv from sklearn.ensemble import RandomForestClassifier from sklearn.model_selection import RandomizedSearchcv   
from sklearn.ensemble import RandomForestClassifier from scipy.stats import randint param_dist={   
param_grid=I 'n_estimators':randint（100,500),   
'n_estimators[100,200,300], 'max_depth':randint(5,20),   
'max_depth:[5,10,15], 'min_samples_split:randint(2,10)   
‘min_samples_split:[2,5] random_search $=$ RandomizedSearchcV(   
grid_search= GridSearchcV( estimator=RandomForestClassifier),   
estimator=RandomForestClassifier(), param_distributions=param_dist,   
param_grid=param_grid, n_iter=20,#采样20组参数   
scoring='accuracy, scoring='accuracy,   
CV=5 CV=5, random_state=42   
grid_search.fit(X_train,_train) random_search.fit（x_train,y_train)   
print（最佳参数：“grid_search.best_params_) print（最佳参数：“，random_search.best_params_)   
print("最佳得分："grid_search.best_score_) print("最佳得分：",random_search.best_score_)  

# 参数调优：GridSearch、RandomSearch  

可以先用RandomSearch粗调，找到合适区间。再用Grid Search精调在局部范围内搜索。  

<html><body><table><tr><td>特性</td><td>Grid Search</td><td>Random Search</td></tr><tr><td>搜索策略</td><td>穷举所有组合</td><td>随机采样部分组合</td></tr><tr><td>计算成本</td><td>高</td><td>较低</td></tr><tr><td>适合场景</td><td>参数空间较小</td><td>参数空间较大</td></tr><tr><td>全局最优性</td><td>能找到全局最优</td><td>近似全局最优</td></tr><tr><td>对连续变量支持</td><td>差</td><td>好</td></tr><tr><td>可重复性</td><td>固定</td><td>需设置随机种子</td></tr></table></body></html>  

# 提升模型的泛化能力  

泛化（Generalization）是机器学习和统计学中的一个重要概念，指的是让模型在未见过的新数据上也能表现良好，而不仅仅在训练数据上取得高准确率。换句话说，泛化能力是衡量一个模型是否“学到规律”而不是“记住例子”的关键指标。  

如果一个模型在训练集上表现很好，但在测试集或现实数据上表现明显变差，就说明它的泛化能力不足（通常是过拟合）。  

# 影响泛化能力的主要因素  

模型复杂度  
数据量与数据多样性特征选择与预处理  
模型训练策略  

# 拟合  

拟合（fitting）指的是对训练数据的学习程度。良好的拟合意味着模型能够准确捕捉数据的特征和模式。  

1.欠拟合（Underfitting）：模型过于简单，无法捕捉数据的真实规律  

2.良好拟合（GoodFit）：模型准确地捕捉了数据的特征，在训练集和测试集上都表现出色。  

3.过拟合（Overfitting）：模型过于复杂，学习到了训练数据中的噪声和细节，在训练集上表现很好，在测试集上表现不佳。  

![](images/b7786d6c4128ff327c4666a93a30b59eef64470635363c0c69916d8b25d040d4.jpg)  

# 防止过拟合：决策树  

以决策树为例，生成的决策树往往对训练数据有很好的分类能力。但对未知的测试数据却未必有很好的分类能力，可能发生过拟合现象。需要对已生成的树自下而上进行剪枝，将树变得更简单，从而使它具有更好的泛化能力。  

1输入：使用特征重要性筛选，减少余特征。  

# 2常用配置：  

参数名 含义 举例说明max_depth 树的最大深度（从根到叶的层数上限） 若设为3，则树最多分三层（根→叶）min_samples_split 节点分裂前所需的最小样本数 若节点样本 $<10$ ，则不会再分裂min_samples_leaf 叶节点中允许的最小样本数 若分裂后某个叶节点样本 $<5$ ，则该分裂被禁止max_leaf_nodes 树中允许的最大叶节点数 若设为8，则树最多有8个叶节点  

![](images/6040fb5412a15d57c3e9a79015965d9495422304cd45579ac0d63bea173ed0db.jpg)  
可能过拟合的决策树  

![](images/de53be051a4a8cbca524c6b6d1071c6c7bf331b2132a258029475e73285b2afa.jpg)  
良好拟合的决策树  

通过减少不需要的特征，指定每个节点的最小记录数，来控制模型的复杂性。  

# 拟合程度的：识别与评估方法  

除了K折交叉验证来评估模型在不同数据子集上是否稳定。  
也可以通过可视化的方式，比如学习曲线来观察评估。  

学习曲线：训练集与验证集误差随样本数变化的曲线  

过拟合（Overfitting）：训练集和验证集的误差差距大。  

![](images/0143bba01fee697f98ab658370c97982c067bfe5f0fb8a120589393dfbcb1f06.jpg)  

欠拟合（Underfitting）：两条误差曲线都较高且接近  

# 防止过拟合与改进欠拟合，哪一个更难  

# 3 2  

1.欠拟合（Underfitting）  
2.良好拟合（Good Fit）  
3.过拟合（Overfitting）  

# 难易程度对比  

# 过拟合与欠拟合的比较  

<html><body><table><tr><td>对比项</td><td>过拟合</td><td>欠拟合</td></tr><tr><td>检测难度</td><td>较难检测（训练集误差低但验证集误差高）</td><td>容易检测（训练集误差高）</td></tr><tr><td>原因</td><td>模型容量太大、训练过久、正则不足</td><td>模型容量太小、特征不足</td></tr><tr><td>解决手段</td><td>加正则化、用更少特征、提前停止</td><td>加模型复杂度、训练更久、增加特征</td></tr><tr><td>实战难度</td><td>困难：要平衡“泛化能力”和“训练精度</td><td>简单：多加点复杂度或特征即可</td></tr></table></body></html>  

# 通过正则化的方式，控制过拟合  

正则化（regularization）是一个在机器学习、统计学、信号处理等领域常见的概念，主要目的是防止模型过拟合（overfitting）。  

# 原始模型：  

优化目标=损失函数（预测误差）  

# 加上正则化：  

优化目标=损失函数+入×惩罚项  

入（lambda）是“约束力度”：·入大→模型更简单（防过拟合）·入小→模型更灵活（容易过拟合）  

# 通过正则化的方式，控制过拟合  

正则化（regularization）是一个在机器学习、统计学、信号处理等领域常见的概念，主要目的是防止模型过拟合（overfitting）。  

<html><body><table><tr><td>模型类型</td><td>正则化方式 简单理解</td></tr><tr><td>决策树</td><td>限制树深度、最小样本数 不让树太「细」</td></tr><tr><td>随机森林</td><td>多树平均、随机特征 减少单棵树的偏差</td></tr><tr><td>XGBoost 样、学习率</td><td>树复杂度惩罚（y、入、α）、样本/特征采 给“树的复杂度”收税，让模型更稳不乱学</td></tr></table></body></html>  

# 正则化的方法：决策树  

围绕单颗树的参数设置 from sklearn.tree import DecisionTreeClassifier tree_model =DecisionTreeClassifier( max_depth $=3$ #树最大深度 min_samples_split=10，#分裂前节点最少样本数 min_samples_leaf=5，#叶节点最少样本数 max_leaf_nodes=8, #最大叶节点数 random_state $=42$  

<html><body><table><tr><td>参数名</td><td>说明 含义</td><td></td></tr><tr><td>max_depth</td><td>树的最大深度（从根到叶的层数上限）</td><td>若设为3，则树最多分三层（根→叶）</td></tr><tr><td>min_samples_split</td><td>节点分裂前所需的最小样本数</td><td>若节点样本<10，则不会再分裂</td></tr><tr><td>min_samples_leaf</td><td>叶节点中允许的最小样本数</td><td>若分裂后某个叶节点样本<5，则该分裂被禁止</td></tr><tr><td>max_leaf_nodes</td><td>树中允许的最大叶节点数</td><td>若设为8，则树最多有8个叶节点</td></tr></table></body></html>  

# 正则化的方法：随机森林  

随机森林是多棵树的平均，天然具有Bagging降方差效果。但单棵树仍可能过拟合，因此参数依然关键。  

<html><body><table><tr><td>参数名</td><td>含义</td><td>说明</td><td></td></tr><tr><td>n_estimators</td><td>树的数量</td><td>越多越稳定，但计算成本增 加。建议100~500。</td><td rowspan="2">from sklearn.ensemble import RandomForestClassifier model =RandomForestClassifier(</td></tr><tr><td>max_depth</td><td>每棵树最大深度</td><td>与决策树同理，常为5~15。</td></tr><tr><td>max_features</td><td>每次划分考虑的特征数</td><td>建议分类任务用sqrt，回归 用log2。</td><td>n_estimators=300, #树的数量 max_depth=10, #最大深度，防止树太深 max_features='sqrt', #每次分裂使用部分特征 min_samples_split=10，#节点继续划分所需的最小样本数 min_samples_leaf=5,</td></tr><tr><td>min_samples_split</td><td>一个节点继续划分所需的最 小样本数</td><td>提高该值可减少分裂、降低 过拟合；如设为10或20。</td><td>#叶节点的最小样本数 bootstrap=True, #有放回采样，增加随机性 random_state=42 #固定随机种子，保证结果可复现</td></tr><tr><td>min_samples_leaf</td><td>叶节点的最小样本数</td><td>增大该值可让叶节点更稳 健；如设为5或10。</td><td></td></tr><tr><td>bootstrap</td><td>是否有放回采样</td><td>通常设为 True （默认）以保 证随机性。</td><td></td></tr></table></body></html>  

# 正则化的方法：XGBoost  

XGBoost的每一棵树都拟合前一棵树的残差，优点是拟合能力强，但过拟合风险更高，需要更强的正则化与控制。  

<html><body><table><tr><td>参款</td><td>含义</td><td>推辣范围/作用</td><td rowspan="6">from xgboost import XGBClassifier model =XGBClassifier( n_estimators=300, #树的数量，越多越容易过拟合 #每棵树的最大深度，控制模型复杂度 #学习率（步长），越小越稳但需要更多树 #训练样本采样比例，防止模型过拟合 colsample_bytree=0.8，#每棵树特征采样比例，增加随机性降低方差 #分裂惩罚项（最小损失减少量），越大越保守 early_stopping_rounds=50，#验证集性能多轮未提升时提前停止训练 eval_metric=logloss'#评估指标，可根据任务调整，如auc'、‘rmse</td></tr><tr><td>n_estimators</td><td>树的数量</td><td>太多会过拟合，一般100~500；配合 early_stopping控制。</td></tr><tr><td>max_depth</td><td>每棵树的最大深度</td><td>控制模型复杂度；推荐3~6。 max_depth=5,</td></tr><tr><td>learning_rate(或eta）</td><td>学习率（步长）</td><td>较小更稳（如0.05或0.1），但需更多树。 learning_rate=0.1, subsample=0.8,</td></tr><tr><td>subsample</td><td>样本采样比例</td><td>通常0.7~0.9；防止模型过于依赖训练集。 gamma=0.1,</td></tr><tr><td>colsample_bytree</td><td>每棵树特征采样比例</td><td>一般设0.7~0.9；引1入随机性降低方差。</td></tr><tr><td>gamma early_stopping_rounds</td><td>分裂惩罚项（最小损失减少量） 提前停止</td><td>增大可让模型更保守。 如果验证集性能不再提升，提前终止训练。</td></tr></table></body></html>  

# 小结  

模型调优与评估是给机器学习模型「打磨雕琢」的过程。从一开始的“形”，到通过不断尝试不同算法、挑选合适特征、调整参数，逐步能让它逐渐闪闪发光。  

在这个过程中，可以通过GridSearch、RandomSearch来找到最优的参数组合。同时，也需要通过交叉验证的方式，检验模型是否“经得起不同数据的考验”。最终，让模型不仅在训练集上表现优异，更能在真实世界中稳定发挥，实现真正的泛化能力。  

# 模型可解释性  

「知其然知其所以然」  

什么是模型可解释性？模型可解释性的分类。常用的方法与工具。  

# 什么是模型可解释性？  

在机器学习中，模型可解释性指的是我们理解和解释模型决策过程的能力，也就是能够回答这样的问题：“模型为什么会做出这样的预测？  

在信用评分模型中：模型为什么判定某人信用风险高？在物流延误模型中：模型为什么预测某批货物会延误？  

# 模型可解释性的重要性  

可解释高的模型，有助于提升信任、确保合规、优化性能并减少偏见。  

1.增强对于模型结果的信任  
2.提升业务的可控性  
3.带来新的洞察发现  
4.满足合规性的要求（金融行业更关注算法的可解释性）  

模型的可解释性与精确性此消彼长，需要综合考虑。  

# 模型可解释性的分类  

围绕模型的可解释性，可以有不同的划分方式  

自解释与基于结果的解释  

简单模型：（线性回归、决策树）生成的参数与规则容易理解。  
复杂模型：可以基于训练结果，通过输入输出观察（黑盒）。  

全局解释与局部解释：  

·全局：基于模型层面对自变量（)、因变量（y)的相关关系进行解释，包括特征重要性等。  
·局部：对单个样本解释模型如何预测，如：货物延误和天气以及距离有关。  

# 线性回归－可解释性  

线性回归是在分析市场现象自变量和因变量之间关系的基础上，建立变量之间的回归方程，并将回归方程作为预测模型。  

![](images/66661b1951a82ced1dd1ad99fa682b5da9923eb4024689815e693580bd74c345.jpg)  

因变量：收入自变量：学历、工龄  

员工收入 $=3808.69+290.18\times$ 学历编码 $+\,335.28\times=$ 广齿  
学历编码：  
·将学历按等级转换为数字高中=0，大专=1，本科=2，硕士=3，博士=4  

决策树是一种基于特征划分数据集的模型，它通过构建一个类似树的结构来决定不同特征如何影响预测结果。  

![](images/f0110e2c4fbbe1586be4faa45b5118dce7eb0385904d4cd46948c09349dbc1bc.jpg)  
决策树-可解释性  

# 聚类结果的解释  

各个群组的参数值的特性分布  

<html><body><table><tr><td>Cluster String</td><td>Size Number(integer)</td><td>No_Claims Number(double)</td><td>Mean(No... Number(double)</td><td>Age Number(double)</td><td>Mean(Age) Number (double)</td><td>Car_Price Number(double)</td><td>Mean(Car... Number(double)</td></tr><tr><td>cluster_o</td><td>1367</td><td>-1.559</td><td>-2.843</td><td>-0.123</td><td>30.677</td><td>-0.832</td><td>110,343.927</td></tr><tr><td>cluster_1</td><td>1748</td><td>-0.279</td><td>-0.479</td><td>-0.782</td><td>24.248</td><td>0.27</td><td>176,803.492</td></tr><tr><td>cluster_2</td><td>1914</td><td>0.939</td><td>1.771</td><td>-0.004</td><td>31.845</td><td>0.486</td><td>189,855.932</td></tr></table></body></html>  

# 观察聚类结果的各个群组，从业务视角进行解释与命名：  

$\cdot$ Cluster1数量少，年龄较小，车价最高，出险最少 $=>$ 青年高价低风险组$\cdot$ Cluster2数量中等，年龄中，车价较高，出险较少 $=>$ 中年高价低风险组$\cdot$ Cluster3数量较多，年龄中，车价最低，出险最多 $=>$ 中年低价高风险组  

![](images/b800396de994dcebab0a7a9f003c61382cedacaf20551303daa5560dc48f1dea.jpg)  

# 模型解释的常用方法与工具  

除了观察特征的重要性，通常也会使用SHAP的方法（支持全局与局部解释）。  

特征重要性：衡量每个特征对预测结果的总体贡献。  
SHAP：基于博弈论的特征贡献分配方法。  

# 特征重要性：树模型  

树模型（决策树、随机森林、XGBoost等），使用模型的feature_importances基于模型的：如树模型的feature_importances基于置换的：通过打乱单个特征测量性能变化。  

![](images/5836f3b59b367b74b9774e657b9805131b902af768e05f627675b5af9554d039.jpg)  

$x=$ pd.get_dummies（data.drop（"准时交付”,axis=1),drop_first=True)   
$y=$ data[准时交付"]   
X_train,X_test,y_train,y_test $=$ train_test_split(X,y,test_size=0.3,   
random_state=42)   
dt $=$ DecisionTreeClassifier(random_state=42)   
dt.fit(x_train,y_train) 特征 重要性 供应商等级 0.380   
#特征重要性 天气 0.296   
pd.Series(dt.feature_importances_, 节假日 0.294   
index=X.columns).sort_values(ascending=False) 仓库编码 0.031  

# 特征重要性：基于置换的重要性  

衡量“某个特征是否那么重要”，另一种直观做法是：把这个特征打乱，看模型性能下降多少。  

1.先计算模型原本的性能（比如准确率、召回率等）。  
2.选择一个特征A，把测试集中这一列的值随机打乱（即“置换”）。  
3.再用模型进行预测，看看性能变化（下降很多，说明重要）。  

4.对每个特征都重复这个过程。  

<html><body><table><tr><td>特征</td><td>打乱后准确率</td><td>性能下降 重婴性</td></tr><tr><td>交付距高</td><td>0.70</td><td>+0.20 很高</td></tr><tr><td>客户等级</td><td>0.89</td><td>↓0.01 很低</td></tr><tr><td>发货时间</td><td>0.80</td><td>↓0.10 中等</td></tr><tr><td>天气情况</td><td>0.88</td><td>↓0.02 很低</td></tr></table></body></html>  

from sklearn.inspection import permutation_importance   
model =DecisionTreeClassifier(random_state=42)   
model.fit(x_train,y_train)   
#模型原始性能   
base_score=model.score(X_test,y_test)   
#基于置换的重要性   
result=permutation_importance( model,test,y_tst,rat=10,random_stat42,coring=accuray   
importance_df $\mathbf{\Psi}=\mathbf{\Psi}$ pd.DataFrame( "feature":X.columns,"importance_mean":result.importances_mean,"importance_std":   
result.importances_std   
1).sort_values(by="importance_mean",ascending=False)  

# SHAP  

SHAP值（Shapleyvalue）来源于博弈论，用于衡量每个特征对模型输出的边际贡献。回答：每个特征对模型预测结果的影响有多大，以及方向如何？  

一致性：特征重要性不会因模型不同而随意变化。  
可解释性：每个样本、每个特征的影响都能量化。  
模型无关性：适用于各种模型。  

假设预测 “是否准时交付”，模型准确率是0.90。  

整体  


<html><body><table><tr><td>特征 平均绝对SHAP值</td><td></td></tr><tr><td>整体 交付距离 0.25</td><td>重要性</td></tr><tr><td>发货时间 0.18</td><td>最重要（距离越远，准时概率越低）</td></tr><tr><td>天气情况 0.12</td><td>较重要（早发货→更准时） 一定影响（坏天气→延误）</td></tr><tr><td>客户等级 0.08</td><td></td></tr><tr><td></td><td>较小影响（VIP稍微更准时）</td></tr></table></body></html>  

![](images/5564b4558e7393f5817c2bfc1caa595620bd08baf6dc191aed7c967035727326.jpg)  

特征 特征值 SHAP值 含义  
客户等级 VIP +1.62 高等级客户 $\rightarrow$ 优先处理，有助于准时交付  
发货时间 下午 -0.98 下午发货→时间紧张，不利于准时交付虽然天气一般，但可能伴随其它正面因素，略有助于  
天气情况 雨天 +0.48 准时  
交付距离 47.6km -0.01 距离远→稍微不利于准时交付  

# 物流发货的特征重要性  

物流发货，预测是否准时交付？  

<html><body><table><tr><td colspan="2">交付柜高</td><td>客户等级 发员时间</td><td>天气情况</td><td>是否准时</td></tr><tr><td>D</td><td>19.4</td><td>普通</td><td>上午</td><td>萌朗</td></tr><tr><td>1</td><td>47.6</td><td>VIP</td><td>下午</td><td>雨天 1</td></tr><tr><td>2V</td><td>36.9</td><td>VIP</td><td>下午</td><td>天 1</td></tr><tr><td></td><td>30.3</td><td>VIP</td><td>上午</td><td>1</td></tr><tr><td></td><td>8.6</td><td>誉道</td><td>上午</td><td>雨天</td></tr></table></body></html>  

# import..... import shap  

x=data_encoded.drop（columns=["是否准时")   
y=data_encoded["是否准时"]   
model=xgb.xGBClassifier(eval_metric="logloss")   
model.fit(x,y)  

explainer= shap.Explainer（model)#计算 SHAP值 shap_values=explainer(x)  

绘制全局特征重要性   
plt.title（“全局特征重要性（SHAP Summary Plot）“ shap.summary_plot(shap_values,X,show=False) plt.show0  

![](images/01a5233c05646a460ec2ba8610ece1bb1c5756d14f695f1be25ef71c62b9ec05.jpg)  

![](images/31deaa3d1241154e4df3bd6b6475badc3a10ecaef6ce10801e671af8a278fe2e.jpg)  

# 物流发货的特征重要性  

模型内部的特征重要性排序与SHAP的计算顺序可能会不一样。  

import pandas aspd import matplotlib.pyplot asplt  

#计算特征重要性并排序   
feature_importance $=$   
pd.Series(model.feature_importances_,   
index=X.columns).sort_values(ascending=True)   
#画条形图  

模型内部的特征重要性是从“模型结构”的角度看的SHAP特征重要性是从“预测影响”的角度看的。两者出发点不同，所以排序往往不同。  

![](images/3233b78bf3d2a828934fa5179640735ad7d4e95568a478bea80f0147444d6457.jpg)  

# 小结  

模型的可解释性与精确性此消彼长。在日常工作中，不管是业务解释的需要，还是模型与特征优化的需要，我们都需要从模型本身或输入输出的结果中，来整理、分析、解释。  

如果是树模型，可以方便的看出特征的重要性或整理出规则逻辑。对于非树模型，我们也可以基于置换的方式或SHAP方法，观察总体、样本的特征的贡献率。  

![](images/2f35e2464f9a1378a4e0200fe31ca8600a13f2c3e4efc9edf4eac22104cde756.jpg)  
《2001太空漫游》里的黑石碑  

# 异常检测算法与应用  

异常检测的目标是识别不符合正常模式的数据点或行为。  

为什么要做异常检测  
异常数据的特点  
异常检测的思路与流程  
物流场景的异常检测  
应用one-classSVM算法  
应用lsolationForest（孤立森林） 算法  

# 为什么要做异常检测  

异常检测在不同的行业都有应用，比如金融风控、T运维、制造业等。  
在供应链的各个环节（来购、库存、运输等）也都有需求。  

# 异常检测的目的：  

提升系统可靠性与安全性  
提高数据质量  
支持自动化决策  
发现未知模式  
供应商的行为模式、物流路径  

![](images/6e6a3fb7ab3b48c3f58878dbbbcc4a50df9a2cec07b93c51ce1b8008300410fe.jpg)  

# 异常数据的特点  

异常数据 (Outliers) 通常具有以下特征：  

稀有性  
不一致  
多样性  
环境依赖性 （是否正常要基于当前环境）  

![](images/000a7b1c2d948132b7a24b050e114603353bcf33227442db47e55de1b4c56003.jpg)  

# 异常检测的通用思路  

学习 “正常”模式，然后识别偏离该模式的点。  

统计学方法：Z-score、IQR。  

Detecting Outliers withz-Scores  

![](images/25a70fa8d925412e6c6629a2c47a4edbb193f6cd9856a5c1b63212a63f0f8784.jpg)  
超出3倍的标准差  

![](images/def24f18464d38687c133230e33d75e909290a09f76bbadf6295a4845bc2a5ed.jpg)  
超出1.5倍IQR  

# 异常检测的通用思路  

学习 “正常”模式，然后识别偏离该模式的点。  

距离与密度方法：KNN-baSed、DBSCAN（密度聚类）  

更多机器学习方法  

类型 数据需求 思想 示例算法有监督 需要异常标签 分类思想（正常vs异常） 随机森林、XGBoost半监督 只训练正常样本 学“正常分布” One-Class SVM无监督 不需要任何标签 利用密度或孤立性 Isolation Forest  

# 异常检测的机器学习流程：半监督  

半监督的One-Class SVM，需要先学习（训练）正常的样本，再对新的数据进行检测。  

阶段 关键问题  
1特征提取 能体现正常／异常差异吗？  
2模型训练 是否只用正常数据？  
3异常打分 如何定义“异常程度”？  
4國值判断 灵敏or保守？  
5结果评估 哪些指标反映性能？  

# 异常检测的机器学习流程：无监督  

无监督的IsolationForest（孤立森林），则直接用全部数据建模，通过样本的孤立程度判断异常。  

阶段  

# 关键问题  

1特征提取 特征能否体现样本间的孤立性差异？  
2模型训练 随机划分特征空间以学习并计算样本的孤立结构。  
3异常打分 如何根据孤立程度得到异常分数？  
4闯值判断 灵敏or保守？  
5结果评估 无标签或少量标签时如何评估模型效果？  

# 物流异常检测  

在供应链与物流系统中，异常运输（延迟、绕路、堵车、数据错误）会导致：成本上升、客户投诉、计划失效的问题。需要识别“偏离正常运输行为”的记录，从而提前预警问题。  

异常类型 示例 可能原因速度异常 平均速度低于间值（如 $20{-}30k m/h)$ 交通拥堵、设备故障路线异常 偏离标准路线 $20{-}50\%$ 绕路、GPS漂移时间异常 总运输时长过长 延误、装卸问题停靠异常 过多中途停靠 非计划停留  

# 物流异常检测：简化的例子  

为了方便查看，假设只使用：平均速度与路线偏离度二维的数据。  

类型 范围（速度/偏离） 场景说明城区运输（ClusterA） 60-80 km/h / 0-5% 城区内短途运输高速运输（Cluster B） 90-110 km/h / 10-15% 高速长途运输  

可能的异常：过快、过慢、偏离度高。可能的原因：非安全驾驶、堵车、绕路、GPS漂移等  

# 物流异常检测：平均速度与偏离度  

日常的数据，可以看出有两个分布，以及少量的数据点异常。  

![](images/48bbec317590e6d26875d9aa598482d529467d431eea495022fd2044f757cd50.jpg)  

# 物流异常检测：流程  

以半监督算法 (One-Class SVM) 为例。  

1.输入特征 （每次运输的数据）  

平均速度与路线偏离度  

2.建立模型使用正常运输记录训练模型·对新样本计算偏离程度  

# 3.输出结果  

正常（1）异常（-1）或自定义闯值判断  

# One-ClassSVM （单类支持向量机）  

One-ClassSVM是专门为异常检测设计的算法。通过学习“正常样本”的分布边界，判断哪些点偏离该分布。  

通过将正常样本通过核函数映射到高维空间，找到一个能够包围大多数样本的超平面，超出这个区域的点就被认为是异常。  

# 适用场景：  

只有“正常数据”，几乎没有异常样本  

# 输出结果  

$_{1\rightarrow}$ 模型认为是正常点$-1\rightarrow$ 模型认为是异常点  

![](images/73e8c05b87c331e32d4f4c9c09b653e9e4867b53adeaf66da4470ca88ee55de9.jpg)  

# 使用One-ClassSVM进行异常检测  

# 代码调用很简单，参数也不多。  

import numpy asnp  
import pandas aspd  
from sklearn.svm import OneclassSVM  

#读取训练数据X_train $=$  

$\#==$ 训练One-ClassSVM 模型（平滑边界） $===$ model $=$ OneClassSvM(kernel='rbf,gamma $1{=}0.005$ $n u=0.08$ model.fit(X_train)  

#预测与统计 y_pred $=$ model.predict（x_train)  

![](images/ab86039065dc8ce710737fd9e93c317778ed736f556e580e78239c89b5527c6e.jpg)  

预测结果统计：-1异常：161 正常：189  

# 使用One-ClassSVM进行异常检测  

绘制边界线与等高线 model $=$ oneclasssvm(kernel='rbf,gamma=0.005, $n u=0.08)$  

![](images/2146d5db6001986d3d1c2af0a48e0c6685db0b4c685fa9825d623c5f5725abf5.jpg)  

gamma（弯曲程度）：·常见范围：0.001\~0.05·大→看得近，边界复杂。·小→看得远，边界平滑。  

nu（严格程度）：·常见范围： $0.05\sim0.2$ ·大 $\to$ 严格，检出更多异常$1!\rightarrow$ 宽松，检出更少异常  

# 使用One-ClassSVM进行异常检测  

训练好的模型，如何应用于新的数据？  

速度（km/h） 路线偏离度 预测结果  
60 2 正常  
90 10 正常  
120 20 异常  
50 30 异常  

#应用模型进行预测 y_test_pred $=$ model.predict(x_test)  

#合并测试数据和预测结果，并显示  
test_result_df $\v{U}=\v{U}$ pd.DataFrame(“速度 $(k m/h)^{\ast}$ test_speed,“路线偏离度"：test_deviation，“预测结果”：[“正常”if $p==1$ else"异常"for pin y_test_pred]  
display(test_result_df)  

![](images/34700b1b63256c18334daf1e9ef226513ca619aa854d45631e804c1983d99025.jpg)  

# 使用One-ClassSVM进行异常检测  

放宽值，使用样本点到「决策边界的距离」，来决定是否异常。  

![](images/18da1369f7632f3901a1c9a225996658d63f81d3a652ce265e84677cb6460c7f.jpg)  

# lsolation Forest （孤立森林）  

IsolationForest是一种专门用于异常检测（OutlierDetection）的算法。通过构建随机决策树来“孤立”数据点，正常样本需要更多切分才能被隔离，而异常样本往往在少数几次切分后就能被孤立。  

它的目标是：学习正常样本的分布特征，通过孤立难易程度来判断哪些点偏离整体模式。  

# 适用场景：  

只有“正常数据”，几乎没有异常样本。  
输出结果：$_{1\rightarrow}$ 模型认为是正常点$-1\rightarrow$ 模型认为是异常点  

![](images/47dd941b1329cd3c69e9ba18a3859127e9127b977d9695f3788ccc3772de9532.jpg)  

# Isolation Forest （孤立森林） 算法介绍  

核心思想：异常点更容易被孤立（异常样本通常位于稀疏区域）。通过构建多棵随机树来度量样本被孤立的难易程度。  

![](images/ce4bbcb8cd292d86897c5e504fd6c91af12747028fe748aba8037c71fcf73a67.jpg)  

1.随机选择一个特征。  
2.在该特征的取值范围内随机选择一个分割点。  
3.递归划分数据，直到样本被单独划分或达到最大树深。  
4.重复生成多棵树（通常数百棵），形成“孤立森林”。  
5.计算平均路径长度：a.异常点 $\to$ 平均路径短b.正常点 $\rightarrow$ 平均路径长  

![](images/aef468dee00c3eac99c2c2e9aa6b72edd0ef944b6b5fada575b0ab1245affc95.jpg)  

# 使用lsolationForest进行异常检测  

无监督，直接对完整的数据进行预测  

$\#==$ 训练Isolation Forest 模型 $===$   
model $=$ IsolationForest( n_estimators=200, #树数量 contamination=0.08，#预期异常比例 random_state=42  

$\#==$ 预测与统计== y_pred $=$ model.predict（x_train)  

![](images/d2f56236fc12da2fae11da11bdd175ad8acef5eafb134607e84111665a236584.jpg)  

预测结果统计：-1异常：171 正常：188  

# 使用lsolationForest进行异常检测  

contamination 模型倾向小（0.01\~0.05） 严格、保守，异常少中（0.05\~0.15） 平衡大（>0.15） 宽松，异常多  

边界形状  
边界更紧  
边界适中  
边界更松、正常区更大  

![](images/b0393dfb636b238b2e2e4d0f7393f5f2f48a41068fa297bd9b24e367a6c61816.jpg)  

contamination = 0.01异常：3正常：202  

![](images/ebc9701a304d59c37d469982fb0bb840a98d25c4896845976a490e5a8455e0b3.jpg)  

![](images/0cd1b871162e9060aaec0977cdec04bc01f5c8a61ef34a99929143491844e414.jpg)  

contamination $=0.2$ 异常：41正常：164  

# IsolationForest常用参数  

常用的参数不多且易于理解  

from sklearn.ensembleimport IsolationForest   
model $=$ IsolationForest( n_estimators=200, #树数量 contamination=0.08，#预期异常比例 random_state=42  

<html><body><table><tr><td>参数</td><td>作用</td><td>常见取值</td><td>说明</td></tr><tr><td>n_estimators</td><td>森林中树的数量</td><td>100~300</td><td>越多越稳定，但训练稍慢。</td></tr><tr><td>max_samples</td><td>每棵树使用的样本数</td><td>'auto'或整数</td><td>auto'表示min（256,n_samples），减少过拟合。</td></tr><tr><td>contamination</td><td>预期异常比例</td><td>0.05~0.15</td><td>只影响异常阅值，不影响训练结构。</td></tr><tr><td>max_features</td><td>每棵树使用的特征数</td><td>1.0或<1.0的比例</td><td>降低特征维度时可增强泛化。</td></tr><tr><td>bootstrap</td><td>是否采用有放回采样</td><td>False（默认）</td><td>设为 True 可形成Bagging效果。</td></tr><tr><td>random_state</td><td>随机数种子</td><td>整数（如42）</td><td>保证结果可重复。</td></tr></table></body></html>  

# 小结  

机器学习的异常检测的算法原理会有差异，但核心的思路与流程是类似的。这也和异常数据的特点有关。在使用的过程中，除了特征的选择，参数优化外，我们还会通过调整值，来提高或降低敏感度。  

阶段 关键问题  
1特征提取 能体现正常/异常差异吗？  
2模型训练 是否只用正常数据？  
3异常打分 如何定义“异常程度”？  
4闯值判断 灵敏or保守？  
5结果评估 哪些指标反映性能？  

![](images/d8bc4ea83c481aa7157bc9203fa53fc1d2bf93b1ef36347fbb7203df1c084ae0.jpg)  

# 机器学习中的AI辅助  

AI在机器学习中可辅助数据匹配、清洗与标注，自动检测异常与重复项；利用文本分析实现分类、打标签与情感识别；并参与数据质量监控。通过AutoML，模型训练与优化过程也实现自动化，显著提升效率与准确性。  

1.数据探索与理解  
2.数据清洗  
3.数据标注、匹配、语义理解  
4.AI辅助建模 (AutoML)  
5.AI生成模型报告与改进建议  

![](images/ab7aa5100ea0c793c6908d7c97228ea0e02ce59edbdacf04d3b81d270d57589b.jpg)  

# 数据探索与理解  

在拿到初始的数据时，会需要对数据进行快速的探查与分析。在以往，这样的工作需要借助BI工具，手工方式进行图表的制作与总结。  

AI辅助生成数据摘要、统计洞察AI识别潜在问题（分布偏差、异常、缺失）  

![](images/0d76fc8ae225bc960cd9e39dc0208d5c12684a4e1d58df8fdeb4d6e5155a3e58.jpg)  

# 数据清洗  

在数据清洗的过程中，我们会通过技术视角、业务视角来对数据进行检查判断。  

异常检测、重复检测、自动修复建议  
编码与缺失值填补的智能化  
AI辅助语义标准化（例如不同系统间“城市名称”的对齐）  

![](images/57e68c22f2ac0150d1dbcecce3079b09267d389f5da264eb9f198a6f2c3a96cd.jpg)  

# 数据清洗  

上传表格数据，告知任务要求，Al会生成对应的Python代码，进行检查。  

#1.检查重复行Pelass duplicate_rows= df[df.duplicated(]duplicate_count= duplicate_rows.shape[o]Palsson Mastet. #2.检查数值异常（如负数或不合理范围）Gosta Lesrardanomalies={)#Age应该在0-100范围内(Elsabeth anomaliesAge_outofrange]=df(dfAge]o）(dfAge]>Vilhetmiru Berg!Nasser,Mrs. 100]1010 #Fare应该非负Sandstrom,Miss. anomalies['Fare_negative'] $\boldsymbol{\mathbf{\rho}}=$ df[df'Fre']<0]为我完成如下的数据清洗工作： 异常检测、重复检测、自动修复建议 #3.缺失值修复建议repair _suggestions={Age：使用乘客舱位（Pclass）、性别（Sex）的中位数进行填充，Cabin：填充为“Unknown”或提取首字母作为舱段类别，Embarked：使用出现频率最高的值（众数）填充  

# 数据清洗  

输出的结果。  

<html><body><table><tr><td>基本检测结果 检测项 结果</td><td>缺失值统计 列名 缺失值数量</td></tr><tr><td>总行数 891</td><td>Age 177</td></tr><tr><td>总列数 12</td><td>Cabin 687</td></tr><tr><td>重复行 0</td><td>Embarked 2</td></tr><tr><td>年龄异常值（Age<0或> 0</td><td>其他列 0</td></tr><tr><td>100) 票价异常值（Fare<0） 0</td><td></td></tr></table></body></html>  

<html><body><table><tr><td>自动修复建议 列名 修复建议</td><td></td></tr><tr><td>Age</td><td>使用舱位（Pclass）与性别（Sex）的中位数进行分组填充（如：一等舱女性→</td></tr><tr><td>Cabin</td><td>中位数年龄填充） 填充为“Unknown”或提取首字母（如A、B、C）表示舱段类别</td></tr><tr><td>Embarked</td><td>使用出现频率最高的值（通常为"S）进行填充</td></tr></table></body></html>  

# 数据标注与匹配  

AI辅助匹配数值与标签的标注。  

·可以通过表格产品（Excel，WPS）的行级的AI公式来计算（分类、总结、自定义）  
·语义理解生成特征（主题、关键词、情感分析）  
·任务比较简单，还可以通过本地模型来处理  

![](images/28462ab453234a91943ecf41b271980c2fa6dd9b3eb788bc77105c3dc6e7578c.jpg)  

# AI辅助建模 (AutoML)  

AutoML（AutomatedMachineLearning，自动化机器学习）是一种让机器学习的开发过程自动化的技术。目的是让非专业的开发者也能构建高质量的机器学习模型，同时为专业用户节省时间和精力。  

传统的机器学习开发流程  

1.数据预处理（清洗、特征选择、编码等）  
2.模型选择（决定使用随机森林、XGBoost、神经网络等）  
3.超参数调优（调整学习率、深度、正则化等）  

4.模型评估与集成  

通过算法和搜索策略自动化。 YES  

# AutoML系统的主要组成  

围绕传统的机器学习开发流程展开  

模块 功能瓷明自动选择、组合或生成新的特征。  
自动特征工程在多种算法中自动选择最合适的模型。  
植型搜象（Model Selection）  
超参数优化（HPO） 自动尊我最佳参数组合，如用贝叶斯优化、遇传算法等。  
模型集成（Ensembling） 自动将多个模型结果融合，以提升性能。  
模型解释与部暑 自动生成可解释性报告与部署接口。  

![](images/4da6fde780a98d271962f9690aa6b292730e6bd0ce9e404ad32295b553bfe0f2.jpg)  

模型集成，将多个性能不同的模型组合起来，让它们“投票”或“加权平均”以获得比单个模型更好的预测效果。  

# 常见AutoML框架  

各大云厂商都有自己服务集成，为了方便验证，可以优先考虑开源的版本。  

<html><body><table><tr><td>框架</td><td>语言 特点</td><td></td></tr><tr><td>Google Cloud AutoML</td><td>云服务</td><td>与 Google Cloud集成，支持图像/文本/ 结构化数据。</td></tr><tr><td>Microsoft Azure AutoML</td><td>云服务</td><td>与Azure 生态无缝整合，UI 友好。</td></tr><tr><td>Auto-sklearn</td><td>Python</td><td>基于scikit-learn，使用元学习与贝叶斯 优化。（只支持Linux环境）</td></tr><tr><td>H20 AutoML</td><td>Java/Python/R</td><td>高性能、可扩展，支持分布式计算。</td></tr><tr><td>AutoGluon</td><td>Python</td><td>支持多模态，易用性好。</td></tr></table></body></html>  

# AutoGluon 简介  

由Amazon开发，基于深度学习与集成学习，支持图像、文本、表格数据等多模态任务；易用性强，一行代码即可完成自动特征工程、模型调优与集成；兼容MXNet与PyTorcho  

AutoGluon  

![](images/26aff0deaf227104d0ccf3be53c1957941128468131b7f5e44e8bc4336a5b128.jpg)  

Fast ahd Accurate ML in3 Lines of Code  

github.com/autogluon/autogluon pip install autogluon  

# AutoGluon 简介  

主要的特点：  

·自动化程度高：从数据预处理、模型选择、超参优化到模型集成，全流程自动完成。  
·多任务支持：支持分类、回归、文本、图像、表格、时间序列预测等。  
·模型集成（Ensembling）：自动集成多个模型以提升性能·易用性强：只需几行代码即可完成复杂的机器学习流程。  
?可解释性支持：提供模型特征重要性分析。  

![](images/801854850b05bd89653eb67066e4715fe53aa7f93e280259bd3a4c0e80ec1389.jpg)  

# AutoGluon  

Fast and Accurate ML in 3 Linesof Code  

# AutoGluon 常用模块  

不考虑多模态的部分，通常tabular、timeseries即可。  

<html><body><table><tr><td>模块</td><td>主要功能</td><td>典型应用</td></tr><tr><td>autogluon.tabular</td><td>表格数据（结构化数据）的自动化建 模，包括分类、回归等。</td><td>如价格预测、客户流失预测</td></tr><tr><td>autogluon.timeseries</td><td>时间序列预测（Time Series Forecasting)</td><td>销售量预测、能源消耗预测</td></tr><tr><td>autogluon.core</td><td>提供统一的核心函数，如配置管理、任 务抽象、日志、数据处理等。</td><td>底层支持模块</td></tr><tr><td>autogluon.features</td><td>特征工程模块，负责自动特征选择、类 型检测、缺失值填充、编码等。</td><td>自动特征处理</td></tr></table></body></html>  

# AutoGluon 应用举例  

以泰坦尼克数据集为例，回归问题，预测年龄。  

from autogluon.tabularimport TabularDataset,TabularPredictor from sklearn.model_selection import train_test_split importpandasaspd  

titanic $=$ pd.read_csv(\`titanic.csv') titanic $=$ titanic['SurvivedPclass'Sex'Age'SibSp'Parch"Fare'Embarked'}] titanic $=$ titanic.dropna（subset=[Age']）#删除Age 缺失值 label $=$ 'Age'#设置目标变量为Age  

train_data,test_data $=$ train_test_split（titanic,test_size=0.2,random_state $=42$  

#训练模型（回归任务）   
predictor $:=$ TabularPredictor( label=label, eval_metric=root_mean_squared_error, #RMSE verbosity=0#不输出过程日志   
).fit（train_dataresets=medium_quality）#medium_quality般质量  

# 输出：  

('root_mean_squared_error':np.float64(-11.654902523581148), 'mean_squared_error:-135.8367528341782,'mean_absolute_error': -9.024857328488277,'r2':0.2673480302743033,pears0nr: 0.5375087977702689,'median_absolute_error':-7.485696792602539}  

#输出回归的预测结果（年龄）   
preds $=$ predictor.predict（test_data.drop(columns=[label]))   
print(preds.head(3))  

149 32.155373   
407 5.893414   
53 31.808929  

# AutoGluon 应用举例  

以泰坦尼克数据集为例，分类问题，是否获救（Survived）  

from autogluon.tabular import TabularDataset,TabularPredictor from sklearn.model_selection import train_test_split importpandasaspd  

titanic=pd.read_csv('titanic.csv) titanic=titanic[SurvivedPclass’Sex'Age'Sibsp'ParchFare'Embarked1 $=$  

train_data,test_data = train_test_split(titanic,test_size=0.2, random_state=42,stratify=titanic['Survived]#保持类别H  

label ='Survived'  

# #训练模型  

predictor=TabularPredictor( label=label, eval_metric='accuracy#准确率 verbosity=0#不输出过程日志 ).fit（train_data,presets='medium  

#输出模型评估结果：   
performance = predictor.evaluate(test_data)   
print(performance)  

# 输出：  

('accuracy':0.8100558659217877,'balanced_accuracy': np.float64(0.777931488801054),'mcc':0.5926051618768544,'roc_auc': np.float64(0.8177206851119894),f1':0.7213114754098361,'precision': 0.8301886792452831,'recall':0.63768115942028981  

#输出分类的结果   
preds = predictor.predict(test_data.drop(columns=[label]))   
print(preds.head(3))  

565 0   
160 1   
553 0  

#输出分类的结果概率 $=$   
preds = predictor.predict_proba(test_data.drop(columns=[label]))   
print(preds.head(3))  

0 1 5650.767477 0.232523 160 0.624235 0.375765 553 0.6920170.307983  

# AutoGluon查看模型列表与特征重要性  

为了提升预测的准确性，AutoGluon会自动将多个模型结果融合，以提升性能。可以通过predictor.leaderboard(或predictor.fit_summary()查看明细  

leaderboard =predictor.leaderboard(silent=True) 模型名称，验证集分数，训练时长，预测时长 display(leaderboard[l'model,'score_val,'fit_time,'pred_time_val']])  

importance =predictor.feature_importance(test_data) print(importance)  

model score_val fit_time pred_time_val 23 1 WeightedEnsemble_L2 LightGBMLarge 0.860140 0.874126 0.874126 3.040572 0.740575 3.061102 0.000939 0.000827 0.001084 0.282366 0.001489 info=predictor.info)#查看超参数信息 display(infol'model_info'j['xGBoost'Jl'hyperparameters'])  

importance stddev p_value   
Sex 0.174302 0.027197 0.000069   
Pclass 0.105028 0.013338 0.000031   
Age 0.045810 0.024796 0.007240   
Fare 0.043575 0.016478 0.002048   
SibSp 0.015642 0.010746 0.015615  

$\cdot$ importance：特征的重要性分数（值越大越重要）stddev：重要性分数的标准差（用于衡量稳定性）p_value：假设检验的显著性水平，值越小说明特征更显著  

# AutoGluon 性能优化  

在原型验证阶段，可以通过降低精度，指定模型列表，限制运行时间，来提升选代的用时与效率。  

# 训练速度  

# 限制训练时间与指定模型列表  

predictor $=$ TabularPredictor( label=label, eval_metric='accuracy' verbosity=o   
).fit(train_data,presets='medium_quality')  

predictor $\underline{{\underline{{\mathbf{\Pi}}}}}$ TabularPredictor(label='target').fit(train_data=train_df,time_limit=600，#指定训练时间上限（单位：秒）hyperparameters={XGB：0，#使用XGBoost模型'RF:0，#使用随机森林模型  

medium_quality good_quality high_quality best_quality  

# AutoGluon 报告输出  

使用predictor.fit_summary（show_plot=True）输出完整的模型、参数的文本信息与图表。  

![](images/313a4533692dfed87e02672e89be6019e844c2702f9c7ff5be5fc2d41b6b52bf.jpg)  

# 小结  

Al的文本处理、代码生成，text2sql，以及Agent的自主探索规划的能力，不仅可以提升商业分析的效率，也可以通过代码框架、产品化的方式，来为机器学习的流程提效与自动化。  

在日常工作中，除了手工的特征选择、调参迭代，也可以参考尝试AutoML的工具，本质上还是为了得到性能好，健壮，易用，可解释的模型。  

![](images/97ae63bda43c9ef8ff81133a1c83c9977ca197741af7830fa6a2448e7e8bb54c.jpg)  

# 总结  

为了做好机器学习，不仅是工具与技术，还需要我们了解业务知识，熟悉机器学习总体的流程与算法选择，从业务与技术的视角评估与优化。两天的课程，可以帮助你前进一小步，同时提升自己的眼界思路，这会有助于之后的学习与实践。  

![](images/cf09e16c438ccbe5630eb829fc09dc30305ac1a35df106186e7a929a35656d75.jpg)  