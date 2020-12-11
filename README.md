# Onecity 编程大赛复赛第二名

## 比赛地址：
https://www.dcjingsai.com/v2/cmptDetail.html?id=457
![LB](https://github.com/ymcdull/onecity/blob/main/LB.PNG)

## 文件：
- **Preprocess.ipynb**： 读取csv和xls文件，对同一文件按照不同的方式读取文件不同的部分以做到数据增强
- **Get Pinyin To Chinese Map.ipynb**：通过数据分析，发现很多的表格的表头部分有拼音的首字母出现，进而准备拼音到中文的匹配
- **Bert_with_filename.ipynb**： 对于有文件名的部分，对于训练集和测试集， 拼接文件名和文件内容，使用data augmentation, 用BERT训练并预测结果
- **Bert_content_only.ipynb**： 对于没有文件名的部分，对于训练集和测试集， 只使用文件内容，用BERT训练并预测结果
- **Rules.ipynb**: 通过文件分布的分析，发现有很大一部分的文件可以通过直接匹配训练集或者建立简单规则来获取结果，对于剩余部分的数据，通过BERT模型来预测结果，最后拼接成提交的最终文件

## 模型测试环境：
Kaggle Kernel TPU v3-8
依据[这里](https://www.kaggle.com/c/flower-classification-with-tpus/discussion/131158)的描述: The TPUv3-8 is actually 4 chips connected together where each chip is physically similar to the GPU V100 ($8,500), i.e. they both have 32GB memory and similar compute. If you connect 4xGPU V100, then you have a similar comparison to the TPUv3-8 and you will observe that they both operate at similar speeds and similar batch size capacity.
可以合理假定TPU的速度是V100卡的四倍，所以将TPU上运行时间控制在了3个小时以内

## 运行时间：
- **数据读取和预处理**： < 1h (CPU)
- **BERT with filename模型**： 1448.462 seconds (TPU)
- **BERT content only模型**：6360.778 seconds (TPU)

## 复赛思路：
- 用xlrd读取数据比pd.read_excel要准确
- 通过对复赛数据集的数据分布分析，发现有很大一部分数据直接通过匹配训练集或者简单规则就可以直接得到准确的预测，剩余部分绝大多数是没有文件名的样本，这样将复赛的重点放到提升content-only的模型
- 数据增强（通过读取文件的不同部分）在本地CV起到很大的作用
- 对于content-only的模型，删除了训练集中绝大部分重复数据，加快模型训练速度
- 很多文件的表头部分都是拼音的首字母缩写，做了一些中文到拼音首字母的匹配，做了一些数据清理（没有具体试验这部分有没有收益，可能保留拼音首字母，bert-base-chinese也可以学习到很多东西）
- 感谢Kaggle提供免费TPU资源，模型训练速度飞快