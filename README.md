# Data-Aanlysis

# Mice Protein Expression 聚类分析

## 数据

- **来源**: `Data_Cortex_Nuclear.csv`（UCI Machine Learning Repository）
- **内容**: 小鼠大脑皮层中 77 种蛋白质的表达水平
- **目标变量**: `class`（共 8 个类别）

## 方法

### 预处理
- 删除缺失率 >10% 的列
- 均值填充剩余缺失值
- 删除无分析价值的 `MouseID` 列
- 对分类变量 (`Treatment`, `Behavior`, `Genotype`) 进行 one‑hot 编码
- Min‑Max 缩放

### 降维
- **主成分分析 (PCA)**：保留 6 个分量（解释 80% 方差）或 2 个分量（用于可视化，解释 39% 方差）

### 聚类算法
- K‑means（肘部法和轮廓系数选择 k=8）
- K‑medoids（PAM，k‑medoids++ 初始化）
- 层次聚类（Ward 连接）
- 模糊 C‑均值 (FCM)
- DBSCAN（调参 eps 和 min_samples）
- OPTICS（并提取 DBSCAN 标签）

### 评估指标
- 轮廓系数 (Silhouette Score)
- 惯性 (Inertia，用于 centroid‑based 模型)

### 后处理预测
- 基于 K‑means 聚类结果，使用 K‑近邻 (KNN) 对新样本进行聚类标签预测

## 依赖库

`pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `scikit-learn-extra`, `yellowbrick`, `fcmeans`, `scipy`

## 运行

```bash
python Mice_Protein_Expression.py
