---
title: "2025 11 07 Build a Rga With Laravel"
date: 2025-11-07T10:57:03-03:00
draft: true
---


Lately, I've been studing about AI: How create prompt efficiently, how build a RGA and how to use fine-tuning.
For fixe my knowledge, I'm going to build a RGA with Laravel.

My goal with this project is build a simple implementation of RGA, where I can demonstrate details by detaisl all the process.
It's a simple projetct, , but I can use this project like scallfold for other posts. I will improve this project in every steps I will create a post about it.


Let's start!

## What is RGA?

RAG (Retrieval-Augmented Generation) is a techinique for augmented the quality of the generated text.
You can increase the range the context of your Ai model.

We can use RAG when we need to specifics information and update, like read company's documents, read data form database or, for example, support system.
Case we dont use this technique, the model can generate halluciantions or even wrong answers.

![Imagem RAG](/images/rag.jpg)

## Setting up enviroment

Let's go install Laravel and  ollama-php.
First, we go to install laravel and create a new project.:

````
    composer create-project laravel/laravel rag-laravel
    cd rag-laravel    
````

After finished the installation, wee need to install ollama-php. This package is library that allow acess the Ollama API.

````

composer require ardagnsrn/ollama-php

````
Now, we can install the Ollama and run this model. For this project I'm using qwen2.5:1.5b,
operation system is Ubuntu 22.04 and Mardown Files.
If you are using other operation system, I highly recommend you follow the ollama's doc and follow the instruction to install the model.

Run this command to install the Ollama:
````
curl -fsSL https://ollama.com/install.sh | sh
````
After that, we can run the model:

````
ollama pull qwen2.5:1.5b

````

I chosse this mode becaust it's a simple model and we dont need to have a good computer.
By the way, how it's a simple model the answer can be take a long time and the response quality can be low.


## Indexing documents

Now, with the enviroment ready, we can startu to build a RAG, but first, I need to understand about indexing documents.
Embedding technique allow us generate number from text, this way the model understand the context of the text.

For example, if we send a big book to the model, the model cannot understand the context of the book, because have a lot of information so this can generatve halluciantions or inconsistencies.
Therefore, we need to create embeddings for each document and store in a database.

When this user make a question, this question will be generate a embedding and the model will search in the database for the closest embedding.

Now enter in the project's directory and run this command:
```
 php artisan make:command  embedding

```
Before the create index with the complex tools we need to understando the concept behind hoods  how the algorithm works.
For this reason, I will create a simple function that will generate the embedding:
```
  private function gerarembeddingimples(string $texto): array
    {
        // Quebra o texto em palavras únicas e ordenadas
        $palavras = array_unique(str_word_count(strtolower($texto), 1));
        sort($palavras);
    
        // Cria um hash numérico simples (mock de embedding)
        return array_map(fn($p) => crc32($p) % 1000 / 1000, $palavras);
    }
```
# Explain the code

