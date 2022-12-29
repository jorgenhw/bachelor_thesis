<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://i.imgur.com/BtQCfMu.png">
    <img src="https://i.imgur.com/BtQCfMu.png" alt="Logo" width=200 height=200>
  </a>
  
  <h1 align="center">A Dive Into Danish NLP</h1> 
  <h2 align="center"><i>Exploring the Strengths and Weaknesses of Danish Language Models using a new Fine-Grained Evaluation Technique</i></h2> 
  <h3 align="center">Cognitive Science // Bachelor Thesis 2023</h3>


  <p align="center">
    Jørgen Højlund Wibe & Niels Aalund Krogsgaard
  </p>
</p>

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About the project</a></li>
    <li><a href="#section-1">Section 1: <i>Topic Modelling</i></a></li>
     <ul>
      <li><a href="#example1">Example 1</a></li>
      <li><a href="#example2">Example 2</a></li>
    </ul>
    <li><a href="#section-2">Section 2: <i>Fine-Tuning Models</i></a></li>
    <li><a href="#section-3">Section 3: <i>Evaluation Method</i></a></li>
    <li><a href="#data">Data</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About the project

This project consists of three phases: In the first phase, we test and compare four different topic modelling methods to find the one that produces the most human interpretable topics from a Danish Twitter dataset. In the second phase, we fine-tune 11 Danish language models on a multilabel classification task on the same Twitter dataset. In the last phase, we outline a new method for doing model error analysis on the subgroups made by the best topic model. 

#### Structure of the readme file
This readme file will be structured according to the above outlined phases. Thus, **section 1** contains details on which topic models were compared and provides links to notebooks which will enable a replication of the results presented in the bachelor thesis. Similarly, **section 2** contains details on which models were trained along with links to individual notebooks containing the scripts used for fine-tuning. The last **section (3)** contains a reproducible R-markdown script outlining how the sub-group error analysis was performed.

## Requirements to reproduce results

* A machine with a GPU (we used Google Colab: a virtual notebook environment that executes code on virtual machines with GPU)
* Python 3.6 or higher
* An R-markdown capable IDE

<br />
<p align="center">  
  <h1 align="center">Section 1</h1>
  <h2 align="center"><i>Topic modelling</i></h2>
</p>


## Set up
1. Clone this repository:

```
git clone https://github.com/jorgenhw/bachelor_thesis
cd bachelor_thesis/topic_modelling
```

2. Install the required packages:
```
pip install -r requirements.txt
```
3. Open respective notebooks

Run the notebook with the name of the model you want to examine e.g. ```jonfd/electra-small-nordic.ipynb```
The below table outlines which notebooks contains which models along with a link to a the notebooks on Google Colab
| Model      | Filename | Colab link |
| ----------- | ----------- | ----------- |
| ScandiBERT      | Title       | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)       |
| XLM-RoBERTa Large   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| XLM-RoBERTa Base   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| Nordic ELECTRA-Small   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| AELAECTRA   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| RøBÆRTa   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| Danish BERT BotXO   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| DeBERTaV3   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| Twitter-XLM-Roberta-base   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| NB-BERT-large   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |


## Finetuning
1. Choose the GPT-3 model that you want to use for finetuning. You can find a list of available models and their sizes here: https://beta.openai.com/docs/models/gpt-3

2. Set your hyperparameters
```
model = 'davinci'  # can be ada, babbage, curie or davinci
n_epochs = 4
batch_size = 4
learning_rate_multiplier = 0.1
prompt_loss_weight = 0.1
```
Replace 'davinci' with the model that you have chosen

3. Fine-tune the model on your dataset using the OpenAI API:

```
!openai api fine_tunes.create \
    -t $train_file \
    -m $model \
    --n_epochs $n_epochs \
    --batch_size $batch_size \
    --learning_rate_multiplier $learning_rate_multiplier \
    --prompt_loss_weight $prompt_loss_weight
```


## Evaluation
Evaluate the performance of the finetuned model by generating lyrics and comparing them to a sample of the training data. You can also use metrics such as perplexity and BLEU score to quantitatively evaluate the model.

## Conclusion
In this project, we have successfully finetuned the GPT-3 model on a lyrics generation task. You can further improve the performance of the model by using a larger dataset, increasing the number of training epochs, fine-tuning on a specific artist or genre and last but not least, optimizing the hyperparameters.

This project is part of an exam projekt in Cultural Data Science at Aarhus University, Denmark, 2023.

## Contact

Feel free to contact the authors, [Jørgen Højlund Wibe](https://github.com/jorgenhw) or [Niels Aalund Krogsgaard](https://github.com/nielsaak) for any questions regarding the project.
You may do so through our emails ([Jørgen](mailto:201807750@post.au.dk), [Niels](mailto:202008114@post.au.dk))
<br />

## Acknowledgements
The tools provided in this readme are all developed and provided by [OpenAI](https://openai.com/). We refer to their [documentation page](https://beta.openai.com/docs/introduction) for more detailed information.
