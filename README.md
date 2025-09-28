# Qwen3-from-scratch

Welcome! This project is a from-scratch implementation of the core architecture behind Qwen 3, a state-of-the-art large language model series by Alibaba Cloud. Here, every line is written and explained for clarity and intuition. The aim is not just to build a model, but to deeply understand how LLMs work—mechanistically, mathematically, and in code.

## What is Qwen 3?

Qwen 3 sets new benchmarks in reasoning, multilingual ability, and efficient scaling. Its architecture pushes the frontier of transformer design, introducing innovations such as grouped query attention (GQA), SwiGLU activations, and hybrid inference modes. This repo is both a research companion and an educational resource: you’ll see gradients flow, weights update, and intelligence emerge, step by step.

---

## Key Features and Innovations

- **Modern Transformer Backbone**  
  Implements decoder-only transformers with multi-head self-attention, layer normalization, and the proven tricks from the latest LLM research.

- **Grouped Query Attention (GQA)**  
  Instead of one key/value head per query head, Qwen 3 shares 4 key/value heads across 8 query heads, halving KV cache memory and accelerating inference—critical for real-world deployments.

- **SwiGLU Feedforward Layers**  
  Uses the SwiGLU activation for improved expressivity and optimization stability, as found in the latest high-end models.

- **Rotary Positional Embeddings (RoPE)**  
  Elegant, efficient, and now the default in all top models. RoPE encodes position by rotating query/key vectors, enabling extrapolation to long sequences.

- **Sliding Window Attention Ready**  
  The code is structured to allow easy toggling between full and sliding window attention, supporting long-context training and inference.

- **Muon Optimizer (Experimental)**  
  Implements the cutting-edge Muon optimizer for 2D matrices. This optimizer orthonormalizes updates (via Newton-Schulz) to eliminate pathological gradient scaling, enabling higher learning rates and faster convergence in practice. AdamW remains available for comparison.

- **Transparent Hyperparameterization**  
  Every architectural and training hyperparameter is exposed, explained, and can be tuned for your hardware budget—batch size, sequence length, number of layers, attention heads, etc. Emphasis is placed on memory-reducing tricks and training stability.

- **Educational Focus**  
  Every core submodule—attention, feedforward, optimizer, data pipeline—is self-contained and documented, with references to the original papers. This project is made to be hackable, readable, and a starting point for your own research.

---

## Data and Tokenization

- Uses the `small-lm-corpus` from HuggingFace, a clean and compact dataset ideal for rapid experiments and prototyping.
- Tokenization is handled with an efficient, prebuilt tokenizer. Data is streamed and batched via a minimal, readable PyTorch dataset class.
- The code is designed to make it trivial to swap in your own corpus or tokenizer.

---

## Training and Evaluation

- Implements a full training loop with learning rate scheduling, weight decay, dropout, and gradient clipping.
- Supports gradient accumulation for training large batches on limited hardware.
- Logs training loss, validation loss, perplexity, and accuracy at customizable intervals.
- Best checkpoints are saved for reproducible results and future inference.

---

## Inference

- Provides fast, modular text generation routines with temperature, top-k, and top-p (nucleus) sampling.
- Interactive prompt mode: talk to your model and see its knowledge emerge after just minutes of training.
- All inference logic is explicit and hackable—no hidden calls, no magic.

---

## A Note on Philosophy

This project is for those who want to **see under the hood**—to break, fix, and extend the engine of LLMs. No proprietary glue, no unexplained “magic numbers.” If you want to push boundaries, experiment with optimizers, change attention mechanisms, or just understand what makes modern LLMs tick, you’re in the right place.

If you’re familiar with Andrej Karpathy’s style: clear code, careful structure, and relentless curiosity—this project is for you.

---

*Made by [drmarcoaron](https://github.com/drmarcoaron). For research, for learning, for fun. Enjoy!*
