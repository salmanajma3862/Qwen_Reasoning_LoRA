[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/salmanajma3862/Qwen_Reasoning_loRA/blob/main/Qwen_Reasoning_Finetuning.ipynb)

🚀 Qwen2.5-3B Reasoning Fine-Tuning with Unsloth
This repository contains a Google Colab notebook to fine-tune Qwen2.5-3B-Instruct into a reasoning model (O1-style). By using LoRA (Low-Rank Adaptation) and the Unsloth library, we achieve 2x faster training and 70% less VRAM usage, making it possible to train on a free T4 GPU.

📌 Project Overview
The goal of this project is to teach a smaller language model to "think" before responding. We use a ChatML-style prompt template that forces the model to generate a Chain-of-Thought (CoT) inside <think>...</think> tags before providing the final answer.

Model: unsloth/Qwen2.5-3B-Instruct

Dataset: FreedomIntelligence/medical-o1-reasoning-SFT (subset of 500 samples)

Optimization: 4-bit quantization via BitsAndBytes & Unsloth.

Method: Parameter-efficient fine-tuning (PEFT) using LoRA.

🛠️ Key Features
Unsloth Integration: Significantly reduces the hardware barrier for LLM fine-tuning.

Custom Prompt Template: Structured specifically for reasoning tasks:

Plaintext

<|im_start|>system
You are a helpful assistant that thinks step-by-step before answering.<|im_end|>
<|im_start|>user
{Question}<|im_end|>
<|im_start|>assistant
<think>
{Reasoning}
</think>
{Response}<|im_end|>
Memory Efficient: Fits comfortably within 16GB VRAM (T4 GPU).

🚀 How to Run
1. Open in Google Colab
Click the "Open in Colab" badge at the top of this README to launch the notebook directly.

2. Configure Hardware
Ensure your Colab runtime is set to T4 GPU (or better).

3. Installation & Training
The notebook handles the installation of:

unsloth

xformers

trl, peft, accelerate, and bitsandbytes

The training script is set to 60 steps for demonstration but can be increased for higher accuracy.

📈 Example Result
User: Alice knows that Bob knows that Carol is wrong...

Model Output:

<think>

Analyze Alice's knowledge: Alice knows (Bob knows Carol is wrong).

Analyze Carol's knowledge: Carol knows (Bob doesn't know if Alice is lying).

Evaluation: ... </think> Based on the logic of mutual knowledge, Alice cannot definitively know that Carol knows the truth because...

📝 Technical Details (LoRA Config)
Rank (r): 16

Target Modules: q_proj, k_proj, v_proj, o_proj, gate_proj, up_proj, down_proj

Alpha: 16

Learning Rate: 2e-4

🤝 Contributing

Feel free to fork this repo, open issues, or submit PRs if you have suggestions for better reasoning datasets or hyperparameter optimizations!

🔗 Connect with me on LinkedIn

[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/salman-ajmal2/)
