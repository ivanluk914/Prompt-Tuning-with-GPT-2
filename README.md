# Prompt Tuning with GPT-2

This repository contains an implementation of prompt tuning on GPT-2 to improve task-specific performance, using [PEFT](https://github.com/huggingface/peft) and Hugging Face's [transformers](https://huggingface.co/docs/transformers) library. The focus of this project is to explore lightweight fine-tuning techniques by training a small number of parameters while leveraging the pre-trained knowledge of large language models.

## What is Prompt Tuning?

Prompt tuning is a technique that trains a small number of parameters (virtual tokens) alongside existing pre-trained model parameters. Unlike traditional fine-tuning, it doesn't modify the entire model, making it a computationally efficient alternative while still enabling task-specific adaptation.

For this project:
- **Dataset**: Hugging Face dataset `fka/awesome-chatgpt-prompts`, which contains various task-specific prompt-response mappings.
- **Model**: GPT-2, used for causal language modeling (CLM).

## Key Features
1. **PEFT for Efficient Tuning**:
   - Only trains task-specific virtual tokens added to the original input sequence without updating GPT-2 parameters.
   - Reduces memory and resource requirements compared to full fine-tuning.

2. **Dynamic Configurations**:
   - Number of virtual tokens and epochs are easily adjustable for optimization.
   - Optimal configuration: 10 epochs and 20 virtual tokens.

3. **Evaluation**:
   - Qualitative evaluation based on contextual relevance, coherence, and adherence to prompt instructions.
   - Improvements observed over the base model in terms of dialog quality and task alignment.

## Methods

1. **Model Setup**:
    - Pre-trained **GPT-2** loaded via Hugging Face library.
    - Applied prompt tuning using the `PromptTuningConfig` and **PEFT** library.

2. **Configuration**:
    - Initial Configuration: 
      - Virtual tokens: 5 
      - Epochs: 5
    - Optimized Configuration:
      - Virtual tokens: 20 
      - Epochs: 10

3. **Training**:
    - Used Hugging Face's `Trainer` API to fine-tune the embeddings.
    - Optimization handled with the AdamW optimizer.

4. **Evaluation**:
    - Compared outputs of the base GPT-2 model with the fine-tuned version for qualitative improvements.

## Results
- Increasing epochs and the number of virtual tokens significantly improved model performance.
- **Initial Results** (5 epochs, 5 virtual tokens):
  - Model failed to produce coherent and task-relevant responses consistently.
- **Optimized Results** (10 epochs, 20 virtual tokens):
  - The tuned model displayed substantial improvements in fluency and adherence to input prompts, while remaining highly resource-efficient.

## Example
- Input Prompt: `"I want you to act as a rapper."`
- Base Model Output: A generic response with little task-specific context.
- Prompt-Tuned Model Output: More relevant outputs emphasizing a rap-style language.

## Installation

Ensure you have Python 3.9+ and install the required dependencies using pip:

```bash
pip install transformers peft datasets jupyter pandas
```

## Getting Started

To rerun the notebook or reproduce the results:
1. Clone this repository and navigate to the project directory.
2. Install the required dependencies listed above.
3. Open `prompt-tuning_with_gpt2.ipynb` in Jupyter Notebook or any IDE supporting `.ipynb` files.

## Dataset

The dataset is sourced from [Hugging Face](https://huggingface.co/datasets/fka/awesome-chatgpt-prompts), containing task-oriented prompts and expected responses. It is preprocessed using the tokenizer for GPT-2.


## References
- Hugging Face's Transformers ([link](https://huggingface.co/docs/transformers))
- Hugging Face PEFT Library ([link](https://github.com/huggingface/peft))
- Dataset: [awesome-chatgpt-prompts](https://huggingface.co/datasets/fka/awesome-chatgpt-prompts)
