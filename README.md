# Code for paper "Political dogwhistles and community divergence in semantic change"

This repository contina the code for the paper "Political dogwhistles and community divergence in semantic change".

## Data
The original data sets are hosted by  [Språkbanken](https://spraakbanken.gu.se/): 
* *[Flashback](https://spraakbanken.gu.se/lb/resurser/meningsmangder/flashback-politik.xml.bz2)*
* *[Familjeliv](https://spraakbanken.gu.se/lb/resurser/meningsmangder/familjeliv-allmanna-samhalle.xml.bz2)*


## Preprocessing
### Step 1
The XML files have, after decompression, been processed by `data/FILE`, which extracts only the text of each example (without tags) and save to a text file corresponding to its year (one example per line).
### Step 2
Data from Step 1 were further preprocessed through `data/FILE`. 

#### SGNS
...

#### BERT
...

## Additional features
Modeling and results uses two additional features:

* counts of words of the vocabulary 
* token counts (nmber of words and examples per year)

```
CODE
```

## Models
### Skipgram with negative sampleing (SGNS)
Models are built through `sgns/sgns.py`, which implements `word2vec` from [Gensim](https://radimrehurek.com/gensim/). The procedure for training models with shuffled controls is implemented in a Bash script, `sgns/train_serial.sh`. Parameters of training are altered within the Bash script. A big thank you goes to [`semantic-shift-in-social-networks`](https://github.com/GU-CLASP/semantic-shift-in-social-networks) for code on which this code is built. 

### BERT, averageing


### BERT, clusters



## Results


