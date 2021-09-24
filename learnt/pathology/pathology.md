# Pathology

This article is a sum-up of three surveys of digital pathology image analysis[^1][^2][^3]. I mainly followed the structure of the MIA research[^1] and used the other two[^2][^3] as supplement.



## Tasks









![image-20210922172744898](imgs/image-20210922172744898.png)

## Dataset

| Dataset                                                      | Field            | Size         | Sample                                                       |
| ------------------------------------------------------------ | ---------------- | ------------ | ------------------------------------------------------------ |
| [TCGA](https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga/using-tcga) | Cancer related   | > 470 TB     | ![image-20210923155258152](imgs/image-20210923155258152.png) |
| [TUPAC16](https://tupac.grand-challenge.org/Dataset/)        | Tumor mitosis    | ≈ 821 slides | ![image-20210923155853306](imgs/image-20210923155853306.png) |
| [Camelyon](https://camelyon17.grand-challenge.org/Data/)     | Breast cancer    | ≈ 3 TB       | ![image-20210923160158270](imgs/image-20210923160158270.png) |
| [Kimia Path24](https://kimialab.uwaterloo.ca/kimia/index.php/pathology-images-kimia-path24/) | Pathology Images | 24 WSIs      | ![image-20210923155839690](imgs/image-20210923155839690.png) |







## Methodology

![image-20210922172310509](imgs/image-20210922172310509.png)

### Supervised Learning

![image-20210922172542275](imgs/image-20210922172542275.png)

### Weekly Supervised Learning

![image-20210922172625620](imgs/image-20210922172625620.png)

### Unsupervised Learning

![image-20210922172648473](imgs/image-20210922172648473.png)

### Transfer Learning









---

**Reference**

[^1]: Srinidhi, Chetan L., Ozan Ciga, and Anne L. Martel. "Deep neural network models for computational histopathology: A survey." *Medical Image Analysis* (2020): 101813. [[paper]](https://arxiv.org/pdf/1912.12378.pdf)

[^2]: Deng, Shujian, et al. "Deep learning in digital pathology image analysis: A survey." *Frontiers of medicine* (2020): 1-18. [[paper]](https://journal.hep.com.cn/fmd/EN/article/downloadArticleFile.do?attachType=PDF&id=27600)

[^3]: Li, Chen, et al. "A State-of-the-art Survey of Artificial Neural Networks for Whole-slide Image Analysis: from Popular Convolutional Neural Networks to Potential Visual Transformers." *arXiv preprint arXiv:2104.06243* (2021). [[paper]](https://arxiv.org/pdf/2104.06243.pdf)

