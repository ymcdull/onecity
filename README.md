# Onecity 编程大赛复赛第二名

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