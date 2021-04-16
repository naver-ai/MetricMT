# MetricMT - Reward Optimization for Neural Machine Translation with Learned Metrics

This is our official code repository. To read the paper, please see ([arxiv](https://arxiv.org/abs/2104.07541)).

**Authors**: Raphael Shu, Kang Min Yoo, Jung-Woo Ha (NAVER AI Lab)

## What is it about

In short, we optimize NMT models with the state-of-the-art metric, [BLEURT](https://ai.googleblog.com/2020/05/evaluating-natural-language-generation.html), and found the translations to have higher adequacy and coverage compared to both the baseline and models trained with BLEU.

In machine translation, BLEU has been a dominating evaluation metric for years. However, the criticism on BLEU dates back as early as 2006 [(Callison-Burch et al., 2006)](https://www.aclweb.org/anthology/E06-1032.pdf). The best overall paper of ACL 2020 [(Mathur, 2020)](https://www.aclweb.org/anthology/2020.acl-main.448.pdf) again shows that BLEU's correlation with human drops to zero or negative territory when comparing only a few top tier systems. The author calls for stopping the use of BLEU in the paper.

Recently, several model-based metrics are proposed (ESIM, Yisi-1, BERTScore, BLEURT). They are all using or building with BERT. These metrics typically achieve much higher human correlation by tuning themselves with human judgment data.

In our paper, we attempt to directly optimize NMT models with the state-of-the-art learned metric, BLEURT. The benefit is obvious, as BLEURT is tuned with human scores, it can potentially reflect human preference on translation quality.

For reward optimization, we found a stable ranking-based sequence-level loss performs well and is suitable to use with large NMT and metric models.

## How it works

We propose to use the following *contrastive-margin loss*, which is a pairwise ranking loss that differentiates two candidates with the best and worst rewrad in a candidate space. The loss has the following form:
<img align="center" src="https://user-images.githubusercontent.com/1029280/114988251-173a9200-9ed1-11eb-8180-b59d839a876a.png" />

Here, ![ql_69480ecf125de512baaae19eee3ac7ab_l3](https://user-images.githubusercontent.com/1029280/114988978-edce3600-9ed1-11eb-87c8-6331ed4b661f.png) is the reward function. After we obtain a set of candidates using beam search,  ![ql_c06661d77e2e10c2d1f7b60157aa98de_l3](https://user-images.githubusercontent.com/1029280/114988983-eeff6300-9ed1-11eb-832f-cc99d3bc1b58.png) denotes the candidate with the best reward. ![ql_9fbd1e8e69cb5b6061fb4bf273485b6d_l3](https://user-images.githubusercontent.com/1029280/114988981-ee66cc80-9ed1-11eb-9986-51154469fbc8.png) is the candidate with the worst reward.



## Results

We perform automatic and human evaluations to compare models trained with smoothed BLEU and BLEURT to the baseline models. The automatic evaluation results show that the reward optimization with BLEURT is able to increase the metric scores by a large margin, in contrast to limited gain when training with smoothed BLEU:

![Automatic Evaluation](https://user-images.githubusercontent.com/73585370/114983594-c5dbd400-9ecb-11eb-9996-dbe40010f57f.png)

Our human evaluation on multiple criteria also shows that models trained with BLEURT improve translations, making them appear more natural to human judges:

![Human Evaluation](https://user-images.githubusercontent.com/73585370/114983685-e1df7580-9ecb-11eb-8fde-a157de9b2aec.png)

Our method can be applied to any MT metrics (including non-differentiable ones) highly correlated with human judgments. We invite others to try our method with various metrics!

## Getting Started ##

We will release the source code to reproduce our method very soon. Stay tuned!

## Citing our Work ##

```
@article{shu2021reward,
    title={Reward Optimization for Neural Machine Translation with Learned Metrics},
    author={Shu, Raphael and Yoo, Kang Min and Ha, Jung-Woo},
    year={2021},
    journal={arXiv preprint arXiv:2104.07541},
}
```
