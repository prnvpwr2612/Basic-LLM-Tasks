
# 🚀 QLoRA Fine-tuned Model - Deployment Guide

## Quick Start

from transformers import AutoTokenizer, AutoModelForCausalLM
from peft import PeftModel

Load base model
base_model = AutoModelForCausalLM.from_pretrained("microsoft/Phi-3-mini-4k-instruct")
tokenizer = AutoTokenizer.from_pretrained("microsoft/Phi-3-mini-4k-instruct")

Load fine-tuned adapters
model = PeftModel.from_pretrained(base_model, "/path/to/qlora/adapters")

Generate text
def generate_response(prompt, max_length=200):
inputs = tokenizer(prompt, return_tensors="pt")
outputs = model.generate(**inputs, max_length=max_length, do_sample=True)
return tokenizer.decode(outputs, skip_special_tokens=True)

Example usage
response = generate_response("Explain machine learning in simple terms:")
print(response)


## Model Specifications
- **Memory Requirements**: ~4.6GB GPU memory
- **Inference Speed**: ~1.2s per response (T4 GPU)
- **Max Context**: 4096 tokens
- **Fine-tuned for**: Instruction following tasks

## Performance Characteristics
- **Training Loss**: 2.85
- **Validation Loss**: 2.78
- **Parameter Efficiency**: 0.88% trainable parameters
- **Memory Efficiency**: 75% reduction vs full precision

## Use Cases
- Question answering
- Code explanation
- Educational content generation
- General instruction following

## Limitations
- Limited to instruction-following format
- Context limited to 4K tokens
- May require prompt engineering for optimal results
