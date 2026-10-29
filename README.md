# Testing Borealis 2 (preview) on 30 Norwegian prompts

This project is a small reproducible test of the [Borealis 2](https://huggingface.co/NbAiLab/borealis2-26b-a4b-preview-gguf) quantized preview model from NbAiLab at the National Library of Norway (Nasjonalbiblioteket). Nasjonalbiblioteket has been tasked by the Norwegian government with developing language models for the Norwegian language and culture, including Bokmål, Nynorsk, and Sámi versions. The preview model was run as a quantized GGUF (Q4_K_M) with llama.cpp on a Google Colab GPU and given 30 prompts about the Norwegian language and Norwegian society. The responses are published here unedited.

**Read the results:** [Testing Borealis 2 (preview) on 30 Norwegian prompts](https://hhval.github.io/borealis2/)

**Read the analysis:** [Language analysis of the Borealis 2 test set](https://hhval.github.io/borealis2/analysis.html)

## What's in this repo

| File | What it is |
|---|---|
| `borealis2.ipynb` | Colab notebook that downloads the model, checks that inference works, and runs the 30-prompt test set. |
| `borealis_test_prompts_v1.json` | The test set: 30 prompts in six categories. |
| `borealis2_results_20260921_164657.json` | Raw results from the run on 21 September 2026: every prompt, the model's response, token usage, and generation time. |
| `index.html` | The results presented as a readable page, grouped by category. |
| `analysis.md` | A read-through of the 30 responses: what the model does well, and the language errors and issues it makes. |
| `analysis.html` | The analysis presented as a readable page. |
| `LICENSE` | MIT License, covering the code. |
| `LICENSE-CONTENT` | CC BY 4.0, covering the test set and documentation. |

## The test set

The prompts are written in Norwegian and are meant to give a quick sense of how the model handles things that are specific to Norwegian and Norway, rather than of its general capability. Five prompts in each category:

| | Category | Tests |
|---|---|---|
| A | General Norwegian | Explaining everyday concepts and idioms («dugnad», «is i magen», «langstrakt land»). |
| B | Bokmål | Writing natural Bokmål, rewriting stiff text, spelling questions such as «hverken» vs. «verken». |
| C | Nynorsk | Writing natural Nynorsk and converting Bokmål to Nynorsk. |
| D | Grammar | Judging correctness, «da» vs. «når», definite and indefinite forms, sentence repair. |
| E | Terminology and style | Norwegian alternatives to anglicisms, «i forhold til», «ta en beslutning», «feedback» vs. «tilbakemelding». |
| F | Norwegian government and society | The political system (Stortinget, regjeringen, the courts), the Norwegian school, kommune and fylke, folketrygden and NAV, constitutional monarchy. |

The prompts are stored as a JSON list. To test your own prompts, use the same shape:

```json
[
  {
    "id": 1,
    "category": "A. General Norwegian",
    "prompt": "Forklar enkelt forskjellen mellom vær og klima."
  }
]
```

## Run settings

| Setting | Value |
|---|---|
| Model | `NbAiLab/borealis2-26b-a4b-preview-gguf`, file `*Q4_K_M.gguf` |
| Runtime | `llama-cpp-python` (CUDA 12.4 wheel), all layers on GPU, context 4096 |
| Hardware | Google Colab, NVIDIA L4 |
| Sampling | `max_tokens=2048`, `temperature=0.7`, `top_p=0.95` |
| Prompting | Each prompt sent as a single user message, no system prompt |

The run of 30 prompts took about 3 minutes 20 seconds and generated 12,228 tokens, roughly 61 tokens per second.

## Running it yourself

1. Open `borealis2.ipynb` in Google Colab and pick a GPU runtime with an L4 or better. The quantized model is too large for the free CPU runtime, so this needs Colab Pro or pay-as-you-go compute units.
2. Upload `borealis_test_prompts_v1.json` to `MyDrive/borealis2/` on your Google Drive. The notebook mounts Drive and reads the test set from there.
3. Run the cells top to bottom. The model weights download to the Colab VM's local disk; results are saved to `MyDrive/borealis2/borealis2_results_<timestamp>.json`.
4. The last cell disconnects the runtime. Check Runtime → Manage sessions in Colab to make sure nothing is still running.

## About the model

Borealis 2 is a preview release. According to the model card it is based on `google/gemma-4-26B-A4B-it`, with continued pre-training on `aurora`, a 47-billion-word corpus dominated by Norwegian and other Nordic languages and including licensed newspaper text, followed by supervised fine-tuning on Norwegian instructions. The model card states that the preview has not been fully safety-aligned and should not be used for safety-critical applications.

The responses in this repo have not been fact-checked or corrected. Any errors in them are the model's own, and that is part of what the test is meant to show. See the model card for the model's license and terms of use.

## License

Everything in this repo that is mine to give away is freely reusable, including commercially, as long as you credit it.

| What | License |
|---|---|
| Code (`borealis2.ipynb`) | [MIT](LICENSE) |
| Test set, documentation, and the structure of the results page | [CC BY 4.0](LICENSE-CONTENT) |
| The model's responses | Not mine to license; see the [model card](https://huggingface.co/NbAiLab/borealis2-26b-a4b-preview-gguf) |

The responses are reproduced here as raw output from someone else's model. The test set, the categories, the notebook, and the page around them are my own work, and those are what the two licenses above cover.
