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
This repository contains all the notebooks and files necessarry to reproduce the results found in the paper _'A Deep Dive into Danish NLP'_.

The project consists of three phases: In the first phase, we test and compare four different topic modelling methods to find the one that produces the most human interpretable topics from a Danish Twitter dataset. In the second phase, we fine-tune 11 Danish language models on a multilabel classification task on the same Twitter dataset. In the last phase, we outline a new method for doing model error analysis on the subgroups made by the best topic model. 

#### Structure of the readme file
This readme file will be structured according to the above outlined phases. Thus, **section 1** contains details on which topic models were compared and provides links to notebooks which will enable a replication of the results presented in the bachelor thesis. Similarly, **section 2** contains details on which models were trained along with links to individual notebooks containing the scripts used for fine-tuning. The last **section (3)** contains a reproducible R-markdown script outlining how the sub-group error analysis was performed.

## Requirements to reproduce results

* A machine with a GPU (we used Google Colab: a virtual notebook environment that executes code on virtual machines with GPU)
* Python 3.6 or higher
* An R-markdown capable IDE

<br />
<p align="center">  
  <h1 align="center">Section 1</h1>
  <h2 align="center"><i>Topic Modelling</i></h2>
</p>



<br />
<p align="center">  
  <h1 align="center">Section 2</h1>
  <h2 align="center"><i>Model Fine-tuning</i></h2>
</p>


## Set up
1. Clone this repository:

```
git clone https://github.com/jorgenhw/model_fine_tuning
cd bachelor_thesis/model_fine_tuning
```

2. Open notebook of interest

Open the notebook with the name of the model you want to examine e.g. ```jonfd/electra-small-nordic.ipynb``` either through your own IDE or through Google Colab (links are provided in the table below).

The below table outlines which notebooks contains which models.

| Model      | Filename | Colab link |
| ----------- | ----------- | ----------- |
| ScandiBERT      | Title       | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Sluei065T_VH_XgXQi85OzmfPBlVoARc)       |
| XLM-RoBERTa Large   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1IoNVFxeqQTJTztl9ezG12BnC4NDEAt-M)        |
| XLM-RoBERTa Base   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1q1WYhRYJYb13hMwGvZRZ0MxP5X3eWVp0)        |
| Nordic ELECTRA-Small   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1P6t6s52G6ySedTDg_09bO_c_7SyQlv9u)        |
| AELAECTRA   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| RøBÆRTa   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| Danish BERT BotXO   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| DeBERTaV3   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| Twitter-XLM-Roberta-base   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1S0gwDVc3tvnO3uvM8i3oOiAPHBFZoKXH#scrollTo=O6svYNzcBB4X)        |
| NB-BERT-large   | Text        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1kFfVYTD47VFat5BOJH4I8rLVn8R1rmLt)        |


#### Content of each notebook
Each notebook consist of five steps

1. Initialization of GPU, installation of necesarry packages and setup of WANDB
2. Importing libraries, data, and the language model
3. Data preprocessing
4. Fine-tuning
5. Evaluation

#### Conclusion
In this project, we have successfully finetuned 11 Danish language models to demonstrate how a more fine-grained sub group error analysis metric can reveal new insights into language models. Suggestions for further research can be found in the paper _'A Deep Dive Into Danish NLP'_ (link provided in the top of this readme).

This project is part of a bachelor thesis in Cognitive Science at Aarhus University, Denmark, 2023.

<br />
<p align="center">  
  <h1 align="center">Section 3</h1>
  <h2 align="center"><i>Evaluation Method</i></h2>
</p>

## Contact

Feel free to contact the authors, [Jørgen Højlund Wibe](https://github.com/jorgenhw) or [Niels Aalund Krogsgaard](https://github.com/nielsaak) for any questions regarding the project.
You may do so through our emails ([Jørgen](mailto:201807750@post.au.dk), [Niels](mailto:202008114@post.au.dk))
<br />

## Acknowledgements
We gratefully acknowledge HuggingFace for developing an open source API for fine-tuning language models as well as providing us with easy-to-use language models off the batch. 

Last but not the least, we thank the Google Team for the Google Colab and the use of GPU through this service.
