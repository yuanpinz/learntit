# Co-teaching: Robust Training of Deep Neural Networks with Extremely Noisy Labels
## Terminology

- **memorization effects**

  - Deep models can memorize easy instances first, and gradually adapt to hard instances as training epochs become large
  - This phenomenon does not change with the choice of training optimizations or network architectures 

  D. Arpit, S. Jastrz˛ebski, N. Ballas, D. Krueger, E. Bengio, M. Kanwal, T. Maharaj, A. Fischer, A. Courville, and Y. Bengio. A closer look at memorization in deep networks. In ICML, 2017.

  C. Zhang, S. Bengio, M. Hardt, B. Recht, and O. Vinyals. Understanding deep learning requires rethinking generalization. In ICLR, 2017

- Learning to teach

  Y. Fan, F. Tian, T. Qin, J. Bian, and T. Liu. Learning to teach. In ICLR, 2018.

- boosting

   Y. Freund and R. Schapire. A desicion-theoretic generalization of on-line learning and an
  application to boosting. In European COLT, 1995.

   Y. Freund, R. Schapire, and N. Abe. A short introduction to boosting. Journal-Japanese Society
  For Artificial Intelligence, 14(771-780):1612, 1999.

- active learning

  D. Cohn, Z. Ghahramani, and M. Jordan. Active learning with statistical models. Journal of
  Artificial Intelligence Research, 4:129–145, 1996.

- Co-training

  A. Blum and T. Mitchell. Combining labeled and unlabeled data with co-training. In COLT, 1998.

## Model

- each network views its small-loss instances (like self-paced MentorNet) as the useful knowledge

- **Q1. Why can sampling small-loss instances based on dynamic R(T) help us find clean instances?** 
  - Intuitively, when labels are correct, small-loss instances are more likely to be the ones which are correctly labeled
  - “memorization” effect will help: Namely, on noisy data sets, even with the existence of noisy labels, deep networks will learn clean and easy pattern in the initial epochs. So, they have the ability to filter out noisy instances using their loss values at the beginning of training.
  - keep more instances in the mini-batch at the start
  - keep clean instances and drop those noisy ones before our networks memorize them
- **Q2. Why do we need two networks and cross-update the parameters?**
  - boosting and active learning are sensitive to outliers and noise, and a few wrongly selected instances can deteriorate the learning performance of the whole model 
  - Intuitively, different classifiers can generate different decision boundaries and then have different abilities to learn
  - these two networks will adaptively correct the training error by the peer network if the selected instances are not fully clean

