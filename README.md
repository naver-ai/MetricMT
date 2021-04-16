# Reward Optimization for Neural Machine Translation with Learned Metrics

This is our official code repository of our proposed NMT training algorithm, MetricMT. ([arxiv](https://arxiv.org/abs/2104.07541))

**Authors**: Raphael Shu, Kang Min Yoo, Jung-Woo Ha (NAVER AI Lab)

## About the Paper ##

* We propose a *constrastive-margin loss* that enables fast and stable reward optimization with large NMT and metric models. 
* On multiple translation pairs, We found that the reward optimization with BLEURT is able to boost the score significantly, allowing the NMT to generate more adaquate and fluent translations and score better in human evaluations.

Neural machine translation (NMT) models are conventionally trained with token-level negative log-likelihood (NLL), which does not guarantee that the generated translations will be optimized for a selected sequence-level evaluation metric. Multiple approaches are proposed to train NMT with BLEU as the reward, in order to directly improve the metric. However, it was reported that the gain in BLEU does not translate to real quality improvement, limiting the application in industry. 

Recently, it became clear to the community that BLEU has a low correlation with human judgment when dealing with state-of-the-art models. This leads to the emerging of model-based evaluation metrics. [These new metrics are shown to have a much higher human correlation.](https://ai.googleblog.com/2020/05/evaluating-natural-language-generation.html)

In our work, we investigate whether it is beneficial to optimize NMT models with the state-of-the-art model-based metric, BLEURT. We propose a contrastive-margin loss for fast and stable reward optimization suitable for large NMT models:

![Contrastive-Margin Loss](https://user-images.githubusercontent.com/73585370/114983109-2cacbd80-9ecb-11eb-9f04-661b1d468f03.png)

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
