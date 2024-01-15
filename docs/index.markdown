---
layout: default
---

We introduce <span class="sys-name">Prometheus-Vision</span>, an evaluator Vision-Language Model (VLM) that 1) is **open-source**, 2) offers **reproducible** evaluation, and 3) is **inexpensive** to use. We construct <span class="sys-name">Perception-Collection</span>, the first multimodal feedback dataset for training an evaluator VLM, which includes 15K **fine-grained scoring criteria** defined for each instance. <span class="sys-name">Prometheus-Vision</span> trained on <span class="sys-name">Perception-Collection</span> shows high correlation with human evaluators and GPT-4V, paving the way for accesible and transparent evaluation of VLMs.

<br/>

## VLM-as-a-Judge for Fine-Grained Evaluation

Recent VLMs exhibit impressive visual instruction-following capabilities. To assess and compare the quality of VLM-generated outputs, we utilize VLMs as evaluator of VLMs, naming the approach as VLM-as-a-Judge. 

{: .sys-img}
![vlm_as_a_judge](/assets/img/vlm_as_a_judge.svg)  

Traditional metrics for VLM evaluation measure the similarity between a response and the ground-truth answer. However, such automatic metrics fail to capture the rich context within the output. Also, these metrics do not explain what is missing or present in the response.  

An evaluator VLM can adhere to specific criteria of interest to focus on nuanced details in the visual context and instruction. Moreover, it can provide detailed language feedback that helps the user understand the reasoning behind the scoring.  

<br/>


## Multimodal Feedback Data

The <span class="sys-name">[Perception-Collection](https://huggingface.co/datasets/kaist-ai/Perception-Collection)</span> dataset is targeted for fine-grained multimodal feedback generation. Each instance consists of 5 input components: an instruction, a real-world image, a response to evaluate, a customized score rubric, and a reference answer. Based on this, an evaluator VLM is trained to generate a language feedback and a score decision.

{: .sys-img}
![perception_collection](/assets/img/prometheus_vision_components.svg)  

We collect 5K real-world images sampled from the [COCO dataset](https://cocodataset.org/#home) and the [MMMU benchmark](https://arxiv.org/abs/2311.16502). Then, we augment the data manually and using GPT-4V through 4 stages:

{: .text-left}
1. Hand-craft 50 seed score rubrics
2. Brainstorm and refine 15K fine-grained score rubrics
3. Augment 30K instructions and reference answers related to the score rubric
4. Augment 150K responses and language feedback for training 

{: .img-right}
![perception_collection_stats](/assets/img/perception_collection_stats.png)  

We also release a held-out test set of the <span class="sys-name">Perception-Collection</span> called <span class="sys-name">[Perception-Bench](https://huggingface.co/datasets/kaist-ai/Perception-Bench)</span>.

<br/>

## Performance of <span class="sys-name">Prometheus-Vision</span>

Using the <span class="sys-name">Perception-Collection</span>, we use [LLaVA-1.5](https://arxiv.org/abs/2310.03744) (7B & 13B) as our backbone model and train <span class="sys-name">Prometheus-Vision</span> ([7B](https://huggingface.co/kaist-ai/prometheus-vision-7b-v1.0) & [13B](https://huggingface.co/kaist-ai/prometheus-vision-13b-v1.0)). Through experiments, we demonstrate that <span class="sys-name">Prometheus-Vision</span> can be an effective open-source alternative to using human or GPT-4V for VLM evaluation.

<br/>

### Simulating Human Evaluators

<span class="sys-name">Prometheus-Vision</span> shows high correlation with human evaluators on instances with real-world images. Also, <span class="sys-name">Prometheus-Vision</span> 13B's feedback is as good as or better than GPT-4V's feedback 57.78% of the time.

{: .img-left}
![human_corr](/assets/img/human_corr.svg)

{: .img-right}
![pairwise_win_rate](/assets/img/pairwise_win_rate.svg)

<br/>

### Simulating GPT-4V

<span class="sys-name">Prometheus-Vision</span> demonstrates the highest correlation with GPT-4V among open-source VLMs and outperforms GPT-3.5-Turbo and GPT-4 (LM-as-a-Judge) in LLaVA-Bench and <span class="sys-name">Perception-Bench</span>. 

{: .sys-img}
![instructionfollowing_results](/assets/img/instructionfollowing_results.png)

------

## Bibtex
If you find our work useful in your work, please consider citing our paper:

<pre>
@misc{lee2024prometheusvision,
      title={Prometheus-Vision: Vision-Language Model as a Judge for Fine-Grained Evaluation}, 
      author={Seongyun Lee and Seungone Kim and Sue Hyun Park and Geewook Kim and Minjoon Seo},
      year={2024},
      eprint={2401.06591},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
</pre>

------

{: .logos}
[![Logo of KAIST](/assets/img/kaist_logo.png)](https://kaist.ac.kr)
[![Logo of LKLab](/assets/img/lklab_logo.jpg)](https://lklab.kaist.ac.kr/)
[![Logo of NAVER AI LAB](/assets/img/naver_ai_lab_logo.png)](https://www.facebook.com/NAVERAILAB)
[![Logo of NAVER Cloud](/assets/img/naver_cloud_logo.png)](https://www.navercloudcorp.com/lang/en/)

<!-- {: .center .acknowledgement}
This research was supported by the **KAIST-NAVER Hypercreative AI Center**. -->