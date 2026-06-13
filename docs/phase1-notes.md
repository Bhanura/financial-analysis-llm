# Difference Between NLP and LLMs

- *NLP (Natural Language Processing)* is the broader field focused on enabling computers to understand, interpret, and generate human language. NLP encompasses many techniques and tasks such as sentiment analysis, named entity recognition, and machine translation.

- *LLMs (Large Language Models)* are a powerful subset of NLP models characterized by their massive size, extensive training data, and ability to perform a wide range of language tasks with minimal task-specific training. Models like the Llama, GPT, or Claude series are examples of LLMs that have revolutionized what’s possible in NLP.

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

