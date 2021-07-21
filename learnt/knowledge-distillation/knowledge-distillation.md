# Knowledge Distillation

## Survey

[Gou J, Yu B, Maybank S J, et al. Knowledge distillation: A survey[J]. International Journal of Computer Vision, 2021, 129(6): 1789-1819.](https://arxiv.org/abs/2006.05525)

## Repos

[FLHonker/Awesome-Knowledge-Distillation](https://github.com/FLHonker/Awesome-Knowledge-Distillation)

[dkozlov/awesome-knowledge-distillation](https://github.com/dkozlov/awesome-knowledge-distillation)

[peterliht/knowledge-distillation-pytorch](https://github.com/peterliht/knowledge-distillation-pytorch)

[AberHu/Knowledge-Distillation-Zoo](https://github.com/AberHu/Knowledge-Distillation-Zoo)

## Note

Knowledge Distillation is one of model compression and acceleration techniques. Other techniques include 1) Parameter pruning and sharing; 2) Low-rank factorization; 3) Transferred compact convolutional filters

The framework of KD is shown below.

![kd-structure](imgs/image-20210721153844316.png)

### Knowledge

![image-20210721155028916](imgs/image-20210721155028916.png)

#### Response-Based Knowledge

- use the last output layer of the teacher model
- Distillation loss is defined as $L_{ResD}(z_t,z_s)= \mathcal{L}_{R}(z_t,z_s)$​​

 
