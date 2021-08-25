# Introduction
This repository includes my codes to evaluate regulatory documents for NLP based information extraction (IE). 
Python were used for coding. Employed technologies include SpaCy library for Named Entity Recognition (NER) and SOAT pre-trained BERT (via Transformers) for Question Answer (QA) IE.

# Getting started
The Jupyter Notebok file of [01_EDA_IE.ipynb](https://github.com/alilajevardi/Regulatory-Insight/blob/main/01_EDA_IE.ipynb) is the start point for Exploratory Data Analysis.

In fine-tuning of pre-trained BERT for QA I used SQuAD 2.0 dataset. The Regulatory dataset is proprietary one and I can not share it here.

# Environment setup
As it is tested, the program works with python 3.7-3.8 and pytorch cudatoolkit=10.1.
You can install Anaconda and create a new environment with

    conda env create -f env.yml
then activate it with

    conda activate nlp_reg

You may need to install english dictionary via
    
    python -m spacy download en


# Derieved insight
Most of reg document are form US. 

![picture](https://github.com/alilajevardi/Regulatory-Insight/blob/main/artifacts/UIDs_Countries.png)

Dataset includes two document types of PDF and HTML. The latter needs cleaning attention.

![picture](https://github.com/alilajevardi/Regulatory-Insight/blob/main/artifacts/HTML_PDF.png)


# Methods and Outcomes
Extracting dates form reg document via string manipulation has difficulty to come up with a pattern to capture the many ways a date can be written. A second difficulty is to identify numbers or expressions where we can be reasonable sure that the number signifies a date and not something like document code.

My first attempt was to use Spacy NER in order to extract various dates of a reg doc. It need to be followed by ependency parsing that reconstructs the grammatical structure from a text. SpaCy has support for word vectors with very fast engine. It is recommended to use Spacy NER for production over Stanford NER. However results for extracting various dates of a reg doc is not a trivial task for SpaCy engine and results are not promising.
![picture](https://github.com/alilajevardi/Regulatory-Insight/blob/main/artifacts/pipeline_Spacy_NER.png)


Sophisticated techniques of empolying SOTA pre-trained networks (BERT or XLNet) illustrate a promising direction to solve the problem. 
The pre-trained modles can be employed to extract dates via QA method. Fine-tuning of pre-trained models is a vital step in enhancing results, however it requires a annotated database with reasonably high number of records for each document type.

Lack of broad coverage datasets for date QA is a limiting factor for this proposed date QA method. Another promising emerging method to solve this problem is  Temporal Knowledge Graphs that provides temporal scopes and can enhance date extraction from requlatory text.


