# Google Colab notebook SetUp

-  use pip for the installation, which is the package manager for Python. you can run system commands by preceding them with the ! character

- you can install the 🤗 Transformers library as follows:


```bash
!pip install transformers
```

You can make sure the package was correctly installed by importing it within your Python runtime:

```bash
import transformers
```

This installs a very light version of 🤗 Transformers. In particular, no specific machine learning frameworks (like PyTorch or TensorFlow) are installed. Since we’ll be using a lot of different features of the library, we recommend installing the development version, which comes with all the required dependencies for pretty much any imaginable use case:

```bash
!pip install transformers[sentencepiece]
```

# Python virtual environment

You have to installed python on your pc
you can check it by

```bash
python --version
```

When running a Python command in your terminal, such as python --version, you should think of the program running your command as the “main” Python on your system. We recommend keeping this main installation free of any packages, and using it to create separate environments for each application you work on — this way, each application can have its own dependencies and packages, and you won’t need to worry about potential compatibility issues with other applications.

In Python this is done with virtual environments, which are self-contained directory trees that each contain a Python installation with a particular Python version alongside all the packages the application needs. Creating such a virtual environment can be done with a number of different tools, but we’ll use the official Python package for that purpose, which is called venv.

create a virtual environment using the Python venv module:

```bash
python -m venv .env
```
You can jump in and out of your virtual environment with the activate and deactivate scripts:

```bash
# Activate the virtual environment
.env/Scripts/activate

# Deactivate the virtual environment
deactivate
```

As in the previous section on using Google Colab instances, you’ll now need to install the packages required to continue. Again, you can install the development version of 🤗 Transformers using the pip package manager:

```bash
pip install "transformers[sentencepiece]"
```
You’re now all set up and ready to go!

# NLP and LLMs
## Difference Between NLP and LLMs

- **NLP (Natural Language Processing)** is the broader field focused on enabling computers to understand, interpret, and generate human language. NLP encompasses many techniques and tasks such as sentiment analysis, named entity recognition, and machine translation.

- **LLMs (Large Language Models)** are a powerful subset of NLP models characterized by their massive size, extensive training data, and ability to perform a wide range of language tasks with minimal task-specific training. Models like the Llama, GPT, or Claude series are examples of LLMs that have revolutionized what’s possible in NLP.

## The Rise of Large Language Models (LLMs)

In recent years, the field of NLP has been revolutionized by Large Language Models (LLMs).

*A large language model (LLM) is an AI model trained on massive amounts of text data that can understand and generate human-like text, recognize patterns in language, and perform a wide variety of language tasks without task-specific training. They represent a significant advancement in the field of natural language processing (NLP).*


## LLM Characteristics

- **Scale**: They contain millions, billions, or even hundreds of billions of parameters.
- **General capabilities**: They can perform multiple tasks without task-specific training.
- **In-context learning**: They can learn from examples provided in the prompt.
- **Emergent abilities**: As these models grow in size, they demonstrate capabilities that weren’t explicitly programmed or anticipated.

The LLMs shifted the paradigm for building different different NLP models for different different tasks, becouse LLMs can perform wide range of task by prompting and fine-tuning.

## LLM Limitations

- **Hallucinations**: They can generate incorrect information confidently
- **Lack of true understanding**: They lack true understanding of the world and operate purely on statistical patterns
- **Bias**: They may reproduce biases present in their training data or inputs.
- **Context windows**: They have limited context windows (though this is improving)
- **Computational resources**: They require significant computational resources

# The 🤗 Transformers library

## The pipeline() function
It connects a model with its necessary preprocessing and postprocessing steps, allowing us to directly input any text and get an intelligible answer.

```bash
from transformers import pipeline

classifier = pipeline("sentiment-analysis")
classifier("I've been waiting for a HuggingFace course my whole life.")
```
```bash
[{'label': 'POSITIVE', 'score': 0.9598047137260437}]
```

We can even pass several sentences!

```bash
classifier(
    ["I've been waiting for a HuggingFace course my whole life.", "I hate this so much!"]
)
```
```bash
[{'label': 'POSITIVE', 'score': 0.9598047137260437},
 {'label': 'NEGATIVE', 'score': 0.9994558095932007}]
```

By **default**, this pipeline selects a particular pretrained model that has been fine-tuned for **sentiment analysis in English**. The model is downloaded and cached when you create the classifier object. If you rerun the command, the cached model will be used instead and there is no need to download the model again.

There are three main steps involved when you pass some text to a pipeline:

1. The text is preprocessed into a format the model can understand.
2. The preprocessed inputs are passed to the model.
3. The predictions of the model are post-processed, so you can make sense of them.

## Available pipelines for different modalities

- Text pipelines
* text-generation: Generate text from a prompt
* text-classification: Classify text into predefined categories
* summarization: Create a shorter version of a text while preserving key information
* translation: Translate text from one language to another
* zero-shot-classification: Classify text without prior training on specific labels
* feature-extraction: Extract vector representations of text

- Image pipelines
* image-to-text: Generate text descriptions of images
* image-classification: Identify objects in an image
* object-detection: Locate and identify objects in images

- Audio pipelines
* automatic-speech-recognition: Convert speech to text
* audio-classification: Classify audio into categories
* text-to-speech: Convert text to spoken audio

- Multimodal pipelines
* image-text-to-text: Respond to an image based on a text prompt