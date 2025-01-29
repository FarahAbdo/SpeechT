# SpeechT
# Arabic-to-English Speech Translation

## Dataset
The dataset used for this project is [farahabdou/FLEURS-AR-EN-split](https://huggingface.co/datasets/farahabdou/FLEURS-AR-EN-split), a subset of the FLEURS dataset, specifically tailored for Arabic-to-English translation tasks. 

FLEURS (Fluent and Less-Extensive Universal Recognition of Speech) is a multilingual dataset designed for speech recognition and translation tasks. The dataset includes audio recordings in Arabic paired with their corresponding English translations. The data is split into training, validation, and test sets to facilitate model training and evaluation.

This dataset is particularly useful for:
- End-to-end speech translation tasks
- Cascaded approaches involving separate speech recognition and machine translation models

## Modelling Approaches
Two distinct approaches were employed for the Arabic-to-English translation task:

### 1. End-to-End Model
The first model utilizes OpenAI's `whisper-small` model, a pre-trained speech-to-text model capable of handling end-to-end speech translation. This model directly translates Arabic speech into English text without intermediate steps. 

The model was fine-tuned on the `FLEURS-AR-EN-split` dataset to optimize its performance for the specific task of Arabic-to-English translation.

### 2. Cascaded Model
The second approach follows a cascaded system that combines two models:

- **Speech-to-Text (ST):** OpenAI's `whisper-small` model is used to transcribe Arabic speech into Arabic text.
- **Machine Translation (MT):** Facebook's `nllb-200-distilled-600M` model is then used to translate the transcribed Arabic text into English.

This cascaded approach leverages the strengths of both models, with `whisper-small` handling speech recognition and `nllb-200` focusing on the translation task.

## Evaluation
The results indicate that the cascaded model outperforms the end-to-end model in terms of translation quality:

| Model              | BLEU Score | chrF++ Score |
|-------------------|------------|--------------|
| End-to-End Model | 15.06      | 39.03        |
| Cascaded Model   | 24.38      | 51.79        |

These results suggest that separating the tasks of speech recognition and machine translation leads to better translation accuracy, as each model can specialize in its respective task. However, the end-to-end model offers the advantage of simplicity and faster inference, making it a viable option for scenarios where speed is prioritized over translation quality.

## Conclusion
- The **cascaded model** provides better translation accuracy by utilizing specialized models for speech recognition and translation.
- The **end-to-end model** offers a simpler and faster approach, though at the cost of lower translation quality.
- The choice of model depends on the use case: **accuracy vs. inference speed**.

