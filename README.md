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

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)

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
  <h1 align="center"><u>Section 1<u/></h1>
  <h2 align="center"><i>Topic modelling<i/></h2>
</p>


## Set up
1. Clone this repository:

```
git clone https://github.com/jorgenhw/GrundtviGPT-3
cd GrundtviGPT-3
```

2. Install the required packages:
```
pip install -r requirements.txt
```
3. Set up the OpenAI API key:
```
export OPENAI_API_KEY=your_api_key
```
## Data
We will be using a dataset of song lyrics from *Højskolesangbogen* as our training data. You can use any dataset of song lyrics that you like, or you can scrape lyrics from the internet. Make sure to preprocess the data and save it in a .txt or .csv file. The OpenAI API has a built in tool that 1) checks if your data is properly prepared and 2) if not makes the corrections automatically and then 3) converts your file into the .jsonl format that GPT-3 requires. You call the tool with the following line:
```
!openai tools fine_tunes.prepare_data -f $path
```
where ```path``` refers to your file.

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
