# MetricMT - Reward Optimization for Neural Machine Translation with Learned Metrics

This is our official code repository. To read the paper, please see ([arxiv](https://arxiv.org/abs/2104.07541)).

**Authors**: Raphael Shu, Kang Min Yoo and [Jung-Woo Ha](https://github.com/jungwoo-ha) (NAVER AI Lab)

## What is it about

In short, we optimize NMT models with the state-of-the-art metric, [BLEURT](https://ai.googleblog.com/2020/05/evaluating-natural-language-generation.html), and found the translations to have higher adequacy and coverage compared to both the baseline and models trained with BLEU.

In machine translation, BLEU has been a dominating evaluation metric for years. However, the criticism on BLEU dates back as early as 2006 [(Callison-Burch et al., 2006)](https://www.aclweb.org/anthology/E06-1032.pdf). The best overall paper of ACL 2020 [(Mathur, 2020)](https://www.aclweb.org/anthology/2020.acl-main.448.pdf) again shows that BLEU's correlation with human drops to zero or negative territory when comparing only a few top tier systems. The author calls for stopping the use of BLEU in the paper.

Recently, several model-based metrics are proposed (ESIM, Yisi-1, BERTScore, BLEURT). They are all using or building with BERT. These metrics typically achieve much higher human correlation by tuning themselves with human judgment data.

In our paper, we attempt to directly optimize NMT models with the state-of-the-art learned metric, BLEURT. The benefit is obvious, as BLEURT is tuned with human scores, it can potentially reflect human preference on translation quality. We want to know whether the training just changes the NMT parameter to hack the metric, or it yields meaningful improvement.

For reward optimization, we found a stable ranking-based sequence-level loss performs well and is suitable to use with large NMT and metric models.

## How it works

We propose to use the following *contrastive-margin loss*, which is a pairwise ranking loss that differentiates two candidates with the best and worst rewrad in a candidate space. The loss has the following form:

<p align="center">
   <img align="center" src="https://user-images.githubusercontent.com/1029280/114988251-173a9200-9ed1-11eb-8180-b59d839a876a.png" />
</p>

Here, ![ql_69480ecf125de512baaae19eee3ac7ab_l3](https://user-images.githubusercontent.com/1029280/114988978-edce3600-9ed1-11eb-87c8-6331ed4b661f.png) is the reward function. After we obtain a set of candidates using beam search,  ![ql_c06661d77e2e10c2d1f7b60157aa98de_l3](https://user-images.githubusercontent.com/1029280/114988983-eeff6300-9ed1-11eb-832f-cc99d3bc1b58.png) denotes the candidate with the best reward. ![ql_9fbd1e8e69cb5b6061fb4bf273485b6d_l3](https://user-images.githubusercontent.com/1029280/114988981-ee66cc80-9ed1-11eb-9986-51154469fbc8.png) is the candidate with the worst reward.

This reward optimizing loss has a lower memory footprint comparing with risk minimization loss, and is more stable than REINFORCE and max-margin loss. In the paper, we show this loss can effectively optimize both smoothed BLEU and BLEURT as rewards.


## Results

We perform automatic and human evaluations to compare optimized models with the baselines. The experiments are conducted on German-English, Romanian-English, Russian-English and Japanese-English datasets. They are all to-English datasets as the pretrained BLEURT is for English language.

The results are interesting. In three over four language pairs, we found BLEURT is significantly increased after optimizing it, however, this optimization hurts BLEU. Here are the automatic scores:

<p align="center">
<img width="663" alt="Automatic Evaluation" src="https://user-images.githubusercontent.com/1029280/114991517-a1382a00-9ed4-11eb-94ed-e21fb727ced1.png">
</p>

Then we performed pairwise human evaluation on three criteria: adequacy, fluency and coverage. These are the results

<p align="center">
<img width="607" alt="Human Evaluation" src="https://user-images.githubusercontent.com/1029280/114990716-c4160e80-9ed3-11eb-9c13-e6f5fab084a5.png">
</p>

We can see that the BLEURT optimized model tends to have better adequacy and coverage, and it performs better than models trained with smoothed BLEU. For fluency, annotators didn't find much difference overall, which may indicate the NLL loss is already good at improving fluency. Please check our paper for more details. 

## Getting Started ##

Our method can be applied to any MT metrics (including non-differentiable ones) for improving human perceived quality. We invite others to try our method with various metrics!

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
