This example shows how to build a full author disambiguation pipeline.
The pipeline is made of two steps:

- Supervised learning, for inferring a distance or affinity function
  between publications. This estimator is learned from labeled paired data
  and models whether two publications have been authored by the same
  person. To perform supervised learning, run ``distance.py`` file.

- Semi-supervised block clustering, for grouping together publications
  from the same author. Publications are blocked by last name + first
  initial, and then clustered using hierarchical clustering together with
  the affinity function learned at the previous step. For each block,
  the best cut-off threshold is chosen so as to maximize some scoring
  metric on the provided labeled data. To perform clustering, run
  ``clustering.py`` file.

1.sampling.py
  输入：input_cluster.json
  功能：处理输入的作者信息数据，为下一步训练分类器提供数据
  输出：分类器训练数据（my_pairs.json）

2.distance.py
  输入：input_records.json input_signatures.json
  功能：根据第一步获得训练数据，训练分类器
  输出：分类器文件 distance_model

3.clustering.py
  输入：input_records.json input_signatures.json input_cluster.json
  功能：对同名作者聚类
  输出：聚类结果 output_cluster.json