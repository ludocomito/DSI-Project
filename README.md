# DSI-Project

![Cover](/assets/Project_cover.png)

## Introduction

In the modern landscape of the approaches to Information Retrieval, one of the most interesting solutions was published in the paper “*Transformer Memory as a Differentiable Search Index*”, where a single encoder-decoder architecture was trained in a multitask fashion to perform both indexing and retrieval of documents at the same time. The core idea is to map string queries directly to relevant docids, simplifying the retrieval process. With this project, we explore solutions based on the same DSI concept, but exploring new architectures and new training approaches to further deepen our understanding of the original paper and trying to clarify and uncover its strengths and weaknesses.

## Project description

The original DSI model is based on an encoder-decoder architecture, specifically a pre-trained T5 model. In the DSI approach, the model is trained to perform both indexing and retrieval at the same time in a multi-task fashion. We chose as our baseline the Okapi BM25 scores and as the base model to work with the T5, as specified in the aforementioned paper. From there we proceeded to experiment with the model’s architecture. More specifically we implemented the use of a model belonging to a recently presented class of models (Lamini) pretrained using knowledge distillation. Finally, we repeated the experiment again but with a custom encoder-decoder architecture. Furthermore we tried to tinker with various pre-processing strategies, first leveraging the multi-task approach as suggested by the referenced paper and, after that, following our own intuition applying data augmentation through query generation taking inspiration from.

## Results

The T5-base model scored 2.53% in MAP and 1.92% in Recall@10, and was outperformed by the Lamini Flan T5 in both metrics while utilizing the same hyperparameters (batch size 32 and learning rate 0.0005). As the Lamini Flan T5 model demonstrated better performances, we decided to conduct hyperparameter tuning on it, by experimenting with different batch sizes and learning rates. The best result was achieved with batch size 64 and learning rate 0.0005, achieving 3.34% MAP and 2.62% Recall@10.
Our hypothesis is that thanks to its extensive pre-training and the Lamini knowledge distillation techniques, the Lamini Flan T5 model has higher capabilities at dealing with multi-task learning tasks.

| Model                | Batch Size | Learning Rate | Mean Average Precision | Recall@10 |
|----------------------|------------|---------------|------------------------|-----------|
| BM-25 baseline       | 32         | 0.0005        | 0.003%                 | 0.002%    |
| T5 Base              | 32         | 0.0005        | 2.53%                  | 1.92%     |
| Lamini Flan T5       | 32         | 0.0005        | 3.31%                  | 2.62%     |
| Lamini Flan T5       | 32         | 0.0001        | 1.81%                  | 1.44%     |
| Lamini Flan T5       | 64         | 0.0005        | 3.34%                  | 2.62%     |
| Lamini Flan T5 QG    | 32         | 0.0005        | 3.31%                  | 2.61%     |
| BERT-GPT2 custom E-D | 32         | 0.0005        | 0.0019%                | 0.0016%   |
