# [Rephrasing the Web: A Recipe for Compute and Data-Efficient Language Modeling](https://arxiv.org/abs/2401.16380)

## Summary

Using an off-the-shelf instruction-tuned model, they paraphrase web documents to be in specific styles like Wikipedia or in QA-format and use this data to pretrain an LLM. This speeds up pretraining by a factor of three compared to C4 (not taking into account the compute required to generate the data).

They ran a number of ablations:
### Paraphrase styles
- Easy (toddler-level)
- Medium (Wikipedia-level)
- Hard (Terse and abstruse)
- QA (conversation QA format)
QA and Medium perform best, while no paraphrasing performs worst

### Model
- finetuned T5-base (220M)
- Qwen-1.8B
- Mistral-7B
- Vicuna-13B
Qwen, Mistral and Vicuna all perform quite similarly, with Mistral slightly on top, whereas T5 is significantly worse

### Data mix
- They mix the generated data with the original data to increase diversity. This improves performance on benchmarks
- Adding in the QA data results in a significant improvement on perplexity, as well as 0-shot QA tasks (obviously)
- A ratio of 1:2 C4 to synthetic is slightly better than 1:1

## Relevance to survey topic (1-5)

Relevance: 4

## Algorithms

NA

## Benchmarks
Perplexity on
- Wiki
- OWT2
- Books2
- Books
- ArXiv
- StackX
- Github
- Math
- HNews
- Enron
- Pubmed-C
- Ubuntu
- Pubmed-A
- FreeLaw
- NIH
- USPTO
- PG-19
- Phil
- Youtube
- OpenSubs
- CC

General knowledge benchmarks
- ARC Easy
- BoolQ
- Winogrande
- PIQA
- HellaSwag
- TruthfulQA
- OpenBookQA
- LogiQA-2

Specialised knowledge benchmarks
- ARC Challenge
- SciQ
- PubMedQA
- MathQA
- MMLU


## Other comments

Synthetic data seems to be the future for pretraining data as well. Their results show that "in many cases it may not be possible to offset the performance advantage of pre-training on synthetic data by merely training on more real data"

Currently their method is limited to shorter samples: "each example has a maximum of 300 tokens, which was decided based on our empirical observation that asking an LLM to rephrase more than 300 tokens, often led to loss of information."
