# Code for paper "Political dogwhistles and community divergence in semantic change"

This repository contina the code for the paper "Political dogwhistles and community divergence in semantic change".

## Data
The original data sets are hosted by  [Språkbanken](https://spraakbanken.gu.se/): 
* *[Flashback](https://spraakbanken.gu.se/lb/resurser/meningsmangder/flashback-politik.xml.bz2)*
* *[Familjeliv](https://spraakbanken.gu.se/lb/resurser/meningsmangder/familjeliv-allmanna-samhalle.xml.bz2)*


## Preprocessing
### Step 1
The XML files have, after decompression, been processed by `data/read_large_xml.py`, which extracts only the text of each example (without tags) and save to a text file corresponding to its year (one example per line).
### Step 2
Data from Step 1 were further preprocessed through `data/preprocess2.py`. 

#### SGNS
For the SGNS model, data are preprocessed with configuation file `data/utils/pp_sgns_config.json`. Example:

```
python preprocess2.py CORPUS_IN CORPUS_OUT --config utils/pp_sgns_config.json
```

#### BERT
For the BERT models, data are preprocessed with configuation file `data/utils/pp_bert_config.json`. Example:

```
python preprocess2.py CORPUS_IN CORPUS_OUT --config utils/pp_bert_config.json
```

## Additional features
Modeling and results uses two additional features:

* counts of words of the vocabulary 
* token counts (nmber of words and examples per year)

```
CODE
```

## Models
The general procedure for semantic change modeling is:

* A input corpus of text files; a directory with text files such that every file correspond to a time bin (here: years) and every line of a file correspond to a sentence.
* An algortihm to build vectors for every time bin (here: years).
* An output directory of results: vectors of terms over time. 
 
### Skipgram with negative sampleing (SGNS)
Models are built through `sgns/sgns.py`, which implements `word2vec` from [Gensim](https://radimrehurek.com/gensim/). The procedure for training models with shuffled controls is implemented in a Bash script, `sgns/train_serial.sh`. Parameters of training are altered within the Bash script. A big thank you goes to [`semantic-shift-in-social-networks`](https://github.com/GU-CLASP/semantic-shift-in-social-networks) for code on which this code is built. 

### BERT
#### From text to vectors
For BERT models - both averaging and clustering approach - sentences were first vectorized through code in `bert/text2bert.ipynb`.
#### Averageing SBERT
For building average vectors of each time period as well as for shuffled controls, the procedure was implemented with `bert/bert_change.ipynb`.
#### Clustering SBERT
For the clustering approach, results were built from `bert/cluster_over_time.ipynb`. 
## Results
With the vectors produced, results are built with `analysis/create_df_mp.py`. Bash scripts ...

