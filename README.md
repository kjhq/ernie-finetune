# ernie-finetune

lora fine-tuning of baidu ernie-4.5 0.3b using unsloth + trl. knowledge distillation from gemini and claude.

![python](https://img.shields.io/badge/python-3776AB?style=flat-square&logo=python&logoColor=white)
![pytorch](https://img.shields.io/badge/pytorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![huggingface](https://img.shields.io/badge/huggingface-FFD21E?style=flat-square&logo=huggingface&logoColor=black)
![unsloth](https://img.shields.io/badge/unsloth-18181B?style=flat-square)

`pytorch` `unsloth` `lora` `trl`

---

## overview

supervised fine-tuning (sft) of ernie-4.5 for conversational ability using instruction-following data from multiple sources.

---

## datasets

| dataset | source | size |
|---------|--------|------|
| gemini 3 flash preview | TeichAI/gemini-3-flash-preview-1000x | ~1,000 |
| claude haiku 4.5 | TeichAI/claude-haiku-4.5-1700x | ~1,700 |
| gemini 2.5 flash lite | TeichAI/gemini-2.5-flash-lite-2509-preview-1000x | ~1,000 |

**total**: ~3,700 examples (90% train / 10% eval)

---

## model

**base**: baidu ERNIE-4.5-0.3B-Base-PT

| parameter | value |
|-----------|-------|
| architecture | Ernie4_5ForCausalLM |
| hidden size | 1,024 |
| layers | 18 |
| attention heads | 16 |
| max sequence length | 131,072 |
| dtype | bfloat16 |

### lora config

| parameter | value |
|-----------|-------|
| rank (r) | 16 |
| alpha | 64 |
| target modules | q/k/v/o_proj, gate/up/down_proj |

---

## training

| parameter | value |
|-----------|-------|
| optimizer | adamw 8-bit |
| learning rate | 5.0 × 10⁻⁵ |
| scheduler | cosine annealing |
| epochs | 5 |
| effective batch size | 64 |
| best eval loss | **1.289** (step 100) |

---

## dependencies

- unsloth — fast fine-tuning + flash attention
- transformers, trl, torch, datasets

see training notebook for full list.

---

## references

- [ERNIE-4.5 on huggingface](https://huggingface.co/baidu/ERNIE-4.5-0.3B-Base-PT)
- [unsloth](https://github.com/unslothai/unsloth)
- [trl docs](https://huggingface.co/docs/trl/)

---

<div align="center">

built by [kjhq](https://kjhq.dev) · [@kjhqdev](https://x.com/kjhqdev)

</div>
