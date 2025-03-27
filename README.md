
# Introducing StoryMoE - A Smaller MoE based Language Model for Bedtime Stories! 

- So, I trained a MoE based a 124M (8x12M) architecture I coded from ground up to build a small instruct model, going through the below-mentioned stages from scratch.
- Trained on TiyStories dataset form HuggingFace consisting of 1M tokens for a total of 14000 steps



 ###  Pretraining

#### Dataset

 - I used the [TinyStories](https://huggingface.co/datasets/roneneldan/TinyStories) dataset from HuggingFace.

  1) Train dataset - 2 M records approx
  2) Val dataset - 26K records approx



---

####  ModelArgs (Hyperparameters)
# Model Configuration (`ModelArgs`)

This dataclass defines hyperparameters and configuration settings for a neural network model, optimized for modern deep learning tasks.

## Hyperparameters Overview

### Architecture
| Parameter | Default | Description |
|-----------|---------|-------------|
| `block_size` | 256 | Context window length for sequential data |
| `embeddings_dims` | 512 | Dimension size for embeddings |
| `no_of_heads` | 8 | Number of attention heads in multi-head attention |
| `no_of_decoder_layers` | 8 | Number of transformer decoder layers |
| `vocab_size` | 32768 | Vocabulary size (recommended as power of 2) |

### Training
| Parameter | Default | Description |
|-----------|---------|-------------|
| `epochs` | 4 | Total training epochs |
| `batch_size` | 64 | Samples per batch |
| `val_epochs` | 2 | Validation frequency (in epochs) |
| `clip` | 1.0 | Gradient clipping threshold |

### Regularization
| Parameter | Default | Description |
|-----------|---------|-------------|
| `attn_dropout` | 0.1 | Dropout probability for attention layers |
| `dropout` | 0.1 | General dropout probability |

### Optimization
| Parameter | Default | Description |
|-----------|---------|-------------|
| `max_lr` | 1e-4 | Maximum learning rate |
| `weight_decay_optim` | 0.01 | L2 regularization strength |
| `beta_1` | 0.9 | AdamW first momentum factor |
| `beta_2` | 0.95 | AdamW second momentum factor |

### Mixture-of-Experts (MoE)
| Parameter | Default | Description |
|-----------|---------|-------------|
| `experts` | 8 | Total number of experts in MoE layer |
| `top_experts` | 2 | Number of active experts per token |
| `noisy_topk` | False | Enable noisy top-k expert selection |

### Hardware
| Parameter | Default | Description |
|-----------|---------|-------------|
| `device` | 'cuda' | Training accelerator (GPU/CPU) |
| `dtype` | auto | Floating precision (bfloat16/float16) |
| `use_checkpointing` | True | Enable gradient checkpointing |


 - Used P100 on Kaggle
---

#### Frameworks:
**Pytorch**


--- 

#### Epochs/Steps
- Iterations (train) = 14k 

- Val iterations = every 50 steps
---

#### Losses
- Train loss - 2.08

- Val loss - 1.7

---

#### Screenshots of the loss curves

- Loss Curves (Train and Val)

![Loss Curves (Train and Val)](data/loss.jpg)

--- 
#### Output

```python
/data/generations.txt
```

---

<!-- ### Local setup


### Requirements



```python
git [clone the repo](https://github.com/YuvrajSingh-mist/StoryLlama.git)
cd StoryLlama
bash ./install.sh

```
- A wandb.ai account for plotting graphs for your loss curves

- On your terminal run
```python
wandb login
```

- Enter the api key and follow the instructions and once you are succesfully logged in follow the given steps


- Download the model

```python
cd gradio/

python app.py
```


---

### Running 


#### Training a model

- Kindly change 'device' to any of your available cuda gpus.

To run:

```python
bash ./install.sh
```

```python
torchrun --standalone --nproc_per_node=gpu trainer.py \
    --epochs 10 \
    --block_size 256 \
    --batch_size 128 \
    --embeddings_dims 768 \
    --attn_dropout 0.2 \
    --no_of_heads 12 \
    --dropout 0.2 \
    --val_epochs 3 \
    --max_lr 5e-4 \
    --no_of_decoder_layers 6 \
    --weight_decay_optim 0.01 \
    --beta_1 0.85 \
    --beta_2 0.99 \
    --clip 0.5 \
    --device "cuda" \
    --no_kv_heads 4 \
    --vocab_size 50257 \
    --eps 1e-6 \
    --dtype "float16" \
    --save_checkpoint_dir "model_checkpoints" \
    --prompt "Once upon a time" \
    --save_checkpoint_iter 100 \
    --total_iters 5000 \
    --eval_iters 200 \
    --eval_check 500 \
    --warmup_iters 1000 \
    --min_lr 1e-5 \
    --lr_decay_iters 2000 \
    --total_batch_size 262144 \
    --micro_batch_size 128 \
    --gradient_accumulation_steps 4

```
--standalone - if all the gpu are on one server
--npro_per_node - number of gpus available and use the keyword gpu to use all

#### Inference on a model

```python 
python inference.py --prompt "Once upon a time" --max_length 100 --temperature 0.8 --topk 50 
```
 -->
