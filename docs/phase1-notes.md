# 🤗 Hugging Face Transformers - Study Notes

# Environment Setup

## Google Colab Setup

Google Colab allows you to run Python code directly in the browser without installing software locally.

### Install Transformers

```python
!pip install transformers
```

Verify the installation:

```python
import transformers
```

### Install Full Transformers Package

For most NLP, Computer Vision, and Speech tasks:

```python
!pip install "transformers[sentencepiece]"
```

This installs additional dependencies required for many Hugging Face models and pipelines.

---

## Python Virtual Environment Setup

### Check Python Installation

```bash
python --version
```

### Create a Virtual Environment

```bash
python -m venv .env
```

### Activate the Virtual Environment

Windows:

```bash
.env\Scripts\activate
```

Linux/macOS:

```bash
source .env/bin/activate
```

### Deactivate the Environment

```bash
deactivate
```

### Install Transformers

```bash
pip install "transformers[sentencepiece]"
```

---

# NLP and LLMs

## What is NLP?

**Natural Language Processing (NLP)** is the field of Artificial Intelligence focused on enabling computers to understand, process, and generate human language.

Common NLP tasks include:

* Sentiment Analysis
* Machine Translation
* Text Classification
* Named Entity Recognition (NER)
* Question Answering
* Summarization

---

## What are Large Language Models (LLMs)?

**Large Language Models (LLMs)** are advanced NLP models trained on massive amounts of text data.

Examples:

* GPT Series
* Llama Series
* Claude Series
* Gemma Series

LLMs can:

* Understand natural language
* Generate human-like text
* Answer questions
* Summarize documents
* Translate languages
* Write code
* Follow instructions

---

## NLP vs LLMs

| NLP                                          | LLMs                                  |
| -------------------------------------------- | ------------------------------------- |
| Broad field of study                         | Subset of NLP                         |
| Often task-specific                          | General-purpose                       |
| Requires separate models for different tasks | One model can perform many tasks      |
| Traditional ML and DL techniques             | Large Transformer-based architectures |
| Limited flexibility                          | Highly adaptable                      |

---

## Key Characteristics of LLMs

### Scale

* Millions to hundreds of billions of parameters

### General Capabilities

* Perform multiple tasks without retraining

### In-Context Learning

* Learn from examples provided in prompts

### Emergent Abilities

* Unexpected capabilities appear as model size increases

---

## Limitations of LLMs

### Hallucinations

May generate incorrect information confidently.

### Lack of True Understanding

Operate using statistical patterns rather than genuine reasoning.

### Bias

Can reflect biases present in training data.

### Context Window Limitations

Limited memory of previous text.

### High Computational Cost

Require significant computational resources.

---

# The 🤗 Transformers Library

The Transformers library provides easy access to thousands of pretrained models.

Official Website:

https://huggingface.co

---

# The `pipeline()` Function

The `pipeline()` API is the simplest way to use pretrained Transformer models.

It automatically handles:

1. Preprocessing
2. Model Inference
3. Postprocessing

Example:

```python
from transformers import pipeline

classifier = pipeline("sentiment-analysis")

classifier(
    "I've been waiting for a Hugging Face course my whole life."
)
```

Output:

```python
[
  {
    'label': 'POSITIVE',
    'score': 0.9598
  }
]
```

Multiple inputs:

```python
classifier([
    "I've been waiting for a Hugging Face course my whole life.",
    "I hate this so much!"
])
```

---

# Available Pipelines

## Text Pipelines

| Pipeline                 | Purpose                                       |
| ------------------------ | --------------------------------------------- |
| text-generation          | Generate text                                 |
| text-classification      | Categorize text                               |
| summarization            | Summarize text                                |
| translation              | Translate languages                           |
| zero-shot-classification | Classification without task-specific training |
| feature-extraction       | Generate embeddings                           |

---

## Image Pipelines

| Pipeline             | Purpose                     |
| -------------------- | --------------------------- |
| image-classification | Identify objects            |
| object-detection     | Detect and locate objects   |
| image-to-text        | Generate image descriptions |

---

## Audio Pipelines

| Pipeline                     | Purpose                 |
| ---------------------------- | ----------------------- |
| automatic-speech-recognition | Speech-to-text          |
| audio-classification         | Audio categorization    |
| text-to-speech               | Convert text into audio |

---

## Multimodal Pipelines

| Pipeline           | Purpose                       |
| ------------------ | ----------------------------- |
| image-text-to-text | Answer questions about images |

---

# Common NLP Use Cases

## 1. Zero-Shot Classification

