# Jigsaw Toxic Comment Identification (Keras, CapsNet, Python)

## Info
The purpose of this notebook is to showcase the use of **Capsule Layers** / **CapsNet**, particularly in solving an NLP problem, where contextuality and superposition of data is important. In this case, we'll be attempting to classify online comments as toxic or nontoxic. You can read more CapsNets here [1](https://towardsdatascience.com/capsule-neural-networks-are-here-to-finally-recognize-spatial-relationships-693b7c99b12), [2](https://hackernoon.com/what-is-a-capsnet-or-capsule-network-2bfbe48769cc), [3](https://en.wikipedia.org/wiki/Capsule_neural_network). Toxic comments will also have a further classification, delineating between 1 of a few different "styles" of toxicity mentioned below. We'll be using **Datmo**'s [open source CLI](https://github.com/datmo/datmo) to help us get our environment setup and to track our experiment results and repository states along the way. 

The specific goal of this model, as mentioned in the original [Kaggle competition](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge) prompt, is to create a "multi-headed model that’s capable of detecting different types of of toxicity like threats, obscenity, insults, and identity-based hate". The __training and test datasets__ are comprised of comments from Wikipedia’s talk page edits.

This notebook is a fork of the final [CapsNet+GRU kernel](https://www.kaggle.com/chongjiujjin/capsule-net-with-gru) submitted to the competition by [chongjiujjin](https://www.kaggle.com/chongjiujjin/).


## Content:

The example notebook (`capsnet-keras.ipynb`) will cover the following:

* Training the Model
    * Load Data
    * Define optimization/scoring function
    * Tokenize Data
    * Load GloVe embeddings
    * Define model architecture
    * Fit model
    * Save weights
    * Create snapshot (end of training)
    * Predicting on the Kaggle test set
    * Create snapshot (post-prediction on test set)
* Predicting on new data
    * Instantiate model architecture
    * Load saved weights
    * Predict on manually defined strings
    * Predict on user-defined CSV
    * Writing model predictions to CSV

## Running the example:

**Setup:**

0. Install and launch [Docker](https://docs.docker.com/install/#supported-platforms)
1. `$ pip install datmo`
2. Clone the repository
3. Download the GloVe embedding file [from this link](http://nlp.stanford.edu/data/glove.840B.300d.zip) (Warning: large file, around 2GB)
4. Unzip the GloVe file and move it into the `input/` directory. Also unzip the `test.csv.zip` and `train.csv.zip` files already in `input/`.

Before proceeding, your repository should look as follows:
```
.
├── README.md
├── best.hdf5
├── capsnet-keras.ipynb
├── input
│   ├── glove.840B.300d.txt
│   ├── test.csv
│   ├── test.csv.zip
│   ├── train.csv
│   └── train.csv.zip
└── output
```

**Setting up the environment:**

5. Initialize your datmo repo with `$ datmo init` 
6. When asked about setting up an environment, type `y`
7. Select the `cpu` environment type
8. Select the `kaggle` environment

**Running the notebook:**

9. Initialize a jupyter notebook with `$ datmo notebook` (Setting up the environment will take a while the first time you do it)
10. Select the notebook (`capsnet-keras.ipynb`). Follow the instructions and run cells from top to bottom.
11. For predicting on your own data, add your `.csv` dataset to the `input/` directory.

## Things to watch out for:
1. The GloVe embeddings will be loaded into memory before the training, requiring around 6gb of available RAM. If the RAM is not available on your system, you will likely receive a generic python kernel crash error after a long-running cell.

2. If you run into a kernel crash during embedding file loading, it is likely because your system is limiting the available memory allotted for docker. To fix this, see the following [issue on Stack Overflow](https://stackoverflow.com/questions/44533319/how-to-assign-more-memory-to-docker-container).
