# Stable Diffusion Anime LoRA Fine-tuning

Fine-tuning Stable Diffusion v1.5 on anime face images using LoRA (Low-Rank Adaptation) to generate anime-styled images.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Ragul2526/stable-diffusion-anime-finetune-lora/blob/main/anime_lora_finetune.ipynb)

---

## What is LoRA?

LoRA (Low-Rank Adaptation) is a parameter-efficient fine-tuning technique that trains only a small fraction of the model's parameters instead of the full model. This makes fine-tuning possible on a free Google Colab T4 GPU.
Full fine-tuning  →  860M parameters trained
LoRA fine-tuning  →  797K parameters trained (0.09%)

---

## Dataset

**huggan/anime-faces** from HuggingFace — 21,551 anime face images, no login required, loads automatically when you run the notebook.

### Sample images from dataset
<img width="1473" height="593" alt="image" src="https://github.com/user-attachments/assets/4b0b0456-ffa8-40d7-b3c5-87e960ba8c96" />

---

## Results

### Base Stable Diffusion vs LoRA Fine-tuned
<img width="957" height="1965" alt="image" src="https://github.com/user-attachments/assets/5b934484-924d-4e18-b4d3-c20ecc0d413e" />

The LoRA fine-tuned model shows clear style transfer towards anime aesthetics:
- Larger, more expressive eyes
- Softer facial features
- Characteristic anime color palette

---

## How to run

1. Click the **Open in Colab** badge above
2. Run all cells from top to bottom
3. Training takes ~90+ minutes per epoch on Colab free T4 GPU
4. LoRA weights are saved to your Google Drive at `/content/drive/MyDrive/lora-anime-output`

> No API keys or accounts needed — dataset loads automatically from HuggingFace

---

## Saved Weights
LoRA weights are saved to Google Drive after training. To load and 
continue fine-tuning or generate images without retraining, mount 
your Drive and load from:
/content/drive/MyDrive/lora-anime-output

---

## Model details

| Setting | Value |
|---------|-------|
| Base model | runwayml/stable-diffusion-v1-5 |
| Fine-tuning method | LoRA |
| LoRA rank | 4 |
| LoRA alpha | 32 |
| Target layers | Attention (to_k, to_q, to_v, to_out) |
| Dataset | huggan/anime-faces (5000 images used) |
| Epochs | 1 |
| Batch size | 2 |
| Learning rate | 1e-4 |
| Image resolution | 512×512 |
| Training hardware | Google Colab T4 GPU |

---

## Observations
- Trained for 1 epoch on 5000 images
- LoRA model shifts towards chibi/moe anime style from the dataset
- Slight blurriness due to low resolution (64×64) source images upscaled to 512×512

## Limitations
- Source dataset images are 64×64 — upscaling introduces blur
- 1 epoch is not enough for full convergence

## Future improvements
- Train on higher resolution dataset
- Increase epochs to 3-5
- Experiment with higher LoRA rank (r=8 or r=16)
- Add negative prompts for better quality outputs

---

## Requirements
All dependencies are installed automatically in the notebook:
