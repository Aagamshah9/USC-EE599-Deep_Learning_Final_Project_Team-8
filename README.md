## Handwriting synthesis using recurrent neural networks (RNN)
Implementation of handwriting generation with use of recurrent neural networks in tensorflow. Based on Alex Graves paper (https://arxiv.org/abs/1308.0850).

## How to train a model and generate synthesized handwriting

#### 1. Download dataset
First you need to download dataset from (http://www.fki.inf.unibe.ch/databases/iam-on-line-handwriting-database). Download the [data/original-xml-part.tar.gz]. Unzip it in repository directory.

#### 2. Preprocess dataset
```
python preprocess.py
```

This scipt searches local directory for `xml` files with handwriting data and preprocessing like normalizing data and spliting strokes in lines is performed. As a result it will create `data` directory with preprocessed dataset.

#### 3. Train model
```
python train.py
```

This will launch training with default settings. By default it will create `summary` directory with separate `experiment` directories for each run. So if we want to restore training we just need provide a path to the experiment we want to continue.
```
python train.py --restore=summary\experiment-0
```
We can lookup losses in command line or with tensorboard. 

With default settings training took about 10h (using Aamazon AWS EC2 p3 instance).


#### 4. Generate handwriting!
```
python generate.py --model=path_to_model
```

When model is trained we can use `generate.py` script to test how it works. Without providing `--text` argument this script will ask in order to what to generate in a loop.

Additional options for generation:
* `--bias` (`float`) - with higher bias generated handwriting is more _clear_ (Alex Graves paper)
* `--noinfo` - it will plot only generated handwriting (without attention window)
* `--style` - style of handwriting, `int` from 0 to 7 (How each style looks like in stored in the `imgs` folder)