Classify text using custom labels without additional training.

```python
from transformers import pipeline

classifier = pipeline("zero-shot-classification")

classifier(
    "This is a course about the Transformers library",
    candidate_labels=[
        "education",
        "politics",
        "business"
    ]
)
```

Output:

```python
{
 'labels': ['education', 'business', 'politics'],
 'scores': [0.84, 0.11, 0.04]
}
```

---

## 2. Text Generation

Generate text from a prompt.

```python
from transformers import pipeline

generator = pipeline("text-generation")

generator(
    "In this course, we will teach you how to"
)
```

Control generation length:

```python
generator(
    "In this course, we will teach you how to",
    max_length=30,
    num_return_sequences=2
)
```

---

## Using Custom Models

Browse models:

https://huggingface.co/models

Example:

```python
from transformers import pipeline

generator = pipeline(
    "text-generation",
    model="HuggingFaceTB/SmolLM2-360M"
)
```

---

## 3. Mask Filling

Predict missing words.

```python
from transformers import pipeline

unmasker = pipeline("fill-mask")

unmasker(
    "This course will teach you all about <mask> models.",
    top_k=2
)
```

Output:

```python
[
  {
    'token_str': 'mathematical'
  },
  {
    'token_str': 'computational'
  }
]
```

---

## 4. Named Entity Recognition (NER)

Identify entities such as:

* People
* Organizations
* Locations

```python
from transformers import pipeline

ner = pipeline(
    "ner",
    grouped_entities=True
)

ner(
    "My name is Sylvain and I work at Hugging Face in Brooklyn."
)
```

Output:

```python
[
  {
    'entity_group': 'PER',
    'word': 'Sylvain'
  },
  {
    'entity_group': 'ORG',
    'word': 'Hugging Face'
  },
  {
    'entity_group': 'LOC',
    'word': 'Brooklyn'
  }
]
```

---

## 5. Question Answering

Answer questions using provided context.

```python
from transformers import pipeline

qa = pipeline("question-answering")

qa(
    question="Where do I work?",
    context="My name is Sylvain and I work at Hugging Face in Brooklyn"
)
```

Output:

```python
{
 'answer': 'Hugging Face'
}
```

---

## 6. Summarization

Reduce long text into concise summaries.

```python
from transformers import pipeline

summarizer = pipeline("summarization")

summary = summarizer(long_text)
```

Control output length:

```python
summarizer(
    long_text,
    max_length=100,
    min_length=30
)
```

---

## 7. Translation

Translate text between languages.

Example:

```python
from transformers import pipeline

translator = pipeline(
    "translation",
    model="Helsinki-NLP/opus-mt-fr-en"
)

translator(
    "Ce cours est produit par Hugging Face."
)
```

Output:

```python
[
  {
    'translation_text':
    'This course is produced by Hugging Face.'
  }
]
```

---

# Image and Audio Pipelines

## Image Classification

```python
from transformers import pipeline

classifier = pipeline(
    "image-classification",
    model="google/vit-base-patch16-224"
)

result = classifier(image_path)
print(result)
```

Applications:

* Object Recognition
* Image Tagging
* Content Moderation

---

## Automatic Speech Recognition (ASR)

Convert speech into text.

```python
from transformers import pipeline

transcriber = pipeline(
    "automatic-speech-recognition",
    model="openai/whisper-large-v3"
)

result = transcriber(audio_file)
print(result)
```

Applications:

* Voice Assistants
* Meeting Transcription
* Subtitles

---

# Combining Data from Multiple Sources

Transformer models can combine information across multiple modalities.

Examples:

### Multi-Database Search

Search information across:

* Documents
* Images
* Audio

### Multimodal Question Answering

Combine:

* Image Inputs
* Text Prompts

to generate meaningful responses.

### Unified Information Retrieval

Merge:

* Metadata
* Documents
* Multimedia Content

into a single coherent answer.

---

# Key Takeaways

✅ NLP is the broader field of language processing.

✅ LLMs are advanced Transformer-based NLP models.

✅ Hugging Face Transformers provides thousands of pretrained models.

✅ The `pipeline()` API offers the easiest way to use Transformer models.

✅ Transformers support:

* Text
* Images
* Audio
* Multimodal Applications

✅ Common tasks include:

* Classification
* Generation
* Translation
* Summarization
* Question Answering
* Speech Recognition

---

# Useful Resources

* Hugging Face: https://huggingface.co
* Model Hub: https://huggingface.co/models
* Transformers Documentation: https://huggingface.co/docs/transformers
* Hugging Face Course: https://huggingface.co/learn
